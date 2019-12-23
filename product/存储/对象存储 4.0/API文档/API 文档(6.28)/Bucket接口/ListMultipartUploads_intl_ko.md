## 기능 설명
List Multipart Uploads는 진행 중인 멀티파트 업로드를 조회하는 데 사용됩니다. 1회 요청 작업은 최대 1000개의 진행 중인 멀티파트 업로드를 열거할 수 있습니다.

>주의: 해당 요청은 버킷의 읽기 권한이 필요합니다.

## 요청
### 요청 예제

```
GET /?uploads HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조).

### 요청 헤더

#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 섹션을 참조하십시오.

#### 비공통 헤더
해당 요청 작업은 특별한 요청 헤더 정보가 없습니다.

### 요청 매개 변수

구체적인 내용은 다음과 같습니다. <style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

| 이름               | 설명                                       | 유형     | 필수 선택 여부   |
| ---------------- | ---------------------------------------- | ------ | ---- |
| delimiter        | 구분 문자는 하나의 부호로 Object 이름에 대해 지정 접두사를 포함하며, 처음 나타난 delimiter 문자 간의 Object를 그룹 요소 common prefix로 합니다. prefix가 없다면 경로 시작점으로부터 시작합니다 | String | 아니요    |
| encoding-type    | 반환값의 인코딩 방식을 규정하며 유효한 값: url                               | String | 아니요    |
| prefix           | 반환된 Object key가 Prefix를 접두사로 하도록 한정합니다. </br>prefix를 사용하여 조회할 때, 반환된 key에는 Prefix가 포함되어 있습니다 | String | 아니요    |
| max-uploads      | 최대 반환 multipart 수량을 설정하며, 유효한 값은 1부터 1000까지이고 기본값은 1000입니다                       | String | 아니요    |
| key-marker       | upload-id-marker와 함께 사용합니다. <Br/>upload-id-marker가 지정되지 않았을 때, ObjectName 알파벳 순서가 key-marker 뒤에 있는 항목이 나열됩니다. <Br/>upload-id-marker가 지정되었을 때, ObjectName 알파벳 순서가 key-marker 뒤에 있는 항목이 나열되며 ObjectName 알파벳 순서가 key-marker와 같고 동시에 UploadID가 upload-id-marker 뒤에 있는 항목이 나열됩니다. | String | 아니요    |
| upload-id-marker | key-marker와 함께 사용합니다. <Br/>key-marker가 지정되지 않았을 때, upload-id-marker는 무시되며, <Br/>key-marker가 지정되었을 때, ObjectName 알파벳 순서가 key-marker 뒤에 있는 항목이 나열되며, ObjectName 알파벳 순서가 key-marker와 같고 동시에 UploadID가 upload-id-marker 뒤에 있는 항목이 나열됩니다. | String | 아니요    |

### 요청체
해당 요청의 요청체는 비어 있습니다.

## 응답

### 응답 헤더
#### 공통 응답 헤더
해당 응답 패킷은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.
#### 고유의 응답 헤더
해당 응답은 특별한 응답 헤더가 없습니다.

### 응답 본문
해당 응답 본문은 **application/xml** 데이터를 반환합니다. 완전한 노드 데이터를 포함한 내용은 다음과 같습니다.

```
<ListMultipartUploadsResult>
  <Bucket></Bucket>
  <Encoding-Type></Encoding-Type>
  <KeyMarker></KeyMarker>
  <UploadIdMarker></UploadIdMarker>
  <NextKeyMarker></NextKeyMarker>
  <NextUploadIdMarker></NextUploadIdMarker>
  <MaxUploads></MaxUploads>
  <IsTruncated></IsTruncated>
  <Prefix></Prefix>
  <Delimiter></Delimiter>
  <Upload>
    <Key></Key>
    <UploadID></UploadID>
    <StorageClass></StorageClass>
    <Initiator>
      <ID></ID>
	<DisplayName></DisplayName>
    </Initiator>
    <Owner>
      <ID></ID>
	<DisplayName></DisplayName>
    </Owner>
    <Initiated></Initiated>
  </Upload>
  <CommonPrefixes>
    <Prefix></Prefix>
  </CommonPrefixes>
