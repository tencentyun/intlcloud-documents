## 소개

본 문서는 객체의 고급 인터페이스, 간단한 조작, 파트 작업과 관련된 API 개요 및 SDK 예시 코드를 제공합니다.

**간단한 조작**

| API                                                          | 작업명         | 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 리스트 조회   | 버킷 하위의 일부 또는 전체 객체 조회            |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 간단한 객체 업로드   | 객체 하나를 버킷에 업로드                      |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회 | 객체의 메타데이터 정보 조회                  |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 객체를 로컬에 다운로드        |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사 설정   | 파일을 타깃 경로에 파일 복사                        |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 단일 객체 삭제   | 버킷에서 지정 객체 삭제 |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 다수의 객체 삭제   | 버킷에서 지정 객체 일괄 삭제                |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 보관된 객체 복구 | 아카이브 유형의 객체 검색 후 액세스           |

**파트 작업**

| API                                                          | 작업명         | 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | Multipart Upload 작업 초기화     |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 멀티파트 업로드       | 파일 멀티파트 업로드                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 멀티파트 복사       | 다른 객체를 한 파트로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 멀티파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 파일의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 멀티파트 업로드 작업 중지 및 업로드된 멀티파트 제거 |

## 간단한 작업

### 객체 리스트 조회

#### 기능 설명

버킷의 일부 또는 모든 객체를 조회합니다.

#### 방법 모델

```java
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest) throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-get-bucket)
```java
// Bucket의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// bucket 이름을 설정합니다.
listObjectsRequest.setBucketName(bucketName);
// prefix는 나열된 object의 key가 prefix로 시작함을 의미합니다.
listObjectsRequest.setPrefix("images/");
// delimiter는 세퍼레이터를 의미합니다. /로 설정되면 현재 디렉터리의 object 나열을, 공백으로 설정되면 전체 object 나열을 의미합니다.
listObjectsRequest.setDelimiter("/");
// 순회 가능한 객체의 최대 수량을 설정합니다. listobject는 1회당 최대 1000개를 지원합니다.
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;
do {
    try {
        objectListing = cosClient.listObjects(listObjectsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }
    // common prefix는 delimiter로 차단된 경로를 표시합니다. 예를 들어 delimiter가 /로 설정되어 있으면 common prefix는 모든 서브 디렉터리의 경로를 표시합니다.
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // object summary는 나열된 모든 object 리스트를 표시합니다.
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // 파일의 경로 key
        String key = cosObjectSummary.getKey();
        // 파일의 etag
        String etag = cosObjectSummary.getETag();
        // 파일의 길이
        long fileSize = cosObjectSummary.getSize();
        // 파일의 스토리지 유형
        String storageClasses = cosObjectSummary.getStorageClass();
    }

    String nextMarker = objectListing.getNextMarker();
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());
```


#### 매개변수 설명

| 매개변수 이름           | 설명             | 유형               |
| ------------------ | ---------------- | ------------------ |
| listObjectsRequest | 파일 리스트 요청을 획득합니다. | ListObjectsRequest |

Request 멤버 설명:

| Request 멤버 | 설정 방법&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            | 설명                                                         | 유형    |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName   | 구조 함수 또는 set 방법 | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String  |
| prefix       | 구조 함수 또는 set 방법 | 반환되는 결과 객체를 제한하고 prefix를 접두사로 합니다. 기본적으로 Bucket의 모든 멤버를 제한하지 않습니다.<br>기본값은 공백: "" | String  |
| marker       | 구조 함수 또는 set 방법 | list의 시작 위치를 표시합니다. 처음에는 공백으로 설정해도 되지만, 다음 요청은 이전 listObjects 반환 값의 nextMarker로 설정해야 합니다. | String  |
| delimiter    | 구조 함수 또는 set 방법 | 세퍼레이터입니다. prefix로 시작하며 delimiter가 처음 나타나 끝나는 경로의 반환을 제한합니다. | String  |
| maxKeys      | 구조 함수 또는 set 방법 | 멤버 최대 반환 수(1000을 초과할 수 없음).<br>기본값: 1000          | Integer |

#### 반환 결과 설명

- 성공: 모든 멤버 및 nextMarker를 포함한 ObjectListing 유형을 반환합니다.  
- 실패: 오류 sClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.


### 간단한 객체 업로드

#### 기능 설명

객체를 지정한 버킷에 업로드합니다(PUT Object). 로컬 파일 또는 길이를 알고 있는 입력 스트림 콘텐츠를 COS에 업로드합니다. 이미지나 크기가 작은 파일(20MB 이하) 업로드에 적합하며, 최대 5GB까지 지원합니다. 5GB를 초과하는 파일은 [멀티파트 업로드](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) 또는 [고급 API](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)로 업로드하여 주십시오.

- 업로드 과정에서 기본적으로 파일의 길이와 MD5에 대한 인증을 진행합니다(MD5 인증 비활성화는 예시 코드 참조).
- COS에 Key가 동일한 객체가 있을 경우 업로드 과정에서 덮어쓰기가 진행됩니다.
- 업로드 후 동일한 key로 GetObject 인터페이스를 호출하여 파일을 로컬에 다운로드할 수 있고, [사전 서명 링크](https://intl.cloud.tencent.com/document/product/436/31536)를 생성(다운로드 시 method를 GET으로 지정하십시오. 상세한 인터페이스 설명은 아래를 참조하십시오)하여 다른 포트로 전송 후 다운로드할 수도 있습니다.

#### 방법 모델

```java
// 방법1 로컬 파일을 COS에 업로드합니다.
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// 방법2 입력 스트림을 COS에 업로드합니다.
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// 방법3 위의 두 가지 방법 패키지에 데이터 분할 정도가 더 세밀한 매개변수 제어를 지원합니다(예: content-type, content-disposition 등).
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-put-object-flex)
```java
// Bucket의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 방법1 로컬 파일을 업로드합니다.
File localFile = new File(localFilePath);
String key = "exampleobject";
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, localFile);
String etag = putObjectResult.getETag();  // 파일의 etag 획득

// 방법2 입력 스트림을 업로드합니다(입력 스트림의 길이를 사전에 알려야 합니다. 그렇지 않으면 oom 문제가 발생할 수 있습니다).
FileInputStream fileInputStream = new FileInputStream(localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// 입력 스트림의 길이를 500으로 설정합니다.
objectMetadata.setContentLength(500);
// Content type을 설정합니다. 기본값은 application/octet-stream입니다.
objectMetadata.setContentType("application/pdf");
putObjectResult = cosClient.putObject(bucketName, key, fileInputStream, objectMetadata);
etag = putObjectResult.getETag();
// 입력 스트림을 비활성화합니다...

// 방법3 데이터 분할 정도가 더 세밀한 매개변수 제어를 지원합니다. 일반적인 설정은 다음과 같습니다.
// 1 storage-class 스토리지 유형의 열거 값은 Standard, Standard_IA, Archive이며, 기본값은 Standard입니다. 더 많은 스토리지 유형은 https://intl.cloud.tencent.com/zh/document/product/436/30925를 참조하십시오.
// 2 content-type, 로컬 파일 업로드의 기본값은 로컬 파일의 접미사에 따라 매핑됩니다(예: jpg 파일은 image/jpeg로 매핑).
// 스트림 업로드의 기본값은 application/octet-stream입니다.
// 3 업로드와 동시에 권한을 지정합니다(API set object acl 호출을 통한 설정도 가능합니다).
// 4 전역에서 MD5 업로드 인증을 비활성화하려면 시스템 환경 변수를 설정해야 합니다. 이 설정은 모든 업로드 인증에 영향을 줍니다. 기본값은 인증 활성화입니다.
// MD5 인증 비활성화: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
// MD5 인증 활성화: System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, null);
localFile = new File(localFilePath);
key = "picture.jpg";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// 스토리지 유형을 표준IA로 설정합니다.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
// 사용자 정의 속성을 설정합니다(예: content-type, content-disposition 등).
objectMetadata = new ObjectMetadata();
// 사용 단위는 bit/s로 제한되며, 설정된 업로드 대역폭은 10MB/s로 제한되어 있습니다.
putObjectRequest.setTrafficLimit(80*1024*1024);
// Content type을 설정합니다. 기본값은 application/octet-stream입니다.
objectMetadata.setContentType("image/jpeg");
putObjectRequest.setMetadata(objectMetadata);
putObjectResult = cosClient.putObject(putObjectRequest);
// 객체의 Etag를 획득합니다.
etag = putObjectResult.getETag();
// 객체의 CRC64를 획득합니다.
String crc64Ecma = putObjectResult.getCrc64Ecma();
```


