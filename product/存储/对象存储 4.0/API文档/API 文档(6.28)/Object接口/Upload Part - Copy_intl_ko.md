## 기능 설명
Upload Part - Copy 요청은 객체의 파트 내용을 소스 경로에서 대상 경로로 복사합니다. x-cos-copy-source를 통해 소스 객체를 지정하며, x-cos-copy-source-range를 통해 바이트 범위(파트의 크기는 5MB - 5GB)를 지정합니다.

>!
>- 대상 개체와 소스 개체가 각기 다른 지역에 속하고 대상 개체 파트가 5GB를 초과하면 멀티파트 업로드 또는 파트 복사 API를 통해 객체를 복사해야 합니다.
>- 파트 객체 업로드를 사용하려면 우선 멀티파트 업로드를 초기화해야 합니다. 멀티파트 업로드 초기화 응답에서 유일한 설명자(upload ID) 1개를 반환합니다. 멀티파트 업로드 요청에 이 ID를 휴대해야 합니다.

### 버전
버킷이 여러 버전을 활성화하였을 경우, x-cos-copy-source는 복사된 개체의 현재 버전을 식별합니다. 현재 버전이 삭제 표기이고 x-cos-copy-source가 버전을 지정하지 않았을 경우, COS는 해당 개체가 삭제된 것으로 식별하고 404 오류를 반환합니다. x-cos-copy-sourceand에서 versionId를 지정하고 versionId가 삭제 표기일 경우, COS는 HTTP 400 오류를 반환합니다. 삭제 표기는 x-cos-copy-source 버전으로 사용할 수 없기 때문입니다.

## 요청
### 요청 예제

```http
PUT /examplebucket?partNumber=PartNumber&uploadId=UploadId  HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
x-cos-copy-source: <Bucketname>-<APPID>.cos.<Region>.myqcloud.com/filepath
x-cos-copy-source-range: bytes=first-last
x-cos-copy-source-if-match: etag
x-cos-copy-source-if-none-match : etag
x-cos-copy-source-if-unmodified-since: time_stamp
x-cos-copy-source-if-modified-since: time_stamp
```

>Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하십시오.).


### 요청 헤더

#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 문서를 참조하십시오.

#### 비공통 헤더

**필수 헤더**

해당 요청 작업은 다음 필수 헤더를 사용하여 구현됩니다.

| 이름         | 설명           | 유형     | 필수 여부   |
| ----------- | ----------- | ------------- | ---- |
| x-cos-copy-source     | 소스 개체 URL 경로로 versionid 서브 리소스를 통해 히스토리 버전을 지정할 수 있습니다.         | String | 예    |


**추천 헤더**

해당 요청 작업은 다음 추천 요청 헤더 정보를 사용하여 구현됩니다.

| 이름          | 설명      | 유형     | 필수 여부   |
| ---------------- | ---------- | ------ | -------- |
| x-cos-copy-source-range                    | 소스 개체의 바이트 범위로 범위값은 반드시 bytes=first-last 형식을 사용해야 합니다. first와 last 모두 0부터 시작하는 오프셋을 기반으로 합니다. <br>예를 들어 bytes=0-9는 소스 개체의 맨 처음 10개 바이트 데이터를 복사하길 원함을 의미합니다. 지정하지 않으면 전체 개체 복사를 의미합니다.       | Integer | 예    |
| x-cos-copy-source-If-Modified-Since   | Object가 지정 시간 후 수정되면 작업을 실행하고, 그렇지 않을 경우 412를 반환합니다. <br>x-cos-copy-source-If-None-Match와 함께 사용할 수 있으며, 기타 조건과 함께 사용하면 충돌을 반환합니다. | string | 아니요    |
| x-cos-copy-source-If-Unmodified-Since | Object가 지정 시간 후 수정되지 않으면 작업을 실행하고, 그렇지 않을 경우 412를 반환합니다. <br>x-cos-copy-source-If-Match와 함께 사용할 수 있으며, 기타 조건과 함께 사용하면 충돌을 반환합니다. | string | 아니요    |
| x-cos-copy-source-If-Match            | Object의 Etag가 주어진 것과 일치할 경우 작업을 실행하며, 그렇지 않을 경우 412를 반환합니다. <br>x-cos-copy-source-If-Unmodified-Since와 함께 사용할 수 있으며 기타 조건과 함께 사용하면 충돌을 반환합니다. | String | 아니요    |
| x-cos-copy-source-If-None-Match       | Object의 Etag가 주어진 것과 일치하지 않을 경우 작업을 실행하며, 그렇지 않을 경우 412를 반환합니다. <br>x-cos-copy-source-If-Modified-Since와 함께 사용할 수 있으며 기타 조건과 함께 사용하면 충돌을 반환합니다. | string | 아니요    |

