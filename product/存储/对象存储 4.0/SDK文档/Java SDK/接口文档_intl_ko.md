COS 서비스 XML Java SDK 조작 성공은 각 종류의 API에 대응하는 유형을 반환하고, 실패하면 이상비(CosClientException 및 CosServiception)을 보고합니다. 그 중 CosClientException은 네트워크 이상, 요청 발송 실패 등의 클라이언트 이상입니다. CosServiceException은 사용자 요청이 서버 처리로 인해 실패한 이유, 오류 코드 등을 포함합니다. 만일 권한이 없으면 존재하지 않는 파일에 접근합니다. 자세한 설명은 문서 맨 마지막에 있는 이상 유형 설명을 참조하십시오.
SDK에서 각 API를 사용하는 올바른 방법은 다음과 같습니다. 요약을 위해 후속 API 예시는 이상 캡쳐의 예시를 더이상 제공하지 않으며, API 사용 예시만 제공합니다.

```java
try {
   //버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
   String bucketName = "movie-1251668577";
   String key = "abc/def.jpg";
   cosClient.deleteObject(bucket, key);
} catch (CosClientException cle) {
  // 인쇄 이상 등 사용자 지정의 이상 처리
  log.error("del object failed.", cle);
  // ...
} catch (CosServiceException cse) {
   // 인쇄 이상 등 사용자 지정의 이상 처리
  log.error("del object failed.", cse);
  // ...
}
```

## Bucket API 설명

### Put Bucket

Bucket을 새로 생성합니다. Bucket은 제한된 리소스로서, Bucket은 디렉터리와 같지 않으며 Bucket 하의 파일 수량은 무제한이므로, Bucket을 많이 생성하지 않을 것을 권장합니다. Bucket 생성은 저빈도 작업이므로 일반적으로 콘솔에서 Bucket을 생성하고 SDK에서 Object 의 조작을 진행할 것을 권장합니다.

- **방법 원형**

```java
public Bucket createBucket(String  bucketName) throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은{name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |

- **반환값**
  - 성공:   Bucket 유형, 관련 Bucket 의 설명(Bucket 의 이름, owner 및 생성 날짜)이 포함됩니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상 CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
Bucket bucket = cosClient.createBucket(bucketName);
```

### Delete Bucket

이미 비어 있는 Bucket을 삭제합니다.

- **방법 원형**

```java
 public void deleteBucket(String bucketName) throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
cosClient.deleteBucket(bucketName);
```

### Head Bucket

Bucket 의 존재 여부를 조회합니다.

- **방법 원형**

```java
public boolean doesBucketExist(String bucketName)
  throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은{name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |

- **반환값**
  - 성공: 존재하면 true를 반환, 그렇지 않으면 false를 반환합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상 CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
boolean bucketExistFlag = cosClient.doesBucketExist(bucketName);
```

### Get Bucket Location

Bucket 소재 Region을 조회합니다.

- **방법 원형**

```java
public String getBucketLocation(String bucketName)
throws CosClientException， CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |

- **반환값**
  - 성공: Bucket 소재 region을 반환합니다.
  - 실패: 오류 발생(예: Bucket 이 존재하지 않음), 이상 CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String location = cosClient.getBucketLocation("movie-1251668577");
```

### List Buckets

계정하의 모든 Bucket 나열

- **방법 원형**

```java
public List<Bucket> listBuckets() throws CosClientException, CosServiceException;
```

- **매개변수 설명**

없음

- **반환값**
  - 성공: 모든 Bucket 유형의 리스트를 반환하고, Bucket 유형에는 bucket 멤버, location 등의 정보가 포함됩니다.
  - 실패: 오류 발생(예: Bucket 이 존재하지 않음), 이상 CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 설명을 참조하십시오.
- **예시**

```java
List<Bucket> buckets = cosClient.listBuckets();
for (Bucket bucketElement : buckets) {
    String bucketName = bucketElement.getName();
    String bucketLocation = bucketElement.getLocation();
}
```

### Get Bucket(모든 Objects를 나열합니다)

획득한 COS 의 파일 리스트를 조회합니다.

- **방법 원형**

```java
// 파일 리스트 획득
public ObjectListing listObjects(ListObjectsRequest listObjectsRequest)
            throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명         | 매개변수 유형           |
| ------------------ | ---------------- | ------------------ |
| listObjectsRequest | 파일 리스트 획득 요청 | ListObjectsRequest |

Request 멤버 설명 :

| Request 멤버 | 설정 방법            | 설명                                                         | 유형   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName   | 생성자 또는 set 방법 | bucket 의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |
| prefix       | 생성자 또는 set 방법 | 플래그 list 는 prefix를 접두사로 한 멤버로서, 기본으로 제한하지 않는, 즉  Bucket 의 모든 멤버입니다.<br>기본값: "" | String |
|   marker   |  생성자 또는 set 방법 | 플래그 list 의 시작 위치, 처음은 비어 있고, 후속은 마지막 list 의 반환값의 marker입니다 |String  
| delimiter  | 생성자 또는 set 방법 | 구분 문자, 반환 제한하는 것은 prefix로 시작하고, 한번 나타난 delimiter 로 끝나는 경로입니다 |String  
|  maxKeys   | 생성자 또는 set 방법 |           최대 반환 멤버 개수( 1000을 초과하지 말아야 함)   <br>기본값: 1000          |Integer |  

- **반환값**
  - 성공: ObjectListing 유형을 반환하며 모든 멤버 및 nextMarker를 포함합니다.  
  - 실패: 이상 CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";

// bucket 하의 멤버를 획득합니다( delimiter 설정)
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
listObjectsRequest.setBucketName(bucketName);
// list의 prefix 설정하여, list한 파일 key 는 모두 이 prefix 로 시작함을 나타냅니다
listObjectsRequest.setPrefix("");
// delimiter 는 /로 설정합니다. 즉 직접 멤버를 획득하고 디렉터리 하의 순환 서브 멤버를 포함하지 않습니다
listObjectsRequest.setDelimiter("/");
// marker 을 설정합니다. (marker 는 마지막 list에서 획득하거나 또는 첫 번째 list marker 는 비어 있습니다)
listObjectsRequest.setMarker("");
// list 에 최대 100개 멤버를 설정합니다. (설정하지 않으면, 기본으로 1000개이며, 최대 1회 list 에 1000개 key 를 허용합니다)
listObjectsRequest.setMaxKeys(100);

ObjectListing objectListing = cosClient.listObjects(listObjectsRequest);
// 다음 번 list의 marker 을 획득합니다
String nextMarker = objectListing.getNextMarker();
// 이미 list 되었는지를 판단하며, list 가 끝나면, isTruncated는 false이고, 그렇지 않으면 true입니다
boolean isTruncated = objectListing.isTruncated();
List<COSObjectSummary> objectSummaries = objectListing.getObjectSummaries();
for (COSObjectSummary cosObjectSummary : objectSummaries) {
// 파일 경로
String key = cosObjectSummary.getKey();
// 파일 길이 획득
long fileSize = cosObjectSummary.getSize();
// 파일 ETag 획득
String eTag = cosObjectSummary.getETag();
// 마지막 수정 시간 획득
Date lastModified = cosObjectSummary.getLastModified();
// 파일 스토리지 클래스 획득
String StorageClassStr = cosObjectSummary.getStorageClass();
}
```

### Bucket ACL

버킷의 액세스 접근 제어 리스트ACL을 설정합니다.

Set Bucket  ACL은 커버 작업으로, 기존의 권한 설정을 커버합니다.

ACL은 사전 정의된 권한 정책(CannedAccessControlList) 또는 사용자 지정의 권한 제어(AccessControlList)를 포함합니다. 두 가지 유형의 권한을 동시에 설정하면 사전 정의된 정책이 무시되고 사용자 지정 정책이 위주로 됩니다. 관련 권한 세부 정보는 권한 섹션을 참조하십시오.

- **방법 원형**

```java
// 방법 1 (사용자 지정 정책 설정)
public void setBucketAcl(String bucketName, AccessControlList acl)
  throws CosClientException, CosServiceException;
// 방법 2 (사전 정의 정책 설정)
public void setBucketAcl(String bucketName, CannedAccessControlList acl) throws CosClientException, CosServiceException;
// 방법 3 (위의 두 가지 방법 패키징하고, 두 가지 정책 설정을 포함하고, 동시 설정할 경우 사용자 지정 정책이 위주)
public void setBucketAcl(SetBucketAclRequest setBucketAclRequest)
  throws CosClientException, CosServiceException;
```

- **매개변수 설명**

방법3의 매개변수는 1과 2를 포함하므로 방법3을 예로 소개합니다.

| 매개변수 이름     | 매개변수 설명       | 유형                |
| ------------------- | -------------- | ------------------- |
| setBucketAclRequest | 권한 설정 요청 유형 | SetBucketAclRequest |

Request 멤버 설명:

| Request 멤버 | 설정 방법            | 설명                                                         | 유형                    |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName   | 생성자 또는 set 방법 | bucket의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String                  |
| acl          | 생성자 또는 set 방법 | 사용자 지정 권한 정책                                               | AccessControlList       |
| cannedAcl    | 생성자 또는 set 방법 | 사전 정의 정책, 예: 공개 읽기, 공개 읽기/쓰기, 비공개 읽기 등                         | CannedAccessControlList |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상 CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
// 사용자 지정 ACL 설정
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
owner.setId("qcs::cam::uin/2779643970:uin/2779643970");
acl.setOwner(owner);
String id = "qcs::cam::uin/2779643970:uin/734505014";
UinGrantee uinGrantee = new UinGrantee("qcs::cam::uin/2779643970:uin/734505014");
uinGrantee.setIdentifier(id);
acl.grantPermission(uinGrantee, Permission.FullControl);
cosClient.setBucketAcl(bucketName, acl);