#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 방법 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   | 설명                                                         | 유형   | 필수 |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName   | 구조 함수 또는 set 방법 | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String         | 예|
| key          | 구조 함수 또는 set 방법 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String         | 예|
| file         | 구조 함수 또는 set 방법 | 로컬 파일                                                     | File           |아니오|
| input        | 구조 함수 또는 set 방법 | 입력 스트림                                                       | InputStream    | 아니오|
| metadata     | 구조 함수 또는 set 방법 | 객체의 메타데이터                                                 | ObjectMetadata | 아니오|
|trafficLimit | set 방법| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|아니오|

ObjectMetadata 유형은 객체의 메타데이터를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | 캐시의 타임아웃 시간은 HTTP 응답 헤더의 Expires 필드 값입니다. | Date                |
| ongoingRestore  | 현재 CAS 유형에서 해당 객체를 복구하고 있습니다.                        | Boolean             |
| userMetadata    | 접두사가 x-cos-meta-인 사용자 정의 메타데이터입니다.               | Map<String, String> |
| metadata        | 사용자 정의 메타데이터를 제외한 기타 헤더입니다.                    | Map<String, String> |
| restoreExpirationTime  | 보관된 객체 복구 사본의 만료 기한입니다.  | Date |


#### 반환 결과 설명

- 성공: 파일의 eTag 등 정보를 포함한 PutObjectResult입니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.

#### 반환 매개변수 설명

PutObjectResult 유형은 결과 정보 반환에 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | 요청 ID | String                |
| dateStr  | 현재 서버 시간                        | String             |
| versionId    | 버전을 제어하는 버킷을 활성화한 후 객체의 버전 ID를 반환합니다.              | String |
| eTag        | 인터페이스가 반환한 객체의 MD5 값을 간단하게 업로드합니다.                    | String |
|crc64Ecma| 서버는 객체 콘텐츠가 계산한 CRC64를 따릅니다.| String |


### 객체 메타데이터 조회

#### 기능 설명

지정한 객체가 버킷에 있는지 확인합니다.

#### 방법 모델

```java
public ObjectMetadata getObjectMetadata(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-head-object)
```java
// Bucket의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(bucketName, key);
```


#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |

#### 반환 결과 설명

- 성공: 사용자 정의 헤더, Etag 등 객체 메타데이터를 포함한 ObjectMetadata 유형을 반환합니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.

#### 반환 매개변수 설명

ObjectMetadata 유형은 객체의 메타데이터를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | 캐시의 타임아웃 시간은 HTTP 응답 헤더의 Expires 필드 값입니다. | Date                |
| ongoingRestore  | 현재 CAS 유형에서 해당 객체를 복구하고 있습니다.                        | Boolean             |
| userMetadata    | 접두사가 x-cos-meta-인 사용자 정의 메타데이터입니다.               | Map<String, String> |
| metadata        | 사용자 정의 메타데이터를 제외한 기타 헤더입니다.                    | Map<String, String> |
| restoreExpirationTime  | 보관된 객체 복구 사본의 만료 기한입니다.  | Date |


### 객체 다운로드

#### 기능 설명

객체를 로컬에 다운로드합니다(GET Object).

#### 방법 모델

```java
// 방법1 파일을 다운로드하고 입력 스트림을 획득합니다.
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
// 방법2 파일을 로컬에 다운로드합니다.
public ObjectMetadata getObject(GetObjectRequest getObjectRequest, File destinationFile)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-get-object)
```java
// Bucket의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// 방법1 입력 스트림을 다운로드합니다.
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
// 사용 단위는 bit/s로 제한되며, 설정된 다운로드 대역폭은 10MB/s로 제한되어 있습니다.
getObjectRequest.setTrafficLimit(80*1024*1024);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
// 객체의 CRC64를 다운로드합니다.
String crc64Ecma = cosObject.getObjectMetadata().getCrc64Ecma();
// 입력 스트림을 비활성화합니다.
cosObjectInput.close();

// 방법2 파일을 로컬에 다운로드합니다.
String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```


