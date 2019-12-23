## 기능 설명
Complete Multipart Upload API 요청은 전체 멀티파트 업로드 완성을 구현합니다. Upload Parts를 사용해서 모든 멀티파트를 업로드한 후에는 해당 API를 호출하여 전체 파일의 멀티파트 업로드를 완료해야 합니다. 해당 API를 사용할 경우 멀티파트의 정확성을 검증하도록 요청 본문에서 각 멀티파트의 PartNumber와 ETag를 제시해야 합니다.
멀티파트 업로드가 끝난 후에 합병해야 하고 합병하는 데 몇 분의 시간이 필요하기 때문에 파트를 합병하기 시작할 때 COS가 즉시 200의 상태 코드를 반환합니다. 합병 과정에서 합병이 완료될 때까지 COS는 주기적으로 스페이스 메시지를 반환하여 연결이 활성화되도록 유지하고, COS는 본문에서 합병된 후의 파트 내용을 반환합니다.
- 업로드 파트 크기가 1MB보다 작을 경우 해당 API를 호출하면 400 EntityTooSmall을 반환합니다.
- 업로드 파트 번호가 연속되지 않을 경우 해당 API를 호출하면 400 InvalidPart를 반환합니다.
- 요청 본문 중의 파트 정보가 번호 오름차순으로 배열되지 않을 경우 해당 API를 호출하면 400 InvalidPartOrder를 반환합니다.
- UploadId가 존재하지 않을 경우 해당 API를 호출하면 404 NoSuchUpload를 반환합니다.

>!이미 업로드했지만 중지하지 않은 파트는 저장 공간을 차지하고 비용을 발생하기 때문에 즉시 멀티파트 업로드를 완료하거나 멀티파트 업로드를 포기하도록 권장합니다.

## 요청

### 요청 예제
```shell
POST /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조하십시오.)


### 요청 헤더

#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 섹션을 참조하십시오.

#### 비공통 헤더
해당 요청 작업은 특별한 요청 헤더 정보가 없습니다.

### 요청체
해당 API 요청 본문의 구체적인 노드 내용은 다음과 같습니다.
```shell
<CompleteMultipartUpload>
  <Part>
    <PartNumber>1</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9773"</ETag>
  </Part>
  <Part>
    <PartNumber>2</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9773"</ETag>
  </Part>
    ...
</CompleteMultipartUpload>
```

구체적인 데이터 내용은 다음과 같습니다.

| 노드 이름(키워드)              | 부모 노드  | 설명              | 유형        | 필수 선택 여부   |
| :---------------------- | :--- | :-------------- | :-------- | :--- |
| CompleteMultipartUpload | 없음    | 이번 멀티파트 업로드의 모든 정보를 설명하는 데 사용됩니다. | Container | 예    |

Container 노드 CompleteMultipartUpload의 내용:

| 노드 이름(키워드) | 부모 노드                     | 설명                | 유형        | 필수 여부   |
| :-------- | :---------------------- | :---------------- | :-------- | :--- |
| Part      | CompleteMultipartUpload | 이번 멀티파트 업로드 중 모든 파트의 정보를 설명하는 데 사용됩니다. | Container | 예    |

Container 노드 Part의 내용:

| 노드 이름(키워드)  | 부모 노드                          | 설명               | 유형      | 필수 선택 여부   |
| :--------- | :--------------------------- | :--------------- | :------ | :--- |
| PartNumber | CompleteMultipartUpload.Part | 파트 번호              | Integer | 예    |
| ETag       | CompleteMultipartUpload.Part | 모든 파트 파일의 MD5 알고리즘 검사값 | String  | 예    |

## 응답

### 응답 헤더
#### 공통 응답 헤더
해당 응답은 공통 응답 헤더를 사용합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.
#### 고유의 응답 헤더
**서버 암호화 관련 응답**

업로드 시 서버 암호화 사용을 지정한 경우, 응답 헤더는 다음 정보를 포함하게 됩니다.

| 이름                           | 설명                                       | 유형     |
| ---------------------------- | ---------------------------------------- | ------ |
| x-cos-server-side-encryption | 개체에 서버 암호화를 활성화하는 방식을 지정합니다.<br/>COS 기본 키를 사용하여 암호화: AES256 | String |

### 응답 본문
해당 응답 본문은 **application/xml** 데이터를 반환합니다. 완전한 노드 데이터를 포함한 내용은 다음과 같습니다.
```shell
<CompleteMultipartUploadResult>
    <Location>examplebucket-1250000000.cos.ap-beijing.myqcloud.com/ObjectName</Location>
    <Bucket>examplebucket-1250000000</Bucket>
    <Key>examplebucket</Key>
    <ETag>"3a0f1fd698c235af9cf098cb74aa25bc"</ETag>
</CompleteMultipartUploadResult>
```
구체적인 데이터 내용은 다음과 같습니다.

| 노드 이름(키워드)                    | 부모 노드  | 설명       | 유형        |
| :---------------------------- | :--- | :------- | :-------- |
| CompleteMultipartUploadResult | 없음    | 모든 반환 정보를 설명합니다. | Container |

Container 노드 CompleteMultipartUploadResult의 내용:

| 노드 이름(키워드) | 부모 노드                           | 설명                                       | 유형     |
| :-------- | :---------------------------- | :--------------------------------------- | :----- |
| Location  | CompleteMultipartUploadResult | 생성한 객체의 공중망 접근 도메인 이름                         | URL    |
| Bucket | CompleteMultipartUploadResult  | 멀티파트 업로드 대상 버킷은 사용자 지정 문자열과 시스템이 생성한 appid 숫자열을 대시로 연결하여 생성됩니다. 예: examplebucket-1250000000 | String |
| Key       | CompleteMultipartUploadResult | 객체 이름                                | String |
| ETag      | CompleteMultipartUploadResult | 합병 후 객체의 유일한 태그값으로 해당 값은 객체 내용의 MD5 검증값이 아니며 객체의 유일성을 검사하는 데만 사용됩니다.                        | String |

## 실제 사례

### 요청
```shell
POST /exampleobject?uploadId=1484728886e63106e87d8207536ae8521c89c42a436fe23bb58854a7bb5e87b7d77d4ddc48 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484729794;32557625794&q-key-time=1484729794;32557625794&q-header-list=host&q-url-param-list=uploadId&q-signature=23627c8fddb3823cce4257b33c663fd83f9f820d
Content-Length: 138

<CompleteMultipartUpload>
  <Part>
    <PartNumber>1</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9773"</ETag>
  </Part>
  <Part>
    <PartNumber>2</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9774"</ETag>
  </Part>
</CompleteMultipartUpload>
```

### 응답
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 277
Connection: keep-alive
Date: Wed，18 Jan 2017 16:17:03 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjJlMjVfNDYyMDRlXzM0YzRfMjc1

<CompleteMultipartUploadResult>
    <Location>examplebucket-1250000000.cos.ap-beijing.myqcloud.com/ObjectName</Location>
    <Bucket>examplebucket-1250000000</Bucket>
    <Key>examplebucket</Key>
    <ETag>"3a0f1fd698c235af9cf098cb74aa25bc"</ETag>
</CompleteMultipartUploadResult>
```
