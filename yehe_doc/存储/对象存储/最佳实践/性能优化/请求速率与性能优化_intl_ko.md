>!
>현재 COS는 하위 인덱스 분산 메커니즘을 통해 높은 QPS를 구현했으며 더 높은 성능의 QPS가 필요한 경우 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의할 수 있습니다. 파일을 정리하는 일상적인 프로세스에서 여전히 이 문서의 요구 사항을 따르고 지나치게 중앙 집중화된 인덱스 저장소를 피하는 것이 좋습니다.

## 소개
본문은 Tencent Cloud Cloud Object Storage(COS)에서 요청 속도 성능 최적화를 위한 모범 사례를 설명합니다.

Tencent Cloud COS는 초당 30000 PUT 요청 또는 초당 30000 GET 요청의 일반적인 워크로드 용량을 지원합니다. 워크로드가 위의 임계값을 초과하는 경우 이 가이드에 따라 요청 속도 성능을 확장하고 최적화할 수 있습니다.

>? 요청 로드는 동시 연결 수가 아닌 초당 시작된 요청 수를 나타냅니다. 즉, 문제 없이 수천 개의 기존 연결을 유지하면서 초당 수백 개의 새로운 연결 요청을 보낼 수 있습니다.
>


Tencent Cloud COS는 더 높은 요청률을 제공하기 위해 성능 확장을 지원합니다. GET 요청 로드가 높은 경우 Tencent Cloud CDN 제품과 함께 COS를 사용하는 것이 좋습니다. 자세한 내용은 [도메인 관리](https://intl.cloud.tencent.com/document/product/436/18424)를 참고하십시오. 버킷의 전체 요청 속도가 초당 30000 PUT/LIST/DELETE 요청을 초과할 것으로 예상되는 경우 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의하여 워크로드에 대비하고 요청 제한을 피할 수 있습니다.

>? 가끔 초당 30000에 도달하고 버스트 중에 초당 30000을 초과하지 않는 혼합 요청 로드가 있는 경우 이 가이드를 무시할 수 있습니다.
>

## 실행 순서
### 혼합 요청 로드

대량의 객체를 업로드하는 경우, 선택한 객체 키의 성능에 문제가 생길 수 있습니다. 다음은 Tencent Cloud COS가 Object 키 값을 저장하는 방법을 간략히 소개합니다.

Tencent Cloud는 COS의 모든 서비스 리전에 버킷(Bucket)과 객체(Object)의 키 값을 인덱스로 유지하고 있습니다. 객체 키는 UTF-8 이진법의 순서로 저장됩니다. 이처럼 많은 키 값으로 인해 타임스탬프나 알파벳 순서 등을 사용하면 키 값이 위치한 파티션의 읽기/쓰기 성능 용량이 소모될 수 있습니다. 버킷 경로 `examplebucket-1250000000.cos.ap-beijing.myqcloud.com`을 예시로 인덱스 성능 용량을 소모할 수 있는 몇 가지 경우는 다음과 같습니다.

```bash
20170701/log120000.tar.gz
20170701/log120500.tar.gz
20170701/log121000.tar.gz
20170701/log121500.tar.gz
...
image001/indexpage1.jpg
image002/indexpage2.jpg
image003/indexpage3.jpg
...
```

일반적인 워크로드가 초당 30000개 요청을 초과하는 경우 위의 경우와 같이 순차 키 값을 사용하지 않아야 합니다. 일련 번호, 날짜 또는 시간 값과 같은 문자를 객체 키로 사용해야 하는 경우 키 이름에 임의의 접두사를 추가하여 여러 인덱스 파티션의 키 값을 관리하고 중앙 집중식 로드 성능을 개선할 수 있습니다. 다음은 키 값에 임의의 요소를 추가하는 몇 가지 방법입니다.

>!단일 버킷의 액세스 성능을 향상시키기 위해 다음 방법을 모두 사용할 수 있습니다. 업무의 일반적인 부하가 초당 30000 요청을 초과하는 경우에도 다음 방법을 수행하는 동안에도 미리 업무 부하에 대비하기 위해 [고객센터](https://intl.cloud.tencent.com/contact-sales)로 문의하십시오.

#### 16진법 해시 접두사 추가

객체 키에 랜덤성을 높이는 가장 직접적인 방법은 키 이름의 맨 앞에 해시 문자열 접두사를 추가하는 것입니다. 예를 들어 객체를 업로드할 때 경로 키 값의 SHA1 또는 MD5 해시를 계산하고 키 이름에 접두사로 몇 개의 문자를 추가합니다. 일반적으로 길이가 2 - 4자인 해시 접두사로 충분합니다.
<pre>
<font color="red">faf1</font>-20170701/log120000.tar.gz
<font color="red">e073</font>-20170701/log120500.tar.gz
<font color="red">333c</font>-20170701/log121000.tar.gz
<font color="red">2c32</font>-20170701/log121500.tar.gz
</pre>

>!Tencent Cloud COS의 키 값은 UTF-8 바이너리 순서로 인덱싱되므로 원래의 완전한 20170701 접두사 구조를 얻으려면 65536 GET Bucket 작업을 시작해야 할 수 있습니다.

#### 열거된 값 접두사 추가

여전히 객체 키를 쉽게 검색할 수 있는지 확인하려면 파일 유형에 따라 접두사를 열거하여 객체를 그룹화할 수 있습니다. 동일한 열거 값을 가진 접두사는 접두사가 위치한 인덱스 파티션의 기능을 공유합니다.

```bash
logs/20170701/log120000.tar.gz
logs/20170701/log120500.tar.gz
logs/20170701/log121000.tar.gz
...
images/image001/indexpage1.jpg
images/image002/indexpage2.jpg
images/image003/indexpage3.jpg
...
```

열거된 접두사에 대한 액세스 로드가 초당 30000개 이상의 요청으로 유지되는 경우 이전 방법을 참고하여 열거된 값 뒤에 해시 접두사를 추가하여 다중 인덱스 파티션을 구현하여 읽기/쓰기 성능을 향상시킬 수 있습니다.
<pre>
logs/<font color="red">faf1</font>-20170701/log120000.tar.gz
logs/<font color="red">e073</font>-20170701/log120500.tar.gz
logs/<font color="red">333c</font>-20170701/log121000.tar.gz
...
images/<font color="red">0165</font>-image001/indexpage1.jpg
images/<font color="red">a349</font>-image002/indexpage2.jpg
images/<font color="red">ac00</font>-image003/indexpage3.jpg
...
</pre>

#### 키 이름 문자열 반전

증분 ID 또는 날짜를 사용해야 하거나 단일 업로드에서 접두사가 연속적인 많은 객체를 업로드하려면 다음 방법을 참고하십시오.

```shell
20170701/log0701A.tar.gz
20170701/log0701B.tar.gz
20170702/log0702A.tar.gz
20170702/log0702B.tar.gz
...
id16777216/album/hongkong/img20170701121314.jpg
id16777216/music/artist/tony/anythinggoes.mp3
id16777217/video/record20170701121314.mov
id16777218/live/show/date/20170701121314.mp4
...
```

상기 키 값에 대한 네이밍 방식은 2017과 ID가 붙은 키 값이 위치한 인덱스 파티션의 성능을 쉽게 소모합니다. 이 경우 임의의 특정 요소를 허용하기 위해 키 접두사의 일부를 반전시킵니다.

```bash
10707102/log0701A.tar.gz
10707102/log0701B.tar.gz
20707102/log0702A.tar.gz
20707102/log0702B.tar.gz
...
61277761di/album/hongkong/img20170701121314.jpg
61277761di/music/artist/tony/anythinggoes.mp3
71277761di/video/record20170701121314.mov
81277761di/live/show/date/20170701121314.mp4
...
```

### 높은 GET 요청 로드

워크로드가 주로 GET 요청(예: 다운로드 요청)과 관련된 경우 위 지침을 준수하는 것 외에도 Tencent Cloud CDN 서비스와 함께 COS를 사용하는 것이 좋습니다.

Tencent Cloud CDN은 콘텐츠를 사용자에게 배포할 때 대기 시간을 최소화하고 속도를 향상시키는 데 사용할 수 있는 중국과 전 세계에 엣지 가속 노드를 보유하고 있습니다. 핫 파일은 프리패치 기능을 사용하여 캐시할 수 있으므로 COS 원본 서버로 반환되는 GET 요청 수를 줄일 수 있습니다. 자세한 내용은 [도메인 관리](https://intl.cloud.tencent.com/document/product/436/18424)를 참고하십시오.
