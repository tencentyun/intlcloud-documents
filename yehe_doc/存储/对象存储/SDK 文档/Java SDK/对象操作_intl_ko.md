## 소개

본 문서는 객체의 고급 인터페이스, 간단한 작업, 멀티파트 작업 관련 API 개요 및 SDK 예시 코드를 제공합니다.

**간단한 작업**

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket(List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | 객체 리스트 조회   | 버킷의 일부 또는 모든 객체 조회            |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | 객체 버전 조회 |   버킷의 일부 또는 모든 객체와 이전 버전 정보 조회   |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 객체 메타데이터 조회 | 객체의 메타데이터 정보 조회                  |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 객체 업로드   | 객체를 버킷에 업로드                      |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | 객체 추가 업로드 | 멀티파트에 추가하는 방식으로 객체 업로드               |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 객체 다운로드       | 로컬에 객체 다운로드        |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 객체 복사   | 파일을 타깃 경로에 복사                        |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 객체 삭제   | 버킷에서 지정 객체 삭제 |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 객체 일괄 삭제   | 버킷에서 지정 객체를 일괄 삭제                |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 보관된 객체 복구 | 아카이브 유형의 객체 검색 및 액세스           |

**멀티파트 작업**

| API                                                          | 작업명         | 작업 설명                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 멀티파트 업로드 조회   | 현재 진행 중인 멀티파트 업로드 정보 조회         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 멀티파트 업로드 초기화 | Multipart Upload 작업 초기화     |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 파트 업로드       | 파일 멀티파트 업로드                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 멀티파트 복사       | 다른 객체를 한 파트로 복사             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 업로드된 파트 조회   | 특정 멀티파트 업로드 작업에서 업로드된 파트 조회   |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 멀티파트 업로드 완료   | 전체 파일의 멀티파트 업로드 완료               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 멀티파트 업로드 중지   | 하나의 멀티파트 업로드 작업 중지 및 이미 업로드한 파트 삭제 |

## 간단한 작업

### 객체 리스트 조회

#### 기능 설명

버킷의 일부 또는 모든 객체를 조회합니다.

#### 메소드 프로토타입

```java
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest) throws CosClientException, CosServiceException;
```

>! COS에서 나열된 객체 키가 project/ 이면 비어있는 객체를 통해 전형적인 폴더 표시 방법으로 재현한 것입니다. [폴더와 디렉터리](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오.
>

#### 요청 예시

[//]: # ".cssg-snippet-get-bucket"
```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// bucket 이름 설정
listObjectsRequest.setBucketName(bucketName);
// prefix는 나열된 object의 key가 prefix로 시작함을 의미합니다.
listObjectsRequest.setPrefix("images/");
// delimiter는 세퍼레이터를 의미합니다. /로 설정하면 현재 디렉터리의 object를 나열하고, 공백으로 설정하면 전체 object를 나열합니다.
listObjectsRequest.setDelimiter("/");
// 순회할 객체의 최대 수량을 설정합니다. listobject 1회당 최대 1000개까지 지원합니다.
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
    // common prefix는 delimiter로 잘린 경로를 표시합니다. 예를 들어 delimiter를 /로 설정하면 common prefix는 모든 서브 디렉터리의 경로를 표시합니다.
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // object summary는 나열된 모든 object 리스트를 표시합니다.
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // 파일의 경로 key
        // "aaa/"와 같은 파일이 나열될 수 있습니다. 디렉터리로 착각하지 마십시오. 실제로는 일반 파일이기도 합니다.
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
| listObjectsRequest | 파일 리스트 요청 획득 | ListObjectsRequest |

Request 멤버 설명 :

| Request 멤버 | 설정 방법          | 설명                                                         | 유형    |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName   | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String  |
| prefix       | 구조 함수 또는 set 메소드 | 반환되는 결과 객체를 제한하고 prefix를 접두사로 합니다. 기본적으로 Bucket의 모든 멤버를 제한하지 않습니다.<br>기본값: ""(공백) | String  |
| marker       | 구조 함수 또는 set 메소드 | list의 시작 위치를 표시합니다. 처음에는 공백으로 설정해도 되지만, 다음 요청은 이전 listObjects 반환값의 nextMarker로 설정해야 합니다. | String  |
| delimiter    | 구조 함수 또는 set 메소드 | 세퍼레이터. prefix로 시작하며 delimiter가 처음 나타나 끝나는 경로의 반환을 제한합니다. | String  |
| maxKeys      | 구조 함수 또는 set 메소드 | 멤버 최대 반환 수(1000을 초과할 수 없음).<br>기본값: 1000          | Integer |

#### 반환 결과 설명

- 성공: 모든 멤버 및 nextMarker를 포함한 ObjectListing 유형을 반환합니다.  
- 실패: CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

### 객체 버전 조회

#### 기능 설명

버킷의 일부 또는 모든 객체 및 이전 버전 정보를 조회합니다.

#### 메소드 프로토타입

```java
public VersionListing listVersions(ListVersionsRequest listVersionsRequest)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";

ListVersionsRequest listVersionsRequest = new ListVersionsRequest();
listObjectsRequest.setBucketName(bucketName);
// prefix는 나열된 object의 key가 prefix로 시작함을 의미합니다.
listVersionsRequest.setPrefix("");
// 순회할 객체의 최대 수량을 설정합니다. listobject 1회당 최대 1000개까지 지원합니다.
listObjectsRequest.setMaxKeys(1000);

VersionListing versionListing = null;

do {
    try {
        versionListing = cosclient.listVersions(listVersionsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }

    List<COSVersionSummary> cosVersionSummaries = versionListing.getVersionSummaries();
    for (COSVersionSummary cosVersionSummary : cosVersionSummaries) {
        System.out.println(cosVersionSummary.getKey() + ":" + cosVersionSummary.getVersionId());
    }

    String keyMarker = versionListing.getNextKeyMarker();
    String versionIdMarker = versionListing.getNextVersionIdMarker();

    listVersionsRequest.setKeyMarker(keyMarker);
    listVersionsRequest.setVersionIdMarker(versionIdMarker);

} while (versionListing.isTruncated());
```

#### 매개변수 설명

| 매개변수 이름           | 설명             | 유형               |
| ------------------ | ---------------- | ------------------ |
| listVersionsRequest | 객체 버전 정보 요청 획득 | ListVersionsRequest |

Request 멤버 설명 :

| Request 멤버 | 설정 방법            | 설명                                                         | 유형    |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| bucketName   | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String  |
| prefix       | 구조 함수 또는 set 메소드 | 반환되는 결과 객체를 제한하고 prefix를 접두사로 합니다. 기본적으로 Bucket의 모든 멤버를 제한하지 않습니다. <기본값: ""(공백) | String  |
| keyMarker       | 구조 함수 또는 set 메소드 | list의 시작 위치를 표시합니다. 처음에는 공백으로 설정해도 되지만, 다음 요청은 이전 listObjects 반환값의 nextKeyMarker로 설정해야 합니다. | String  |
| versionIdMarker | 구조 함수 또는 set 메소드 | list의 시작 위치를 표시합니다. 처음에는 공백으로 설정해도 되지만, 다음 요청은 이전 listObjects 반환값의 nextVersionIdMarker로 설정해야 합니다. | String  |
| delimiter    | 구조 함수 또는 set 메소드 | 세퍼레이터. prefix로 시작하며 delimiter가 처음 나타나 끝나는 경로의 반환을 제한합니다. | String  |
| maxResults      | 구조 함수 또는 set 메소드 | 멤버 최대 반환 수(1000을 초과할 수 없음). 기본값: 1000          | Integer |

#### 반환 결과 설명

- 성공: 모든 멤버 및 nextKeyMarker와 nextVersionIdMarker를 포함한 ObjectListing 유형을 반환합니다.
- 실패: CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

### 객체 메타데이터 조회

#### 기능 설명

지정한 객체가 버킷에 있는지 확인합니다.

#### 메소드 프로토타입

```java
public ObjectMetadata getObjectMetadata(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # ".cssg-snippet-head-object"
```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(bucketName, key);

// 이번 요청의 requestId 획득
System.out.println(objectMetadata1.getRequestId());
// 객체의 CRC64 검사값 획득
System.out.println(objectMetadata.getCrc64Ecma());
// 객체의 마지막 업로드 시간 획득
System.out.println(objectMetadata1.getLastModified());
// 객체의 크기 획득
System.out.println(objectMetadata.getContentLength());
// COS 유형 획득
System.out.println(objectMetadata.getStorageClass());
```

#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |

#### 반환 결과 설명

- 성공: 사용자 정의 헤더, Etag 등 객체 메타 정보를 포함한 ObjectMetadata 유형을 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

ObjectMetadata 유형은 객체의 메타 정보를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | 캐시의 타임아웃 시간은 HTTP 응답 헤더의 Expires 필드 값 | Date                |
| ongoingRestore  | 현재 CAS 유형에서 해당 객체를 복구하는 중                        | Boolean             |
| userMetadata    | 접두사가 x-cos-meta-인 사용자 정의 메타 정보               | Map&lt;String, String&gt; |
| metadata        | 사용자 정의 메타 정보를 제외한 기타 헤더                    | Map&lt;String, String&gt; |
| restoreExpirationTime  | 보관된 객체 복구 사본의 만료 시간  | Date |


### 객체 업로드(폴더 생성)

#### 기능 설명

객체를 지정한 버킷에 업로드합니다(PUT Object). 로컬 파일 또는 길이를 알고 있는 입력 스트림 콘텐츠를 COS에 업로드합니다. 이미지 유형의 크기가 작은 파일(20MB 이하) 업로드에 적합하며, 최대 5GB까지 지원합니다. 5GB를 초과하는 파일은 [멀티파트 업로드](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) 또는 [고급 API](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89)로 업로드하십시오.

- 업로드 과정에서 기본적으로 파일의 길이와 MD5에 대한 검사를 진행합니다. MD5 검사 비활성화는 예시 코드를 참고하십시오.
- COS에 Key가 동일한 객체가 있을 경우 업로드 과정에서 덮어씁니다.
- 업로드 후 동일한 key로 GetObject 인터페이스를 호출하여 파일을 로컬에 다운로드할 수 있으며, [사전 서명된 링크](https://intl.cloud.tencent.com/document/product/436/31536)를 생성(다운로드 시 method를 GET으로 지정. 자세한 인터페이스 설명은 아래 참고)하여 다른 포트로 전송 후 다운로드할 수도 있습니다.
- COS는 '/'로 구분하는 객체 경로를 가상 폴더로 인식합니다. 이러한 특성에 따라 이름이 '/'로 끝나는 빈 스트림을 업로드하면 COS에 빈 폴더를 생성할 수 있습니다.
또는, '/'로 구분되는 객체 이름을 업로드하면 파일이 포함된 폴더를 자동으로 생성합니다. 이에 따라 해당 폴더에 새로운 파일을 추가할 경우 COS에 파일 업로드 시 Key를 해당 디렉터리 접두사로 입력하기만 하면 됩니다. 

#### 메소드 프로토타입

```java
// 방법1  로컬 파일을 COS에 업로드
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// 방법2  입력 스트림을 COS에 업로드
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// 방법3  위의 두 가지 방법 패키지에 더 세분화된 매개변수 제어를 지원(예: content-type, content-disposition 등)
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### 요청 예시1: 로컬 파일 업로드

[//]: # ".cssg-snippet-put-object-flex"
<dx-codeblock>
:::  java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";

File localFile = new File(localFilePath);
String key = "exampleobject";
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, localFile);
String etag = putObjectResult.getETag();  // 파일의 etag 획득
:::
</dx-codeblock>

#### 요청 예시2: 가상 디렉터리에 업로드

<dx-codeblock>
:::  java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";

File localFile = new File(localFilePath);
// COS의 가상 디렉터리는 사실 경로에서 '/'로 끝나는 접두사입니다.
String dir = "exampledir/";
String filename = "exampleobject";

String key = dir+filename;
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, localFile);
String etag = putObjectResult.getETag();  // 파일의 etag 획득
:::
</dx-codeblock>

#### 요청 예시3: 입력 스트림에서 업로드. 입력 스트림의 길이를 사전에 알려야 하며, 그렇지 않을 경우 oom 문제가 발생할 수 있습니다.

<dx-codeblock>
:::  java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";

FileInputStream fileInputStream = new FileInputStream(localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// 입력 스트림 길이를 설정합니다.(STREAMLENGTH는 자신의 스트림 크기에 맞게 교체)
objectMetadata.setContentLength(STREAMLENGTH);
// Content type을 설정. 기본값: application/octet-stream
objectMetadata.setContentType("application/pdf");
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, fileInputStream, objectMetadata);
String etag = putObjectResult.getETag();
// 입력 스트림 비활성화...
:::
</dx-codeblock>

#### 요청 예시4: 디렉터리 생성(빈 바이트 스트림의 객체 업로드)

<dx-codeblock>
:::  java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";

// 생성할 디렉터리 이름을 지정합니다. '/'로 끝나야 합니다.
String key = "cos_dir/";
// 크기가 0인 스트림 생성
InputStream emptyContent = new ByteArrayInputStream(new byte[0]);
ObjectMetadata metadata = new ObjectMetadata();
metadata.setContentLength(0);
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, emptyContent, objectMetadata);
String etag = putObjectResult.getETag();
// 입력 스트림 비활성화...
:::
</dx-codeblock>

#### 요청 예시5: 업로드 속도 제한

<dx-codeblock>
:::  java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";

// 1 storage-class 스토리지 유형의 열거 값은 Standard, Standard_IA, Archive이며, 기본값은 Standard입니다. 더 많은 스토리지 유형은 https://intl.cloud.tencent.com/document/product/436/30925를 참고하십시오.
// 2 content-type, 로컬 파일 업로드의 기본값은 로컬 파일의 확장명에 따라 매핑됩니다(예: jpg 파일은 image/jpeg로 매핑).
// 스트림 업로드의 기본값은 application/octet-stream입니다.
// 3 전역에서 MD5 업로드 검사를 비활성화하려면 시스템 환경에 변수를 설정해야 합니다. 이 설정은 모든 업로드 검사에 영향을 줍니다. 기본값은 검사 활성화입니다.
// MD5 검사 비활성화:  System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
// MD5 검사 활성화:  System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, null);
File localFile = new File(localFilePath);
String key = "picture.jpg";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// 스토리지 유형을 표준IA로 설정
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
// 사용자 정의 속성을 설정(예: content-type, content-disposition 등)
objectMetadata = new ObjectMetadata();
// 속도 제한 단위는 bit/s이며, 업로드 속도를 10MB/s로 제한합니다.
putObjectRequest.setTrafficLimit(80*1024*1024);
// Content type을 설정. 기본값: application/octet-stream
objectMetadata.setContentType("image/jpeg");
putObjectRequest.setMetadata(objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
// 객체의 Etag 획득
String etag = putObjectResult.getETag();
// 객체의 CRC64 획득
String crc64Ecma = putObjectResult.getCrc64Ecma();
:::
</dx-codeblock>



#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 방법    | 설명                                                         | 유형   | 필수 입력 |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName   | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String         | Yes|
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String         | Yes|
| file         | 구조 함수 또는 set 메소드 | 로컬 파일                                                     | File           |No|
| input        | 구조 함수 또는 set 메소드 | 입력 스트림                                                       | InputStream    | No|
| metadata     | 구조 함수 또는 set 메소드 | 객체의 메타데이터                                                 | ObjectMetadata | No|
|trafficLimit | set 메소드| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|No|

ObjectMetadata 유형은 객체의 메타 정보를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | 캐시의 타임아웃 시간은 HTTP 응답 헤더의 Expires 필드 값 | Date                |
| ongoingRestore  | 현재 CAS 유형에서 해당 객체를 복구하는 중                        | Boolean             |
| userMetadata    | 접두사가 x-cos-meta-인 사용자 정의 메타 정보               | Map&lt;String, String&gt; |
| metadata        | 사용자 정의 메타 정보를 제외한 기타 헤더                    | Map&lt;String, String&gt; |
| restoreExpirationTime  | 보관된 객체 복구 사본의 만료 시간  | Date |


#### 반환 결과 설명

- 성공: 파일의 eTag 등 정보를 포함한 PutObjectResult입니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

PutObjectResult 유형은 결과 정보 반환에 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | 요청 ID | String                |
| dateStr  | 현재 서버 시간                        | String             |
| versionId    | 버전을 제어하는 버킷을 활성화한 후 객체의 버전 넘버 ID를 반환              | String |
| eTag        | 간편 업로드 인터페이스에서 반환하는 객체의 MD5값                    | String |
|crc64Ecma| 서버에서 객체 콘텐츠에 따라 계산한 CRC64| String |

### 객체 추가 업로드

#### 기능 설명

멀티파트 추가 방식으로 객체를 업로드합니다(APPEND Object).

#### 메소드 프로토타입

```java
public AppendObjectResult appendObject(AppendObjectRequest appendObjectRequest)
        throws CosServiceException, CosClientException
```

#### 요청 예시

```java
// bucket 이름에는 반드시 appid가 포함됨
String bucketName = "examplebucket-1251668577";
String key = "aaa/bbb.txt";
try {
    File localFile = new File("1M.txt");
    AppendObjectRequest appendObjectRequest = new AppendObjectRequest(bucketName, key, localFile);
    appendObjectRequest.setPosition(0L);
    AppendObjectResult appendObjectResult = cosclient.appendObject(appendObjectRequest);
    long nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);

    localFile = new File("2M.txt");
    appendObjectRequest = new AppendObjectRequest(bucketName, key, localFile);
    appendObjectRequest.setPosition(nextAppendPosition);
    appendObjectResult = cosclient.appendObject(appendObjectRequest);
    nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```

#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| -------------------- | ------------ | ---------------- |
| appendObjectRequest | 파일 추가 업로드 요청 | AppendObjectRequest |

AppendObjectRequest 참석자 설명: 

| Request 멤버 | 설정 방법   | 설명                                                         | 유형   | 필수 입력 여부 |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String         | Yes|
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String         | Yes|
| localfile    | 구조 함수 또는 set 메소드 | 로컬 파일                                                     | File           |No|
| input        | 구조 함수 또는 set 메소드 | 입력 스트림                                                       | InputStream    | No|
| metadata     | 구조 함수 또는 set 메소드 | 객체의 메타데이터                                                 | ObjectMetadata | No|
|trafficLimit | set 메소드| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|No|
| position | set 메소드| 작업 시작 위치 추가, 단위: byte | Long | Yes |

#### 반환 결과 설명

- 성공: AppendObjectResult.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

AppendObjectResult 유형은 결과 정보 반환에 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| metadata | 헤더 반환 | ObjectMetadata               |
| nextAppendPosition| 다음에 추가될 위치 | Long |


### 객체 다운로드

#### 기능 설명

객체를 로컬에 다운로드합니다(GET Object).

#### 메소드 프로토타입

```java
// 방법1 파일을 다운로드하고 입력 스트림을 획득
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
// 방법2 로컬에 파일 다운로드.
public ObjectMetadata getObject(GetObjectRequest getObjectRequest, File destinationFile)
            throws CosClientException, CosServiceException;
```

#### 요청 예시1: 다운로드한 파일의 입력 스트림 획득

[//]: # ".cssg-snippet-get-object"
```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();

// 입력 스트림
byte[] bytes = null;
try {
    bytes = IOUtils.toByteArray(cosObjectInput);
} catch (IOException e) {
    e.printStackTrace();
} finally {
    cosObjectInput.close(); 
}

//객체의 CRC64 다운로드
String crc64Ecma = cosObject.getObjectMetadata().getCrc64Ecma();

// 방법2 로컬에 파일 다운로드
String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

#### 요청 예시2: 로컬에 파일 다운로드

```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

#### 요청 예시3: 다운로드 속도 제한

[//]: # ".cssg-snippet-get-object"
```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
// 속도 제한 단위는 bit/s이며, 다운로드 속도를 10MB/s로 제한합니다.
getObjectRequest.setTrafficLimit(80*1024*1024);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();

// 입력 스트림
byte[] bytes = null;
try {
    bytes = IOUtils.toByteArray(cosObjectInput);
} catch (IOException e) {
    e.printStackTrace();
} finally {
    cosObjectInput.close();
}

// 객체의 CRC64 다운로드
String crc64Ecma = cosObject.getObjectMetadata().getCrc64Ecma();
```

#### 매개변수 설명

| 매개변수 이름         | 설명           | 유형             |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | 파일 다운로드 요청   | GetObjectRequest |
| destinationFile  | 로컬 저장 파일 | File             |

Request 멤버 설명:

| Request 멤버 | 설정 방법         | 설명                                                         | 유형   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName   | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| range  | set 메소드             | 다운로드 range 범위                                            | Long[] |
| trafficLimit | set 메소드    | 객체 다운로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다.  | Int |


#### 반환 결과 설명

- **방법1 (다운로드한 파일의 입력 스트림 획득)**
  - 성공: 입력 스트림 및 객체 속성을 포함한 COSObject 유형을 반환합니다.
  - 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.
- **방법2 (로컬에 파일 다운로드)**
  - 성공: 파일의 사용자 정의 헤더와 content-type 등 속성을 포함한 파일의 속성 ObjectMetadata를 반환합니다.
  - 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

COSObject 유형은 결과 정보 반환에 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| bucketName   |  Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key          | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| metadata | 객체의 메타데이터  | ObjectMetadata |
| objectContent | COS 객체 콘텐츠를 포함한 데이터 스트림  | COSObjectInputStream |


### 객체 복사

#### 기능 설명 

한 객체를 다른 객체에 복사합니다(Put Object Copy). 리전 간, 계정 간, Bucket 간 복사를 지원하며, 원본 파일의 읽기 권한 및 타깃 파일의 쓰기 권한이 필요합니다. 최대 5GB의 파일 복사를 지원하며, 5GB 이상의 파일은 [고급 API](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A1)를 사용해 복사하십시오.

#### 메소드 프로토타입

```java
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
            throws CosClientException, CosServiceException
```

#### 요청 예시1: 객체 복사

[//]: # ".cssg-snippet-copy-object"
```java
// 리전 내 동일 계정 복사
// 원본 Bucket. Bucket 이름 생성 형식은 BucketName-APPID이며, 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String srcBucketName = "sourcebucket-1250000000";
// 복사할 원본 파일
String srcKey = "sourceObject";
// 타깃 버킷. Bucket 이름 생성 형식은 BucketName-APPID이며, 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String destBucketName = "examplebucket-1250000000";
// 복사할 타깃 파일
String destKey = "exampleobject";
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketName, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);

// 계정 간, 리전 간 복사(원본 파일의 읽기 권한 및 타깃 파일의 쓰기 권한 필요)
String srcBucketNameOfDiffAppid = "bucket-own-by-others-1251668577";
Region srcBucketRegion = new Region("ap-shanghai");
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketNameOfDiffAppid, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);
// 객체의 CRC64 획득
String crc64Ecma = copyObjectResult.getCrc64Ecma();
```

#### 요청 예시2: COS 유형 수정

>!표준 스토리지는 표준IA 스토리지, 인텔리전트 티어링 스토리지, 아카이브 스토리지 및 딥 아카이브 스토리지 등으로 수정할 수 있습니다. 아카이브 스토리지 또는 딥 아카이브 스토리지 객체를 다른 스토리지 유형으로 수정하려면 먼저 PostRestore를 사용하여 아카이브 스토리지 또는 딥 아카이브 스토리지 객체가 워밍업해야만 이 인터페이스를 사용하여 스토리지 유형 수정을 요청할 수 있습니다. 스토리지 유형에 대한 자세한 설명은 [스토리지 유형 개요](https://intl.cloud.tencent.com/ko/document/product/436/30925)를 참고하십시오.

```java
// 리전 내 동일 계정 복사
// 원본 Bucket. Bucket 이름 생성 형식은 BucketName-APPID이며, 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String srcBucketName = "sourcebucket-1250000000";
// 복사할 원본 파일
String srcKey = "sourceObject";
// 타깃 버킷. Bucket 이름 생성 형식은 BucketName-APPID이며, 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String destBucketName = "examplebucket-1250000000";
// 복사할 타깃 파일
String destKey = "exampleobject";
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketName, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);

// 계정 간, 리전 간 복사(원본 파일의 읽기 권한 및 타깃 파일의 쓰기 권한 필요)
String srcBucketNameOfDiffAppid = "bucket-own-by-others-1251668577";
Region srcBucketRegion = new Region("ap-shanghai");
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketNameOfDiffAppid, srcKey, destBucketName, destKey);
// 객체 스토리지 유형을 Standard_IA로 설정
copyObjectRequest.setStorageClass(StorageClass.Standard_IA);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);
// 객체의 CRC64 획득
String crc64Ecma = copyObjectResult.getCrc64Ecma();
```


#### 매개변수 설명

| 매개변수 이름          | 설명         | 유형              |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | 파일 복사 요청 | CopyObjectRequest |

Request 멤버 설명:

| 매개변수 이름              | 설명                                                         | 유형   |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion    | 원본 Bucket region. 기본값은 현재 clientConfig의 region과 일치하며, 리전 내 복사를 의미합니다. | String |
| sourceBucketName      | 원본 버킷 이름. 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| sourceKey             | 원본 객체 키. 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| sourceVersionId       | 원본 파일 version id(버전 제어를 활성화한 원본 Bucket에 적용). 기본값: 원본 파일의 최신 버전 | String |
| destinationBucketName | 타깃 버킷의 이름. Bucket의 이름 생성 형식은 BucketName-APPID이며, name은 알파벳, 숫자, 하이픈으로 구성됩니다.| String |
| destinationKey        | 타깃 객체 키. 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| storageClass          | 복사된 타깃 파일의 스토리지 유형. 열거 값은 Standard, Standard_IA이며 기본값은 Standard입니다. 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. | String |

#### 반환 결과 설명

- 성공: 신규 파일의 Etag 등 정보를 포함한 CopyObjectResult가 반환됩니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 객체 삭제

#### 기능 설명

버킷에서 지정 Object(파일/객체)를 삭제합니다.

#### 메소드 프로토타입

```java
public void deleteObject(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # ".cssg-snippet-delete-object"
```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
cosClient.deleteObject(bucketName, key);
```


#### 매개변수 설명

| 매개변수 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String             |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |

#### 반환 결과 설명

- 성공: 반환값 없음.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 객체 일괄 삭제

#### 기능 설명

다수의 지정 객체를 삭제합니다(DELETE Multiple Objects).

#### 메소드 프로토타입

```java
public DeleteObjectsResult deleteObjects(DeleteObjectsRequest deleteObjectsRequest)
    throws MultiObjectDeleteException, CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # ".cssg-snippet-delete-multi-object"
```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// 삭제할 key 리스트를 설정합니다. 한 번에 최대 1000개까지 삭제할 수 있습니다.
ArrayList<DeleteObjectsRequest.KeyVersion> keyList = new ArrayList<DeleteObjectsRequest.KeyVersion>();
// 삭제할 파일 이름 전송
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder1/picture.jpg"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/text.txt"));
keyList.add(new DeleteObjectsRequest.KeyVersion("project/folder2/music.mp3"));
deleteObjectsRequest.setKeys(keyList);