#### 매개변수 설명

| 매개변수 이름         | 설명           | 유형             |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | 파일 다운로드 요청   | GetObjectRequest |
| destinationFile  | 로컬 저장 파일 | File             |

Request 멤버 설명:

| Request 멤버 | 설정 방법&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            | 설명                                                         | 유형   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName   | 구조 함수 또는 set 방법 | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| key          | 구조 함수 또는 set 방법 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |
| range  | set 방법             | 다운로드 range 범위                                            | Long[] |
| trafficLimit | set 방법    | 객체 다운로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다.  | Int |


#### 반환 결과 설명

- **방법1 (입력 스트림을 다운로드합니다.)**
  - 성공: 입력 스트림 및 객체 속성을 포함한 COSObject 유형을 반환합니다.
  - 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.
- **방법2 (파일을 로컬에 다운로드합니다.)**
  - 성공: 파일의 사용자 정의 헤더와 content-type 등 속성을 포함한 파일의 속성 ObjectMetadata를 반환합니다.
  - 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.

#### 반환 매개변수 설명

COSObject 유형은 결과 정보 반환에 사용됩니다. 주요 멤버는 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| bucketName | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| key          | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |
| metadata | 객체의 메타데이터  | ObjectMetadata |
| objectContent | COS 객체 콘텐츠를 포함한 데이터 스트림  | COSObjectInputStream |


### 객체 복사 설정

#### 기능 설명 

한 객체를 다른 객체에 복사합니다(Put Object Copy). 리전 간, 계정 간, Bucket 간 복사를 지원하며, 원본 파일의 읽기 권한 및 타깃 파일의 쓰기 권한이 필요합니다. 최대 5G의 파일 복사를 지원하며, 5G를 초과하는 파일은 [고급 API](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A1)로 복사하십시오.

#### 방법 모델

```java
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
            throws CosClientException, CosServiceException
```

#### 요청 예시

[//]: # (.cssg-snippet-copy-object)
```java
// 리전 내 동일 계정을 복사합니다.
// 원본 Bucket. Bucket의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String srcBucketName = "sourcebucket-1250000000";
// 복사할 원본 파일입니다.
String srcKey = "sourceObject";
// 타깃 버킷. Bucket의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String destBucketName = "examplebucket-1250000000";
// 복사할 타깃 파일입니다.
String destKey = "exampleobject";
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketName, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);

// 계정 간, 리전 간 복사(원본 파일의 읽기 권한 및 타깃 파일의 쓰기 권한 필요)를 진행합니다.
String srcBucketNameOfDiffAppid = "bucket-own-by-others-1251668577";
Region srcBucketRegion = new Region("ap-shanghai");
copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketNameOfDiffAppid, srcKey, destBucketName, destKey);
copyObjectResult = cosClient.copyObject(copyObjectRequest);
// 객체의 CRC64를 획득합니다.
String crc64Ecma = copyObjectResult.getCrc64Ecma();
```


#### 매개변수 설명

| 매개변수 이름          | 설명         | 유형              |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | 파일 복사 요청 | CopyObjectRequest |

Request 멤버 설명:

| 매개변수 이름              | 설명                                                         | 유형   |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion    | 원본 Bucket region입니다. 기본값은 현재 clientConfig의 region과 일치하며, 리전 내 복사를 의미합니다. | String |
| sourceBucketName      | 원본 버킷 이름입니다. 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| sourceKey             | 원본 객체 키입니다. 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |
| sourceVersionId       | 원본 파일 version id입니다(버전을 제어하는 원본 Bucket 활성화에 적합합니다). 기본값은 원본 파일의 최신 버전입니다. | String |
| destinationBucketName | 타깃 버킷 이름입니다. Bucket의 이름 생성 포맷은 BucketName-APPID이며, name은 알파벳, 숫자, 하이픈으로 구성됩니다.| String |
| destinationKey        | 타깃 객체 키입니다. 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |
| storageClass          | 복사된 타깃 파일의 스토리지 유형입니다. 열거 값은 Standard, Standard_IA이며 기본값은 Standard입니다. 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참조하십시오. | String |

#### 반환 결과 설명

- 성공: 신규 파일의 Etag 등 정보를 포함한 CopyObjectResult가 반환됩니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.


### 단일 객체 삭제

#### 기능 설명

버킷에서 지정 Object(파일/객체)를 삭제합니다.

#### 방법 모델

```java
public void deleteObject(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-delete-object)
```java
// Bucket의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
cosClient.deleteObject(bucketName, key);
```


#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |

#### 반환 결과 설명

- 성공: 반환 값이 없습니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.


### 다수의 객체 삭제

#### 기능 설명

다수의 지정 객체를 삭제합니다(DELETE Multiple Objects).

#### 방법 모델

```java
public DeleteObjectsResult deleteObjects(DeleteObjectsRequest deleteObjectsRequest)
    throws MultiObjectDeleteException, CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-delete-multi-object)
