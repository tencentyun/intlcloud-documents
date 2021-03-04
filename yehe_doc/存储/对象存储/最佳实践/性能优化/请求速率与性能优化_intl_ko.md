## 소개
본 문서에서는 Tencent Cloud COS의 요청 속도 성능을 최적화하기 위한 모범 사례를 소개합니다.

Tencent Cloud COS에서 제공하는 기본 워크로드는 초당 PUT 요청 3만 개 또는 초당 GET 요청 3만 개입니다. 만약 워크로드가 이 수준을 초과할 경우, 다음 가이드를 참고하여 요청 속도를 향상 및 최적화하십시오.

>요청 부하는 초당 발생하는 요청 수이며, 동시에 접속하는 수를 의미하지 않습니다. 즉, 접속 수가 수천 개인 상태에서도 여전히 1초당 수백 개의 새로운 접속 요청을 할 수 있습니다.


Tencent Cloud COS는 요청 속도 향상을 위해 성능 강화 서비스를 지원합니다. 부하가 높은 GET 요청을 할 경우, Tencent Cloud의 CDN 제품을 함께 이용할 수 있습니다. 자세한 내용은 [도메인 관리](https://intl.cloud.tencent.com/document/product/436/18424)를 참조해 주십시오. 버킷의 초당 PUT/LIST/DELETE 복합 요청이 3만 개를 초과 발생할 것으로 예상되는 경우, 요청 실행 시 장애가 없도록 워크로드와 관련된 조치가 필요하므로 [고객센터](https://intl.cloud.tencent.com/support)로 문의하십시오.

>복합 요청 부하가 초당 3만 개에 육박하는 경우가 드물고 돌발 상황에서도 초당 3만 개가 넘지 않는다면, 본 가이드를 따르지 않아도 됩니다.

## 실행 순서
### 복합 요청 부하

대량의 객체를 업로드하는 경우, 선택한 객체 키의 성능에 문제가 생길 수 있습니다. 다음은 Tencent Cloud COS가 Object 키 값을 저장하는 방법을 간략히 소개합니다.

Tencent Cloud는 COS의 모든 서비스 리전에 버킷(Bucket)과 객체(Object)의 키 값을 인덱스로 점검하고 있습니다. 객체 키는 UTF-8 이진법의 순서로 인덱스의 여러 파티션에 저장됩니다. 타임스탬프나 알파벳 순서와 같이 많은 키 값을 사용하면 속한 파티션의 읽기/쓰기에 과부하가 올 수 있습니다. 다음은 버킷 경로 `examplebucket-1250000000.cos.ap-beijing.myqcloud.com`을 사례로 인덱스가 과부하되는 상황을 소개합니다.

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

비지니스에서 통상적으로 초당 3만 개를 초과하는 요청이 발생하는 경우, 상술한 예시의 순서에 따라 키 값을 정렬하지 마십시오. 순번이나 날짜, 시간 등의 문자로 객체 키를 설정해야 하는 비즈니스라면 객체 키 이름에 랜덤 접두사를 추가하는 식으로 여러 인덱스 파티션에 대한 키 값을 관리하여 과부하 상황에서 성능을 향상시킬 수 있습니다. 다음은 키 값에 랜덤 방식을 적용하는 방법입니다.

>다음 소개하는 방식들은 개별 버킷의 액세스 성능을 강화하는 데 한정될 수 있습니다. 통상적으로 초당 3만 개를 초과하는 요청이 발생하는 비즈니스라면 다음 방식을 실행하는 한편, 비즈니스 부하 개선을 위한 사전 조치가 필요하므로 [고객센터](https://intl.cloud.tencent.com/support)로 문의하십시오.

#### 16진법 해시 접두사 추가

객체 키에 랜덤성을 부여할 수 있는 가장 직접적인 방법입니다. 객체 키 이름 앞에 해시 문자열을 접두사로 추가합니다. 예를 들어 객체를 업로드할 때 경로 키 값에 SHA1이나 MD5 ComputeHash를 실행한 뒤 몇 바이트의 문자를 접두사로 선택하여 키 값 이름 앞에 붙입니다. 보통 2~4바이트의 문자를 해시 접두사로 설정하면 사용에 무리가 없습니다.
<pre>
<font color="red">faf1</font>-20170701/log120000.tar.gz
<font color="red">e073</font>-20170701/log120500.tar.gz
<font color="red">333c</font>-20170701/log121000.tar.gz
<font color="red">2c32</font>-20170701/log121500.tar.gz
</pre>

>Tencent Cloud COS의 키 값 인덱스는 UTF-8 이진법 순서를 인덱스로 설정하기 때문에 객체 나열(GET Bucket) 작업을 실행할 때 해당 작업을 65536번 실행해야 완전한 20170701 접두사 구조를 출력할 수 있습니다.

#### 열거 값 접두사 추가

객체 키 인덱스를 간편하게 관리하고 싶다면 파일 유형에 열거형 접두사를 추가하여 객체를 그룹화할 수 있습니다. 동일한 열거 값 접두사로 묶인 인덱스 파티션의 기능을 공유하게 됩니다.

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

동일한 열거형 접두사를 추가한 상태에서 초당 3만 개가 넘는 요청이 지속적으로 발생하는 액세스 과부하가 일어난다면 상술한 16진법 해시 접두사 방식을 활용하십시오. 열거 값 뒤에 해시 접두사를 추가해 여러 개의 인덱스 파티션을 실행하면 읽기/쓰기 성능을 높일 수 있습니다.
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

#### 키 값 이름 문자열 순서 뒤집기

비즈니스 특성상 ID나 날짜가 지속적으로 증가하거나 한 번에 대량의 연속 접두사 객체를 업로드해야 할 경우, 일반적으로 다음의 방법을 활용할 수 있습니다.

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

위와 같은 방법으로 키 값의 이름을 생성하면 2017과 ID가 접두사인 키 값이 속한 인덱스 파티션이 쉽게 과부하됩니다. 이때 키 값 접두사 일부의 순서를 뒤집은 뒤 랜덤성을 부여할 수 있습니다.

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

### GET 요청 과부하

비즈니스 특성상 주로 GET 요청(다운로드 요청) 부하가 발생한다면 상술한 방법 외에도 Tencent Cloud의 CDN 서비스를 함께 사용하는 것을 권장합니다.

Tencent Cloud의 CDN은 전국 및 전 세계에 분포한 엣지 가속 노드를 이용하여 낮은 딜레이와 빠른 속도로 사용자에게 콘텐츠를 전송합니다. 핫 파일은 프리패치 방식으로 캐싱함으로써 COS로 Origin-pull되는 GET 요청 수를 줄입니다. 자세한 내용은 [도메인 관리](https://intl.cloud.tencent.com/document/product/436/18424) 문서를 참조하십시오.
