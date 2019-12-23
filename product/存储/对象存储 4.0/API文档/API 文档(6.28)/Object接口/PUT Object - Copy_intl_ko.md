## 기능 설명
PUT Object - Copy 요청은 1개의 파일을 소스 경로에서 대상 경로로 복사합니다. 파일 크기는 1M부터 5G까지로 권장하며, 5G를 초과한 파일은 멀티파트 업로드 Upload - Copy를 사용하십시오. 복사 과정 중, 파일의 메타 속성과 acl은 수정될 수 있습니다.
사용자는 해당 API를 통해 파일 이동, 파일 이름 재설정, 파일 속성 수정과 복제본 생성을 구현할 수 있습니다.

### 버전

기본 상황에서 대상 버킷에서 버전 제어를 활성화하면, COS는 복사 중인 개체에 유일한 버전 ID를 생성합니다. 이 버전 ID는 소스 개체의 버전 ID와 다릅니다. COS는 x-cos-version-id 응답의 응답 헤더에 복사 개체의 버전 ID를 반환합니다.
대상 버킷에 버전 제어를 활성화하지 않았거나 버전 제어를 일시 정지했을 경우, COS가 생성한 버전 ID는 줄곧 null이 됩니다.

>!계정 간 복사의 경우, 먼저 복사할 파일의 권한을 공개 읽기로 하거나 대상 계정에 대한 권한을 부여해야 합니다. 다만, 같은 계정일 경우는 권한 부여할 필요가 없습니다.

## 요청
### 요청 예제