// 사전 정의 ACL 설정
// 비공개 읽기/쓰기 설정(새로 생성된 버킷은 기본으로 모두 비공개 읽기/쓰기임)
cosClient.setBucketAcl(bucketName, CannedAccessControlList.Private);
// 공개 읽기 및 비공개 쓰기 설정
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicRead);
// 공개 읽기/쓰기 설정
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicReadWrite);
```

### Get Bucket ACL

Bucket의 접근 정책 ACL을 조회합니다.

- **방법 원형**

```java
public AccessControlList getBucketAcl(String bucketName)
       throws CosClientException, CosServiceException
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은{name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |

- **반환값**
  - 성공: 하나의 Bucket의 ACL을 반환합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상 CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
AccessControlList acl = cosClient.getBucketAcl(bucketName);
```

### Set Bucket CORS

Bucket의 크로스 도메인 접근 규칙을 설정합니다.

- **방법 원형**

```java
public void setBucketCrossOriginConfiguration(String bucketName, BucketCrossOriginConfiguration bucketCrossOriginConfiguration);
```

- **매개변수 설명**

| 매개변수 이름                         | 매개변수 설명                                                     | 유형                           |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------ |
| bucketName                     | bucket의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String                         |
| bucketCrossOriginConfiguration | 설정한 Bucket의 크로스 도메인 정책                                       | BucketCrossOriginConfiguration |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
BucketCrossOriginConfiguration bucketCORS = new BucketCrossOriginConfiguration();
List<CORSRule> corsRules = new ArrayList<>();
CORSRule corsRule = new CORSRule();
// 규칙 이름
corsRule.setId("set-bucket-cors-test");  
// 허용하는 HTTP 방법
corsRule.setAllowedMethods(AllowedMethods.PUT, AllowedMethods.GET, AllowedMethods.HEAD);
corsRule.setAllowedHeaders("x-cos-grant-full-control");
corsRule.setAllowedOrigins("http://mail.qq.com", "http://www.qq.com",
        "http://video.qq.com");
corsRule.setExposedHeaders("x-cos-request-id");
corsRule.setMaxAgeSeconds(60);
corsRules.add(corsRule);
bucketCORS.setRules(corsRules);
cosClient.setBucketCrossOriginConfiguration(bucketName, bucketCORS);
```

### Get Bucket CORS

Bucket의 크로스 도메인 접근 규칙을 획득합니다.

- **방법 원형**

```java
public BucketCrossOriginConfiguration getBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은{name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |

- **반환값**
  - 성공: Bucket의 크로스 도메인 규칙을 반환합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
BucketCrossOriginConfiguration corsGet = cosClient.getBucketCrossOriginConfiguration(bucketName);
List<CORSRule> corsRules = corsGet.getRules();
for (CORSRule rule : corsRules) {
List<AllowedMethods> allowedMethods = rule.getAllowedMethods();
List<String> allowedHeaders = rule.getAllowedHeaders();
List<String> allowedOrigins = rule.getAllowedOrigins();
List<String> exposedHeaders = rule.getExposedHeaders();
int maxAgeSeconds = rule.getMaxAgeSeconds();
}
```

### Delete Bucket CORS

Bucket의 크로스 도메인 접근 규칙을 삭제합니다.

- **방법 원형**

```java
public void deleteBucketCrossOriginConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은{name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상 CosClientException 또는 CosServiceException을 throw합니다. 구체적인 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
cosClient.deleteBucketCrossOriginConfiguration(bucketName);
```

### Set Bucket MultiVersioning

Bucket의 버전 관리를 활성화합니다. 버전 관리를 활성화한 후에는 각 파일이 여러 버전으로 유지됩니다.

- **방법 원형**

```java
public void setBucketVersioningConfiguration(SetBucketVersioningConfigurationRequest setBucketVersioningConfigurationRequest)
    throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름                                  | 매개변수 설명                                                     | 유형                                    |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| bucketName                              | bucket의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String                                  |
| setBucketVersioningConfigurationRequest | 버전 관리 구성                                                 | SetBucketVersioningConfigurationRequest |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
String bucketName = "movie-1251668577";

// 버전 관리 활성화
cosClient.setBucketVersioningConfiguration(
        new SetBucketVersioningConfigurationRequest(bucketName,
                new BucketVersioningConfiguration(BucketVersioningConfiguration.ENABLED)));

// 버전 관리 끄기
cosClient.setBucketVersioningConfiguration(
        new SetBucketVersioningConfigurationRequest(bucketName,
                new BucketVersioningConfiguration(BucketVersioningConfiguration.SUSPENDED)));
```

### Get  Bucket MultiVersioning

Bucket 의 버전 관리 상태를 획득합니다

- **방법 원형**

```java
// 방법1 bucket 이름을 입력하면 됩니다
public BucketVersioningConfiguration getBucketVersioningConfiguration(String bucketName)
            throws CosClientException, CosServiceException;

// 방법2 GetBucketVersioningConfigurationRequest를 통해 획득합니다			
public BucketVersioningConfiguration getBucketVersioningConfiguration(
    GetBucketVersioningConfigurationRequest getBucketVersioningConfigurationRequest)
        throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름                                  | 매개변수 설명                                                     | 유형                                    |
| --------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| bucketName                              | bucket의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String                                  |
| getBucketVersioningConfigurationRequest | 버전 관리 구성 요청 획득                                               | SetBucketVersioningConfigurationRequest |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
String bucketName = "movie-1251668577";

// 버전 관리 획득
BucketVersioningConfiguration bvc =
        cosClient.getBucketVersioningConfiguration(bucketName);

// 버전 관리 획득
BucketVersioningConfiguration bvc2 = cosClient.getBucketVersioningConfiguration(
                new GetBucketVersioningConfigurationRequest(bucketName));
```

### Set Bucket Replication

bucket 교차 지역 복사를 설정합니다. 교차 지역 복사는 버전 관리에 의존하므로 먼저 버전 관리를 활성화하십시오

- **방법 원형**

```java
public void setBucketReplicationConfiguration(
        SetBucketReplicationConfigurationRequest setBucketReplicationConfigurationRequest)
                throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름                                   | 매개변수 설명                                                     | 유형                                    |
| ---------------------------------------- | ------------------------------------------------------------ | --------------------------------------- |
| bucketName | bucket의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String                                  |
| setBucketReplicationConfigurationRequest | 교차 지역 복사 구성                                               | SetBucketVersioningConfigurationRequest |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
String bucketName = "movie-1251668577";

ReplicationRule replicationRule = new ReplicationRule();
replicationRule.setStatus(ReplicationRuleStatus.Enabled);
replicationRule.setPrefix("");

ReplicationDestinationConfig replicationDestinationConfig =
     new ReplicationDestinationConfig();
// bucketQCS는 복사하려는 대상 bucket을 설명하는 데 사용됩니다. 형식은 qcs:id/0:cos:${dest-region}:appid/${appid}:${bucketname-not-contain-appid}입니다
String bucketQCS = "qcs:id/0:cos:ap-chongqing:appid/1251668577:moviebak-chongqing";
replicationDestinationConfig.setBucketQCS(bucketQCS);
replicationDestinationConfig.setStorageClass(StorageClass.Standard);
replicationRule.setDestinationConfig(replicationDestinationConfig);
BucketReplicationConfiguration bucketReplicationConfiguration =
     new BucketReplicationConfiguration();
// ruleName구성 qcs::cam::uin/${uin}:uin/${uin}
String ruleName = "qcs::cam::uin/111222333:uin/111222333";
bucketReplicationConfiguration.setRoleName(ruleName);
// ruid는 복사 규칙의 ID를 설명하는 데 사용됩니다
String ruleId = "moviebak-chongqing-copy";
bucketReplicationConfiguration.addRule(ruleId, replicationRule);
cosClient.setBucketReplicationConfiguration(bucketName, bucketReplicationConfiguration);
```

### Get Bucket Replication

bucket 교차 지역 복사를 획득합니다.

- **방법 원형**

```java
// bucket 지역 간 복사 구성 획득 방법1
public BucketCrossOriginConfiguration getBucketCrossOriginConfiguration(String bucketName)
        throws CosClientException, CosServiceException;

// bucket 지역 간 복사 획득 방법2		
public BucketCrossOriginConfiguration getBucketCrossOriginConfiguration(
        GetBucketCrossOriginConfigurationRequest getBucketCrossOriginConfigurationRequest)
                throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름                                   | 매개변수 설명                                                     | 유형                                     |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName                               | bucket의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String                                   |
| getBucketCrossOriginConfigurationRequest | 지역 간 복사 구성 획득 요청                                   | GetBucketCrossOriginConfigurationRequest |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
String bucketName = "movie-1251668577";

// bucket 지역 간 복사 구성 획득 방법1
BucketReplicationConfiguration brcfRet = cosClient.getBucketReplicationConfiguration(bucketName);

// bucket 지역 간 복사 구성 획득 방법2
BucketReplicationConfiguration brcfRet2 = cosClient.getBucketReplicationConfiguration(
                new GetBucketCrossOriginConfigurationRequest(bucketName));
```

### Delete Bucket Replication

bucket 교차 지역 복사를 삭제합니다.

- **방법 원형**

```java
// bucket 지역 간 복사 구성 삭제 방법1
public void deleteBucketCrossOriginConfiguration(String bucketName)
        throws CosClientException, CosServiceException;

// bucket 지역 간 복사 삭제 방법2		
public void deleteBucketCrossOriginConfiguration(
        DeleteBucketCrossOriginConfigurationRequest deleteBucketCrossOriginConfigurationRequest)
                throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름                                      | 매개변수 설명                                                     | 유형                                        |
| ------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------- |
| bucketName | bucket의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |
| deleteBucketCrossOriginConfigurationRequest | 지역 간 복사 구성 삭제 요청                                   | DeleteBucketCrossOriginConfigurationRequest |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
String bucketName = "movie-1251668577";

// bucket 지역 간 복사 구성 삭제 방법1
BucketReplicationConfiguration brcfRet =  cosClient.deleteBucketReplicationConfiguration(bucketName);

// bucket 지역 간 복사 구성 삭제 방법2
BucketReplicationConfiguration brcfRet2 = cosClient.getBucketReplicationConfiguration(
                new DeleteBucketCrossOriginConfigurationRequest(bucketName));
```

### Set Bucket LifeCycle

Bucket 의 수명 주기 규칙을 설정합니다.

- **방법 원형**

```java
public void setBucketLifecycleConfiguration(String bucketName, BucketLifecycleConfiguration bucketLifecycleConfiguration)
        throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름                       | 매개변수 설명                                                     | 유형                         |
| ---------------------------- | ------------------------------------------------------------ | ---------------------------- |
| bucketName | bucket의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String                       |
| bucketLifecycleConfiguration | 수명 주기 구성                                                 | BucketLifecycleConfiguration |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
List<Rule> rules = new ArrayList<>();
// 규칙1  30일 후 경로가 hongkong_movie/ 로 시작되는 파일을 삭제합니다
Rule deletePrefixRule = new Rule();
deletePrefixRule.setId("delete prefix xxxy after 30 days");
deletePrefixRule
.setFilter(new LifecycleFilter(newLifecyclePrefixPredicate("hongkong_movie/")));
// 파일 업로드 또는 변경 후, 30일 후 삭제합니다
deletePrefixRule.setExpirationInDays(30);
// 규칙을 유효한 상태로 설정합니다
deletePrefixRule.setStatus(BucketLifecycleConfiguration.ENABLED);

// 규칙2  20일 후 저빈도로 침전하고 1년 후에 삭제합니다
Rule standardIaRule = new Rule();
standardIaRule.setId("standard_ia transition");
standardIaRule.setFilter(new LifecycleFilter(new LifecyclePrefixPredicate("standard_ia/")));
List<Transition> standardIaTransitions = new ArrayList<>();
Transition standardTransition = new Transition();
standardTransition.setDays(20);
standardTransition.setStorageClass(StorageClass.Standard_IA.toString());
standardIaTransitions.add(standardTransition);
standardIaRule.setTransitions(standardIaTransitions);
standardIaRule.setStatus(BucketLifecycleConfiguration.ENABLED);
standardIaRule.setExpirationInDays(365);

// 두 가지 규칙을 정책 집합에 추가합니다
rules.add(deletePrefixRule);
rules.add(standardIaRule);

// bucketLifecycleConfiguration 생성
BucketLifecycleConfiguration bucketLifecycleConfiguration =
new BucketLifecycleConfiguration();
bucketLifecycleConfiguration.setRules(rules);

//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
SetBucketLifecycleConfigurationRequest setBucketLifecycleConfigurationRequest =
new SetBucketLifecycleConfigurationRequest(bucketName, bucketLifecycleConfiguration);

// 수명 주기 설정
cosClient.setBucketLifecycleConfiguration(setBucketLifecycleConfigurationRequest);
```

### Get Bucket LifeCycle

Bucket 의 수명 주기 규칙을 획득합니다.

- **방법 원형**

```java
public BucketLifecycleConfiguration getBucketLifecycleConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은{name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |

- **반환값**
  - 성공: BucketLifecycleConfiguration 유형을 반환하며, bucket 의 수명 주기 규칙을 포함합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
BucketLifecycleConfiguration queryLifeCycleRet =
        cosClient.getBucketLifecycleConfiguration(bucketName);
List<Rule> ruleLists = queryLifeCycleRet.getRules();
```

### Delete Bucket LifeCycle

비어 있는 Bucket의 수명 주기 규칙을 삭제합니다.

- **방법 원형**

```java
public void deleteBucketLifecycleConfiguration(String bucketName)
throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은{name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
cosClient.deleteBucketLifecycleConfiguration(bucketName);
```

## Object API 설명

### PUT Object( Object 업로드)

로컬 파일 또는 알려진 길이의 입력 스트림 내용을 COS에 업로드합니다. 이미지 유형의 작은 파일(20MB 이하)을 업로드하는 데 적용되며, 최대 5GB(포함)까지 지원합니다. 5GB 이상은 멀티파트 업로드 또는 고급 API 업로드를 사용하십시오.

- 업로드 과정 중에 기본으로 파일 길이와 MD5 에 대해 인증을 진행합니다( MD5 인증 끄기는 샘플 코드 참조).
-  COS 에 이미 같은 Key의 객체가 존재하면 업로드 시 덮어쓰기 됩니다.
-  현재 접근 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 업로드 시 설정하지 마십시오. 기본으로 Bucket 권한은 상속됩니다.
- 업로드 후에 같은 `key` 로 `GetObject` API를 호출하여 로컬에 파일을 다운로드하거나 사전 서명 링크를 생성하고(다운로드는 method 를 `GET` 로 지정하십시오. 자세한 API 설명은 아래 참조), 다른 포트로 발송하여 다운로드합니다.


- **방법 원형**

```java
// 방법1  로컬 파일을 COS에 업로드합니다
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// 방법2  입력 스트림을 COS에 업로드합니다
public PutObjectResult putObject(String bucketName, String key, InputStream input,
ObjectMetadata metadata) throws CosClientException, CosServiceException;
// 방법3  위의 두 가지 방법의 패키징에 대해 더 세분화된 매개변수 제어를 지원합니다(예: content-type,  content-disposition 등).
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름           | 매개변수 설명     | 매개변수 유형         |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 방법            | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | 생성자 또는 set 방법 | bucket 의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String         |
| key          | 생성자 또는 set 방법 | 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | string         |
| file         | 생성자 또는 set 방법 | 로컬 파일                                                     | File           |
| input        | 생성자 또는 set 방법 | 입력 스트림                                                       | InputStream    |
| metadata     | 생성자 또는 set 방법 | 파일의 메타 정보                                                 | ObjectMetadata |

- **반환값**
  - 성공: PutObjectResult, 파일의 ETag 등 정보를 포함합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
// 방법1 로컬 파일 업로드
File localFile = new File("/data/test.txt");
String key = "aaa.txt";
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, localFile);
String etag = putObjectResult.getETag();  // 파일의 etag 획득

// 방법2 입력 스트림에서 업로드(사전에 입력 스트림의 길이를 알려야 하며, 그렇지 않으면 oom를 초래할 수 있습니다)
FileInputStream fileInputStream = new FileInputStream(localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// 입력 스트림의 길이는 500으로 설정합니다
objectMetadata.setContentLength(500);  
// Content type 를 설정합니다. 기본 설정은 application/octet-stream
objectMetadata.setContentType("application/pdf");
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, fileInputStream, objectMetadata);
String etag = putObjectResult.getETag();
// 입력 스트림 끄기...

// 방법3 더 많은 세분화된 제어를 제공하며, 자주 사용하는 설정은 아래와 같습니다
// 1 storage-class 스토리지 클래스, 표준(기본), 저빈도, 니어 라인 설정에 사용됩니다
// 2 content-type, 로컬 파일 업로드에 대해, 기본으로 로컬 파일의 접미사를 기반으로 매핑합니다(예: jpg 파일 매핑은 image/jpeg).
//   스트리밍 업로드에 대한 기본값은 application/octet-stream
// 3 업로드와 동시에 권한을 설정합니다(API set object acl 호출을 통해 설정할 수도 있음)
// 4. MD5 인증 업로드를 전역 끄기 하려면 시스템 환경 변수를 설정해야 합니다. 이 설정은 모든 영향을 받을 수 있는 모든 업로드를 인증합니다. 기본으로 인증을 진행합니다.
// 인증 끄기  System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
// 인증 다시 켜기  System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, null);
File localFile = new File("/data/dog.jpg");
String key = "mypic.jpg";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, file);
// 스토리지 클래스를 저빈도로 설정합니다
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
// 사용자 지정 속성(예: content-type, content-disposition 등)을 설정합니다
ObjectMetadata objectMetadata = new ObjectMetadata();
// Content type 를 설정합니다. 기본 설정은 application/octet-stream
objectMetadata.setContentType("image/jpeg");
putObjectRequest.setMetadata(objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
String etag = putObjectResult.getETag();  // 파일의 etag 획득
```

- **멀티파트 파일 업로드**

멀티파트 파일 업로드는 파일을 여러 개의 작은 파트로 나누어 업로드를 진행하는 것으로, 여러 개의 작은 파트를 동시에 업로드할 수 있으며, 최대 40 TB까지 지원합니다.

멀티파트 파일 업로드의 절차:

1. 멀티파트 업로드를 초기화하고, uploadid를 획득합니다.(initiateMultipartUpload)
2. 멀티파트 데이터를 업로드합니다(동시 발생 가능).(uploadPart)
3. 멀티파트 업로드를 완료합니다.(completeMultipartUpload)

또한 이미 업로드한 멀티파트(listParts)를 획득하고, 멀티파트 업로드를 정지할 수 있습니다(abortMultipartUpload). 멀티파트 업로드의 절차와 조건이 많은 편이므로, 아래 패키징된 고급 API 업로드 사용을 권장합니다.

**Tips**: 멀티파트 업로드 과정 중에 기본으로 각 멀티파트의 파일 길이와 MD5 에 대해 인증을 진행합니다( MD5 인증 끄기는 샘플 코드를 참조하고 이전 섹션 중의 끄기 방법을 참조하십시오).

- **방법 원형**

```java
// 방법1 멀티파트 업로드 초기화
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
// 방법2 데이터 멀티파트 업로드
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest)
            throws CosClientException, CosServiceException;
// 방법3 멀티파트 업로드 완료
public CompleteMultipartUploadResult completeMultipartUpload(
            CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
// 방법4 이미 업로드된 멀티파트 나열
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
// 방법5 멀티파트 업로드 정지
public void abortMultipartUpload(AbortMultipartUploadRequest request)
            throws CosClientException, CosServiceException;
```

- **반환값**
- **방법1 (initiateMultipartUpload)**
  - 성공: InitiateMultipartUploadResult 유형을 반환하며, 후속 멀티파트 업로드에서 반드시 사용하는 upload id를 포함합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상 CosClientException 또는 CosServiceException을 throw합니다. 구체적인 설명은 이상 유형 설명을 참조하십시오.
- **방법2 (uploadPart)**
  - 성공: UploadPartResult를 반환하며, 해당 멀티파트의 Etag 와 partNumber를 포함합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상 CosClientException 또는 CosServiceException을 throw합니다. 구체적인 설명은 이상 유형 설명을 참조하십시오.
- **방법3 (completeMultipartUpload)**
  - 성공: CompleteMultipartUploadResult를 반환하며, 전체 텍스트의 Etag를 포함합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상 CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **방법4 (listParts)**
  - 성공: PartListing을 반환하며, 각 멀티파트의 ETag 와 번호, 그리고 다음 list의 시작점 marker를 포함합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **방법5 (abortMultipartUpload)**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상 CosClientException 또는 CosServiceException을 throw합니다. 구체적인 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
// 멀티파트 초기화
InitiateMultipartUploadRequest initRequest =
                new InitiateMultipartUploadRequest(bucketName, key);
InitiateMultipartUploadResult initResponse = cosClient.initiateMultipartUpload(initRequest);
String uploadId = initResponse.getUploadId()
// 최대 1000개의 멀티파트를 업로드하며, 멀티파트 크기는 1M * 5G를 지원합니다.
// 멀티파트 크기를 4M으로 설정합니다. 총 n개의 멀티파트라면 1~n-1의 멀티파트의 크기는 일치하며, 마지막 멀티파트의 크기는 앞부분의 멀티파트 크기보다 작거나 같습니다
List<PartETag> partETags = new ArrayList<PartETag>();
int partNumber = 1;
int partSize = 4 * 1024 * 1024;
// partStream은 part 데이터의 입력 스트림을 의미하며, 스트림 길이는 partSize입니다
UploadPartRequest uploadRequest =  new    UploadPartRequest().withBucketName(bucketName).
 withUploadId(uploadId).withKey(key).withPartNumber(partNumber).
  withInputStream(partStream).withPartSize(partSize);  
UploadPartResult uploadPartResult = cosClient.uploadPart(uploadRequest);
String eTag = uploadPartResult.getETag();  // part의 Etag 획득
partETags.add(new PartETag(partNumber, eTag));  // partETags는 이미 업로드된 모든 part 의 Etag 정보를 기록합니다
// ... partNumber 2번째부터 n 번째 멀티파트를 업로드합니다

// complete 멀티파트 업로드를 완료합니다.
CompleteMultipartUploadRequest compRequest = new CompleteMultipartUploadRequest(bucketName, key,
           uploadId, partETags);
CompleteMultipartUploadResult result =  cosClient.completeMultipartUpload(compRequest);

// ListPart는 complete 멀티파트 업로드 이전 또는 abort 멀티파트 업로드 이전에 uploadId에 대응하는 이미 업로드된 멀티파트 정보를 획득하는 데 사용되며, partEtags 생성에 사용할 수 있습니다
ListPartsRequest listPartsRequest = new ListPartsRequest(bucket, key, uploadId);
do {
      partListing = cosClient.listParts(listPartsRequest);
      for (PartSummary partSummary : partListing.getParts()) {
           partETags.add(new PartETag(partSummary.getPartNumber(), partSummary.getETag()));
      }
      listPartsRequest.setPartNumberMarker(partListing.getNextPartNumberMarker());
} while (partListing.isTruncated());

// abortMultipartUpload 는 아직 complete 하지 않은 멀티파트 업로드를 중지하는 데 사용됩니다
AbortMultipartUploadRequest abortMultipartUploadRequest =
  									new AbortMultipartUploadRequest(bucket, key, uploadId);
cosClient.abortMultipartUpload(abortMultipartUploadRequest);
```

### Get Object

파일을 로컬에 다운로드하거나 파일 다운로드의 다운로드 스트림을 획득합니다.

- **방법 원형**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
// 방법1 파일을 다운로드하고 입력 스트림을 획득합니다
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
// 방법2 파일을 로컬에 다운로드합니다.
public ObjectMetadata getObject(GetObjectRequest getObjectRequest, File destinationFile)
            throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름           | 매개변수 설명       | 매개변수 유형         |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | 파일 다운로드 요청   | GetObjectRequest |
| destinationFile  | 로컬의 저장 파일 | File             |

Request 멤버 설명:

| Request 멤버 | 설정 방법            | 설명                                                         | 유형   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName   | 생성자 또는 set 방법 | bucket 의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |
| key          | 생성자 또는 set 방법 | 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | string |
| range        | set방법             | 다운로드의 range 범위                                            | Long[] |

- **반환값**
- **방법1 (다운로드 입력 스트림 획득)**
  - 성공: COSObject 유형을 반환하며, 입력 스트림과 파일 속성을 포함합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **방법2 (파일을 로컬에 다운로드)**
  - 성공: 파일의 속성 objectMetadata를 반환하며, 사용자 지정 헤더와 content-type 등 속성을 포함합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
String key = "abc/def.jpg";
// 방법1 다운로드 입력 스트림 획득
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();

// 방법2 파일을 로컬에 다운로드
File downFile = new File("src/test/resources/mydown.txt");
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### Delete Object

COS 의 파일을 삭제합니다.

- **방법 원형**

```java
// 파일 삭제
public void deleteObject(String bucketName, String key)
            throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은{name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |
| key          | 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | string |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
// COS 파일 삭제
// //bucket의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다
String bucketName = "movie-1251668577";
String key = "abc/def.jpg";
cosClient.deleteObject(bucket, key);
```

### Head Object

획득한 COS 의 파일 속성을 조회합니다.

- **방법 원형**

```java
// 파일 속성 획득
public ObjectMetadata getObjectMetadata(String bucketName, String key)
  throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은{name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |
| key          | 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | string |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
// COS 파일 속성 획득
// //bucket의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 이 형식이어야 합니다
String bucketName = "movie-1251668577";
String key = "abc/def.jpg";
ObjectMetadata objectMetadata = cosClient.getObjectMetadata(bucketName, key);
```

### Put Object Copy

Object 를 새 경로 또는 새 Bucket으로 복사합니다. 교차 지역 계정의 Bucket 간 복사를 지원하며, 소스 파일의 읽기 권한 및 대상 파일의 쓰기 권한이 필요합니다. 최대 5G 파일의 copy를 지원하며, 5G 이상 파일은 고급 API copy를 사용하십시오.

- **방법 원형**

```java
// 파일 속성 획득
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
      throws CosClientException, CosServiceException
```

- **매개변수 설명**

| 매개변수 이름            | 매개변수 설명     | 매개변수 유형          |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | 파일 복사 요청 | CopyObjectRequest |

Request 멤버 설명:

| 매개변수 이름                | 매개변수 설명                                                     | 유형   |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion    | 소스 Bucket Region . 기본값: 현재 clientconfig 의 region 과 일치하며, 통일 지역 복사를 표시합니다 | String |
| sourceBucketName      | 소스 Bucket 이름, bucket 의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |
| sourceKey             | 소스 객체 키, 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | string |
| sourceVersionId       | 소스 파일 version id(버전 관리를 활성화한 소스 Bucket에 적용). 기본값: 소스 파일의 현재 최신 버전 | String |
| destinationBucketName | 대상 Bucket 이름, bucket의 명명 규칙은 {name}-{appid} 이며, name은 알파벳 숫자와 대시로 구성됩니다 | String |
| destinationKey        | 대상 객체 키, 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | string |
| storageClass          | 복사한 대상 파일의 스토리지 클래스(표준, 저빈도, 니어 라인) 기본값: 표준   |String |

- **반환값**
  - 성공: CopyObjectResult를 반환하며, 새 파일의 Etag 등 정보를 포함합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
// 같은 지역 같은 계정 복사
// 소스 bucket, bucket 의 명명 규칙은 {name}-{appid} 입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String srcBucketName = "srcBucket-1251668577";
// 복사할 소스 파일입니다.
String srcKey = "aaa/bbb.txt";
// 대상 bucket, bucket의 명명 규칙은 {name}-{appid} 입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String destBucketName = "destBucket-1251668577";
// 복사할 대상 파일입니다.
String destKey = "ccc/ddd.txt";
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketName, srcKey, destBucketName, destKey);
CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);

// 계정 간 교차 지역 복사(소스 파일에 대한 읽기 권한 및 대상 파일에 대한 쓰기 권한이 필요)
String srcBucketNameOfDiffAppid = "srcBucket-125100000";
Region srcBucketRegion = new Region("ap-shanghai");
copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketNameOfDiffAppid, srcKey, destBucketName, destKey);
copyObjectResult = cosClient.copyObject(copyObjectRequest);
```

### Set Object ACL

Object의 접근 제어 리스트(Access Control List)를 설정합니다. Set Object ACL 설정은 조작을 덮어쓰기하며, 기존 권한 설정을 덮어쓰기할 수 있습니다.

>!현재 접근 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 설정하지 마십시오. 기본으로 Bucket 권한은 상속됩니다.

ACL은 사전 정의된 권한 정책(CannedAccessControlList) 또는 사용자 지정의 권한 제어(AccessControlList)를 포함합니다. 두 가지 유형의 권한을 동시에 설정하면 사전 정의된 정책이 무시되고 사용자 지정 정책이 위주로 됩니다. 관련 권한 세부 정보는 권한 섹션을 참조하십시오.

- **방법 원형**

```java
// 방법1 (사용자 지정 정책 설정)
public void setObjectAcl(String bucketName, String key, AccessControlList acl)
       throws CosClientException, CosServiceException
// 방법2 (사전 정의 정책 설정)
public void setObjectAcl(String bucketName, String key, CannedAccessControlList acl)
       throws CosClientException, CosServiceException
// 방법3 (위의 두 가지 방법의 패키징하고, 두 가지 정책 설정을 포함하고, 동시 설정할 경우 사용자 지정 정책이 위주)
public void setObjectAcl(SetObjectAclRequest setObjectAclRequest)
  throws CosClientException, CosServiceException;
```

- **매개변수 설명**
  - **방법3** 매개변수는 1과 2를 포함하므로 방법3을 예로 소개합니다.

| 매개변수 이름              | 매개변수 설명 | 유형                |
| ------------------- | -------- | ------------------- |
| SetObjectAclRequest | 요청 유형   | setObjectAclRequest |

Request 멤버 설명:

| Request 멤버 | 설정 방법            | 설명                                                         | 유형                    |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName   | 생성자 또는 set 방법 | bucket의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String                  |
| key          | 생성자 또는 set 방법 | 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | string                  |
| acl          | 생성자 또는 set 방법 | 사용자 지정 권한 정책                                               | AccessControlList       |
| cannedAcl    | 생성자 또는 set 방법 | 사전 정의 정책, 예: 공개 읽기, 공개 읽기/쓰기, 비공개 읽기 등                         | CannedAccessControlList |

- **반환값**
  - 성공: 반환값이 없습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
String key = "abc/def.jpg";
// 사용자 지정 ACL 설정
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
owner.setId("qcs::cam::uin/2779643970:uin/2779643970");
acl.setOwner(owner);
String id = "qcs::cam::uin/2779643970:uin/734505014";
UinGrantee uinGrantee = new UinGrantee("qcs::cam::uin/2779643970:uin/734505014");
uinGrantee.setIdentifier(id);
acl.grantPermission(uinGrantee, Permission.FullControl);
cosClient.setObjectAcl(buckeName, key, acl);

// 사전 정의 ACL 설정
// 비공개 읽기 권한 설정(Object의 권한은 기본으로 Bucket의 통합)
cosClient.setObjectAcl(buckeName, key, CannedAccessControlList.Private);
// 공개 읽기 및 비공개 쓰기 설정
cosClient.setObjectAcl(buckeName, key, CannedAccessControlList.PublicRead);
// 공개 읽기/쓰기 설정
cosClient.setObjectAcl(buckeName, key, CannedAccessControlList.PublicReadWrite);
```

### Get Object ACL

Object의 접근 정책 ACL을 조회합니다.

- **방법 원형**

```java
public AccessControlList getObjectAcl(String bucketName, String key)
  throws CosClientException, CosServiceException;
```

- **매개변수 설명**

| 매개변수 이름     | 매개변수 설명                                                     | 유형   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | bucket 의 명명 규칙은{name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |
| key          | 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | string |

- **반환값**
  - 성공: Object 소재의 ACL을 반환합니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상 CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
String key = "abc/def.jpg";
AccessControlList acl = cosClient.getObjectAcl(bucketName, key);
```

## 사전 서명 링크 생성

COSClient는 사전 서명 URL 생성을 제공하고 클라이언트에 배포 가능하여 다운로드 또는 업로드에 사용됩니다.단, 파일이 비공개 읽기 권한일 경우 사전 서명 링크는 일정한 기간 동안만 유효함을 주의하십시오.

- **방법 원형**

```java
// 사전 서명 URL 생성
public URL generatePresignedUrl(GeneratePresignedUrlRequest req) throws CosClientException
```

- **매개변수 설명**

| 매개변수 이름 | 매개변수 설명     | 유형                        |
| ------ | ------------ | --------------------------- |
| req    | 사전 서명 요청 유형 | GeneratePresignedUrlRequest |

Request 멤버 설명:

| Request 멤버    | 설정 방법            | 설명                                                         | 유형                    |
| --------------- | ------------------- | ------------------------------------------------------------ | ----------------------- |
| method          | 생성자 또는 set 방법 | HTTP 방법, PUT(업로드에 사용), GET(다운로드에 사용), DELETE(삭제에 사용)    | HttpMethodName          |
| bucketName   | 생성자 또는 set 방법 | bucket 의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String                  |
| key             | 생성자 또는 set 방법 | 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | string                  |
| expiration      | set 방법           | 서명 만료의 시간                                                | Date                    |
| contentType     | set 방법            | 서명을 해야 하는 요청 중의 Content-Type                                | String                  |
| contentMd5      | set 방법            | 서명을 해야 하는 요청 중의 Content-Md5                                 | String                  |
| responseHeaders | set 방법            | 서명의 다운로드 요청 중 덮어쓰기 해야 할 반환 HTTP 헤더                       | ResponseHeaderOverrides |

- **반환값**

URL

- **예시**

예시1: 서명이 있는 다운로드 링크를 생성하며, 예제 코드는 아래와 같습니다.

```java
// 다운로드 링크를 생성합니다
// bucket의 명명 규칙은 {name}-{appid} 입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "mybucket-1251668577";
String key = "aaa.txt";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// 서명 만료 시간을 설정(선택 가능)하며 만약 설정하지 않았을 경우, 기본으로 ClientConfig 중의 서명 만료 시간(1시간)을 사용합니다
// 여기서 서명을 30분 후에 만료되도록 설정합니다
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL downloadUrl = cosClient.generatePresignedUrl(req);
String downloadUrlStr = downloadUrl.toString();
```

예시2: 서명이 있는 다운로드 링크를 생성하고 반환된 공통 헤더(예: content-type, content-language)를 덮어쓰기 하도록 설정합니다. 예제 코드는 아래와 같습니다.

```java
// bucket의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다
String bucketName = "mybucket-1251668577";
String key = "aaa.txt";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// 다운로드 시 반환되는 http 헤더를 설정합니다
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
String responseContentDispositon = "filename=\"abc.txt\"";
String responseCacheControl = "no-cache";
String cacheExpireStr =
        DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24L * 3600L * 1000L));
responseHeaders.setContentType(responseContentType);
responseHeaders.setContentLanguage(responseContentLanguage);
responseHeaders.setContentDisposition(responseContentDispositon);
responseHeaders.setCacheControl(responseCacheControl);
responseHeaders.setExpires(cacheExpireStr);
req.setResponseHeaders(responseHeaders);
// 서명 만료 시간을 설정(선택 가능)하며 만약 설정하지 않았을 경우, 기본으로 ClientConfig 중의 서명 만료 시간(1시간)을 사용합니다
// 여기서 서명을 30분 후에 만료되도록 설정합니다
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);
URL url = cosClient.generatePresignedUrl(req);
```

예시3: 공개 bucket(익명 읽기 가능)을 생성할 경우, 서명 연결이 필요하지 않습니다. 예제 코드는 아래와 같습니다.

```java
// 익명의 요청 서명을 생성하면, 익명의 cosClient를 다시 초기화해야 합니다
// 1 사용자 ID 정보를 초기화하며, 익명 ID는 ak sk를 입력할 필요가 없습니다
COSCredentials cred = new AnonymousCOSCredentials();
// 2 bucket의 지역을 설정하며, COS 지역의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참조하십시오
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
// bucket 이름은 appid를 포함해야 합니다
String bucketName = "mybucket-1251668577";

String key = "aaa.txt";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
URL url = cosClient.generatePresignedUrl(req);

System.out.println(url.toString());

cosClient.shutdown();
```

예시4: 사전 서명의 업로드 링크를 생성할 경우, 직접 클라이언트에 배포하여 파일의 업로드를 진행할 수 있으며, 예제 코드는 아래와 같습니다.

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "mybucket-1251668577";

String key = "aaa.txt";
// 서명 만료 시간을 설정(선택 가능)하며 만약 설정하지 않았을 경우, 기본으로 ClientConfig 중의 서명 만료 시간(1시간)을 사용합니다
// // 서명을 30분 후 만료되도록 설정합니다.
Date expirationTime = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
URL url = cosClient.generatePresignedUrl(bucketName, key, expirationTime, HttpMethodName.PUT);
```

## 서명 생성

COSSigner 유형은 COS 서명 방법 생성을 제공하고, 모바일 SDK에 배포하는데 사용되어 파일의 업로드와 다운로드를 진행합니다.
서명의 경로와 배포 후 작업을 진행하는 key 가 서로 매칭되어야 합니다.

- **방법 원형**

```java
// COS 서명 생성
public String buildAuthorizationStr(HttpMethodName methodName, String resouce_path,
        COSCredentials cred, Date expiredTime);

// COS 서명 생성
// 두 번째 방법은 첫 번째 방법보다 일부 HTTP Header 와 모든 가져오기의 URL 중의 매개변수에 대한 서명을 추가로 제공합니다.
// 더 복잡한 서명 관리에 사용하며, 생성된 서명은 반드시 업로드 및 다운로드 등 작업 시, 대응하는 header 및 param이 있어야 합니다.
public String buildAuthorizationStr(HttpMethodName methodName, String resouce_path,
        Map<String, String> headerMap, Map<String, String> paramMap, COSCredentials cred,
        Date expiredTime);
```

- **매개변수 설명**

| 매개변수 이름       | 매개변수 설명                                                     | 유형           |
| ------------ | ------------------------------------------------------------ | -------------- |
| methodName   | HTTP 요청 방법, PUT, GET, DELETE, HEAD, POST를 설정할 수 있습니다            | HttpMethodName |
| resouce_path | 서명해야 하는 경로, 업로드 파일의 key와 같고, /로 시작해야 합니다.                 | HttpMethodName |
| cred         | 키 정보                                                     | COSCredentials |
| expiredTime  | 만료 시간                                                     | Date           |
| headerMap    | 서명해야 할 HTTP Header map, 가져오기 하는 Content-Type, Content-Md5 및 x 로 시작하는 header 에 대해서만 서명을 진행합니다 | Map            |
| paramMap     | 서명해야 할 URL Param map                                        | Map            |

- **반환값**
String

- **예시**

예시1. 서명 업로드 생성

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "mybucket-1251668577";
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
COSSigner signer = new COSSigner();
//만료 시간을 1시간으로 설정합니다
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// 서명할 key이며, 생성한 서명은 이 key 에 대응하는 업로드에만 사용됩니다
String key = "/aaa.txt";
String sign = signer.buildAuthorizationStr(HttpMethodName.PUT, key, cred, expiredTime);
```

예시2: 다운로드 서명 생성

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "mybucket-1251668577";
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
COSSigner signer = new COSSigner();
//만료 시간을 1시간으로 설정합니다
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// 서명할 key이며, 생성한 서명은 이 key에 대응하는 다운로드에만 사용됩니다
String key = "/aaa.txt";
String sign = signer.buildAuthorizationStr(HttpMethodName.GET, key, cred, expiredTime);
```

예시 3: 서명 삭제 생성

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "mybucket-1251668577";
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
COSSigner signer = new COSSigner();
//만료 시간을 1시간으로 설정합니다
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// 서명할 key이며, 생성한 서명은 이 key에 대응하는 삭제에만 사용됩니다
String key = "/aaa.txt";
String sign = signer.buildAuthorizationStr(HttpMethodName.DELETE, key, cred, expiredTime);
```

## 고급 API 파일 업로드(권장)

고급 API 는 TransferManger 유형으로부터 패키징을 통해 API를 업로드 및 다운로드하며 내부에는 하나의 스레드 풀이 있어 사용자의 업로드 및 다운로드 요청을 접수합니다. 이로써 사용자는 비동기화 제출 작업을 선택할 수 있습니다.

```java
// 스레드 풀의 크기는 클라이언트와 COS 네트워크가 충분한 상황(예: Tencent Cloud의 CVM을 사용하여 같은 지역에 COS를 업로드)에서, 16 또는 32으로 설정하면 네트워크 자원을 상대적으로 충분하게 사용할 수 있습니다.
// 공중망 전송을 사용하고 대역폭 품질이 높지 않은 경우에 대해, 해당 값을 낮출 것을 권장드리며 느린 네트워크 속도로 인한 요청 시간 초과가 발생하지 않도록 하십시오.
ExecutorService threadPool = Executors.newFixedThreadPool(32);
// threadpool 을 가져오기 하며, 스레드 풀을 가져오지 않은 경우, 기본으로 TransferManager 중의 개별 스레드의 기본 스레드 풀이 생성됩니다.
TransferManager transferManager = new TransferManager(cosClient, threadPool);
// .....(업로드 다운로드 요청 제출, 아래와 같습니다)
// TransferManger 종료
transferManager.shutdownNow();
```

### 파일 업로드

업로드한 API는 사용자 파일의 길이에 따라 자동으로 간편 업로드 및 멀티파트 업로드를 선택하여, 사용자의 사용 조건을 낮춥니다. 사용자는 멀티파트 업로드의 매개 절차를 신경 쓸 필요가 없습니다.

Tips는 다른 속성 설정에도 관련되며 스토리지 클래스, MD5 인증 등은 Put Object Api를 참조하십시오.

- **방법 원형**

```java
// 파일 업로드
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

- **매개변수 설명**

| 매개변수 이름           | 매개변수 설명     | 매개변수 유형         |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | 파일 업로드 요청 | PutObjectRequest |

Request 멤버 설명:

| Request 멤버 | 설정 방법            | 설명                                                         | 유형           |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName   | 생성자 또는 set 방법 | bucket 의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String         |
| key          | 생성자 또는 set 방법 | 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | string         |
| file         | 생성자 또는 set 방법 | 로컬 파일                                                     | File           |
| input        | 생성자 또는 set 방법 | 입력 스트림                                                       | InputStream    |
| metadata     | 생성자 또는 set 방법 | 파일의 메타 정보                                                 | ObjectMetadata |

- **반환값**
  - 성공: Upload를 반환하며, 업로드 완료 여부를 조회할 수 있고, 업로드 종료를 동기화하여 대기할 수도 있습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
String key = "/mypic.jpg";
File localFile = new File("/data/dog.jpg");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, file);
// 로컬 파일 업로드
Upload upload = transferManager.upload(putObjectRequest);
 // 전송이 끝날 때까지 기다립니다(업로드 종료를 동기화하여 대기하려면 waitForCompletion을 호출하십시오)
UploadResult uploadResult = upload.waitForUploadResult();
```

### 파일 다운로드

COS 의 파일을 로컬로 다운로드합니다.

- **방법 원형**

```java
// 파일을 다운로드합니다.
public Download download(final GetObjectRequest GetObjectRequest, final File file);
```

- **매개변수 설명**

| 매개변수 이름           | 매개변수 설명           | 매개변수 유형         |
| ---------------- | ------------------ | ---------------- |
| getObjectRequest | 파일 다운로드 요청       | GetObjectRequest |
| file             | 로컬에 다운로드 할 파일 | File             |

Request 멤버 설명:

| Request 멤버 | 설정 방법            | 설명                                                         | 유형   |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName   | 생성자 또는 set 방법 | bucket 의 명명 규칙은 {name}-{appid} 이며, name 은 알파벳 숫자와 대시로 구성됩니다 | String |
| key          | 생성자 또는 set 방법 | 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | string |
| range        | set 방법            | 다운로드의 range 범위                                            | Long[] |

- **반환값**
  - 성공: Download를 반환합니다. 다운로드 종료 여부를 조회할 수 있고, 다운로드 종료를 동기화하여 대기할 수 있습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "movie-1251668577";
String key = "/mypic.jpg";
File localDownFile = new File("/data/dog.jpg");
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, key);
// 파일을 다운로드합니다.
Download download = transferManager.download(getObjectRequest, localDownFile);
 // 전송이 끝날 때까지 기다립니다(업로드 종료를 동기화하여 대기하려면 waitForCompletion을 호출하십시오)
download.waitForCompletion();
```

### 파일 복사

copy API는 파일 크기에 따라 자동으로 copy 또는 멀티파트 copy를 선택하므로 사용자는 copy 의 파일 크기를 신경쓰지 않아도 됩니다.

- **방법 원형**

```java
// 파일 업로드
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

- **매개변수 설명**

| 매개변수 이름            | 매개변수 설명     | 매개변수 유형          |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | 파일 복사 요청 | CopyObjectRequest |

Request 멤버 설명:

| 매개변수 이름                | 매개변수 설명                                                     | 유형   |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion    | 소스 Bucket Region . 기본값: 현재 clientconfig 의 region 과 일치하며, 통일 지역 복사를 표시합니다 | String |
| sourceBucketName      | 소스 Bucket 이름, bucket의 명명 규칙은 {name}-{appid} 입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다 | String |
| sourceKey             | 소스 객체 키, 객체 키(Key)이며, 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | String |
| sourceVersionId       | 소스 파일 version id(버전 관리를 활성화한 소스 Bucket에 적용). 기본값: 소스 파일의 현재 최신 버전 | String |
| destinationBucketName | 대상 Bucket 이름, bucket의 명명 규칙은 {name}-{appid} 입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다 | String |
| destinationKey        | 대상 객체 키, 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)를 참조하십시오 | String      |
| storageClass          | 복사한 대상 파일의 스토리지 클래스(표준, 저빈도, 니어 라인) 기본값: 표준   |String |

- **반환값**
  - 성공: Copy를 반환합니다. Copy 종료 여부를 조회할 수 있고, 업로드 종료를 동기화하여 대기할 수 있습니다.
  - 실패: 오류 발생(예: ID 인증 실패), 이상CosClientException 또는 CosServiceException을 throw합니다. 자세한 설명은 이상 유형 설명을 참조하십시오.
- **예시**

```java
// 복사해야 할 bucket region이며, 교차 지역 복사를 지원합니다
Region srcBucketRegion = new Region("ap-shanghai");
// 소스 bucket, bucket의 명명 규칙은 {name}-{appid} 입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String srcBucketName = "srcBucket-1251668577";
// 복사할 소스 파일입니다.
String srcKey = "aaa/bbb.txt";
// 대상 bucket, bucket의 명명 규칙은 {name}-{appid} 입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String destBucketName = "destBucket-1251668577";
// 복사할 대상 파일입니다.
String destKey = "ccc/ddd.txt";

// 소스 파일 정보의 획득에 사용되는 srcCOSClient 생성
COSClient srcCOSClient = new COSClient(cred, new ClientConfig(srcBucketRegion));
CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
    // 비동기화 결과 copy를 반환합니다. waitForCopyResult 대기와 copy 종료를 동기화하여 호출할 수 있고, 성공하는 경우 CopyResult를 반환하고 실패 시 이상을 throw합니다.
    CopyResult copyResult = copy.waitForCopyResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

## 권한 설정

COS 중의 권한은 SET/GET Object ACL 및 SET/GET Bucket ACL 을 통해 설정 및 획득을 진행합니다. 주요한 두 가지 유형은 AccessControlList 및 CannedAccessList 로 설정하고 획득합니다. object는 기본으로 bucket 권한 상속이며, 현재 COS 는 하나의 계정(appid)에 대해 1000개의 ACL 만 지원합니다. 따라서 개별 및 bucket 권한이 일치하지 않은 object 에 대해서만 ACL을 설정하여 권한 수량이 임계값을 초과하지 않도록 권장합니다. 무제한 acl을 지원하는 기능은 현재 개발 중입니다.

### AccessControlList

사용자 지정 접근 관리 정책으로서, 사용자의 정책 관리 설정에 사용됩니다.

AccessControlList 유형 멤버

| 멤버         | 설명                            | 유형     |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | 권한 부여가 필요한 모든 정보를 포함합니다            | 배열     |
| owner          | Object 또는 Owner의 보유자를 의미합니다 | Owner 유형 |

Grant 유형 멤버

| 멤버 이름         | 설명                            | 유형     |
| ---------- | ------------------------------------------ | ---------- |
| 멤버    | 권한 부여를 받는 사용의 ID 정보                         | 유형    |
| permission | 권한 부여를 받는 권한 정보(예: 읽기 가능, 쓰기 가능, 읽기/쓰기 가능) | Permission |

Owner 유형 멤버

| 멤버      | 설명                           | 유형   |
| ----------- | ------------------------------ | ------ |
| id          | 보유자의 ID 정보               | String |
| displayname | 보유자의 이름(현재는 ID 와 같음) | String |

- **예시**

```java
// 권한 정보 중 ID 정보는 형식 요구가 있으며, 루트 계정과 서브 계정에 대한 규범 형식은 아래와 같습니다.
// 아래의 root_uin 및 sub_uin 는 모두 반드시 유효한 QQ 번호가 있어야 합니다
// 루트 계정 qcs::cam::uin/<root_uin>:uin/<root_uin> 은 루트 계정 root_uin 을 부여한 이 사용자를 의미합니다(즉, 앞뒤에 입력한 uin이 같음)
//  예: qcs::cam::uin/2779643970:uin/2779643970
// 서브 계정 qcs::cam::uin/<root_uin>:uin/<sub_uin>은 root_uin 서브 계정을 부여한 sub_uin 이 사용자를 의미합니다
//  예: qcs::cam::uin/2779643970:uin/73001122  

AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
// owner 의 정보를 설정하며, owner 는 루트 계정여야만 합니다
owner.setId("qcs::cam::uin/2779643970:uin/2779643970");
acl.setOwner(owner);

// 루트 계정 73410000에 읽기/쓰기 가능 권한을 부여합니다
UinGrantee uinGrantee1 = new UinGrantee("qcs::cam::uin/73410000:uin/73410000");
acl.grantPermission(uinGrantee1, Permission.FullControl);
// 2779643970의 서브 계정 72300000에 읽기 가능 권한을 부여합니다
UinGrantee uinGrantee2 = new UinGrantee("qcs::cam::uin/2779643970:uin/72300000");
acl.grantPermission(uinGrantee2, Permission.Read);
// 2779643970의 서브 계정 7234444에 쓰기 가능 권한을 부여합니다
UinGrantee uinGrantee3 = new UinGrantee("qcs::cam::uin/7234444:uin/7234444");
acl.grantPermission(uinGrantee3, Permission.Write);

// object의 acl 설정
cosClient.setObjectAcl(bucket, key, acl);

```

### CannedAccessControlList

CannedAccessControlList는 사전 설정된 정책을 의미하며, 모든 사람을 대상으로 합니다. 하나의 열거 유형으로 열거값은 아래와 같이 나타냅니다.

| 열거값          | 설명                                             |
| --------------- | ------------------------------------------------ |
| Private         | 비공개 읽기/쓰기( owner 만 읽기 쓰기 가능)                  |
| PublicRead      | 공개 읽기 및 비공개 쓰기( owner은 읽기/쓰기 가능, 다른 사용자는 읽기 가능) |
| PublicReadWrite | 공개 읽기/쓰기(전체 읽기/쓰기 가능)                   |

### 클라이언트 암호화

Java sdk 는 클라이언트 암호화를 지원하고, 파일을 암호화한 후 업로드를 진행하며 다운로드 시 암호 해독을 진행합니다. 클라이언트 암호화는 대칭 AES 및 비대칭 RSA 암호화를 지원합니다.
여기서 대칭과 비대칭은 단지 매번 생성되는 임의의 키를 암호화하는 데만 사용되며, 파일 데이터의 암호화는 항상 AES256 대칭 암호화를 사용합니다.
클라이언트 암호화는 민감한 데이터를 저장하는 사용자에게 적용되며 클라이언트 암호화는 부분적으로 업로드 속도에 영향을 미칠 수 있습니다. SDK 내부는 멀티파트 업로드에 대해 직렬 방식으로 업로드를 진행합니다.

### 클라이언트 암호화 사용 전 준비 사항

클라이언트 암호화는 내부에서 AES256을 사용하여 데이터를 암호화하며, 기본으로 JDK6 - JDK8 의 초기 버전은 256 비트 암호화를 지원하지 않습니다. 작동 시 이상`java.security.InvalidKeyException: Illegal key size or default parameters`가 보고된 경우, oracle의 JCE 정책 제한이 없는 권한 파일을 보충하여, 이를 JRE의 환경에 배치해야 합니다. 현재 사용하는 JDK 버전에 따라 대응하는 파일을 각각 다운로드하고, 압축 해제하여 JAVA_HOME 하의 jre/lib/security 디렉터리에 저장하십시오.

1. [JDK6 JCE 보충 패키지](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html).
2. [JDK7 JCE 보충 패키지](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html).
3. [JDK8 JCE 보충 패키지](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html).

### 업로드 암호화 절차

1. 매번 하나의 파일 객체를 업로드하기 전, 임의로 대칭 암호화 키를 생성하고, 임의로 생성한 키는 사용자가 제공하는 대칭 또는 비대칭 키를 통해 암호화를 진행하며, 암호화 후의 결과 base64 코드는 객체의 메타 정보 중에 저장됩니다.
2. 파일 객체의 업로드를 진행할 경우 업로드 시 메모리에서 AES256 알고리즘을 사용하여 암호화합니다.

### 다운로드 암호 해독 과정

1. 파일 메타 정보 중의 필수 암호화 정보를 획득하고, base64 암호 해독 후 사용자 키를 사용하여 암호 해독을 진행하며, 그 시기 암호화 데이터 키를 얻습니다
2. 키를 사용하여 다운로드 입력 스트림에 대해 AES256 을 사용하여 암호 해독을 진행하고, 암호 해독 후의 파일 입력 스트림을 얻습니다.


- **예시**

예시 1: 대칭 AES256 를 사용하여 매번 생성된 임의의 키 샘플을 암호화하며, 완전한 예제 코드는 [클라이언트 대칭 키 암호화의 완전한 예시](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/SymmetricKeyEncryptionClientDemo.java)를 참조하십시오.

```java
// 사용자 ID 정보 초기화(secretId, secretKey)
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXXXXXXXXXX",
		"YYZZZZZZZZZZZZZZZZZ");