// 파일 일괄 삭제
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
| bucketName | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String             |
| quiet      | 삭제한 반환 결과 방식 지정. true, false 중 선택 가능. 기본값은 false. true로 설정할 경우 실패 오류 정보만 반환. false로 설정할 경우 성공과 실패 정보를 모두 반환 | boolean            |
| keys       | 객체 경로 리스트. 객체 버전 넘버를 선택할 수 있습니다.                             | List&lt;DeleteObjectsRequest.KeyVersion&gt; |

DeleteObjectsRequest.KeyVersion 멤버 설명:

| 매개변수 이름 | 설명                                                         | 유형   |
| -------- | ------------------------------------------------------------ | ------ |
| key      | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| version  | 버킷에 버전 제어가 활성화된 경우 삭제할 객체의 버전 넘버를 지정할 수 있습니다(옵션).           | String |

#### 반환 결과 설명

- 성공: 반환값 없음.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 보관된 객체 복구 

#### 기능 설명

아카이브 유형의 객체를 검색하여 액세스합니다(POST Object restore).

#### 메소드 프로토타입

```java
public void restoreObject(RestoreObjectRequest restoreObjectRequest)
    throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # ".cssg-snippet-restore-object"
```java
// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 본 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";

// restore를 설정해 얻는 임시 사본의 유효 기간은 1일입니다.
RestoreObjectRequest restoreObjectRequest = new RestoreObjectRequest(bucketName, key, 1);
// 복구 모드를 Standard로 설정합니다. 기타 옵션 모드에는 Expedited, Bulk가 있습니다. CAS 유형의 데이터를 복구하는 경우 위 세 가지 복구 모드를 모두 지원하며, 선택하는 복구 모드에 따라 비용과 복구 속도가 상이합니다. DEEP ARCHIVE 유형의 데이터를 복구하는 경우 Standard와 Bulk 복구 모드만 지원합니다.
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
| bucketName       | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String           |
| key              | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String           |
| expirationInDays | 복구된 임시 파일의 유효 기간                      | int              |
| casJobParameters | 복구 유형의 설정 정보를 설명합니다. CAS 유형의 데이터를 복구하는 경우 setTier 함수를 호출하여 Tier.Standard, Tier.Expedited, Tier.Bulk의 세 가지 복구 유형 중 하나로 설정할 수 있습니다. DEEP ARCHIVE 유형을 복구할 경우 Tier.Standard와 Tier.Bulk만 지원됩니다. | CASJobParameters |