```java
// Bucket의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// 삭제할 key 리스트를 설정합니다. 한번에 최대 1000개까지 삭제할 수 있습니다.
ArrayList<DeleteObjectsRequest.KeyVersion> keyList = new ArrayList<DeleteObjectsRequest.KeyVersion>();
// 삭제할 파일 이름을 전송합니다.
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder1/picture.jpg"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/text.txt"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/music.mp3"));
deleteObjectsRequest.setKeys(keyList);

// 파일을 일괄 삭제합니다.
try {
    DeleteObjectsResult deleteObjectsResult = cosClient.deleteObjects(deleteObjectsRequest);
    List<DeleteObjectsResult.DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) { // 일부만 삭제에 성공할 경우 MultiObjectDeleteException이 반환됩니다.
    List<DeleteObjectsResult.DeletedObject> deleteObjects = mde.getDeletedObjects();
    List<MultiObjectDeleteException.DeleteError> deleteErrors = mde.getErrors();
} catch (CosServiceException e) { // 매개변수 오류, 실명 인증 오류와 같은 기타 오류인 경우 CosServiceException이 표시됩니다.
    e.printStackTrace();
    throw e;
} catch (CosClientException e) { // COS 연결 불가와 같은 클라이언트 오류인 경우입니다.
    e.printStackTrace();
    throw e;
}
```


#### 매개변수 설명

| 매개변수 이름             | 설명 | 유형                 |
| -------------------- | ---- | -------------------- |
| deleteObjectsRequest | 요청 | DeleteObjectsRequest |

Request 멤버 설명:

| 매개변수 이름   | 설명                                                         | 유형               |
| ---------- | ------------------------------------------------------------ | ------------------ |
| bucketName | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| quiet      | 삭제의 결과 반환 방식을 나타냅니다. true와 false 중 선택할 수 있으며 기본값은 false입니다. true로 설정한 경우 실패의 오류 정보만 반환하며, false로 설정한 경우 성공과 실패의 모든 정보를 반환합니다. | boolean            |
| keys       | 객체 경로 리스트입니다. 객체의 버전 넘버는 선택 가능합니다.                             | `List<DeleteObjectsRequest.KeyVersion>` |

DeleteObjectsRequest.KeyVersion 멤버 설명:

| 매개변수 이름 | 설명                                                         | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |
| version  | 버킷의 버전 제어를 활성화할 때, 삭제된 객체의 버전 넘버를 지정할 수 있습니다.           | String |

#### 반환 결과 설명

- 성공: 반환 값이 없습니다.
- 실패: 오류(예: 실명 인증 실패) 발생, 오류 CosClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.


### 보관된 객체 복구 

#### 기능 설명

보관된 객체를 검색해 액세스합니다(POST Object restore).

#### 방법 모델

```java
public void restoreObject(RestoreObjectRequest restoreObjectRequest)
    throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-restore-object)
```java
// 버킷의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