// bucket의 지역을 설정하며, COS 지역의 약칭은 https://www..com/document/product/436/6224를 참조하십시오
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));

// 파일에 저장된 키를 로딩하며, 존재하지 않을 경우에는 우선 buildAndSaveSymmetricKey를 사용하여 키를 생성하십시오
// buildAndSaveSymmetricKey();
SecretKey symKey = loadSymmetricAESKey();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(symKey);
// AES/GCM 모드를 사용하고 암호화 정보를 파일 메타 정보에 저장합니다.
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
		.withStorageMode(CryptoStorageMode.ObjectMetadata);

// 클라이언트 암호화 EncryptionClient를 생성합니다. COSEncryptionClient 는 COSClient 의 서브 유형으로서 모든 COSClient 를 지원하는 API를 모두 지원합니다.
// EncryptionClient 는 COSClient 업로드 및 다운로드 로직을 덮어쓰기 하며, 작업 내부는 암호화 작업을 실행하고 기타 조작 실행 로직은 COSClient 와 일치합니다
COSEncryptionClient cosEncryptionClient =
		new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
				new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
				cryptoConf);

// 파일 업로드
// 다음은 putObject 의 예시로서, 고급 API 업로드에 대해 TransferManager 생성 시 COSEncryptionClient 객체를 가져오기만 하면 됩니다
String bucketName = "mybucket-1251668577";
String key = "xxx/yyy/zzz.txt";
File localFile = new File("src/test/resources/plain.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
```

예시 2: 비대칭 RSA 를 사용하여 매번 생성된 임의의 키 샘플을 암호화하며, 완전한 예제 코드는 [클라이언트 비대칭 키 암호화의 완전한 예시](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/AsymmetricKeyEncryptionClientDemo.java)를 참조하십시오.

```java
// 사용자 ID 정보 초기화(secretId, secretKey)
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXXXXXXXXXXXXXX",
		"YYZZZZZZZZZZZZZZZZZZ");
