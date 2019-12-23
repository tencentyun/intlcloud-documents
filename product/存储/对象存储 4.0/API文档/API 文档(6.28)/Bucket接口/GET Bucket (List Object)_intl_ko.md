## 기능 설명
GET Bucket 요청은 List Object 요청과 동일하며, 해당 버킷 하의 일부 또는 전체 객체를 열거할 수 있습니다. 해당 API의 작업자는 반드시 버킷에 대한 읽기 권한이 있어야 합니다.

## 요청
### 요청 예제

```shell
GET / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
> Authorization: Auth String(세부 정보는 [요청 서명](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참조).

### 요청 헤더
#### 공통 헤더
해당 요청 작업은 공통 요청 헤더를 사용하여 구현됩니다. 공통 요청 헤더에 대한 세부 정보는 [공통 요청 헤더](https://cloud.tencent.com/document/product/436/7728) 문서를 참조하십시오.
#### 비공통 헤더
해당 요청 작업은 특별한 요청 헤더 정보가 없습니다.

#### 요청 매개변수

이름|유형|설명|필수 여부
---|---|---|---
prefix|string|접두사 매칭, 반환된 파일 접두사 주소를 규정하는 데 사용됩니다. |아니요
delimiter|string|구분 문자는 하나의 부호이며, Prefix가 있으면 Prefix와 delimiter 사이의 동일 경로를 하나의 유형으로 분류되고, Common Prefix라고 정의한 뒤 모든 Common Prefix를 열거합니다. Prefix가 없으면 경로 시작점부터 시작합니다|아니요
Encoding-type|string|반환값의 인코딩 방식을 지정합니다. 선택 가능 값: url |아니요
Marker|string|기본적으로 UTF-8 이진 순서로 항목을 열거하고 모든 열거 항목은 marker부터 시작합니다.|아니요
Max-keys|string|1회에 최대 반환 항목 수, 기본값은 1000, 최대값은 1000 |아니요

### 요청체
해당 요청 본문이 비어 있습니다.

## 응답
### 응답 헤더

#### 공통 응답 헤더
해당 응답은 공통 응답 헤더를 포함합니다. 공통 응답 헤더에 대한 세부 정보는 [공통 응답 헤더](https://cloud.tencent.com/document/product/436/7729) 섹션을 참조하십시오.
#### 고유의 응답 헤더
해당 응답은 특별한 응답 헤더가 없습니다.

### 응답 본문
조회 성공, application/xml 데이터를 반환하며 Bucket의 개체 정보를 포함합니다.

```shell
<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
    <Name>examplebucket-1250000000</Name>
    <Encoding-Type>url</Encoding-Type>
    <Prefix>ela</Prefix>
    <Marker/>
    <MaxKeys>1000</MaxKeys>
    <Delimiter>/</Delimiter>
    <IsTruncated>false</IsTruncated>
    <NextMarker>exampleobject.txt</NextMarker>
    <Contents>
        <Key>photo</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"79f2a852fac7e826c9f4dbe037f8a63b\"</ETag>
        <Size>10485760</Size>
        <Owner>
           <ID>1250000000</ID>
        </Owner>
        <StorageClass>STANDARD</StorageClass>
    </Contents>
    <CommonPrefixes>
      <Prefix>example</Prefix>
    </CommonPrefixes>