```shell
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
x-cos-copy-source: <BucketName-APPID>.cos.<Region>.myqcloud.com/filepath
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조하십시오.).


### 요청 헤더

#### 공통 헤더

해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 섹션을 참조하십시오.

#### 비공통 헤더

이름|설명|유형|필수 여부
---|---|---|---
x-cos-copy-source|소스 파일 URL 경로로 versionid 서브 리소스를 통해 히스토리 버전을 지정할 수 있습니다.|string|예
X-cos-metadata-directive|소스 파일의 메타데이터 복사 여부, 열거값: Copy, Replaced, 기본값 Copy. Copy로 표기되면, 소스 파일의 메타데이터를 복사합니다. Replaced로 표기되면, 이번 요청의 Header 정보에 따라 메타데이터를 수정합니다. 대상 경로와 소스 경로가 일치할 경우, 즉 사용자가 메타데이터 수정을 시도하면, 표기는 반드시 Replaced여야 합니다.|string|아니요
x-cos-copy-source-If-Modified-Since|Object가 지정 시간 후 수정되면 작업을 실행하고, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-None-Match와 함께 사용할 수 있으며, 기타 조건과 함께 사용하면 충돌을 반환합니다.|string|아니요
x-cos-copy-source-If-Unmodified-Since|Object가 지정 시간 후 수정되면 작업을 실행하고, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-Match와 함께 사용할 수 있으며, 기타 조건과 함께 사용하면 충돌을 반환합니다.|string|아니요
x-cos-copy-source-If-Match|Object의 Etag가 주어진 것과 일치할 경우 작업을 실행하며, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-Unmodified-Since와 함께 사용할 수 있으며 기타 조건과 함께 사용하면 충돌을 반환합니다.|string|아니요
x-cos-copy-source-If-None-Match|Object의 Etag가 주어진 것과 일치하지 않을 경우 작업을 실행하며, 그렇지 않을 경우 412를 반환합니다. x-cos-copy-source-If-Modified-Since와 함께 사용할 수 있으며 기타 조건과 함께 사용하면 충돌을 반환합니다.|string|아니요
x-cos-storage-class|Object의 스토리지 클래스를 설정합니다. 열거값: STANDARD, STANDARD_IA, 기본값: STANDARD|string|아니요
x-cos-acl|Object의 ACL 속성을 정의합니다. 유효값: private, public-read, 기본값: private|string|아니요
x-cos-grant-read|권한을 부여받은 자에게 읽기 권한을 부여합니다. 형식: x-cos-grant-read: id="[OwnerUin]"|string|아니요
x-cos-grant-write|권한을 부여받은 자에게 쓰기 권한을 부여합니다. 형식: x-cos-grant-write: id="[OwnerUin]"|string|아니요
x-cos-grant-full-control | 권한을 부여받은 자에게 모든 권한을 부여합니다. 형식: x-cos-grant-full-control: id='[OwnerUin]' | String|  아니요
x-cos-meta-\*|사용자 지정 헤더 접미사와 사용자 지정 헤더 정보를 포함하고, Object 메타데이터 반환으로 사용하며, 크기는 2KB로 제한합니다. <br>**주의: **사용자 지정 헤더 정보는 밑줄을 지원하지만, 사용자 지정 헤더 접미사는 밑줄을 지원하지 않습니다.|string|아니요

**서버 암호화 관련 헤더**

해당 요청 작업은 Tencent Cloud COS가 데이터를 저장할 때, 응용하는 데이터 암호화 보호 정책을 지정합니다. Tencent Cloud COS는 데이터를 데이터 센터에 입력할 때 자동 암호화하고 해당 데이터를 사용할 때 자동 암호화 해제하도록 도와줍니다. 현재는 Tencent Cloud COS 기본 키를 사용하여 데이터에 AES-256 암호화를 지원합니다. 데이터에 대해 서버 암호화를 활성화해야 할 경우, 다음 헤더를 전달해야 합니다.

| 이름         | 설명          | 유형     | 필수 여부     |
| --------- | ---------- | ------ | ------ |
| x-cos-server-side-encryption | 개체에 서버 암호화를 활성화하는 방식을 지정합니다. <br/>COS 기본 키를 사용하여 암호화할 때, AES256을 입력합니다. | String | 암호화가 필요할 경우, 예 |

### 요청체
해당 요청의 요청체는 비어 있습니다.

## 응답
### 응답 헤더

#### 공통 응답 헤더

해당 응답은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 문서를 참조하십시오.

#### 고유의 응답 헤더

| 이름         | 설명          | 유형     |
| --------- | ---------- | ------ |
|X-cos-version-id|대상 버킷에 복사한 개체의 버전입니다. 활성화 또는 활성화 후 일시 정지한 버킷이어야만 이 매개 변수를 응답하게 됩니다.|String|
| x-cos-server-side-encryption | COS 관리 서버 암호화를 통해 개체를 저장한 경우, 응답은 이 헤더와 사용한 암호화 알고리즘 값을 모두 포함합니다. AES256 | string |

### 응답 본문
해당 응답 본문은 **application/xml** 데이터를 반환합니다. 완전한 노드 데이터를 포함한 내용은 다음과 같습니다.

```shell
<CopyObjectResult>
    <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
    <LastModified>2017-08-04T02:41:45</LastModified>
</CopyObjectResult>
```

구체적인 데이터 내용은 다음과 같습니다.

| 이름               | 설명                                       | 유형     |
| ---------------- | ---------------------------------------- | ------ |
| CopyObjectResult | 복사 결과 정보 반환                                 | String |
| ETag             | 파일의 MD5 알고리즘 검사값을 반환합니다. ETag의 값은 Object의 내용이 변경되었는지 여부를 검사하는 데 사용됩니다. | String |
| LastModified     | 파일의 마지막 수정 시간을 GMT 형식으로 반환합니다.                         | String |


## 실제 사례

### 요청

```shell
PUT /exampleobject HTTP/1.1
Host: destinationbucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 04 Aug 2017 02:41:45 GMT
Connection: keep-alive Accept-Encoding: gzip, deflate Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9SmuG00&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=&q-header-list=host&q-signature=eacefe8e2a0dc8a18741d9a29707b1dfa5aa47cc
x-cos-copy-source: sourcebucket-1250000001.cos.ap-beijing.myqcloud.com/picture.jpg
Content-Length: 0
```

### 응답

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 133
Connection: keep-alive
Date: Fri, 04 Aug 2017 02:41:45 GMT
Server: tencent-cos
x-cos-request-id: NTk4M2RlZTlfZDRiMDM1MGFfYTA1ZV8xMzNlYw==

<CopyObjectResult>
    <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
    <LastModified>2017-08-04T02:41:45</LastModified>
</CopyObjectResult>
```