#### 반환 결과 설명

- 성공: 반환값 없음.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


## 멀티파트 작업

다음은 객체의 멀티파트 업로드 작업 내용입니다.

- 객체 멀티파트 업로드: 멀티파트 업로드를 초기화하고 멀티파트를 업로드하면 완료됩니다.
- 멀티파트 이어 보내기: 업로드된 멀티파트를 조회하고 멀티파트를 업로드하면 완료됩니다.
- 업로드된 파트를 삭제합니다.

### 멀티파트 업로드 조회

#### 기능 설명

지정 버킷에서 진행 중인 멀티파트 업로드를 조회합니다(List Multipart Uploads).

#### 메소드 프로토타입

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### 요청 예시

[//]: # ".cssg-snippet-list-multi-upload"
```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
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
| bucketName     | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| keyMarker      | 해당 key값부터 시작하여 항목 열거                                      | String |
| delimiter      | 구분 문자는 하나의 부호입니다. Prefix가 있으면 Prefix에서 delimiter 사이의 동일한 경로를 하나로 분류하고 Common Prefix로 정의한 후 모든 Common Prefix를 나열합니다. Prefix가 없으면 경로의 시작점부터 시작합니다. | String |
| prefix         | 접두사가 Prefix인 Object key를 반환하도록 한정. Prefix를 사용하여 조회할 경우 반환되는 key에는 Prefix가 포함되므로 주의해야 합니다. | String |
| uploadIdMarker | 해당 UploadId 값부터 시작하여 항목 열거                                 | String |
| maxUploads     | 반환되는 최대 multipart 수량 설정. 유효한 값 범위: 1-1000.                 | String |
| encodingType   | 반환값의 인코딩 방식을 규정. 옵션값: url                            | String |

#### 반환 결과 설명

- 성공: 현재 진행 중인 멀티파트 업로드 정보를 포함한 MultipartUploadListing을 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.



### 멀티파트 업로드 초기화

#### 기능 설명

멀티파트 업로드 작업을 초기화합니다(Initiate Multipart Upload).

#### 메소드 프로토타입

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # ".cssg-snippet-init-multi-upload"
```java
// Bucket의 이름 생성 형식은 BucketName-APPID입니다.
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
| bucketName | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key        | 구조 함수 또는 set 메소드 | 멀티파트 업로드할 COS 경로, 즉 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 지정합니다. 예를 들어 객체 키는 folder/picture.jpg입니다.  | String |

#### 반환 결과 설명

- 성공: 이번 멀티파트 업로드의 uploadId를 포함한 InitiateMultipartUploadResult를 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 멀티파트 업로드

멀티파트를 업로드합니다(Upload Part).

#### 메소드 프로토타입

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # ".cssg-snippet-upload-part"
```java
// 멀티파트 업로드 시 최대 10000개까지 가능하며, 1MB-5GB 크기의 멀티파트를 지원합니다.
// 멀티파트 크기를 4MB로 설정합니다. 총 n개의 멀티파트가 있다면 1 ~ n-1개의 멀티파트는 크기가 동일하고, 마지막 한 개 멀티파트는 이전 멀티파트와 동일하거나 작습니다.
List<PartETag> partETags = new ArrayList<PartETag>();
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
// 파트의 Etag 획득
String etag = uploadPartResult.getETag();
// 파트의 CRC64 획득
String crc64Ecma = uploadPartResult.getCrc64Ecma();
partETags.add(new PartETag(partNumber, etag));  // partETags는 업로드된 part의 모든 Etag 정보를 기록합니다.
// ... partNumber가 2인 멀티파트부터 n인 멀티파트까지 업로드합니다.
```


#### 매개변수 설명

| 매개변수 이름          | 설명         | 유형              |
| ----------------- | ---- | ----------------- |
| uploadPartRequest | 요청 | UploadPartRequest |

Request 멤버 설명:

| 매개변수 이름    | 설정 방법 | 설명                                                         | 유형        |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName  | set 메소드  | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String      |
| key         | set 메소드 | 멀티파트 업로드할 COS 경로, 즉 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 지정합니다. 예를 들어 객체 키는 folder/picture.jpg입니다. | String      |
| uploadId    | set 메소드  | 지정한 멀티파트 업로드의 uploadId를 식별                                  | String      |
| partNumber  | set 메소드  | 지정한 멀티파트의 번호를 식별. 번호는 반드시 1보다 크거나 같아야 합니다.                                | int         |
| inputStream | set 메소드  | 멀티파트를 업로드할 입력 스트림을 기다립니다.                                           | InputStream |
|trafficLimit| set 메소드| 멀티파트 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어는 비활성화되어 있습니다.  | Int|


#### 반환 결과 설명

- 성공: 멀티파트 업로드의 eTag 정보를 포함한 UploadPartResult를 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


#### 반환 매개변수 설명

UploadPartResult 유형은 결과 정보 반환에 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름        | 설명                                                | 유형                |
| --------------- | --------------------------------------------------- | ------------------- |
| partNumber | 지정한 멀티파트의 번호를 식별 | String                |
| eTag        | 멀티파트 업로드의 MD5 값을 반환                   | String |
|crc64Ecma| 서버에서 멀티파트 콘텐츠에 따라 계산한 CRC64| String |


### 멀티파트 복사

#### 기능 설명

한 객체의 멀티파트 콘텐츠를 원본 경로에서 타깃 경로로 복사합니다(Upload Part-Copy).

#### 메소드 프로토타입

```java
public CopyPartResult copyPart(CopyPartRequest copyPartRequest) throws CosClientException, CosServiceException
```

#### 요청 예시

[//]: # ".cssg-snippet-upload-part-copy"
```java
// BucketName-APPID 형식의 버킷 이름
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
List<PartETag> partETags = new ArrayList<PartETag>();
partETags.add(copyPartResult.getPartETag());
```


#### 매개변수 설명

| 매개변수 이름        | 설명 | 유형            |
| --------------- | ---- | --------------- |
| copyPartRequest | 요청 | CopyPartRequest |

Request 멤버 설명:

| 매개변수 이름              | 설정 방법 | 설명                                                         | 유형   |
| --------------------- | -------- | ------------------------------------------------------------ | ------ |
| destinationBucketName | set 메소드 | 타깃 버킷의 이름. Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| destinationKey        | set 메소드 | 타깃 객체의 이름. 멀티파트가 복사되어 저장될 COS 경로, 즉 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 지정합니다. 예를 들어, 객체 키는 folder/picture.jpg입니다. | String |
| uploadId              | set 메소드 | 지정한 멀티파트 업로드의 uploadId를 식별                                  | String |
| partNumber            | set 메소드 | 지정한 멀티파트의 번호를 식별. 번호는 반드시 1보다 크거나 같아야 합니다.                                | int    |
| sourceBucketRegion    | set 메소드 | 원본 버킷의 리전                                               | Region |
| sourceBucketName      | set 메소드 | 원본 버킷의 이름                                               | String |
| sourceKey             | set 메소드 | 원본 객체 이름. 복사하기 전에 멀티파트가 속한 COS 경로, 즉 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)입니다. 예를 들어, 객체 키는 folder/picture.jpg입니다. | String |
| firstByte             | set 메소드 | 원본 객체의 첫 바이트 오프셋입니다.                                           | Long   |
| lastByte              | set 메소드 | 원본 객체의 마지막 바이트 오프셋입니다.                                       | Long   |

#### 반환 결과 설명

- 성공: 멀티파트의 ETag 정보를 포함한 CopyPartResult를 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 업로드된 파트 조회

#### 기능 설명

특정 멀티파트 업로드 작업에서 업로드된 파트를 조회합니다(List Parts).

#### 메소드 프로토타입

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # ".cssg-snippet-list-parts"
```java
// ListParts는 멀티파트 업로드 complete 이전 또는 멀티파트 업로드 abort 이전에 업로드된 멀티파트 중에서 uploadId에 해당하는 멀티파트의 정보를 획득하는 데 사용되며, partEtags 구성에도 사용할 수 있습니다.
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
| bucketName       | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key              | 구조 함수 또는 set 메소드 | 객체의 이름                                                   | String |
| uploadId         | 구조 함수 또는 set 메소드 | 이번에 조회할 멀티파트 업로드의 uploadId                               | String |
| maxParts         | set 메소드            | 한 번에 반환 가능한 최대 항목 수. 기본값: 1000                             | String |
| partNumberMarker | set 메소드            | 기본적으로 UTF-8 이진법 순서로 열거되며, 모든 열거 값은 marker부터 시작  | String |
| encodingType     | set 메소드            | 반환값의 인코딩 방식을 규정                                         | String |

#### 반환 결과 설명

- 성공: 모든 파트의 ETag와 번호 및 다음 list의 시작 marker를 포함한 PartListing을 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 멀티파트 업로드 완료 

#### 기능 설명

전체 파일의 멀티파트 업로드를 완료합니다(Complete Multipart Upload).

#### 메소드 프로토타입

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # ".cssg-snippet-complete-multi-upload"
```java
// complete 멀티파트 업로드를 완료합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
CompleteMultipartUploadRequest compRequest = new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
CompleteMultipartUploadResult result = cosClient.completeMultipartUpload(compRequest);
```


#### 매개변수 설명

| 매개변수 이름   | 설정 방법           | 설명                                                         | 유형              |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String            |
| key        | 구조 함수 또는 set 메소드 | 멀티파트 업로드할 COS 경로, 즉 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 지정합니다. 예를 들어 객체 키는 folder/picture.jpg입니다. | String            |
| uploadId   | 구조 함수 또는 set 메소드 | 지정한 멀티파트 업로드의 uploadId를 식별                                  | String            |
| partETags  | 구조 함수 또는 set 메소드 | 멀티파트의 번호와 업로드에서 반환하는 eTag를 식별                            | List&lt;PartETag&gt; |

#### 반환 결과 설명

- 성공: 완료된 객체의 eTag 정보를 포함한 CompleteMultipartUploadResult를 반환합니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 멀티파트 업로드 중지

#### 기능 설명

멀티파트 업로드 작업을 중지하고 업로드된 파트를 삭제합니다(Abort Multipart Upload).

#### 메소드 프로토타입

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### 요청 예시

[//]: # ".cssg-snippet-abort-multi-upload"
```java
// abortMultipartUpload는 아직 complete되지 않은 멀티파트 업로드를 중지하는 데 사용합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
cosClient.abortMultipartUpload(abortMultipartUploadRequest);
```


#### 매개변수 설명

| 매개변수 이름   | 설정 방법            | 설명                                                         | 유형   |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | 구조 함수 또는 set 메소드 | Bucket의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key        | 구조 함수 또는 set 메소드 | 멀티파트 업로드할 COS 경로, 즉 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)입니다. 예를 들어 객체 키는 folder/picture.jpg입니다. | String |
| uploadId   | 구조 함수 또는 set 메소드 | 지정한 멀티파트 업로드의 uploadId를 식별                                  | String            |

#### 반환 결과 설명

- 성공: 반환값 없음.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.



## 고급 인터페이스(권장)

고급 API의 TransferManger 유형은 캡슐화를 통해 인터페이스를 업로드 및 다운로드합니다. 내부에 있는 스레드 풀에서 사용자의 업로드 및 다운로드 요청을 수락하므로 사용자는 비동기화 작업 제출을 선택할 수 있습니다.

[//]: # (.cssg-snippet-transfer-init)
<dx-codeblock>
:::  java
// 스레드 풀의 크기는 클라이언트와 COS 네트워크가 안정적인 상황(예: Tencent Cloud의 CVM을 사용해 리전 내 COS 업로드)에서 16 또는 32로 설정하는 것을 권장합니다. 16 또는 32로도 네트워크 리소스를 충분히 이용할 수 있습니다.
// 공용 네트워크를 이용한 전송 및 네트워크 대역폭의 품질이 좋지 않은 경우 해당 값을 줄이길 권장합니다. 네트워크 속도가 느려져 요청 시간이 초과할 수 있습니다.
ExecutorService threadPool = Executors.newFixedThreadPool(32);
// threadpool을 전송합니다. 스레드 풀을 전송하지 않을 경우 기본적으로 TransferManager에 싱글 스레드의 스레드 풀이 생성됩니다.
TransferManager transferManager = new TransferManager(cosClient, threadPool);
// 고급 인터페이스의 멀티파트 업로드 임계값과 멀티파트 크기를 10MB로 설정합니다.
TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
transferManagerConfiguration.setMultipartUploadThreshold(10 * 1024 * 1024);
transferManagerConfiguration.setMinimumUploadPartSize(10 * 1024 * 1024);
transferManager.setConfiguration(transferManagerConfiguration);
:::
</dx-codeblock>


transferManager를 사용하지 않을 경우 리소스 유출 방지를 위해 수동으로 비활성화하십시오.

```java
// TransferManger를 비활성화하고 그중의 cosClient를 비활성화하십시오.
transferManager.shutdownNow();
```

#### 매개변수 설명

TransferManagerConfiguration 유형은 고급 인터페이스의 설정 정보를 기록하는 데 사용됩니다. 주요 멤버 설명은 다음과 같습니다.

|  멤버 이름 | 설정 방법            | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize   | set 메소드 | 멀티파트 업로드의 파트 크기입니다. 단위는 바이트(Byte)이며, 기본값은 5MB입니다. | long         |
| multipartUploadThreshold   | set 메소드 | 해당 값보다 크거나 같고 동시 접속하는 멀티파트 업로드 파일입니다. 단위는 바이트(Byte)이며, 기본값은 5MB입니다. | long         |
| multipartCopyThreshold         | set 메소드 | 해당 값보다 크거나 같고 동시 접속하는 멀티파트 복사 파일입니다. 단위는 바이트(Byte)이며, 기본값은 5GB입니다. | long           |
| multipartCopyPartSize        | set 메소드 | 멀티파트 복사 시 파트의 크기입니다. 단위는 바이트(Byte)이며, 기본값은 100MB입니다.           | long    |

### 객체 업로드(진행률 가져오기)

#### 기능 설명

고급 업로드 인터페이스는 사용자 파일의 길이와 데이터 유형에 따라 자동으로 간편 업로드 또는 멀티파트 업로드 중 하나를 선택합니다. 자세한 설명은 아래를 참고하십시오.
- 멀티파트 업로드 임계값보다 작거나 Content-Length 헤더가 없는 스트림 업로드의 경우 고급 인터페이스는 간편 업로드를 선택합니다.
- 멀티파트 업로드 임계값보다 크지만 Content-Length 헤더가 없는 스트림 업로드의 경우 고급 인터페이스는 멀티파트 업로드를 선택합니다.
- 데이터 유형이 File 유형인 파일 업로드의 경우 고급 인터페이스는 멀티 스레드로 다수의 파트를 동시에 업로드합니다.
- 고급 업로드 인터페이스는 멀티파트 업로드에 대해 진행률 확인 기능을 제공하며, getProgress() 방법으로 확인할 수 있습니다.
- 파일 크기가 5MB 이상인 파일을 멀티파트 업로드하는 경우, 해당 임계값은 요청 예시 3을 통해 조정할 수 있습니다.

>? 기타 관련 설정 속성, 스토리지 유형, MD5 검사 등은 [PUT Object API](https://intl.cloud.tencent.com/document/product/436/7749)를 참고하십시오.
>

#### 메소드 프로토타입

```java
// 객체 업로드.
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### 요청 예시1: 고급 인터페이스를 사용하여 업로드

[//]: # ".cssg-snippet-transfer-upload-file1"
```java
// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 본 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// 로컬 파일 업로드
Upload upload = transferManager.upload(putObjectRequest);
// 전송 완료 대기
UploadResult uploadResult = upload.waitForUploadResult();
```

#### 요청 예시2: 고급 인터페이스를 사용하여 업로드하고 업로드 진행률 표시

[//]: # ".cssg-snippet-transfer-upload-file2"
```java
// 업로드 시 출력할 업로드 진행률의 콜백 함수를 작성합니다.
void showTransferProgress(Transfer transfer) {
    System.out.println(transfer.getDescription());
    do {
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            return;
        }
        TransferProgress progress = transfer.getProgress();
        long so_far = progress.getBytesTransferred();
        long total = progress.getTotalBytesToTransfer();
        double pct = progress.getPercentTransferred();
        System.out.printf("[%d / %d] = %.02f%%\n", so_far, total, pct);
    } while (transfer.isDone() == false);
    System.out.println(transfer.getState());
}

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 본 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// 로컬 파일 업로드
Upload upload = transferManager.upload(putObjectRequest);
// 업로드 진행률 출력
// 서브 스레드를 통해 이 함수를 호출할 수 있습니다. 하지만 waitForUploadResult 전에 서브 스레드를 실행해야 합니다. 그렇지 않으면 upload 완료로 인해 진행률을 볼 수 없습니다.
showTransferProgress(upload);
// 전송 완료 대기
UploadResult uploadResult = upload.waitForUploadResult();
```

#### 요청 예시3: 고급 인터페이스를 사용하여 업로드 및 멀티파트 업로드의 임계값을 설정
```java
// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 본 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// 파일 크기가 10MB 이상인 파일만 멀티파트 업로드 사용하도록 설정
TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
transferManagerConfiguration.setMultipartUploadThreshold(10*1024*1024);
transferManager.setConfiguration(transferManagerConfiguration);
// 로컬 파일 업로드
Upload upload = transferManager.upload(putObjectRequest);
// 전송 완료 대기
UploadResult uploadResult = upload.waitForUploadResult();
```

#### 매개변수 설명

| 매개변수 이름         | 설명         | 유형             |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 방법          | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | 구조 함수 또는 set 메소드 | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String         |
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String         |
| file         | 구조 함수 또는 set 메소드 | 로컬 파일                                                     | File           |
| input        | 구조 함수 또는 set 메소드 | 입력 스트림                                                       | InputStream    |
| metadata     | 구조 함수 또는 set 메소드 | 파일의 메타데이터                                                 | ObjectMetadata |
|trafficLimit | set 메소드| 객체 업로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다. | Int|

>?다수의 멀티파트를 동시 업로드할 경우 trafficLimit은 모든 멀티파트의 업로드 속도를 제한합니다. 이때 스레드 풀의 스레드 수를 조정하여 파일의 업로드 속도를 제어해야 합니다.

#### 반환값

- 성공: Upload를 반환합니다. 업로드의 종료 여부를 확인할 수 있으며, 업로드가 끝날 때까지 기다릴 수도 있습니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.

#### 반환 매개변수 설명

Upload의 waitForUploadResult() 방법을 호출하여 획득한 객체 업로드 정보는 UploadResult 유형에 기록됩니다. UploadResult 유형의 주요 멤버 설명은 다음과 같습니다.

| 멤버 이름   | 설명                                                         | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key        | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다.<br/>예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| requestId  | 요청 Id                                                       | String |
| dateStr    | 현재 서버 시간                                               | String |
| versionId  | 버킷의 버전 제어 기능이 활성화되면 객체의 버전 넘버 Id 반환                      | String |
| crc64Ecma  | 서버에서 객체 콘텐츠에 따라 계산한 CRC64                           | String |


#### 진행률 가져오기 설명

이 클래스의 getProgress를 업로드하여 TransferProgress 클래스를 얻을 수 있습니다. 이 클래스의 아래 세 가지 방법으로 업로드 진행률을 얻을 수 있습니다.

| 메소드 이름                 | 설명                | 유형    |
| ----------------------- | ------------------ | -----   |
| getBytesTransferred     | 업로드된 바이트 수 획득   | long   |
| getTotalBytesToTransfer | 총 파일의 바이트 수 획득   | long   |
| getPercentTransferred   | 업로드된 바이트 백분율 획득  | double |


### 객체 다운로드(중단된 지점부터 이어서 전송)

#### 기능 설명

COS의 객체를 로컬에 다운로드합니다.

#### 메소드 프로토타입

```java
// 객체 다운로드
public Download download(final GetObjectRequest getObjectRequest, final File file);

// 객체를 중단된 지점부터 이어서 다운로드합니다.
public Download download(final GetObjectRequest getObjectRequest, final File file,
        boolean resumableDownload, String resumableTaskFile,
        int multiThreadThreshold, int partSize);
```

#### 요청 예시1: 고급 인터페이스를 사용하여 객체 다운로드

[//]: # ".cssg-snippet-transfer-download-object"
```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localDownFile = new File(localFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
// 사용 단위는 bit/s로 제한되며, 여기서는 다운로드 대역폭 제한을 10MB/s로 설정합니다.
getObjectRequest.setTrafficLimit(80*1024*1024);
// 파일 다운로드
Download download = transferManager.download(getObjectRequest, localDownFile);
// 전송 종료를 기다립니다. 업로드가 끝날 때까지 기다리려면 waitForCompletion을 호출합니다.
download.waitForCompletion();
```

#### 요청 예시2: 고급 인터페이스를 사용하여 객체를 중단된 지점부터 이어서 다운로드

```java
// 다운로드 시 출력할 다운로드 진행률의 콜백 함수를 작성합니다.
void showTransferProgress(Transfer transfer) {
    System.out.println(transfer.getDescription());
    do {
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            return;
        }
        TransferProgress progress = transfer.getProgress();
        long so_far = progress.getBytesTransferred();
        long total = progress.getTotalBytesToTransfer();
        double pct = progress.getPercentTransferred();
        System.out.printf("[%d / %d] = %.02f%%\n", so_far, total, pct);
    } while (transfer.isDone() == false);
    System.out.println(transfer.getState());
}

// Bucket 이름 생성 형식은 BucketName-APPID이며, 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localDownFile = new File(localFilePath);

GetObjectRequest getObj = new GetObjectRequest(bucketName, key);

Download download = transferManager.download(getObj, localDownFile, true);
// 서브 스레드를 통해 이 함수를 호출할 수 있습니다. 하지만 waitForCompletion 전에 서브 스레드를 실행해야 합니다. 그렇지 않으면 download 완료로 인해 진행률을 볼 수 없습니다.
showTransferProgress(download);
try {
    download.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

transferManager.shutdownNow();
```

#### 매개변수 설명

| 매개변수 이름                 | 설명                                | 유형              | 기본값                       |
| ----------------------- | ---------------------------------- | ---------------- | ---------------------------- |
| getObjectRequest        | 객체 다운로드 요청                         | GetObjectRequest | 없음                            |
| file                    | 다운로드할 로컬 파일                    | File             | 없음                            |
| resumableDownload       |  중단된 지점부터 멀티파트 이어서 다운로드 활성화 여부               | boolean          | false                         |
| resumableTaskFile       | 중단된 지점부터 이어서 다운로드 시 정보가 기록된 파일명            | boolean          | file.cosresumabletask         |
| multiThreadThreshold    | 중단된 지점부터 이어서 다운로드에서 멀티 스레드를 사용해 다운로드하는 파일의 최소 크기  | int              | 20 * 1024 * 1024              |
| partSize                | 중단된 지점부터 이어서 다운로드에서 사용하는 멀티파트 크기              | int              | 8 * 1024 * 1024               |

Request 멤버 설명:

| Request 멤버 | 설정 방법         | 설명                                                         | 유형   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName   | 구조 함수 또는 set 메소드 | 버킷의 이름 생성 형식은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key          | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| range    | set 메소드            | 다운로드 range 범위                       | Long[] |
| trafficLimit | set 메소드    | 객체 다운로드의 트래픽 제어에 사용됩니다. 단위는 bit/s이며, 기본적으로 트래픽 제어가 비활성화되어 있습니다.  | int |

#### 반환값

- 성공: Download를 반환합니다. 다운로드의 종료 여부를 확인할 수 있으며, 다운로드가 끝날 때까지 기다릴 수도 있습니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 객체 복사

#### 기능 설명

Copy 인터페이스는 객체 크기에 따라 자동으로 간편 복사 또는 멀티파트 복사 중 하나를 선택합니다. 사용자는 복사할 파일의 크기를 고려하지 않아도 됩니다.

#### 메소드 프로토타입

```java
// 객체 업로드
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### 요청 예시1: 리전 내 복사

>?리전 내 복사란 동일한 리전의 버킷에서 파일을 복사하는 것을 의미합니다.

[//]: # ".cssg-snippet-transfer-copy-object"
```java
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리합니다.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
// 복사할 bucket region
COSCredentials credentials = new BasicCOSCredentials(secretId, secretKey);
Region bucketRegion = new Region("COS_REGION");

// 원본 Bucket입니다. 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String srcBucketName = "sourcebucket-1250000000";
// 복사할 원본 파일
String srcKey = "sourceObject";
// 타깃 Bucket입니다. 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다.

String destBucketName = "examplebucket-1250000000";
// 복사할 타깃 파일
String destKey = "exampleobject";

COSClient cosClient = new COSClient(credentials, new ClientConfig(bucketRegion));

ExecutorService threadPool = Executors.newFixedThreadPool(5);
// threadpool을 전송합니다. 스레드 풀을 전송하지 않을 경우 기본적으로 TransferManager에 싱글 스레드의 스레드 풀이 생성됩니다.
TransferManager transferManager = new TransferManager(cosClient, threadPool);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);

try {
    Copy copy = transferManager.copy(copyObjectRequest);
    // 비동기 결과 copy를 반환합니다. 동시에 waitForCopyResult를 호출하여 copy 결과를 기다릴 수 있습니다. 성공하면 CopyResult를 반환하고, 실패하면 이상 경고 메시지를 표시합니다.
    CopyResult copyResult = copy.waitForCopyResult();
    // 복사로 생성된 객체의 CRC64 획득
    String crc64Ecma = copyResult.getCrc64Ecma();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

#### 요청 예시2: 리전 간 복제

>!
>- 리전 간 복제란 원본 파일을 다른 리전의 버킷으로 복사하는 것을 의미합니다(예: 파일을 베이징 리전에서 광저우 리전으로 복사).
>- 금융 클라우드 리전과 퍼블릭 클라우드 리전은 서로 통신할 수 없으며, 리전 간 복제를 진행할 수 없습니다.

```java
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리합니다.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";

COSCredentials credentials = new BasicCOSCredentials(secretId, secretKey);

// 복사할 bucket region
Region srcBucketRegion = new Region("COS_SRC_REGION");
Region destBucketRegion = new Region("COS_DEST_REGION");

// 원본 Bucket입니다. 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String srcBucketName = "sourcebucket-1250000000";
// 복사할 원본 파일
String srcKey = "sourceObject";
// 타깃 Bucket입니다. 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다.

String destBucketName = "examplebucket-1250000000";
// 복사할 타깃 파일
String destKey = "exampleobject";

// transferManager에서 타깃 파일의 cosclient를 사용합니다.
COSClient destCOSClient = new COSClient(cred, new ClientConfig(destBucketRegion));
ExecutorService threadPool = Executors.newFixedThreadPool(5);
// threadpool을 전송합니다. 스레드 풀을 전송하지 않을 경우 기본적으로 TransferManager에 싱글 스레드의 스레드 풀이 생성됩니다.
TransferManager transferManager = new TransferManager(destCOSClient, threadPool);

// 원본 파일 정보를 획득하는 데 사용되는 srcCOSClient를 생성합니다.
COSClient srcCOSClient = new COSClient(cred, new ClientConfig(srcBucketRegion));

try {
    Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
    // 비동기 결과 copy를 반환합니다. 동시에 waitForCopyResult를 호출하여 copy 결과를 기다릴 수 있습니다. 성공하면 CopyResult를 반환하고, 실패하면 이상 경고 메시지를 표시합니다.
    CopyResult copyResult = copy.waitForCopyResult();
    // 복사로 생성된 객체의 CRC64 획득
    String crc64Ecma = copyResult.getCrc64Ecma();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

#### 요청 예시3: 비동기화 사용 복제
```java
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리합니다.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
// 복사할 bucket region
COSCredentials credentials = new BasicCOSCredentials(secretId, secretKey);
Region bucketRegion = new Region("COS_REGION");

// 원본 Bucket입니다. 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String srcBucketName = "sourcebucket-1250000000";
// 복사할 원본 파일
String srcKey = "sourceObject";
// 타깃 Bucket입니다. 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다.

String destBucketName = "examplebucket-1250000000";
// 복사할 타깃 파일
String destKey = "exampleobject";

COSClient cosClient = new COSClient(credentials, new ClientConfig(bucketRegion));

ExecutorService threadPool = Executors.newFixedThreadPool(5);
// threadpool을 전송합니다. 스레드 풀을 전송하지 않을 경우 기본적으로 TransferManager에 싱글 스레드의 스레드 풀이 생성됩니다.
final TransferManager transferManager = new TransferManager(cosClient, threadPool);

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(bucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);

try {
    Copy copy = transferManager.copy(copyObjectRequest);
    // 하나의 서브 스레드에서 비동기화 실행된 copy가 완료되었는지 판단합니다.
    new Thread(){
        @Override
        public void run() {
            while(!copy.isDone()) {
                try {
                    Thread.sleep(500);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println("wait for copy done");
            }
            transferManager.shutdownNow();
        };
    }.start();
    // 다른 로직 계속 진행
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
| sourceBucketRegion    | 원본 Bucket Region. 기본값은 현재 clientconfig의 region과 일치하며, 통합 리전 복사를 의미합니다. | String |
| sourceBucketName      | 원본 버킷 이름. 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String |
| sourceKey             | 원본 객체 키. 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| sourceVersionId       | 원본 파일 version id(버전 제어를 활성화한 원본 Bucket에 적용). 기본값: 원본 파일의 최신 버전 | String |
| destinationBucketName | 타깃 버킷 이름. 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 해당 형식을 따라야 합니다. | String |
| destinationKey        | 타깃 객체 키. 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`에서 객체 키는 doc/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String |
| storageClass          | 복사된 타깃 파일의 스토리지 유형. 열거 값은 Standard, Standard_IA이며 기본값은 Standard입니다. 더 많은 스토리지 유형은 [스토리지 유형 개요](https://intl.cloud.tencent.com/document/product/436/30925)를 참고하십시오. | String |

#### 반환값

- 성공: Copy를 반환합니다. Copy의 종료 여부를 확인할 수 있으며, 업로드가 끝날 때까지 기다릴 수도 있습니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 객체 일괄 업로드

#### 기능 설명

로컬 폴더 안에 있는 모든 파일을 업로드합니다.

#### 메소드 프로토타입

```java
public MultipleFileUpload uploadDirectory(String bucketName, String virtualDirectoryKeyPrefix,
            File directory, boolean includeSubdirectories);
```

#### 요청 예시
[//]: # ".cssg-snippet-transfer-upload-directory"
```java
// 업로드 시 출력할 업로드 진행률의 콜백 함수를 작성합니다.
void showTransferProgress(Transfer transfer) {
    System.out.println(transfer.getDescription());
    do {
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            return;
        }
        TransferProgress progress = transfer.getProgress();
        long so_far = progress.getBytesTransferred();
        long total = progress.getTotalBytesToTransfer();
        double pct = progress.getPercentTransferred();
        System.out.printf("[%d / %d] = %.02f%%\n", so_far, total, pct);
    } while (transfer.isDone() == false);
    System.out.println(transfer.getState());
}

// 파일이 bucket에 업로드된 후 접두사 디렉터리를 설정합니다. “”로 설정하는 경우 bucket의 루트 디렉터리로 업로드된 것을 의미합니다.
String cos_path = "/prefix";
// 업로드할 폴더의 절대 경로
String dir_path = "/to/mydir";
// 디렉터리의 서브 디렉터리 재귀 업로드 여부입니다. true이면 서브 디렉터리의 파일도 업로드하고 cos에 디렉터리 구조가 유지됩니다.
Boolean recursive = false;

try {
    // 비동기 결과 Upload를 반환합니다. 동시에 waitForUploadResult를 호출하여 upload 결과를 기다릴 수 있습니
다. 성공하면 UploadResult를 반환하고, 실패하면 이상 경고 메시지를 표시합니다.
    MultipleFileUpload upload = transferManager.uploadDirectory(bucketName, cos_path, new File(dir_path), recursive);

    // 업로드 진행률 조회를 선택할 수 있습니다.
    // 서브 스레드를 통해 이 함수를 호출할 수 있습니다. 하지만 waitForCompletion 전에 서브 스레드를 실행해야 합니다. 그렇지 않으면 upload 완료로 인해 진행률을 볼 수 없습니다.
    showTransferProgress(upload);

    // 또는 정체된 대기를 완료합니다.
    upload.waitForCompletion();

    System.out.println("upload directory done.");
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

#### 매개변수 설명

| 매개변수 이름                   | 설명                  | 유형             |
| ------------------------- | -------------------- | ---------------- |
| bucketName                | cos의 bucket       | GetObjectRequest |
| virtualDirectoryKeyPrefix | cos의 object 접두사   | String           |
| directory                 | 업로드할 폴더의 절대 경로  | File             |
| includeSubDirectory       | 서브 디렉터리 재귀 업로드 여부       | Boolean          |

#### 반환값

- 성공: MultipleFileUpload를 반환합니다. 업로드의 종료 여부를 확인할 수 있으며, 업로드가 끝날 때까지 기다릴 수도 있습니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 객체 일괄 다운로드

#### 기능 설명

COS에서 접두사가 동일한 객체(가상 폴더)를 지정한 로컬 디렉터리로 다운로드합니다.

#### 메소드 프로토타입

```java
public MultipleFileDownload downloadDirectory(String bucketName, String keyPrefix,
        File destinationDirectory) {
```

#### 요청 예시
[//]: # ".cssg-snippet-transfer-upload-directory"
```java
// 진행률 콜백 함수를 작성합니다.
void showTransferProgress(Transfer transfer) {
    System.out.println(transfer.getDescription());
    do {
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            return;
        }
        TransferProgress progress = transfer.getProgress();
        long so_far = progress.getBytesTransferred();
        long total = progress.getTotalBytesToTransfer();
        double pct = progress.getPercentTransferred();
        System.out.printf("[%d / %d] = %.02f%%\n", so_far, total, pct);
    } while (transfer.isDone() == false);
    System.out.println(transfer.getState());
}

// 다운로드할 객체의 공용 접두사(cos의 디렉터리 경로에 해당)를 설정합니다. ""로 설정하면 모든 bucket을 다운로드합니다.
String cos_path = "/prefix";
// 다운로드한 파일의 폴더 절대 경로를 저장합니다.
String dir_path = "/to/mydir";

try {
    // 비동기 결과 download를 반환합니다. 동시에 waitForUploadResult를 호출하여 download 결과를 기다릴 수 있습니다.
    MultipleFileDownload download = transferManager.downloadDirectory(bucketName, cos_path, new File(dir_path));

    // 다운로드 진행률 조회를 선택할 수 있습니다.
    // 서브 스레드를 통해 이 함수를 호출할 수 있습니다. 하지만 waitForCompletion 전에 서브 스레드를 실행해야 합니다. 그렇지 않으면 download 완료로 인해 진행률을 볼 수 없습니다.
    showTransferProgress(download);

    // 또는 정체된 대기를 완료합니다.
    download.waitForCompletion();

    System.out.println("download directory done.");
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

transferManager.shutdownNow();
```

#### 매개변수 설명

| 매개변수 이름                   | 설명                  | 유형             |
| ------------------------- | -------------------- | ---------------- |
| bucketName                | cos의 bucket       | GetObjectRequest |
| keyPrefix                 | cos의 object 접두사   | String           |
| destinationDirectory      | 로컬 폴더의 절대 경로   | File             |

#### 반환값

- 성공: MultipleFileUpload를 반환합니다. 다운로드의 종료 여부를 확인할 수 있으며, 다운로드가 끝날 때까지 기다릴 수도 있습니다.
- 실패: 오류 발생(예: 실명 인증 실패). CosClientException 또는 CosServiceException 오류 발생. 자세한 내용은 [오류 해결](https://intl.cloud.tencent.com/document/product/436/31537)을 참고하십시오.


### 폴더 및 하위 파일 삭제

COS 자체에는 폴더 및 디렉터리의 개념이 없습니다. 사용자의 습관에 맞춰 세퍼레이터 /로 '폴더'를 모방할 수 있습니다.

폴더 및 하위 파일을 삭제하는 시나리오는 사실 COS에서 동일한 접두사를 가진 객체를 삭제하는 것에 해당합니다. 현재 COS Java SDK는 이러한 작업을 실행할 수 있는 인터페이스를 제공하지 않습니다. 그러나 기본 작업인 **객체 리스트 조회**+**객체 일괄 삭제**를 조합하여 폴더 및 하위 파일 삭제 효과를 구현할 수 있습니다.


#### 요청 예시

```java
// 일괄 삭제에 사용합니다.
public void delete(ArrayList<DeleteObjectsRequest.KeyVersion> keyList) {
    DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
    deleteObjectsRequest.setKeys(keyList);
    
    // 파일 일괄 삭제
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
}

// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// bucket 이름 설정
listObjectsRequest.setBucketName(bucketName);
// prefix는 삭제할 폴더를 의미
listObjectsRequest.setPrefix("images/");
// delimiter는 세퍼레이터를 의미합니다. /로 설정하면 현재 디렉터리의 object를 나열하고, 공백으로 설정하면 전체 object를 나열합니다.
listObjectsRequest.setDelimiter("/");
// 순회할 객체의 최대 수량을 설정합니다. listobject 1회당 최대 1000개까지 지원합니다.
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;

do {
    // 삭제할 key 리스트를 설정합니다. 한 번에 최대 1000개까지 삭제할 수 있습니다.
    ArrayList<DeleteObjectsRequest.KeyVersion> keyList = new ArrayList<DeleteObjectsRequest.KeyVersion>();

    try {
        objectListing = cosClient.listObjects(listObjectsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }
    // common prefix는 delimiter로 잘린 경로를 표시합니다. 예를 들어 delimiter를 /로 설정하면 common prefix는 모든 서브 디렉터리의 경로를 표시합니다.
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // object summary는 나열된 모든 object 리스트를 표시합니다.
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // 파일의 경로 key
        String key = cosObjectSummary.getKey();
        keyList.add(new DeleteObjectsRequest.KeyVersion(key));
    }

    try {
        delete(keyList);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }

    String nextMarker = objectListing.getNextMarker();
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());

```

### 객체 이동

COS는 버킷 이름(Bucket)과 객체 키(ObjectKey)로 객체를 식별하므로 객체를 이동하는 경우 해당 객체의 식별자를 수정해야 합니다. 현재 COS Java SDK는 객체의 고유 식별자를 수정할 수 있는 인터페이스를 제공하지 않습니다. 하지만 **객체 복사**와 **객체 삭제**를 함께 사용하는 기본 작업으로 객체 식별자를 수정하고 객체를 이동할 수 있습니다.

예시로 mybucket-1250000000 버킷에 있는 picture.jpg 객체를 동일한 버킷의 doc 경로로 이동할 경우, 먼저 picture.jpg 객체를 doc/picture.jpg 객체로 복사한 후 picture.jpg 객체를 삭제하여 '이동' 효과를 구현할 수 있습니다.

마찬가지로 mybucket-1250000000 버킷의 picture.jpg 객체를 myanothorbucket-1250000000으로 이동하려면 먼저 객체를 myanothorbucket-1250000000 버킷에 복사하고 원본 객체를 삭제합니다.


#### 요청 예시

```java
// 리전 내 복사. [객체 복사] 요청 예시를 참고하십시오.
public void copySameRegion(String srcBucket, String srcKey, String destBucket, String destKey) {
    CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucket, srcKey, destBucket, destKey);
    CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);
}

// 리전 간 복제. [객체 복사] 요청 예시를 참고하십시오.
public void copyDiffRegion(String srcRegion, String srcBucket, String srcKey,
        String destRegion, String destBucket, String destKey){
    CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucket, srcKey, destBucketName, destKey);
    CopyObjetResult copyObjectResult = cosClient.copyObject(copyObjectRequest);
}

// 이동할 객체의 정보
String srcRegion = "ap-shanghai";
String srcBucket = "mybucket-1250000000";
String srcKey = "picture.jpg";

// 이동 후 객체의 정보
String destRegion = "ap-shanghai";
String destBucket = "myanotherbucket-1250000000";
String destKey = "doc/picture.jpg";

// 리전 내 이동. 리전 간에는 리전 간 복제를 사용하십시오.
copySameRegion(srcBcuket, srcKey, destBucket, destKey);

// 복사 완료 후 이동할 객체의 정보를 삭제합니다.
cosClient.deleteObject(srcBucket, srcKey);
```
