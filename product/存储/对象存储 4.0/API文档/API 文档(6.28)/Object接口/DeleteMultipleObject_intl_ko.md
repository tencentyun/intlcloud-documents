## 기능 설명
DELETE Multiple Object API 요청은 지정 버킷에서 객체 일괄 삭제를 구현하며, 1회 요청은 최대 1000개 객체 일괄 삭제를 지원합니다. 응답 결과에 대해 COS는 Verbose와 Quiet 2가지 모드를 제공합니다. Verbose 모드는 각 객체의 삭제 결과를 반환합니다. Quiet 모드는 오류로 보고된 객체 정보만 반환합니다.
>!이 요청은 반드시 Content-MD5를 휴대하여 본문의 무결성을 검사해야 합니다.

### 세부 분석
1. 각 배치 삭제 요청은 최대 1000개의 삭제해야 할 객체만 포함할 수 있습니다.
2. 배치 삭제는 verbose 모드와 quiet 모드 두 가지 모드 반환을 지원하며 verbose 모드를 기본으로 합니다. verbose 모드는 모든 key의 삭제 상황을 반환하며, quiet 모드는 삭제 실패한 key의 상황만 반환합니다.
3. 배치 삭제는 Content-MD5 헤더를 휴대하여 요청 본문이 수정되지 않았음을 검사하는 데 사용됩니다.
4. 배치 삭제 요청은 존재하지 않는 key 삭제를 허가하며 성공한 것으로 간주합니다.

## 요청

구문 예시:
```shell
POST /?delete HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: length
Content-Type: application/xml
Content-MD5: MD5
Authorization: Auth String

<Delete>
  <Quiet></Quiet>
  <Object>
    <Key></Key>
  </Object>
  <Object>
    <Key></Key>
  </Object>
  ...
</Delete>
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조하십시오.).

### 요청행
```shell
POST /?delete HTTP/1.1
```
해당 API는 POST 요청을 수신합니다.

### 요청 헤더

#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 문서를 참조하십시오.

#### 비공통 헤더
**필수 헤더**
해당 요청 작업은 다음 필수 헤더를 사용하여 구현됩니다.
<style rel="stylesheet"> table th:nth-of-type(1) { width: 200px;	} </style>

|이름|설명|유형|필수 선택 여부|
|:---|:---|:---|:---|
| Content-Length | RFC 2616에서 정의한 HTTP 요청 내용 길이(바이트)입니다.| String | 예 |
| Content-MD5 | RFC 1864에서 정의한 Base64로 인코딩된 128-bit 내용 MD5 검증값입니다. 이 헤더는 파일 내용에 변화가 발생했는지 여부를 검사하는 데 사용됩니다.| String | 예 |

### 요청체
해당 요청 본문의 구체적인 노드 내용은 다음과 같습니다.
```shell
<Delete>
  <Quiet></Quiet>
  <Object>
    <Key></Key>
  </Object>
  <Object>
    <Key></Key>
  </Object>
  ...
</Delete>
```

구체적인 내용 설명은 다음과 같습니다.

|노드 이름(키워드)|부모 노드|설명|유형|필수 여부|
|:---|:---|:---|:---|:---|
| DELETE |없음| 이번에 삭제된 반환 결과 방식과 대상 객체를 설명합니다. | Container | 예 |
| Quiet | DELETE|부울값, 이 값은 Quiet 모드 시동 여부를 결정합니다. <br> 값이 true이면 Quiet 모드를 시동하고, 값이 false이면 Verbose 모드를 시동하며 기본값은 False입니다. | Boolean | 아니요 |
| Object |DELETE |삭제해야 할 모든 대상 객체 정보를 설명합니다.| Container | 예 |
| Key | DELETE.Object |대상 객체 파일 이름| String | 예 |


## 응답

### 응답 헤더
#### 공통 응답 헤더 
해당 응답은 공통 응답 헤더를 사용합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 문서를 참조하십시오.
#### 고유의 응답 헤더
해당 요청은 특별한 요청 헤더가 없습니다.

### 응답 본문
해당 응답 본문은 **application/xml** 데이터를 반환합니다. 완전한 노드 데이터를 포함한 내용은 다음과 같습니다.
```shell
<DeleteResult>
  <Deleted>
    <Key></Key>
  </Deleted>
  <Error>
    <Key></Key>
    <Code></Code>
    <Message></Message>
  </Error>