</ListMultipartUploadsResult>
```

구체적인 데이터 내용은 다음과 같습니다.

|노드 이름(키워드)|부모 노드|설명|유형|
|:---|:-- |:--|:--|
| ListMultipartUploadsResult |없음| 모든 멀티파트 업로드 정보를 설명하는 데 사용됩니다 | Container |

Container 노드 ListMultipartUploadsResult의 내용:

|노드 이름(키워드)|부모 노드|설명|유형|
|:---|:-- |:--|:--|
| Bucket | ListMultipartUploadsResult | 멀티파트 업로드 대상 Bucket은 사용자 지정 문자열과 시스템이 생성한 appid 숫자열을 대시로 연결하여 생성됩니다. 예: mybucket-1250000000 |  String |
| Encoding-Type | ListMultipartUploadsResult | 반환값의 인코딩 방식을 규정하며 유효한 값은 url입니다 |  String |
| KeyMarker | ListMultipartUploadsResult| 항목을 해당 key 값부터 시작하여 나열합니다. |  String |
| UploadIdMarker | ListMultipartUploadsResult | 항목을 해당 UploadId 값부터 시작하여 나열합니다. |  String |
| NextKeyMarker | ListMultipartUploadsResult | 반환 항목이 잘리면 반환 NextKeyMarker가 바로 다음 항목의 시작점입니다. | String |
| NextUploadIdMarker | ListMultipartUploadsResult | 반환 항목이 잘리면 반환 UploadId가 바로 다음 항목의 시작점입니다. |  String |
| MaxUploads | ListMultipartUploadsResult | 최대 반환 multipart 수량을 설정하며 유효한 값은 0부터 1000까지입니다 |  String |
| IsTruncated | ListMultipartUploadsResult | 반환 항목 잘렸는지 여부, 부울값: TRUE, FALSE |  Boolean |
| Prefix | ListMultipartUploadsResult | 반환된 Object key가 Prefix를 접두사로 하도록 한정합니다. </br>prefix를 사용하여 조회할 때, 반환된 key에는 Prefix가 포함되어 있습니다. |  String |
| Delimiter | ListMultipartUploadsResult | 구분 문자는 하나의 부호로 object 이름에 지정 접두사를 포함하며, 지정 접두사와 처음 나타난 delimiter 문자 간의 object를 한 그룹의 요소 common prefix로 합니다. prefix가 없다면 경로 시작점으로부터 시작합니다. |  String |
| Upload | ListMultipartUploadsResult  | 모든 Upload의 정보 |  Container |
| CommonPrefixes | ListMultipartUploadsResult | Prefix부터 delimiter까지의 동일 경로를 하나의 유형으로 분류하며 Common Prefix라 정의합니다. |  Container |

Container 노드 Upload 내용:

|노드 이름(키워드)|부모 노드|설명|유형|
|:---|:-- |:--|:--|
| Key | ListMultipartUploadsResult.Upload |  Object의 이름 |  String |
| UploadID | ListMultipartUploadsResult.Upload | 이번 멀티파트 업로드 ID | String |
| StorageClass | ListMultipartUploadsResult.Upload |  파트의 스토리지 클래스를 표시하는 데 사용됩니다. 열거형 값: STANDARD, STANDARD_IA, ARCHIVE |  String |
| Initiator | ListMultipartUploadsResult.Upload |  이번 업로드 개시자의 정보 |  Container |
| Owner | ListMultipartUploadsResult.Upload | 이러한 파트 소유자의 정보 |  Container |
| Initiated | ListMultipartUploadsResult.Upload |  멀티파트 업로드의 시작 시간 |  Date |

Container 노드 Initiator의 내용:

| 노드 이름(키워드)         |부모 노드 | 설명                                    | 유형        |
| ------------ | ------------------------------------- | --------- |:--|
| ID | ListMultipartUploadsResult.Upload.Initiator | 사용자의 유일한 CAM 신분 ID | String  |
| DisplayName | ListMultipartUploadsResult.Upload.Initiator | 사용자 신분 ID의 약칭(UIN)| String  |

Container 노드 Owner의 내용:

| 노드 이름(키워드)         |부모 노드 | 설명                                    | 유형        |
| ------------ | ------------------------------------- | --------- |:--|
| ID | ListMultipartUploadsResult.Upload.Owner | 사용자의 유일한 CAM 신분 ID  | String    |
| DisplayName | ListMultipartUploadsResult.Upload.Owner| 사용자 신분 ID의 약칭(UIN)| String  |

Container 노드 CommonPrefixes의 내용:

| 노드 이름(키워드)         |부모 노드 | 설명                                    | 유형        |
| ------------ | ------------------------------------- | --------- |:--|
| Prefix | ListMultipartUploadsResult.CommonPrefixes | 구체적인 CommonPrefixes를 표시합니다. | String    |

### 오류 분석
다음은 이 요청이 일으킬 수 있는 특별하지만 흔히 볼 수 있는 오류 상황을 설명합니다.

| 오류 코드             | HTTP 상태 코드         |설명                    |
| ------------- | ------------------------------------ | ------------- |
| InvalidArgument | 400 Bad Request |1. Max-uploads는 반드시 정수여야 하고, 값이 0~1000 사이여야 하며 그렇지 않으면 InvalidArgument를 반환합니다. <br>2. encoding-type은 url 값만 취하며 그렇지 않을 경우 InvalidArgument를 반환합니다. |

COS 오류 코드에 대한 세부 정보 또는 제품의 모든 오류 리스트는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

## 실제 사례

### 요청

```
GET /?uploads HTTP/1.1
Host: arlenhuangtestsgnoversion-1251668577.cos.ap-beijing.myqcloud.com
Date: Wed, 18 Jan 2015 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484727508;32557623508&q-key-time=1484727508;32557623508&q-header-list=host&q-url-param-list=uploads&q-signature=5bd4759a7309f7da9a0550c224d8c61589c9dbbf
```

### 응답

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1203
Date: Wed, 18 Jan 2015 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjI0ZGRfNDQyMDRlXzNhZmRfMjRl

<ListMultipartUploadsResult>
    <Bucket>arlenhuangtestsgnoversion-1251668577</Bucket>
    <Encoding-Type/>
    <KeyMarker/>
    <UploadIdMarker/>
    <MaxUploads>1000</MaxUploads>
    <Prefix/>
    <Delimiter>/</Delimiter>
    <IsTruncated>false</IsTruncated>
    <Upload>
        <Key>Object</Key>
        <UploadID>1484726657932bcb5b17f7a98a8cad9fc36a340ff204c79bd2f51e7dddf0b6d1da6220520c</UploadID>
        <Initiator>
           <ID>qcs::cam::uin/14847266009:uin/14847266009</ID>
		<DisplayName>14847266009</DisplayName>
        </Initiator>
        <Owner>
           <ID>qcs::cam::uin/14847266009:uin/14847266009</ID>
		<DisplayName>14847266009</DisplayName>
        </Owner>
        <StorageClass>Standard</StorageClass>
        <Initiated>Wed Jan 18 16:04:17 2017</Initiated>
    </Upload>
    <Upload>
        <Key>Object</Key>
        <UploadID>1484727158f2b8034e5407d18cbf28e84f754b791ecab607d25a2e52de9fee641e5f60707c</UploadID>
        <Initiator>
           <ID>qcs::cam::uin/14847266009:uin/14847266009</ID>
		<DisplayName>14847266009</DisplayName>
        </Initiator>
        <Owner>
           <ID>qcs::cam::uin/14847266009:uin/14847266009</ID>
		<DisplayName>14847266009</DisplayName>
        </Owner>
        <StorageClass>Standard</StorageClass>
        <Initiated>Wed Jan 18 16:12:38 2017</Initiated>
    </Upload>
    <Upload>
        <Key>ObjectName</Key>
        <UploadID>1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e</UploadID>
        <Initiator>
           <ID>qcs::cam::uin/14847266009:uin/14847266009</ID>
		<DisplayName>14847266009</DisplayName>
        </Initiator>
        <Owner>
           <ID>qcs::cam::uin/14847266009:uin/14847266009</ID>
		<DisplayName>14847266009</DisplayName>
        </Owner>
        <StorageClass>Standard</StorageClass>
        <Initiated>Wed Jan 18 16:14:30 2017</Initiated>
    </Upload>
</ListMultipartUploadsResult>

```
