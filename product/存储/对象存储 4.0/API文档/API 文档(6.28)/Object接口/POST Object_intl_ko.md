## 기능 설명
POST Object API 요청은 사용자가 표 형식으로 파일(Object)을 지정된 Bucket에 업로드하도록 합니다. 해당 작업은 요청자가 Bucket에 대한 WRITE 권한을 보유해야 합니다. HTTP 헤더를 휴대한 API 매개 변수는 모두 표 필드 요청를 사용합니다.

### 버전

버킷에 버전 제어를 활성화하면, POST 작업은 추가해야 할 개체에 자동으로 유일한 버전 ID를 생성합니다. COS는 x-cos-version-id 응답 헤더를 사용하여 응답에서 이 ID를 반환합니다.
버킷의 버전 제어를 일시 정지해야 할 경우, COS는 줄곧 해당 null을 버킷에 저장한 개체의 버전 ID로 사용합니다.

### 세부 분석
1. Bucket의 쓰기 권한이 필요합니다.
3. 추가를 시도한 Object의 같은 이름의 파일이 이미 존재할 경우, 새로 업로드한 파일은 기존 파일을 덮어쓰며 성공 시, 200 OK를 반환합니다.

## 요청
### 요청 예제

```shell
POST / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: length
Headers
Form
```

### 요청 헤더

#### 공통 헤더

해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728 "공통 요청 헤더") 문서를 참조하십시오.

#### 비공통 헤더
해당 요청 작업은 다음 필수 요청 헤더를 사용해야 합니다.

|이름|설명|유형| 필수|
|:---|:-- |:---|:-- |
| Content-Length | RFC 2616에서 정의한 HTTP 요청 내용 길이(바이트)입니다.| String | 예 |

### 표 필드

<table>
   <tr>
      <th>이름</td>
      <th>설명</td>
      <th>유형</td>
      <th>필수 여부</td>
   </tr>
   <tr>
      <td>acl</td>
      <td>Object의 ACL 속성을 정의합니다. 유효값은 private, public-read, default이며, 기본값은 default(버킷 권한 승계)입니다. <br>주의: 현재 접근 정책 항목은 1000개로 제한됩니다. Object ACL 제어를 진행할 필요가 없다면, default를 입력하거나 이 항목을 설정하지 마십시오. 버킷 권한 승계를 기본으로 합니다.</td>
      <td>String</td>
      <td>아니요</td>
   </tr>
   <tr>
      <td>Cache-Control, Content-Type, Content-Disposition, Content-Encoding, Expires</td>
      <td>RFC 2616에서 정의한 헤더입니다. 상세한 내용은 <a href="https://cloud.tencent.com/document/product/436/7749">PUT Object</a> 문서를 참조하십시오.</td>
      <td>String</td>
      <td>아니요</td>
   </tr>
   <tr>
      <td>file</td>
      <td>파일 내용을 표의 마지막 필드로 합니다.</td>
      <td>String</td>
      <td>예</td>
   </tr>
   <tr>
      <td>key</td>
      <td>업로드 후 파일 이름, ${filename}을 사용하면 교체가 진행됩니다. 예를 들어 a/b/${filename}, 파일 photo.jpg가 업로드될 경우, 최종 업로드 경로는 a/b/photo.jpg입니다.</td>
      <td>String</td>
      <td>예</td>
   </tr>
   <tr>
      <td>success_action_redirect</td>
      <td>우선 적용을 설정하면 303을 반환하고 Location 헤더를 제공하며 URL 끝부분에 bucket={bucket}&key={key}&etag={%22etag%22} 매개 변수를 추가합니다.</td>
      <td>String</td>
      <td>아니요</td>
   </tr>
   <tr>
      <td>success_action_status</td>
      <td>200, 201, 204를 선택할 수 있으며 기본적으로 204를 반환합니다. Success_action_redirect를 입력하면 이 설정이 생략됩니다.</td>
      <td>String</td>
      <td>아니요</td>
   </tr>
   <tr>
      <td>x-cos-meta-*</td>
      <td>사용자 지정 헤더 접미사와 사용자 지정 헤더 정보를 포함하며, Object 메타데이터로 반환할 예정이며, 크기는 2KB로 제한합니다. 주의: 사용자 지정 헤더 정보는 밑줄을 지원하지만, 사용자 지정 헤더 접미사는 밑줄을 지원하지 않습니다.</td>
      <td>String</td>
      <td>아니요</td>
   </tr>
   <tr>
      <td>x-cos-storage-class</td>
      <td>Object의 스토리지 클래스를 설정합니다. 열거값: STANDARD, STANDARD_IA, 기본값: STANDARD</td>
      <td>String</td>
      <td>아니요</td>
   </tr>
   <tr>
      <td>policy</td>
      <td>Base64 인코딩이며 요청 검사에 사용됩니다. 요청한 내용은 Policy 지정 조건에 부합하지 않으면 403 AccessDenied를 반환합니다.</td>
      <td>String</td>
      <td>아니요</td>
   </tr>
   <tr>
      <td>x-cos-server-side-encryption</td>
      <td>개체에 서버 암호화를 활성화하는 방식을 지정합니다. COS 기본 키를 사용하여 암호화할 때, AES256을 입력합니다.</td>
      <td>String</td>
      <td nowrap="nowrap">암호화가 필요한 경우, 예</td>
   </tr>
