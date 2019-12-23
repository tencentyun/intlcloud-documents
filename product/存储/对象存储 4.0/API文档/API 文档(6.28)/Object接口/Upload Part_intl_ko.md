## 기능 설명
Upload Part API 요청은 개체를 멀티파트 방식으로 COS에 업로드합니다. 최대 10000개 멀티파트를 지원하며, 단일 파트의 크기는 1MB부터 5GB까지이며 마지막 1개 파트는 1MB보다 작을 수 있습니다.

### 세부 분석
1. 멀티파트 업로드는 우선 초기화해야 하며, Initiate Multipart Upload API를 사용하여 구현합니다. 초기화 후에는 uploadId 1개를 획득하며 이번 업로드를 유일하게 식별합니다.
2. Upload Part를 요청할 때마다 partNumber와 uploadId, partNumber를 파트 번호로 휴대하여야 하며 비순차적 업로드를 지원합니다.
3. 전달한 uploadId와 partNumber는 모두 같을 경우 나중에 전달한 멀티파트는 이전에 전달한 멀티파트를 덮어씁니다. uploadId가 존재하지 않을 경우 404 오류, NoSuchUpload를 반환합니다.

## 요청
### 요청 예제

```shell
PUT /<ObjectKey>?partNumber=PartNumber&uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: Size
Authorization: Auth String

[Object]
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조하십시오.)

### 요청 헤더

#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 섹션을 참조하십시오.

#### 비공통 헤더
**필수 헤더**
해당 요청 작업은 필수 헤더를 요청 헤더로 사용해야 합니다. 구체적인 내용은 다음과 같습니다.

| 이름             | 설명                            | 유형     | 필수 여부   |
| :------------- | :---------------------------- | :----- | :--- |
| Content-Length | RFC 2616에서 정의한 HTTP 요청 내용 길이(바이트) | String | 예    |

**추천 헤더**
해당 요청 작업은 추천 헤더를 요청 헤더로 사용하길 권장합니다. 구체적인 내용은 다음과 같습니다.

| 이름          | 설명                                       | 유형     | 필수 여부   |
| :---------- | :--------------------------------------- | :----- | :--- |
| Expect      | RFC 2616에서 정의한 HTTP 요청 내용 길이(바이트)            | String | 아니요    |
| Content-MD5 | RFC 1864에서 정의한 Base64로 인코딩된 128-bit 내용 MD5 검사값입니다. 이 헤더는 파일 내용에 변화가 발생했는지 여부를 검사하는 데 사용됩니다. | String | 아니요    |

#### 요청 매개변수
구체적인 내용은 다음과 같습니다.

| 매개 변수 이름       | 설명                                       | 유형     | 필수 여부   |
| :--------- | :--------------------------------------- | :----- | :--- |
| partNumber | 이번 멀티파트 업로드 번호를 식별합니다.                              | String | 예    |
| uploadId   | 이번 멀티파트 업로드를 식별하는 ID. <br>Initiate Multipart Upload API로 멀티파트 업로드를 초기화하면 하나의 uploadId를 얻게 되며, 이 ID는 이 멀티파트 데이터를 유일하게 식별할 뿐만 아니라 전체 파일 내에서 이 멀티파트 데이터의 상대적인 위치를 식별합니다. | String | 예    |

### 요청체
해당 요청의 요청체는 비어 있습니다.

## 응답

### 응답 헤더
#### 공통 응답 헤더 
해당 응답은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.
#### 고유의 응답 헤더
**서버 암호화 응답 헤더**

업로드 시 서버 암호화 사용을 지정한 경우, 응답 헤더는 다음 정보를 포함하게 됩니다.

| 이름                           | 설명                                       | 유형     |
| ---------------------------- | ---------------------------------------- | ------ |
| x-cos-server-side-encryption | 개체에 서버 암호화를 활성화하는 방식을 지정합니다.<br/>COS 기본 키를 사용하여 암호화: AES256 | String |

### 응답 본문
해당 응답 본문은 비어 있습니다.

## 실제 사례

### 요청
```shell
PUT /exampleobject?partNumber=1&uploadId=1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484727403;32557623403&q-key-time=1484727403;32557623403&q-header-list=host&q-url-param-list=partNumber;uploadId&q-signature=bfc54518ca8fc31b3ea287f1ed2a0dd8c8e88a1d
Content-Length: 10485760

[Object]
```

### 응답
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed，18 Jan 2017 16:17:03 GMT
Etag: "e1e5b4965bc7d30880ed6d226f78a5390f1c09fc"
Server: tencent-cos
x-cos-request-id: NTg3ZjI0NzlfOWIxZjRlXzZmNGJfMWYy

```