</DeleteResult>
```
구체적인 내용은 다음과 같습니다.

|노드 이름(키워드)|부모 노드|설명|유형|
|:---|:---|:---|:---|
| DeleteResult |없음| 이번에 삭제된 반환 결과 방식과 대상 객체를 설명합니다. | Container | 

Container 노드 DeleteResult의 내용:

|노드 이름(키워드)|부모 노드|설명|유형|
|:---|:---|:---|:---|
| Deleted | DeleteResult |이번에 삭제 성공한 객체 정보를 설명합니다. | Boolean | 
| Error| DeleteResult | 이번에 삭제 실패한 객체 정보를 설명합니다. | Container | 

Container 노드 Deleted의 내용:

|노드 이름(키워드)|부모 노드|설명|유형|
|:---|:---|:---|:---|
| Key | DeleteResult.Deleted | 객체의 이름 | String |

Container 노드 Error의 내용:

|노드 이름(키워드)|부모 노드|설명|유형|
|:---|:---|:---|:---|
| Key | DeleteResult.Error | 삭제 실패한 객체의 이름 | String |
| Code  | DeleteResult.Error | 삭제 실패한 오류 코드 | String |
| Message | DeleteResult.Error | 삭제 실패한 오류 정보 | String |


### 오류 분석
다음은 이 요청이 일으킬 수 있는 특별하지만 흔히 볼 수 있는 오류 상황을 설명합니다.

| 오류 코드            |  HTTP 상태 코드         |설명                                       |
| ------------- | --------------------------------------- | -------------- |
| InvalidRequest | 400 Bad Request |필수 입력 필드 Content-MD5를 휴대하지 않으며, `Missing required header for this request: Content-MD5` 오류 정보를 반환합니다. | 
| MalformedXML   | 400 Bad Request |요청한 key의 개수가 1000을 초과하면 MalformedXML 오류를 반환하며 동시에 `delete key size is greater than 1000`을 반환합니다. | 
| InvalidDigest  | 400 Bad Request |휴대한 Content-MD5와 서버 계산의 요청 본문이 일치하지 않습니다.          | 


COS 오류 코드에 대한 세부 정보 또는 제품의 모든 오류 리스트는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

## 실제 사례

### 요청
```shell
POST /?delete HTTP/1.1
Host: lelu06-1252400000.cos.ap-guangzhou.myqcloud.com
Date: Wed, 23 Oct 2016 21:32:00 GMT
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9SmuG00&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=delete&q-header-list=host&q-signature=c54f22fd92232a76972ba599cba25a8a733d2fef
Content-MD5: yoLiNjQuvB7lu8cEmPafrQ==
Content-Length: 125

<Delete>
  <Quiet>true</Quiet>
  <Object>
    <Key>aa</Key>
  </Object>
  <Object>
    <Key>aaa</Key>
  </Object>
</Delete>
```

### 응답
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 17
Connection: keep-alive
Date: Tue, 22 Aug 2017 12:00:48 GMT
Server: tencent-cos
x-cos-request-id: NTk5YzFjZjBfZWFhZDM1MGFfMjkwZV9lZGM3ZQ==

<DeleteResult/>
```

### 요청
```shell
POST /?delete HTTP/1.1
Host: lelu06-1252400000.cos.ap-guangzhou.myqcloud.com
Date: Tue, 22 Aug 2017 12:16:35 GMT
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9SmuG00&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=delete&q-header-list=host&q-signature=c54f22fd92232a76972ba599cba25a8a733d2fef
Content-MD5: V0XuU8V7aqMYeWyD3BC2nQ==
Content-Length: 126

<Delete>
  <Quiet>false</Quiet>
  <Object>
    <Key>aa</Key>
  </Object>
  <Object>
    <Key>aaa</Key>
  </Object>
</Delete>
```

### 응답
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 111
Connection: keep-alive
Date: Tue, 22 Aug 2017 12:16:35 GMT
Server: tencent-cos
x-cos-request-id: NTk5YzIwYTNfMzFhYzM1MGFfMmNmOWZfZWVhNjQ=

<DeleteResult>
 <Deleted>
  <Key>aa</Key>
 </Deleted>
 <Deleted>
  <Key>aaa</Key>
 </Deleted>
</DeleteResult>
```


