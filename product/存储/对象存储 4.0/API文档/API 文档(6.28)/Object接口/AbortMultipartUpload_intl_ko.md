## 기능 설명
Abort Multipart Upload는 하나의 멀티파트 업로드를 중단하고 이미 업로드한 파트를 삭제하는 것을 구현합니다. Abort Multipart Upload를 호출하면 이 Upload Parts 업로드 멀티파트가 사용 중인 경우 Upload Parts는 실패를 반환합니다. 해당 UploadId가 존재하지 않으면 404 NoSuchUpload를 반환합니다.

>!이미 업로드했지만 중지하지 않은 파트는 저장 공간을 차지하고 비용을 발생하기 때문에 즉시 멀티파트 업로드를 완료하거나 멀티파트 업로드를 포기하도록 권장합니다.

## 요청

### 요청 예제
```shell
DELETE /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조).

#### 요청 매개변수

구체적인 내용은 다음과 같습니다.

|매개변수 이름|설명|유형|필수 선택 여부|
|---|---|---|---|
|uploadId| 이번 멀티파트 업로드를 식별하는 ID. <br>Initiate Multipart Upload API로 멀티파트 업로드를 초기화하면 하나의 uploadId를 얻게 되며, 해당 ID는 이 파트 데이터를 유일하게 식별할 뿐만 아니라 전체 파일 내에서 이 파트 데이터의 상대적인 위치를 식별합니다. |String|예|

### 요청 헤더

#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 문서를 참조하십시오.

#### 비공통 헤더
해당 요청 작업은 특별한 요청 헤더 정보가 없습니다.


### 요청체
해당 요청의 요청 본문은 비어 있습니다.

## 응답

### 응답 헤더
#### 공통 응답 헤더
해당 응답은 공통 응답 헤더를 사용합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 문서를 참조하십시오.
#### 고유의 응답 헤더
해당 요청은 특별한 요청 헤더가 없습니다.


### 응답 본문
해당 요청의 응답 본문은 비어 있습니다.


## 실제 사례

### 요청
```shell
DELETE /exampleobject?uploadId=1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 26 Oct 2013 21:22:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484728626;32557624626&q-key-time=1484728626;32557624626&q-header-list=host&q-url-param-list=uploadId&q-signature=2d3036b57cade4a257b48a3a5dc922779a562b18
```

### 응답
```shell
HTTP/1.1 204 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Tue, 26 Oct 2013 21:22:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjI5MzlfOTgxZjRlXzZhYjNfMjBh
```