### 요청 매개 변수

 이름|설명|유형|필수 여부
---|---|---|---
partNumber|파트 복사의 파트 번호|string|예
uploadId|파트 파일 업로드를 사용하려면 우선 멀티파트 업로드를 초기화해야 합니다. 멀티파트 업로드 초기화 응답에서 유일한 설명자(upload ID) 1개를 반환합니다. 멀티파트 업로드 요청에 이 ID를 휴대해야 합니다.|string|예

### 요청체
해당 요청의 요청체는 비어 있습니다.

## 응답

### 응답 헤더
#### 공통 응답 헤더 
해당 응답은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 문서를 참조하십시오.

#### 고유의 응답 헤더

이름|설명|유형
---|---|---
X-cos-copy-source-version-id|소스 버킷에 버전 제어를 이미 활성화하였다면 소스 개체의 버전을 복사합니다.|string
x-cos-server-side-encryption | COS 관리 서버 암호화를 통해 개체를 저장한 경우, 응답은 이 헤더와 사용한 암호화 알고리즘 값 AES256을 포함합니다. | string

### 응답 본문
해당 응답 본문은 **application/xml** 데이터를 반환합니다. 완전한 노드 데이터를 포함한 내용은 다음과 같습니다.

```shell
<?xml version="1.0" encoding="UTF-8" ?>
<CopyPartResult>
   <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
   <LastModified>2017-09-04T04:45:45</LastModified>
</CopyPartResult>
```

구체적인 데이터 내용은 다음과 같습니다.

| 이름          | 설명             | 유형     |
| ---------- | ------------------- | ------ |
| CopyPartResult | 복사 결과 정보 반환           | String |
| ETag             | 객체의 MD5 알고리즘 검사값을 반환합니다. ETag의 값은 객체의 내용이 변경되었는지 여부를 검사하는 데 사용됩니다. | String |
| LastModified     | 개체의 마지막 수정 시간을 GMT 형식으로 반환합니다.        | String |

## 실제 사례
### 요청

```HTTP
PUT /exampleobject?partNumber=1&uploadId=1505706248ca8373f8a5cd52cb129f4bcf85e11dc8833df34f4f5bcc456c99c42cd1ffa2f9 HTTP/1.1
User-Agent: curl/7.19.7 (x86_64-redhat-linux-gnu) libcurl/7.19.7 NSS/3.13.1.0 zlib/1.2.3 libidn/1.18 libssh2/1.2.2
Accept: */*
x-cos-copy-source:examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/exampleobject1
x-cos-copy-source-range: bytes=10-100
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3MqQCn&q-sign-time=1507530223;1508530223&q-key-time=1507530223;1508530223&q-header-list=&q-url-param-list=&q-signature=d02640c0821c49293e5c289fa07290e6b2f05cb2
```

### 응답

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 133 
Connection: keep-alive 
Date: Mon, 04 Sep 2017 04:45:45 GMT
Server: tencent-cos
x-cos-request-id: NTlkYjFjYWJfMjQ4OGY3MGFfNGIzZV9k

<CopyPartResult>
   <ETag>"ba82b57cfdfda8bd17ad4e5879ebb4fe"</ETag>
   <LastModified>2017-09-04T04:45:45</LastModified>
</CopyPartResult>
```