</ListBucketResult>
```

구체적인 데이터 설명은 다음과 같습니다.

노드 이름(키워드)|부모 노드|설명|유형
---|---|---|---
ListBucketResult|없음|Get Bucket 요청 결과의 모든 정보 저장|Container

**Container 노드 ListBucketResult 내용:**

노드 이름(키워드)|부모 노드|설명|유형
---|---|---|---
Name|ListBucketResult|버킷 정보|string
Encoding-Type|ListBucketResult|인코딩 형식|string
Prefix|ListBucketResult|접두사 매칭, 응답 요청에 의해 반환된 파일 접두사 주소를 지정하는 데 사용됩니다|string
Marker|ListBucketResult|기본적으로 UTF-8 이진 순서로 항목이 열거됩니다. 모든 열거 항목은 marker부터 시작합니다|string
MaxKeys|ListBucketResult|1회 응답 요청 내 반환 결과의 최대 항목 수|string
Delimiter|ListBucketResult|구분 문자는 하나의 부호이며, Prefix가 있으면 Prefix와 delimiter 사이의 동일 경로를 하나의 유형으로 분류되고 Common Prefix라고 정의한 뒤 모든 Common Prefix를 열거합니다. Prefix가 없으면 경로 시작점부터 시작합니다|string
IsTruncated|ListBucketResult|응답 요청 항목 잘렸는지 여부, 부울값: true, false|boolean
NextMarker|ListBucketResult|반환 항목이 잘렸다면, 반환된 NextMarker가 바로 다음 항목의 시작점입니다|string
Contents|ListBucketResult|메타데이터 정보|Container
CommonPrefixes|ListBucketResult|Prefix와 delimiter 사이의 동일 경로를 하나의 유형으로 분류되고 Common Prefix라고 정의합니다|Container


**Container 노드 Contents 내용:**

노드 이름(키워드)|부모 노드|설명|유형
---|---|---|--
Key|ListBucketResult.Contents|Object의 Key|string
LastModified|ListBucketResult.Contents|Object의 마지막 수정 시간|string
ETag|ListBucketResult.Contents|파일의 MD-5 알고리즘 검사값|string
Size|ListBucketResult.Contents|파일 크기, 단위는 Byte|string
Owner|ListBucketResult.Contents|버킷 소유자 정보|Container
StorageClass|ListBucketResult.Contents|Object의 스토리지 클래스, 열거형 값: STANDARD, STANDARD_IA, ARCHIVE|string

**Container 노드 Owner 내용:**

노드 이름(키워드)|부모 노드|설명|유형
---|---|---|---
ID|ListBucketResult.Contents.Owner|버킷의 AppID|string


**Container 노드 CommonPrefixes 내용:**

노드 이름(키워드)|부모 노드|설명|유형
---|---|---|---
Prefix|ListBucketResult.CommonPrefixes|단일 Common의 접두사|string


### 오류 코드
해당 요청 작업은 특별 오류 정보가 없습니다.일반적인 오류 정보는 [오류 코드](https://cloud.tencent.com/document/product/436/7730) 문서를 참조하십시오.

## 실제 사례

### 요청

```shell
GET / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 18 Oct 2014 22:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484213451;32557109451&q-key-time=1484213451;32557109451&q-header-list=host&q-url-param-list=&q-signature=0336a1fc8350c74b6c081d4dff8e7a2db9007dc
```

### 응답

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1132
Connection: keep-alive
Vary: Accept-Encoding
Date: Wed, 18 Oct 2014 22:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3NzRjY2VfYmRjMzVfMTc5M182MmIyNg==

<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
    <Name>examplebucket-1250000000</Name>
    <Encoding-Type>url</Encoding-Type>
    <Prefix>ela</Prefix>
    <Marker/>
    <MaxKeys>1000</MaxKeys>
    <Delimiter>/</Delimiter>
    <IsTruncated>false</IsTruncated>
    <NextMarker>exampleobject.txt</NextMarker>
    <Contents>
        <Key>photo</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"79f2a852fac7e826c9f4dbe037f8a63b\"</ETag>
        <Size>10485760</Size>
        <Owner>
            <ID>1250000001</ID>
        </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Contents>
    <Contents>
        <Key>picture</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"3f9a5dbff88b25b769fa6304902b5d9d\"</ETag>
        <Size>10485760</Size>
        <Owner>
            <ID>1250000002</ID>
        </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Contents>
    <Contents>
        <Key>file</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"39bfb88c11c65ed6424d2e1cd4db1826\"</ETag>
        <Size>10485760</Size>
        <Owner>
            <ID>1250000003</ID>
        </Owner>
    <StorageClass>STANDARD</StorageClass>
    </Contents>
    <Contents>
        <Key>world</Key>
        <LastModified>2017-06-23T12:33:26.000Z</LastModified>
        <ETag>\"fb31459ad10289ff49327fd91a3e1f6a\"</ETag>
        <Size>4</Size>
        <Owner>
            <ID>1250000004</ID>
        </Owner>
        <StorageClass>STANDARD</StorageClass>
    </Contents>
</ListBucketResult>
```