</table>

#### 서명 보호

표로 HTTP POST 요청을 업로드할 때 서명 보호가 필요한 경우, 표는 다음과 같이 내용 구조의 form-data 내용을 포함합니다.

| 표 필드         | 설명                                                         |
| ---------------- | ----------------------------------------- |
| policy           | Base64 암호화를 통한 정책 내용으로 정책 내용은 요청 내용을 검사하는 데 사용됩니다. 요청 내용과 정책 지정 조건에 부합하지 않을 경우, 요청이 거절됩니다. |
| q-sign-algorithm | 서명 알고리즘을 계산하는 데 사용되며, Tencent Cloud COS는 현재 SHA1을 지원합니다. 여기에는 소문자 `sha1`을 입력합니다. |
| q-ak             | 사용자의 Tencent Cloud 계정 키 ID, 즉 SecretId입니다.                     |
| q-key-time      | 서명 요청에 사용될 키의 유효 시작 및 종료 시간입니다. Unix 타임스탬프를 통해 시작 및 종료 시간을 초 단위로 설명하며, 형식은 [start-seconds];[end-seconds]입니다. 예를 들어, `1480932292;1481012298`입니다. |
| q-signature      | 상기 요소로 계산한 요청 서명이며, COS는 표 요소와 서명 내용을 사용하여 검사합니다. 서명이 내용과 일치하지 않을 경우, 요청은 거절됩니다. |

#### 서명 계산

서명 q-signature 계산은 세 가지 절차로 나뉩니다.

1. 키 내용을 사용하여 q-key-time의 시간에 대해 계산값 SignKey를 암호화합니다.
2. 1개의 POST 요청 policy를 생성하고 내용을 sha1 암호화하여 StringToSign을 획득합니다.
3. SignKey를 사용하여 StringToSign에 대해 암호화하여 Signature를 생성합니다.

#### Policy
다음은 완전한 policy 예시입니다.

```shell
{ "expiration": "2007-12-01T12:00:00.000Z",
  "conditions": [
    {"acl": "public-read" },
    {"bucket": "examplebucket-1250000000" },
    ["starts-with", "$key", "user/eric/"],
    {"q-sign-algorithm": "sha1" },
    {"q-ak": "AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q" },
    {"q-sign-time": "1480932292;1481012298" }
  ]
}
```

**Expiration**
해당 POST Policy 의 타임아웃 시간을 설정하고, ISO8601 GMT 시간을 사용합니다. 예를 들어 2017-12-01T12:00:00.000Z입니다.

