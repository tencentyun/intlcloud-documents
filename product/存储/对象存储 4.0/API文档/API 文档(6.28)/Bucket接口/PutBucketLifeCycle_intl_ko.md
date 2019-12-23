## 기능 설명
COS는 사용자가 수명 주기 구성의 방식으로 버킷의 객체 수명 주기를 관리할 수 있도록 지원합니다. 수명 주기 구성에는 한 세트의 객체 규칙에 적용될 한 개 또는 여러 개의 규칙 그룹이 포함됩니다(그 중 각 규칙은 COS에 대한 작업을 정의).
이러한 작업은 다음 두 가지 유형으로 구분됩니다.
- **전환 작업: **객체를 다른 스토리지 유형으로 전환하는 시간을 정의합니다. 예를 들어, 객체 생성 30일 후 객체를 저빈도 소토리지(STANDARD_IA, 드문 접근에 적용) 유형으로 전환할 수 있습니다. 동시에 데이터를 보관 스토리지(Archive, 비용이 더 낮으며 현재 중국 대륙 지역 지원)에 보관할 수 있습니다. 구체적인 매개변수는 요청 예시 중 Transition 항목을 참조하십시오.
- **만료 작업: **객체의 만료 시간을 지정합니다. COS는 만료된 객체를 자동 삭제합니다.

### 세부 분석

Put Bucket Lifecycle은 Bucket에 대한 새로운 수명 주기 구성을 생성하는 데 사용됩니다. 해당 Bucket에 수명 주기가 이미 구성되었으면, 해당 API를 사용하여 새 구성을 작성하는 동시에 원래 구성을 덮어 쓰게 됩니다.

## 요청
### 요청 예제

```shell
PUT /?lifecycle HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: length
Date: GMT Date
Authorization: Auth String
Content-MD5: MD5
```
>Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조).

### 요청 헤더

#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 문서를 참조하십시오.

#### 비공통 헤더

**필수 헤더**
해당 요청 작업은 다음 필수 헤더를 사용하여 구현됩니다.

| 이름               | 설명      | 유형     | 필수 선택 여부   |
| ---------------- | ----------- | ------ | ---- |
| Content-MD5       | RFC 1864에서 정의한 **Base64**로 인코딩된 128-bit 내용 MD5 검사값입니다. 이 헤더는 파일 내용에 변화가 발생 여부를 검사하는 데 사용됩니다.| String | 예    |


### 요청체
해당 API 요청 본문의 구체적인 노드 내용은 다음과 같습니다.

```shell
<LifecycleConfiguration>
  <Rule>
    <ID></ID>
    <Filter>
      <Prefix></Prefix>
    </Filter>
    <Status></Status>
    <Transition>
      <Days></Days>
      <StorageClass></StorageClass>
    </Transition>
    <NoncurrentVersionExpiration>
      <NoncurrentDays></NoncurrentDays>
    </NoncurrentVersionExpiration>
  </Rule>
  <Rule>
    <ID></ID>
    <Filter>
      <Prefix></Prefix>
    </Filter>
    <Status></Status>
    <Transition>
      <Days></Days>
      <StorageClass></StorageClass>
    </Transition>
    <NoncurrentVersionTransition>
      <NoncurrentDays></NoncurrentDays>
      <StorageClass></StorageClass>
    </NoncurrentVersionTransition>
  </Rule>
  <Rule>
    <ID></ID>
    <Filter>
      <Prefix></Prefix>
    </Filter>
    <Status></Status>
    <Expiration>
      <ExpiredObjectDeleteMarker></ExpiredObjectDeleteMarker>
    </Expiration>
    <NoncurrentVersionExpiration>
      <NoncurrentDays></NoncurrentDays>
    </NoncurrentVersionExpiration>
  </Rule>
</LifecycleConfiguration>
```

구체적인 내용 설명은 다음과 같습니다.