// bucket의 지역을 설정하며, COS 지역의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참조하십시오
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));


// 파일에 저장된 키를 로딩하며, 존재하지 않을 경우에는 우선 buildAndSaveAsymKeyPair 를 사용하여 키를 생성하십시오
buildAndSaveAsymKeyPair();
KeyPair asymKeyPair = loadAsymKeyPair();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(asymKeyPair);
// AES/GCM모드를 사용하고 암호화 정보를 파일 메타 정보에 저장합니다.
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
		.withStorageMode(CryptoStorageMode.ObjectMetadata);

// 클라이언트 암호화 EncryptionClient를 생성합니다. COSEncryptionClient는 COSClient의 서브 유형으로서 모든 COSClient를 지원하는 API를 모두 지원합니다.
// EncryptionClient는 COSClient 업로드 및 다운로드 로직을 덮어쓰기 하며, 작업 내부는 암호화 작업을 실행하고 기타 조작 실행 로직은 COSClient와 일치합니다
COSEncryptionClient cosEncryptionClient =
		new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
				new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
				cryptoConf);

// 파일 업로드
// 다음은 putObject 예시로서, 고급 API 업로드에 대해 TransferManager 생성 시 COSEncryptionClient 객체를 가져오기만 하면 됩니다
String bucketName = "mybucket-1251668577";
String key = "xxx/yyy/zzz.txt";
File localFile = new File("src/test/resources/plain.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
```

## 비정상 설명

SDK 실패 시, throw하는 이상은 RuntimeExcpetion이며, 현재 SDK에서 흔히 볼 수 있는이상에는 CosClientException, CosServiceException 및 IllegalArgumentException 등이 있습니다.

### CosClientException

클라이언트 이상, 클라이언트의 원인으로 서버와 상호 작용을 완료할 수 없어 초래된 실패를 가리킵니다. 예를 들어 클라이언트가 서버에 연결할 수 없거나 서버가 반환하는 데이터를 해석할 수 없거나 로컬 파일 읽기에 IO 이상이 발생하는 등 현상과 같습니다. CosClientException 은 RuntimeException으로부터 통합되며, 사용자 지정의 멤버 변수가 없고, 사용 방법은 RuntimeException와 같습니다.

### CosServiceException

CosServiceException 서비스 이상, 상호 작용이 정상적으로 완료되었지만 작업이 실패한 시나리오를 가리킵니다. 예를 들어 클라이언트가 존재하지 않는 Bucket에 접근하거나 존재하지 않는 파일을 삭제하거나 어느 작업을 할 권한이 없거나 서버 고장 등과 같습니다. CosServiceException는 서버가 반환한 상태 코드, requestid, 오류 명세 등을 포함합니다. 이상 현상을 캡처한 뒤, 전체 이상 현상을 프린트하길 권장합니다. 다음은 이상 멤버 변수에 대한 설명입니다.

| Request 멤버 | 설명                                                         | 유형      |
| ------------ | ------------------------------------------------------------ | --------- |
| requestId    | 요청 ID, 요청을 표시하는 데 사용되며, 문제 해결에 있어 아주 중요한 부분입니다| String    |
| traceId      | 문제 해결 보조 ID,                                          | String    |
| statusCode   | response의 status 상태 코드,  4xx 란 요청이 클라이언트로 인해 요청이 실패패하고, 5xx 는 서버 이상으로 인해 실패한 것을 의미합니다. [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오 | String    |
| errorType    | 열거 유형, 이상의 종류를 표시하고, 각각 Client, Service, Unknown으로 분류됩니다    | ErrorType |
| errorCode    | 요청 실패 시, body가 반환한 Error Code입니다 [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오 | String    |
| errorMessage | 요청 실패 시  body가 반환한 Error Message입니다  [COS 오류 정보](https://cloud.tencent.com/document/product/436/7730)를 참조하십시오 | String    |

## FAQ

### SDK 를 가져오기 하여 실행한 후, java.lang.NoSuchMethodError 의 이상이 발생했습니다. 그 이유는 무엇입니까?

일반적인 원인은 JAR 패키지 충돌이 발생했기 때문입니다. 예를 들어 사용자 프로젝트 중 HTTP의 JAR 패키지 버전에 A방법이 없지만 SDK가 의존하는 JAR 패키지에는 A 방법이 있습니다. 이때 실행하면 로딩 순서에 문제가 생겨, 사용자 프로젝트의 HTTP 라이브러리가 로딩되고 실행 시 NoSuchMethodError 의 이상을 throw합니다. 해결 방법: 이미 포함된 프로젝트에서 NoSuchMethodError 를 발생시킨 패키지의 버전 및 SDK 중 pom.xml의 해당 라이브러리의 버전을 일치하게 수정합니다.

### SDK 업로드 속도가 느리고, 로그에 자주 IOException이 인쇄됩니다. 그 이유는 무엇입니까?

원인 및 해결 방법:
 a. 우선 공중망을 통해 COS에 접근 여부를 확인하고, 현재 동일한 지역 CVM이 COS에 접근할 때 사설망을 통하는지 확인합니다(사설망 도메인 이름의 IP 는 10, 100, 169 IP 주소 범위). 관련 COS 도메인 이름은 [COS 가용 영역](https://cloud.tencent.com/document/product/436/6224)을 참조하십시오. 공중망을 통하는 경우, 아웃바운드 대역폭이 작은지 또는 다른 응용프로그램이 대역폭 리소스를 점용하고 있는지 확인하십시오.
 b. 생산 환경 중의 로그 수준이 debug가 아닌지 확인해야 하며 INFO 로그 사용을 권장합니다. log4j 의 로그 구성은 [log4j 로그 구성 템플릿](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/resources/log4j.properties)을 참조하십시오.
 c. 현재 간편 업로드 속도는 최대 10MB일 수 있으며, 고급 API는 32 동시 발생의 경우 속도는 60MB까지 가능합니다. 만약 속도가 두개 값보다 훨씬 낮으면 a 및 b를 참조하십시오.
 d. warn 로그가 IOException를 인쇄할 경우 무시할 수 있습니다. SDK 는 재시도를 진행하고 여러 번 재시도한 후에도 여전히 실패하면 IOException 에 인쇄합니다. IOException 의 발생원인은 네트워크 속도가 너무 느린 것입니다. 원인은 a 및 b를 참조하십시오.

### SDK 는 어떻게 디렉터리를 생성합니까?

COS의 파일 및 디렉터리는 모두 객체이며, 디렉터리는 “/”로 끝나는 객체일 뿐입니다. 파일 생성 시, 디렉터리를 생성할 필요가 없습니다. 객체 키를 xxx/yyy/zzz.txt로 하는 파일을 생성할 경우, key를 xxx/yyy/zzz.txt로 설정하기만 하면 되고, xxx/yyy 객체를 생성할 필요가 없습니다. 콘솔에서 표시될 때, “/”로 구분하고 디렉터리의 레이어 효과를 표시합니다. 하지만 이러한 디렉터리 객체는 존재하지 않습니다. 디렉터리 객체를 생성하려면 아래의 예제 코드를 사용할 수 있습니다.

```java
String bucketName = "mybucket-125166000";=
String key = "xxx/yyy/";
// 디렉터리 객체는 /로 끝나는 비어있는 파일이며, 길이가 0인 byte 스트림을 업로드합니다
InputStream input = new ByteArrayInputStream(new byte[0]);
ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setContentLength(0);

PutObjectRequest putObjectRequest =
new PutObjectRequest(bucketName, key, input, objectMetadata);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### SDK 는 어떻게 HTTPS를 사용합니까?

SDK 중 관련 구성은 모두 ClientConfig 유형에 통일적으로 배치되며, COSClient 생성 시 HTTPS 사용을 구성할 수 있습니다. 예제 코드는 아래와 같습니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 bucket의 지역을 설정하며, COS 지역의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참조하십시오
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 사용 https 구성
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3 COS 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
```

### SDK 는 어떻게 프록시를 사용합니까?

프록시를 사용하여 COS에 접근해야 하는 사용자의 경우 ClientConfig 유형에서 프록시 IP (또는 도메인 이름) 및 포트 사용을 구성할 수 있습니다. 예제 코드는 아래와 같습니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 bucket의 지역을 설정하며, COS 지역의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참조하십시오
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 프록시 사용 구성(IP 및 포트를 동시에 설정해야 함)
// 프록시 IP 설정(도메인 이름 가져오기도 가능)
clientConfig.setHttpProxyIp("192.168.2.3");
// 프록시 포트 구성
clientConfig.setHttpProxyPort(8080);
// 3 COS 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
```