// restore를 설정해 얻는 임시 사본의 유효 기간은 1일입니다.
RestoreObjectRequest restoreObjectRequest = new RestoreObjectRequest(bucketName, key, 1);
// 복구 모드를 Standard로 설정합니다. 기타 선택 모드에는 Expedited, Bulk가 있습니다. 세 가지 복구 모드는 요금과 속도에서 차이가 있습니다.
CASJobParameters casJobParameters = new CASJobParameters();
casJobParameters.setTier(Tier.Standard);
restoreObjectRequest.setCASJobParameters(casJobParameters);
cosClient.restoreObject(restoreObjectRequest);
```

#### 매개변수 설명

| 매개변수 이름             | 설명   | 유형                 |
| -------------------- | ------ | -------------------- |
| restoreObjectRequest | 요청 유형 | RestoreObjectRequest |

Request 멤버 설명:

| 매개변수 이름         | 설명                                                         | 유형             |
| ---------------- | ------------------------------------------------------------ | ---------------- |
| bucketName       | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String           |
| key              | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String           |
| expirationInDays | 복구된 임시 파일의 유효 기간                      | int              |
| casJobParameters | 복구 유형의 설정 정보를 설명합니다. setTier 함수를 호출하여 Tier.Standard, Tier.Expedited, Tier.Bulk의 세 가지 복구 유형 중 하나로 설정할 수 있습니다. DEEP ARCHIVE 유형을 복구할 경우 Tier.Standard와 Tier.Bulk만 지원됩니다. | CASJobParameters |

#### 반환 결과 설명

- 성공: 반환 값이 없습니다.
- 실패: 오류(예: 실명 인증 실패) 발생, 오류 CosClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.



## 멀티파트 작업

다음은 객체의 멀티파트 업로드 작업 내용입니다. 

- 객체 멀티파트 업로드 : 멀티파트 업로드 초기화하고 각 파트별로 업로드하면 멀티파트 업로드를 완료합니다.
- 멀티파트 업로드 재개: 업로드된 파트를 조회하고 파트를 업로드하여 멀티파트 업로드를 완료합니다.
- 업로드된 멀티파트를 삭제합니다. 

### 멀티파트 업로드 조회

#### 기능 설명

지정 버킷에서 진행 중인 멀티파트 업로드를 조회(List Multipart Uploads)합니다.

#### 방법 모델

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### 요청 예시

[//]: # (.cssg-snippet-list-multi-upload)
```java
// Bucket의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
ListMultipartUploadsRequest listMultipartUploadsRequest = new ListMultipartUploadsRequest(bucketName);
listMultipartUploadsRequest.setDelimiter("/");
listMultipartUploadsRequest.setMaxUploads(100);
listMultipartUploadsRequest.setPrefix("");
listMultipartUploadsRequest.setEncodingType("url");
MultipartUploadListing multipartUploadListing = cosClient.listMultipartUploads(listMultipartUploadsRequest);
```


#### 매개변수 설명

| 매개변수 이름                    | 설명 | 유형                        |
| --------------------------- | ---- | --------------------------- |
| listMultipartUploadsRequest | 요청 | ListMultipartUploadsRequest |

Request 멤버 설명:

| 매개변수 이름       | 설명                                                         | 유형   |
| -------------- | ------------------------------------------------------------ | ------ |
| bucketName     | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| keyMarker      | 열거된 항목은 해당 key값에서 시작합니다.                                      | String |
| delimiter      | 세퍼레이터는 하나의 부호입니다. Prefix가 있으면 Prefix를 delimiter 사이의 동일 경로에 놓아 하나로 분류하고 Common Prefix로 정의한 후 모든 Common Prefix를 나열합니다. Prefix가 없으면 경로의 시작점부터 시작합니다. | String |
| prefix         | 반환된 Object key는 반드시 Prefix를 접두사로 두어야 합니다. Prefix를 사용하여 조회할 경우 반환되는 key에는 Prefix가 포함되어 있을 가능성이 높으므로 주의해야 합니다. | String |
| uploadIdMarker | 항목 나열은 해당 UploadId 값으로 시작합니다.                                 | String |
| maxUploads     | 반환되는 multipart의 최대 수량을 설정합니다. 설정 가능 범위는 1에서 1000입니다.                 | String |
| encodingType   | 반환 값의 인코딩 방식을 규정합니다. 선택 가능한 값은 url입니다.                            | String |

#### 반환 결과 설명

- 성공: 현재 진행 중인 멀티파트 업로드 정보를 포함한 MultipartUploadListing을 반환합니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.



### 멀티파트 업로드 초기화

#### 기능 설명

멀티파트 업로드 작업을 초기화합니다(Initiate Multipart Upload).

#### 방법 모델

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-init-multi-upload)
```java
// Bucket의 이름 생성 포맷은 BucketName-APPID입니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
InitiateMultipartUploadRequest initRequest = new InitiateMultipartUploadRequest(bucketName, key);
InitiateMultipartUploadResult initResponse = cosClient.initiateMultipartUpload(initRequest);
uploadId = initResponse.getUploadId();
```


#### 매개변수 설명

| 매개변수 이름                       | 설명 | 유형                           |
| ------------------------------ | ---- | ------------------------------ |
| initiateMultipartUploadRequest | 요청 | InitiateMultipartUploadRequest |

Request 멤버 설명:

| 매개변수 이름   | 설정 방법            | 설명                                                         | 유형   |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | 구조 함수 또는 set 방법 | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| key        | 구조 함수 또는 set 방법 | COS의 Object에 저장된 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)입니다. | String |

#### 반환 결과 설명

- 성공: 이번 멀티파트 업로드의 uploadId를 포함한 InitiateMultipartUploadResult를 반환합니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.


### 멀티파트 업로드

멀티파트 업로드합니다(Upload Part).

#### 방법 모델

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-upload-part)
```java
// 멀티파트 업로드 시 최대 10000개까지 가능하며, 1M-5G 크기의 파트를 지원합니다.
// 파트 크기는 4M로 설정합니다. 총 n개의 파트이 있으면 1~n-1개의 파트은 크기가 같고, 마지막 한 개의 파트은 이전의 파트보다 같거나 작습니다.
partETags = new ArrayList<PartETag>();
int partNumber = 1;
int partSize = 4 * 1024 * 1024;
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
byte data[] = new byte[partSize];
ByteArrayInputStream partStream = new ByteArrayInputStream(data);
// partStream은 part 데이터의 입력 스트림을 의미합니다. 스트림 길이가 partSize입니다.
UploadPartRequest uploadRequest = new UploadPartRequest().withBucketName(bucketName).
        withUploadId(uploadId).withKey(key).withPartNumber(partNumber).
        withInputStream(partStream).withPartSize(partSize);
UploadPartResult uploadPartResult = cosClient.uploadPart(uploadRequest);
// 파트의 Etag를 획득합니다.
String etag = uploadPartResult.getETag();
// 파트의 CRC64를 획득합니다.
String crc64Ecma = uploadPartResult.getCrc64Ecma();
partETags.add(new PartETag(partNumber, etag));  // partETags는 업로드된 part의 모든 Etag 정보를 기록합니다.
// ... partNumber가 2인 파트부터 n인 파트까지 업로드합니다.
```


#### 매개변수 설명

| 매개변수 이름          | 설명 | 유형              |
| ----------------- | ---- | ----------------- |
| uploadPartRequest | 요청 | UploadPartRequest |

Request 멤버 설명:

| 매개변수 이름    | 설정 방법 | 설명                                                         | 유형        |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName  | set 방법  | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String      |
| key         | set 방법  | COS의 Object에 저장된 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)입니다. | String      |
| uploadId    | set 방법  | 지정된 멀티파트 업로드의 uploadId를 식별합니다.                                  | String      |
| partNumber  | set 방법  | 지정된 파트의 번호를 식별합니다. 번호는 반드시 1보다 크거나 같아야 합니다.                                | int         |
| inputStream | set 방법  | 파트를 업로드할 입력 스트림을 기다립니다.                                           | InputStream |
|trafficLimit| set 방법| 파트 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다.  | Int|


#### 반환 결과 설명

- 성공: 멀티파트 업로드의 eTag 정보를 포함한 UploadPartResult를 반환합니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.


#### 반환 매개변수 설명

UploadPartResult 유형은 결과 정보 반환에 사용됩니다. 주요 멤버는 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| partNumber | 지정된 파트의 번호를 식별합니다. | String                |
| eTag        | 멀티파트 업로드의 MD5 값을 반환합니다.                   | String |
|crc64Ecma| 서버는 파트 콘텐츠가 계산한 CRC64를 따릅니다.| String |


### 멀티파트 복사

#### 기능 설명

한 객체의 파트 콘텐츠를 원본 경로에서 타깃 경로로 복사합니다(Upload Part-Copy).

#### 방법 모델

```java
public CopyPartResult copyPart(CopyPartRequest copyPartRequest) throws CosClientException, CosServiceException
```

#### 요청 예시

[//]: # (.cssg-snippet-upload-part-copy)
```java
// 버킷 이름. 형식은 BucketName-APPID입니다.
// 타깃 버킷 이름, 객체 이름, 멀티파트 업로드 ID를 설정합니다.
String destinationBucketName = "examplebucket-1250000000";
String destinationTargetKey = "exampleobject";
int partNumber = 1;
CopyPartRequest copyPartRequest = new CopyPartRequest();
copyPartRequest.setDestinationBucketName(destinationBucketName);
copyPartRequest.setDestinationKey(destinationTargetKey);
copyPartRequest.setUploadId(uploadId);
copyPartRequest.setPartNumber(partNumber);
// 원본 버킷의 리전과 이름 및 객체 이름, 오프셋 구간을 설정합니다.
String sourceBucketRegion = "COS_REGION";
String sourceBucketName = "sourcebucket-1250000000";
String sourceKey = "sourceObject";
Long firstByte = 1L;
Long lastByte = 1048576L;
copyPartRequest.setSourceBucketRegion(new Region(sourceBucketRegion));
copyPartRequest.setSourceBucketName(sourceBucketName);
copyPartRequest.setSourceKey(sourceKey);
copyPartRequest.setFirstByte(firstByte);
copyPartRequest.setLastByte(lastByte);