**Conditions 규칙**

| 유형   | 설명                                       |
| ---- | ---------------------------------------- |
| 완전 매칭 | `{"key": "value"}` 또는 `["eq", "$key", "value"]` 방식을 사용하여 표현합니다 |
| 접두사 매칭 | `["starts-with", "$key", "value"]` 방식을 사용하여 표현합니다. value는 비워둘 수 있습니다. |
| 범위 매칭 | `["content-length-range", int1, int2]`에만 사용할 경우 파일 바이트 수는 반드시 int1과 int2 범위 내여야만 합니다.|

**Conditions 매개 변수**
모든 매개 변수는 필수 선택이 아니며, 입력하지 않으면 검사하지 않습니다.

| 이름             | 설명             | 매칭 방식  |
| --------------- | ---------------------- | ----- |
| acl                     | 파일 ACL 속성의 허가 범위, 입력하지 않아도 됩니다.                       | 완전 매칭, 접두사 매칭 |
| bucket                  | 업로드한 Bucket 지정                             | 완전 매칭    |
| content-length-range    | 파일의 업로드 크기 범위 지정                              | 범위 매칭    |
| key                     | 개체의 저장 경로                                  | 완전 매칭, 접두사 매칭 |
| success_action_redirect | 업로드 성공 후 반환된 URL                             | 완전 매칭, 접두사 매칭 |
| success_action_status   | 업로드 성공 후 반환된 상태                               | 완전 매칭    |
| x-cos-meta-\*            | 사용자 지정 헤더 접미사와 사용자 지정 헤더 정보를 포함하고, Object 메타데이터로 반환되며, 크기는 2KB로 제한합니다. <br>**주의: **사용자 지정 헤더 정보는 밑줄을 지원하지만, 사용자 지정 헤더 접미사는 밑줄을 지원하지 않습니다.  | 완전 매칭, 접두사 매칭 |
| x-cos-\*      | 기타 서명해야 할 COS 헤더            | 완전 매칭    |


## 응답
### 응답 헤더
#### 공통 응답 헤더
해당 응답은 공통 응답 헤더를 사용합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 문서를 참조하십시오.

#### 고유의 응답 헤더
해당 요청은 다음 응답 헤더를 반환합니다.

|이름|설명|유형|
|:---|:-- |:-- |
|Success_action_redirect|업로드 성공 시 클라이언트가 리디렉션하는 URL|String|
|X-cos-version-id|대상 버킷에 복사한 개체의 버전입니다. 활성화 또는 활성화 후 일시 정지한 버킷이어야만 이 헤더를 응답하게 됩니다.|String|
|x-cos-server-side-encryption|COS 관리 서버 암호화를 통해 개체를 저장하는 경우, 응답은 이 헤더와 사용한 암호화 알고리즘 값을 포함합니다. AES256|string|


### 응답 매개 변수
|이름|설명|유형|
|:---|:-- |:-- |
| ETag| 파일의 MD5 알고리즘 검사값을 반환합니다. ETag 값은 Object가 업로드 과정 중 훼손 여부를 검사하는 데 사용할 수 있습니다.|String|
| Location| success_action_redirect 업로드를 지정한 경우 해당 값을 반환하고, 지정하지 않은 경우 개체의 완전한 경로를 반환합니다.|String|


### 응답 본문
해당 응답 본문은 application/xml 데이터를 반환합니다. 완전한 노드 데이터를 포함한 내용은 다음과 같습니다.

```shell
<PostResponse>
        <Location>http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/photo.jpg</Location>
        <Bucket>examplebucket-1250000000</Bucket>
        <Key>photo.jpg</Key>
        <ETag>d41d8cd98f00b204e9800998ecf8427e</ETag>
</PostResponse>
```

구체적인 데이터 설명은 다음과 같습니다.

|노드 이름(키워드)|부모 노드|설명|유형|필수 여부|
|:---|:-- |:--|:--|:--|
| PostResponse |없음| POST Object 결과를 저장하는 컨테이너 | Container |예|