|노드 이름(키워드)|    부모 노드|    설명    |유형|    필수 여부|
|---|---|---|---|---|
|LifecycleConfiguration    |없음    |수명 주기 구성    |Container    |예|
|Rule|    LifecycleConfiguration    |규칙 설명    |Container|    예|
|Filter    |LifecycleConfiguration.Rule    |Filter는 규칙이 영향을 주는 객체 집합을 설명하는 데 사용됩니다.    |Container    |예|
|Status    |LifecycleConfiguration.Rule    |규칙 활성화 여부를 지정합니다. 열거형 값: Enabled, Disabled     |Container    |예|
|ID    |LifecycleConfiguration.Rule|규칙을 유일하게 식별하는 데 사용되며, 길이는 255개 문자를 초과할 수 없습니다.    |String    |아니요|
|And    |LifecycleConfiguration.Rule.Filter    |Prefix 조합에 사용됩니다.    |Container    |아니요|
|Prefix    |LifecycleConfiguration.Rule.Filter<br>또는 LifecycleConfiguration.Rule.Filter.And    |규칙에 적용하는 접두사를 지정합니다. 접두사와 매칭한 객체가 해당 규칙의 영향을 받으며, Prefix는 최대 1개만 가능합니다.   |Container    |아니요|
|Expiration    |LifecycleConfiguration.Rule    |규칙 만료 속성    |Container    |아니요|
|Transition    |LifecycleConfiguration.Rule    |규칙 전환 속성으로 객체가 Standard_IA 또는 Archive로 전환되는 시간을 지정합니다.   |Container    |아니요|
|Days    |LifecycleConfiguration.Rule.Transition<br>또는 Expiration    |규칙에 해당하는 동작이 객체 마지막 수정 일자가 지난 며칠 뒤에 작업해야 하는지 지정합니다. Transition일 경우, 해당 필드 유효값은 0과 양의 정수이고, Expiration일 경우, 해당 필드 유효값은 양의 정수이며 최대 3650일을 지원합니다.   |Integer    |아니요|
|Date    |LifecycleConfiguration.Rule.Transition<br>또는 Expiration    |규칙에 해당하는 동작의 작업 시간을 지정합니다.    |String    |아니요|
|ExpiredObjectDeleteMarker    |LifecycleConfiguration.Rule.Expiration    |만료된 객체 삭제 표기입니다. 열거형 값: true, false    |String    |아니요|
|AbortIncompleteMultipartUpload    |LifecycleConfiguration.Rule    |멀티파트 업로드 실행 유지 최대 허가 시간을 설정합니다.    |Container    |아니요|
|DaysAfterInitiation    |LifecycleConfiguration.Rule<br>.AbortIncompleteMultipartUpload    |멀티파트 업로드 시작 후 며칠 이내에 업로드를 완료해야 하는가를 지정합니다.    |Integer    |예|
|NoncurrentVersionExpiration    |LifecycleConfiguration.Rule    |현재 버전이 아닌 객체 만료 시간을 지정합니다.    |Container    |아니요|
|NoncurrentVersionTransition    |LifecycleConfiguration.Rule    |현재 버전이 아닌 객체가 STANDARD_IA 또는 ARCHIVE로 전환되는 시간을 지정합니다.   |Container   |아니요|
|NoncurrentDays    |LifecycleConfiguration.Rule<br>.NoncurrentVersionExpiration<br>또는 NoncurrentVersionTransition    |규칙에 해당하는 동작이 객체가 현재 버전이 아닌 버전으로 변경된 며칠 뒤에 실행되는가를 지정합니다. Transition일 경우, 해당 필드의 유효값은 0과 양의 정수이고, Expiration일 경우, 해당 필드의 유효값은 양의 정수이며 최대 3650일을 지원합니다. |Integer   |아니요|
|StorageClass    |LifecycleConfiguration.Rule.Transition<br>또는 NoncurrentVersionTransition    |객체를 저장한 대상 스토리지 클래스를 지정합니다. 열거형 값: STANDARD_IA, ARCHIVE   |String    |예|


## 응답
### 응답 헤더

#### 공통 응답 헤더
해당 응답은 공통 응답 헤더를 사용합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 문서를 참조하십시오.
#### 고유의 응답 헤더
해당 응답은 특별한 응답 헤더가 없습니다.

### 응답 본문
해당 응답 본문 반환이 비어 있습니다.

### 오류 코드
다음은 이 요청이 일으킬 수 있는 일부 특수하지만 흔히 볼 수 있는 오류 상황을 설명합니다. 구체적인 오류 원인은 반환한 message를 참조하여 검사할 수 있습니다. COS 오류 코드에 대한 세부 정보 또는 제품의 모든 오류 리스트를 획득하려면 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

|오류 코드|HTTP 상태 코드|설명|
|--------|--------|----------|
|NoSuchBucket|404 Not Found|현재 접근한 버킷이 존재하지 않습니다.|
|MalformedXML|400 Bad Request| XML 형식이 잘못되었습니다. restful api 문서와 자세히 비교하십시오. |
|InvalidRequest|400 Bad Reques|요청이 잘못되었습니다. 오류 설명에 "Conflict lifecycle rule"이 표시되었다면 xml 데이터 중 여러 rule에 충돌 부분이 있음을 의미합니다.|
|InvalidArgument|400 Bad Reques|요청 매개 변수가 잘못되었습니다. 오류 설명에 "Rule ID must be unique. Found same ID for more than one rule"이 표시되었다면 이는 여러 개의 Rule ID 필드가 동일함을 의미합니다.|

## 실제 사례

### 요청
```shell
PUT /?lifecycle HTTP/1.1
Host:examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 16 Aug 2017 11:59:33 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1502855771;1502935771&q-key-time=1502855771;1502935771&q-header-list=content-md5;host&q-url-param-list=lifecycle&q-signature=f3aa2c708cfd8d4d36d658de56973c9cf1c24654
Content-MD5: LcNUuow8OSZMrEDnvndw1Q==
Content-Length: 348
Content-Type: application/x-www-form-urlencoded

<LifecycleConfiguration>
  <Rule>
    <ID>id1</ID>
    <Filter>
       <Prefix>documents/</Prefix>
    </Filter>
    <Status>Enabled</Status>
    <Transition>
      <Days>100</Days>
      <StorageClass>ARCHIVE</StorageClass>
    </Transition>
  </Rule>
  <Rule>
    <ID>id2</ID>
    <Filter>
       <Prefix>logs/</Prefix>
    </Filter>
    <Status>Enabled</Status>
    <Expiration>
      <Days>10</Days>
    </Expiration>
  </Rule>
</LifecycleConfiguration>
```

### 응답
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Wed, 16 Aug 2017 11:59:33 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDMzYTRfMjQ4OGY3Xzc3NGRfMWY=
```