CopyPartResult copyPartResult = cosClient.copyPart(copyPartRequest);
partETags = new ArrayList<PartETag>();
partETags.add(copyPartResult.getPartETag());
```


#### 매개변수 설명

| 매개변수 이름        | 설명 | 유형            |
| --------------- | ---- | --------------- |
| copyPartRequest | 요청 | CopyPartRequest |

Request 멤버 설명:

| 매개변수 이름              | 설정 방법 | 설명                                                         | 유형   |
| --------------------- | -------- | ------------------------------------------------------------ | ------ |
| destinationBucketName | set 방법 | 타깃 버킷의 이름입니다. Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| destinationKey        | set 방법 | 타깃 객체의 이름입니다. COS의 Object에 저장된 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)입니다. | String |
| uploadId              | set 방법 | 지정된 멀티파트 업로드의 uploadId를 식별합니다.                                  | String |
| partNumber            | set 방법 | 지정된 파트의 번호를 식별합니다. 번호는 반드시 1보다 크거나 같아야 합니다.                                | int    |
| sourceBucketRegion    | set 방법 | 원본 버킷의 지역입니다.                                               | Region |
| sourceBucketName      | set 방법 | 원본 버킷의 이름입니다.                                               | String |
| sourceKey             | set 방법 | 타깃 객체의 이름입니다. COS의 Object에 저장된 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)입니다. | String |
| firstByte             | set 방법 | 원본 객체의 첫 바이트 오프셋입니다.                                          | Long   |
| lastByte              | set 방법 | 원본 객체의 마지막 바이트 오프셋입니다.                                       | Long   |

#### 반환 결과 설명

- 성공: 파트의 ETag 정보를 포함한 CopyPartResult를 반환합니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.


### 업로드된 파트 조회

#### 기능 설명

특정 멀티파트 업로드 작업 중 업로드된 파트(List Parts)를 조회합니다.

#### 방법 모델

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-list-parts)
```java
// ListParts는 멀티파트 업로드 complete 이전 또는 멀티파트 업로드 abort 이전에 업로드된 파트 중에서 uploadId에 상응하는 파트의 정보를 획득하는 데 사용되며, partEtags 구성에도 사용할 수 있습니다.
List<PartETag> partETags = new ArrayList<PartETag>();
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
ListPartsRequest listPartsRequest = new ListPartsRequest(bucketName, key, uploadId);
PartListing partListing = null;
do {
    partListing = cosClient.listParts(listPartsRequest);
    for (PartSummary partSummary : partListing.getParts()) {
        partETags.add(new PartETag(partSummary.getPartNumber(), partSummary.getETag()));
    }
    listPartsRequest.setPartNumberMarker(partListing.getNextPartNumberMarker());
} while (partListing.isTruncated());
```


#### 매개변수 설명

| 매개변수 이름         | 설정 방법            | 설명                                                         | 유형   |
| ---------------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName       | 구조 함수 또는 set 방법 | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| key              | 구조 함수 또는 set 방법 | 객체의 이름입니다.                                                   | String |
| uploadId         | 구조 함수 또는 set 방법 | 이번에 조회할 멀티파트 업로드의 uploadId입니다.                               | String |
| maxParts         | set 방법            | 한번에 반환 가능한 최대 항목 수량입니다. 기본값은 1000입니다.                             | String |
| partNumberMarker | set 방법            | UTF-8 이진법 순서대로 항목을 나열합니다. 모든 나열 항목은 marker로 시작합니다.  | String |
| encodingType     | set 방법            | 반환 값의 인코딩 방식을 규정합니다.                                         | String |

#### 반환 결과 설명

- 성공: 모든 파트의 ETag와 번호 및 다음 list의 시작 marker를 포함한 PartListing을 반환합니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.


### 멀티파트 업로드 완료 

#### 기능 설명

전체 파일의 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 방법 모델

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-complete-multi-upload)
```java
// complete 멀티파트 업로드를 완료합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
CompleteMultipartUploadRequest compRequest = new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
CompleteMultipartUploadResult result = cosClient.completeMultipartUpload(compRequest);
```


#### 매개변수 설명

| 매개변수 이름   | 설정 방법&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            | 설명                                                         | 유형              |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | 구조 함수 또는 set 방법 | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String            |
| key        | 구조 함수 또는 set 방법 | COS의 Object에 저장된 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)입니다. | String            |
| uploadId   | 구조 함수 또는 set 방법 | 지정된 멀티파트 업로드의 uploadId를 식별합니다.                                  | String            |
| partETags  | 구조 함수 또는 set 방법 | 파트의 번호와 업로드 반환의 eTag를 식별합니다.                            | ` List<PartETag>` |

#### 반환 결과 설명

- 성공: 완료된 객체의 eTag 정보를 포함한 CompleteMultipartUploadResult를 반환합니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.


### 멀티파트 업로드 중지

#### 기능 설명

멀티파트 업로드 작업을 중지하고 업로드된 파트는 삭제합니다(Abort Multipart Upload). 

#### 방법 모델

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # (.cssg-snippet-abort-multi-upload)
```java
// abortMultipartUpload는 아직 complete되지 않은 멀티파트 업로드를 중지하는 데 사용됩니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
cosClient.abortMultipartUpload(abortMultipartUploadRequest);
```


#### 매개변수 설명

| 매개변수 이름   | 설정 방법            | 설명                                                         | 유형   |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | 구조 함수 또는 set 방법 | Bucket의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| key        | 구조 함수 또는 set 방법 | COS의 Object에 저장된 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)입니다. | String |
| uploadId   | 구조 함수 또는 set 방법 | 지정된 멀티파트 업로드의 uploadId를 식별합니다.                                  | String |

#### 반환 결과 설명

- 성공: 반환 값이 없습니다.
- 실패: 오류(예: 실명 인증 실패) 발생,  오류 CosClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.



## 고급 인터페이스(권장)

고급 API는 TransferManger가 캡슐화를 통해 인터페이스를 업로드/다운로드합니다. 내부에 있는 스레드 풀이 사용자의 업로드/다운로드 요청을 수락하므로 사용자는 비동기화 작업 제출을 선택할 수 있습니다.

[//]: # (.cssg-snippet-transfer-init)
```java
// 스레드 풀의 크기는 클라이언트와 COS 네트워크가 안정적인 상황(예: Tencent Cloud의 CVM을 사용해 리전 내 COS 업로드)에서 16 또는 32로 설정하기를 권장합니다. 16 또는 32로도 원활한 네트워크 리소스 이용이 가능합니다.
// 공용 네트워크를 이용한 전송 및 네트워크 대역폭의 품질이 좋지 않은 경우 해당 값을 줄이길 권장합니다. 네트워크 속도가 느려져 요청 시간이 초과할 수 있습니다.
ExecutorService threadPool = Executors.newFixedThreadPool(32);
// threadpool을 전송합니다. 스레드 풀을 전송하지 않을 경우 기본적으로 TransferManager에 싱글 스레드의 스레드 풀이 생성됩니다.
TransferManager transferManager = new TransferManager(cosClient, threadPool);
// 고급 인터페이스의 멀티파트 업로드 임계값과 파트 크기를 10MB로 설정합니다.
TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
transferManagerConfiguration.setMultipartUploadThreshold(10 * 1024 * 1024);
transferManagerConfiguration.setMinimumUploadPartSize(10 * 1024 * 1024);
transferManager.setConfiguration(transferManagerConfiguration);
```

transferManager를 사용하지 않을 경우 리소스 유출 방지를 위해 수동으로 비활성화해주십시오.

```java
// TransferManger를 비활성화합니다.
transferManager.shutdownNow();
```

#### 매개변수 설명

TransferManagerConfiguration 유형은 고급 인터페이스의 설정 정보를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

|  멤버 이름 | 설정 방법            | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize   | set 방법 | 멀티파트 업로드의 파트 크기입니다. 단위는 바이트(Byte)이며, 기본값은 5MB입니다. | long         |
| multipartUploadThreshold   | set 방법 | 해당 값보다 크거나 같고 동시 접속하는 멀티파트 업로드 파일입니다. 단위는 바이트(Byte)이며, 기본값은 5MB입니다.  | long         |
| multipartCopyThreshold         | set 방법 | 해당 값보다 크거나 같고 동시 접속하는 파트 복사 파일입니다. 단위는 바이트(Byte)이며, 기본값은 5GB입니다. | long           |
| multipartCopyPartSize        | set 방법 | 파트 복사 시 파트의 크기입니다. 단위는 바이트(Byte)이며, 기본값은 100MB입니다.           | long    |

### 객체 업로드

#### 기능 설명

고급 업로드 인터페이스는 사용자 파일의 길이와 데이터 유형에 따라 자동으로 간단한 업로드와 멀티파트 업로드 중 하나를 선택합니다. 자세한 설명은 아래를 참조하십시오.
- 멀티파트 업로드 임계값보다  작거나 Content-Length 헤더가 없는 스트림 업로드의 경우 고급 인터페이스는 간단한 업로드를 선택합니다.
- 멀티파트 업로드 임계값보다 크지만 Content-Length 헤더가 없는 스트림 업로드의 경우 고급 인터페이스는 멀티파트 업로드를 선택합니다.
- 데이터 유형이 File 유형인 파일 업로드의 경우 고급 인터페이스는 멀티 스레드로 동시 접속하여 다수의 파트를 동시에 업로드합니다.

>?기타 관련 설정 속성, 스토리지 유형, MD5 인증 등은 [PUT Object API](https://intl.cloud.tencent.com/document/product/436/7749)를 참조하십시오.

#### 방법 모델

```java
// 객체 업로드
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### 요청 예시