Container 노드 PostResponse의 내용:

|노드 이름(키워드)|부모 노드|설명|유형|필수 여부|
|:---|:-- |:--|:--|:--|
| Location | PostResponse | 개체의 완전한 경로 |  String |예|
| Bucket | PostResponse | 개체가 위치한 버킷 |  String |예|
| Key | PostResponse | 개체 key 이름 |  String |예|
| ETag | PostResponse | Etag 내용 |  String |예|

### 오류 코드
다음은 이 요청이 일으킬 수 있는 일부 특수하지만 흔히 볼 수 있는 오류 상황입니다. COS 오류 코드와 관련하여 더 많은 정보를 획득하려면 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

| 오류 코드                  |   HTTP 상태 코드                                      |    설명       |
| ------------------- | --------------------------------------- | ------------------ |
| InvalidDigest        |400 Bad Request     | 사용자가 파일을 업로드할 때 Content-MD5 헤더를 휴대하면, COS는 body의 Md5와 사용자가 휴대한 Md5가 일치하는지 검사를 합니다. 일치하지 않을 경우 InvalidDigest를 반환합니다. |
| KeyTooLong           |400 Bad Request     | 파일을 업로드할 때 휴대한 x-cos-meta로 시작하는 사용자 지정 헤더입니다. 단일 사용자 지정 헤더의 key와 value는 4k를 초과하면 KeyTooLong 오류를 반환합니다. |
| MissingContentLength | 411 Length Required |파일을 업로드할 때 Content-Length 헤더를 추가하지 않으면 해당 오류 코드를 반환합니다.     |
| NoSuchBucket         | 404 Not Found       |추가를 시도한 Object가 위치한 Bucket이 존재하지 않으면, 404 Not Found 오류를 반환하며 오류 코드는 NoSuchBucket입니다. |
| EntityTooLarge       | 400 Bad Request     |추가한 파일 길이가 5G를 초과하면 EntityTooLarge를 반환하고 오류 정보 `"Your proposed upload exceeds the maximum allowed object size"`를 반환합니다. |
| InvalidURI           | 400 Bad Request     | 개체 key의 길이는 850으로 제한합니다. 850을 초과하면 InvalidURI를 반환합니다.      |


## 실제 사례
### 요청

```
POST / HTTP/1.1
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 1352
Content-Type: multipart/form-data; boundary=e07f2a7876ae4755ae18d300807ad879

--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="key"

a/${filename}
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="success_action_status"

201
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="Acl"

public-read
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="x-cos-storage-class"

STANDARD
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="Signature"

q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1512983814;1512984814&q-key-time=1512983814;1512984814&q-url-param-list=&q-header-list=host&q-signature=2ffd2ae714e7445a8da000ec5d51771ff5056500
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjogW3siYnVja2V0IjogImtpdG1hbnMzdGVzdDEifSwgWyJjb250ZW50LWxlbmd0aC1yYW5nZSIsIDAsIDEwMDAwMDAwXSwgWyJzdGFydHMtd2l0aCIsICJ4LWNvcy1tZXRhLWJiIiwgIjEyIl1dLCAiZXhwaXJhdGlvbiI6ICIyMDQ3LTEyLTAxVDEyOjAwOjAwLjAwMFoifQ==
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="x-Cos-meta-bb"

124
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="key1"

1
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="file"; filename="empty:a"


--e07f2a7876ae4755ae18d300807ad879--
```

### 응답

```shell
HTTP/1.1 204
Content-Type: application/xml
Content-Length: 232
Connection: keep-alive
Date: Mon, 11 Dec 2017 09:16:56 GMT
ETag: "d41d8cd98f00b204e9800998ecf8427e"
Location: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/photo.jpg
Server: tencent-cos
x-cos-request-id: NWEyZTRkMDZfMjQ4OGY3MGFfNTE4Yl81
```
