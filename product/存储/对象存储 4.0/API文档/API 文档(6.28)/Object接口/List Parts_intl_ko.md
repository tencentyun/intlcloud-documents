## 기능 설명
List Parts는 특정 멀티파트 업로드에서 이미 업로드한 파트 조회에 사용하며, 즉 지정 UploadId에 속한 모든 이미 업로드에 성공한 멀티파트를 나열합니다.

## 요청
### 요청 예제

```
GET /ObjectName?uploadId=UploadId HTTP/1.1
Host: <BucketName>-<APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 섹션을 참조).

### 요청 헤더
#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 섹션을 참조하십시오.
#### 비공통 헤더
해당 요청 작업은 특별한 요청 헤더 정보가 없습니다.

#### 요청 매개변수

이름|유형|필수 여부|설명
---|---|---|---
UploadId|string|예|이번 멀티파트 업로드를 식별하는 ID. Initiate Multipart Upload API로 멀티파트 업로드를 초기화하면 하나의 uploadId를 얻게 되며, 해당 ID는 이 멀티파트 데이터를 유일하게 식별할 뿐만 아니라 전체 파일 내에서 이 파트 데이터의 상대적인 위치를 식별합니다.
Encoding-type|string|아니요|반환값의 인코딩 방식을 규정합니다.
Max-parts|string|아니요|1회 최대 반환 항목 수, 기본값은 1000입니다.
Part-number-marker|string|아니요|기본적으로 UTF-8 이진 순서로 항목을 열거하고 모든 열거 항목은 marker부터 시작합니다.

### 요청체
해당 요청 본문이 비어 있습니다.

## 응답

### 응답 헤더
#### 공통 응답 헤더
해당 응답 패킷은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.
#### 고유의 응답 헤더
해당 응답은 특별한 응답 헤더가 없습니다.

### 응답 본문
조회 성공, **application/xml** 데이터를 반환하며 이미 완료한 파트 정보를 포함합니다.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<ListPartsResult>
  <Bucket>string</Bucket>
  <Encoding-Type>string</Encoding-Type>
  <Key>string</Key>
  <UploadId>string</UploadId>
  <Initiator>
    <ID>string</ID>
    <DisplayName>string</DisplayName>
  </Initiator>
  <Owner>
    <ID>string</ID>
    <DisplayName>string</DisplayName>
  </Owner>
  <StorageClass>string</StorageClass>
  <PartNumberMarker>string</PartNumberMarker>
  <NextPartNumberMarker>string</NextPartNumberMarker>
  <MaxParts>string</MaxParts>
  <IsTruncated>true</IsTruncated>
  <Part>
    <PartNumber>string</PartNumber>
    <LastModified>string</LastModified>
    <ETag>string</ETag>
    <Size>string</Size>
  </Part>
</ListPartsResult>
```

구체적인 데이터 설명은 다음과 같습니다.

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
ListPartsResult|없음|List Parts 요청 결과의 모든 정보를 저장합니다.|Container|예

Container 노드 ListPartsResult의 내용:

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
Bucket|ListPartsResult|멀티파트 업로드 대상 버킷, 버킷 이름은 사용자 지정 문자열과 시스템이 생성한 appid 숫자열을 대시로 연결하여 생성됩니다. 예: mybucket-1250000000|string|예
Encoding-Type|ListPartsResult|인코딩 형식|string|예
Key|ListPartsResult|객체의 이름|string|예
UploadId|ListPartsResult|이번 멀티파트 업로드 ID |string|예
Initiator|ListPartsResult|이러한 파트 소유자의 정보를 표시하는 데 사용됩니다.|Container|예
Owner|ListPartsResult|이러한 파트 소유자의 정보를 표시하는 데 사용됩니다.|Container|예
StorageClass|ListPartsResult|이러한 파트의 스토리지 클래스를 표시하는 데 사용됩니다. 열거형 값: STANDARD, STANDARD_IA, ARCHIVE|string|예
PartNumberMarker|ListPartsResult|기본적으로 UTF-8 이진 순서로 항목을 열거합니다. 모든 열거 항목은 marker부터 시작합니다.|string|예
NextPartNumberMarker|ListPartsResult|반환 항목이 잘리면 반환 NextMarker가 바로 다음 항목의 시작점입니다.|string|예
MaxParts|ListPartsResult|1회 최대 반환 항목 수량|string|예
IsTruncated|ListPartsResult|응답 요청 항목 잘렸는지 여부, 부울값: true, false|boolean|예
Part|ListPartsResult|메타데이터 정보|Container|예
Container 노드 Initiator의 내용:

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
ID|ListPartsResult.Initiator|생성자의 유일한 ID|string|예
DisplayName|ListPartsResult.Initiator|생성자의 사용자 이름 설명|string|예
Container 노드 Owner의 내용:

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
ID|ListPartsResult.Owner|생성자의 유일한 ID|string|예
DisplayName|ListPartsResult.Owner|생성자의 사용자 이름 설명|string|예
Container 노드 Part의 내용:

노드 이름(키워드)|부모 노드|설명|유형|필수 선택 여부
---|---|---|---|---
PartNumber|ListPartsResult.Part|파트의 번호|string|예
LastModified|ListPartsResult.Part|파트가 마지막에 수정된 시간 설명|string|예
ETag|ListPartsResult.Part|파트의 MD-5 알고리즘 검사값|string|예
Size|ListPartsResult.Part|파트 크기를 설명하며 단위는 Byte입니다.|string|예

## 실제 사례

### 요청

```
GET /coss3/test10M_2?uploadId=14846420620b1f381e5d7b057692e131dd8d72dfa28f2633cfbbe4d0a9e8bd0719933545b0&max-parts=1 HTTP/1.1
Host:burning-1251668577.cos.ap-beijing.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3MqQCn&q-sign-time=1484643123;1484646723&q-key-time=1484643123;1484646723&q-header-list=host&q-url-param-list=max-parts;uploadId&q-signature=b8b4055724e64c9ad848190a2f7625fd3f9d3e87
```

### 응답

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 661
Connection: keep-alive
Date: Wed，18 Jan 2017 16:17:03 GMT
x-cos-request-id: NTg3ZGRiMzhfMmM4OGY3XzdhY2NfYw==

<ListPartsResult>
    <Bucket>burning-123456789</Bucket>
    <Encoding-type/>
    <Key>test10M_2</Key>
    <UploadId>14846420620b1f381e5d7b057692e131dd8d72dfa28f2633cfbbe4d0a9e8bd0719933545b0</UploadId>
    <Initiator>
        <ID>123456789</ID>
        <DisplyName>123456789</DisplyName>
    </Initiator>
    <Owner>
        <ID>qcs::cam::uin/156545789:uin/156545789</ID>
        <DisplyName>156545789</DisplyName>
    </Owner>
    <PartNumberMarker>0</PartNumberMarker>
    <Part>
        <PartNumber>1</PartNumber>
        <LastModified>Tue Jan 17 16:43:37 2017</LastModified>
        <ETag>"a1f8e5e4d63ac6970a0062a6277e191fe09a1382"</ETag>
        <Size>5242880</Size>
    </Part>
    <NextPartNumberMarker>1</NextPartNumberMarker>
    <StorageClass>STANDARD</StorageClass>
    <MaxParts>1</MaxParts>
    <IsTruncated>true</IsTruncated>
</ListPartsResult>
```