[//]: # (.cssg-snippet-transfer-upload-file)
```java
// 예시1:
// 버킷의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// 로컬 파일을 업로드합니다.
Upload upload = transferManager.upload(putObjectRequest);
// 전송 종료를 기다립니다(업로드 종료 대기와 동기화를 원하는 경우 waitForCompletion을 호출합니다).
UploadResult uploadResult = upload.waitForUploadResult();

```


#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 방법&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | 구조 함수 또는 set 방법 | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String         |
| key          | 구조 함수 또는 set 방법 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String         |
| file         | 구조 함수 또는 set 방법 | 로컬 파일                                                     | File           |
| input        | 구조 함수 또는 set 방법 | 입력 스트림                                                       | InputStream    |
| metadata     | 구조 함수 또는 set 방법 | 파일의 메타데이터                                                 | ObjectMetadata |
|trafficLimit | set 방법| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|아니오|

>?다수의 파트를 동시 업로드할 경우 trafficLimit는 모든 파트의 업로드 속도를 제한합니다. 이때 스레드 풀의 스레드 수를 조정하여 파일의 업로드 속도를 제어해야 합니다.

#### 반환 값

- 성공: Upload를 반환합니다. 업로드의 종료 여부를 확인할 수 있고, 업로드 종료 대기와 동기화할 수도 있습니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.



#### 반환 매개변수 설명

Upload의 waitForUploadResult() 방법을 호출하여 획득한 객체 업로드 정보는 유형 UploadResult에 기록됩니다. 유형 UploadResult의 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br/>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |
| requestId  | 요청 Id                                                       | String |
| dateStr    | 현재 서버 시간                                               | String |
| versionId  | 여러 버전의 버킷을 활성화하여 객체의 버전 넘버 Id를 반환합니다.                      | String |
| crc64Ecma  | 서버는 객체 콘텐츠가 계산한 CRC64를 따릅니다.                           | String |




### 객체 다운로드

#### 기능 설명

COS의 객체를 로컬에 다운로드합니다.

#### 방법 모델

```java
// 객체 다운로드
public Download download(final GetObjectRequest GetObjectRequest, final File file);
```

#### 요청 예시

[//]: # (.cssg-snippet-transfer-download-object)
```java
// Bucket의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localDownFile = new File(localFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
// 사용 단위는 bit/s로 제한되며, 설정된 다운로드 대역폭은 10MB/s로 제한되어 있습니다.
getObjectRequest.setTrafficLimit(80*1024*1024);
// 파일 다운로드
Download download = transferManager.download(getObjectRequest, localDownFile);
// 전송 종료를 기다립니다(업로드 종료 대기와 동기화를 원하는 경우 waitForCompletion을 호출합니다).
download.waitForCompletion();
```


#### 매개변수 설명

| 매개변수 이름         | 설명               | 유형             |
| ---------------- | ------------------ | ---------------- |
| getObjectRequest | 객체 다운로드 요청       | GetObjectRequest |
| file             | 다운로드할 로컬 파일 | File             |

Request 멤버 설명:

| Request 멤버 | 설정 방법&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            | 설명                                                         | 유형   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName   | 구조 함수 또는 set 방법 | 버킷의 이름 생성 포맷은 BucketName-APPID이며, 세부 사항은 [이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312?lang=en&pg=#bucket-naming-conventions)을 참조하십시오. | String |
| key          | 구조 함수 또는 set 방법 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |
| range    | set 방법            | 다운로드 range 범위                       | Long[] |
| trafficLimit | set 방법    | 객체 다운로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다.  | int |

#### 반환 값

- 성공: Download를 반환합니다. 다운로드의 종료 여부를 확인할 수 있고, 다운로드 종료 대기와 동기화할 수도 있습니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.


### 객체 복사

#### 기능 설명

Copy 인터페이스는 객체 크기에 따라 자동으로 간단한 복사 또는 파트 복사 중 하나를 선택합니다. 사용자는 복사할 파일의 크기를 고려하지 않아도 됩니다.

#### 방법 모델

```java
// 객체 업로드
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### 요청 예시

[//]: # (.cssg-snippet-transfer-copy-object)
```java
// 복사할 bucket region은 리전 간 복사를 지원합니다.
String secretId = "COS_SECRETID";
String secretKey = "COS_SECRETKEY";
COSCredentials srcCredentials = new BasicCOSCredentials(secretId, secretKey);
Region srcBucketRegion = new Region("COS_REGION");
// 원본 Bucket입니다. 버킷의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String srcBucketName = "sourcebucket-1250000000";
// 복사할 원본 파일입니다.
String srcKey = "sourceObject";
// 타깃 Bucket입니다. 버킷의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다.
String destBucketName = "examplebucket-1250000000";
// 복사할 타깃 파일입니다.
String destKey = "exampleobject";
// 원본 파일 정보를 획득하는 데 사용되는 srcCOSClient를 생성합니다.
COSClient srcCOSClient = new COSClient(srcCredentials, new ClientConfig(srcBucketRegion));
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
    // 비동기 결과 copy를 반환합니다. waitForCopyResult를 호출하여 copy 결과 대기와 동기화할 수도 있습니다. 성공하면 CopyResult를 반환하고, 실패하면 이상 경고 메시지를 표시합니다.
    CopyResult copyResult = copy.waitForCopyResult();
    // 복사로 생성된 객체의 CRC64를 획득합니다.
    String crc64Ecma = copyResult.getCrc64Ecma();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```


#### 매개변수 설명

| 매개변수 이름          | 설명         | 유형              |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | 파일 복사 요청 | CopyObjectRequest |

Request 멤버 설명:

| 매개변수 이름              | 설명                                                         | 유형   |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion    | 원본 Bucket Region입니다. 기본값은 현재 clientconfig의 region과 일치하며, 통합 리전 복사를 의미합니다. | String |
| sourceBucketName      | 원본 버킷 이름입니다. 버킷의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String |
| sourceKey             | 원본 객체 키입니다. 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |
| sourceVersionId       | 원본 파일 version id입니다(버전을 제어하는 원본 Bucket 활성화에 적합합니다). 기본값은 원본 파일의 최신 버전입니다. | String |
| destinationBucketName | 타깃 버킷 이름입니다. 버킷의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 포맷을 따라야 합니다. | String |
| destinationKey        | 타깃 객체 키입니다. 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 세부 사항은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참조하십시오. | String |
| storageClass          | 복사된 타깃 파일의 스토리지 유형입니다. 열거 값은 Standard, Standard_IA이며 기본값은 Standard입니다. 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참조하십시오. | String |

#### 반환 값

- 성공: Copy를 반환합니다. Copy의 종료 여부를 확인할 수 있고, 업로드 종료 대기와 동기화할 수도 있습니다.
- 실패: 오류 발생(실명 인증 실패), 오류 osClientException 또는 CosServiceException이 표시됩니다. 세부 사항은 [오류 처리](https://intl.cloud.tencent.com/document/product/436/31537)를 참조하십시오.

