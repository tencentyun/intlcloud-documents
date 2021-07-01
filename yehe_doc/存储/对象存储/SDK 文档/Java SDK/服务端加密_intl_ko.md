## 소개


본 문서에서는 서버 암호화 작업에 대한 API 개요 및 SDK 예시 코드를 제공합니다.


| API                                                          | 작업명         | 작업 설명                       |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33459) | 버킷의 암호화 설정 | 지정 버킷의 기본 암호화 설정 |
| [GET Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33460) | 버킷의 암호화 조회 | 지정 버킷의 기본 암호화 설정 조회 |
| [DELETE Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33461) | 버킷의 암호화 삭제 | 지정 버킷의 기본 암호화 설정 삭제 |



### COS에서 호스팅하는 암호화 키를 사용한 서버 암호화(SSE-COS)로 데이터 보호

#### 기능 설명

Tencent Cloud COS에서 마스터 키를 호스팅하고 데이터를 관리합니다. COS는 데이터센터에 데이터를 쓸 때 자동으로 암호화하며, 해당 데이터 사용 시 자동으로 암호화를 해제합니다. 현재 COS의 마스터 키를 사용한 AES-256 데이터 암호화를 지원합니다.


#### 예시 코드

SDK는 `setServerSideEncryption`과 `setMetadata`를 호출하는 등의 방법으로 작업을 실행하며, 예시는 다음과 같습니다.


```java
 // 사용자의 개인 정보(secretId, secretKey) 초기화
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
 COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
 // bucket의 리전 설정, COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참조
 ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);
// bucket 이름에는 반드시 appid가 포함됨
String bucketName = "examplebucket-1250000000";

String key = "doc/exampleobject.txt";
File localFile = new File("test.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// 암호화 알고리즘을 AES256으로 설정
objectMetadata.setServerSideEncryption(SSEAlgorithm.AES256.getAlgorithm());
putObjectRequest.setMetadata(objectMetadata);
try {
    PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
    // putobjectResult는 파일의 etag를 반환하며, 해당 md5 값은 s3 semantics에 따르는 것으로 객체의 md5가 아니고 유일한 표시임
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
// 클라이언트 종료
cosclient.shutdown();
```

### KMS에서 호스팅하는 암호화 키를 사용한 서버 암호화(SSE-KMS)로 데이터 보호


#### 기능 설명
Tencent Cloud의 키 관리 시스템인 KMS에서 키의 서버 암호화 방식을 호스팅하며, 기본 키 사용 또는 자체구축 키 사용을 선택할 수 있습니다. 키 정보에 대한 자세한 내용은 [KMS 키 생성](https://intl.cloud.tencent.com/document/product/1030/31971)을 참조하고, SSE-KMS에 대한 자세한 정보는 [서버 암호화 개요: SSE-KMS](https://intl.cloud.tencent.com/document/product/436/18145)를 참조하십시오.

#### 예시 코드

예시1: KMS를 사용하여 간편 업로드 객체 암호화

```java
COSCredentials cred = new BasicCOSCredentials("SECRET_ID", "SECRET_KEY");
// 2. bucket의 리전 설정, COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참조
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// https 요청 사용 설정
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);
// bucket 이름에는 반드시 appid가 포함됨
String bucketName = "examplebucket-1250000000";

String key = "doc/exampleobject.txt";
File localFile = new File("/test.log");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
String kmsKeyId = "your-kms-key-id";
String encryptionContext = Base64.encodeAsString("{\"Ssekmstest\":\"Ssekmstest\"}".getBytes());
SSECOSKeyManagementParams ssecosKeyManagementParams = new SSECOSKeyManagementParams(kmsKeyId, encryptionContext);
putObjectRequest.setSSECOSKeyManagementParams(ssecosKeyManagementParams);
// 서버 암호화 시나리오에서 반환되는 etag는 파일의 md5를 의미하지 않으므로 클라이언트의 md5 검증을 삭제해야 함
// 필요한 경우 crc64를 획득하여 자체 검증 가능
System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
try {
    PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
    // putobjectResult는 파일의 etag 반환
    String etag = putObjectResult.getETag();
    String crc64 = putObjectResult.getCrc64Ecma();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// 클라이언트 종료
cosclient.shutdown();
```

예시2: KMS를 사용하여 멀티파트 업로드 객체 암호화

```java
COSCredentials cred = new BasicCOSCredentials("SECRET_ID", "SECRET_KEY");
// 2. bucket의 리전 설정, COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참조
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// https 요청 사용 설정
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);
// bucket 이름에는 반드시 appid가 포함됨
String bucketName = "examplebucket-1250000000";

String key = "doc/exampleobject.txt";
String kmsKeyId = "your-kms-key-id";
String encryptionContext = Base64.encodeAsString("{\"Ssekmstest\":\"Ssekmstest\"}".getBytes());
InitiateMultipartUploadRequest initiateMultipartUploadRequest = new InitiateMultipartUploadRequest(bucketName, key);
SSECOSKeyManagementParams ssecosKeyManagementParams = new SSECOSKeyManagementParams(kmsKeyId, encryptionContext);
// 서버 암호화 시나리오에서 반환되는 etag는 파일의 md5를 의미하지 않으므로 클라이언트의 md5 검증을 삭제해야 함
// 필요한 경우 crc64를 획득하여 자체 검증 가능
System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
initiateMultipartUploadRequest.setSSECOSKeyManagementParams(ssecosKeyManagementParams);
try {
    InitiateMultipartUploadResult initiateMultipartUploadResult = cosclient.initiateMultipartUpload(initiateMultipartUploadRequest);
    List<PartETag> partETags = new LinkedList<>();
    for (int i = 0; i < 2; i++) {
        byte data[] = new byte[1024 * 1024];
        UploadPartRequest uploadPartRequest = new UploadPartRequest();
        uploadPartRequest.setBucketName(bucketName);
        uploadPartRequest.setKey(key);
        uploadPartRequest.setUploadId(initiateMultipartUploadResult.getUploadId());
        // 파트 데이터의 원본 입력 스트림 설정
        uploadPartRequest.setInputStream(new ByteArrayInputStream(data));
        // 파트 길이 설정
        uploadPartRequest.setPartSize(data.length); // 데이터 길이 설정
        uploadPartRequest.setPartNumber(i + 1);     // 업로드할 part 번호를 10으로 가정

        UploadPartResult uploadPartResult = cosclient.uploadPart(uploadPartRequest);
        PartETag partETag = uploadPartResult.getPartETag();
        partETags.add(partETag);
    }
    CompleteMultipartUploadRequest completeMultipartUploadRequest =
    new CompleteMultipartUploadRequest(bucketName, key, initiateMultipartUploadResult.getUploadId(), partETags);
    CompleteMultipartUploadResult completeResult =
    cosclient.completeMultipartUpload(completeMultipartUploadRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// 클라이언트 종료
cosclient.shutdown();
```

예시3: KMS를 사용하여 복사해 생성한 타깃 객체 암호화

```java
COSCredentials cred = new BasicCOSCredentials("SECRET_ID", "SECRET_KEY");
// 2. bucket의 리전 설정, COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참조
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// https 요청 사용 설정
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);
// bucket 이름에는 반드시 appid가 포함됨

String kmsKeyId = "your-kms-key-id";
String encryptionContext = Base64.encodeAsString("{\"Ssekmstest\":\"Ssekmstest\"}".getBytes());

// 복사할 bucket region, 리전 간 복사 지원
Region srcBucketRegion = new Region("ap-guangzhou");
// 원본 bucket, bucket 이름에는 반드시 appid가 포함됨
String srcBucketName = "examplebucket-1250000000";
// 복사할 원본 파일
String srcKey = "doc/exampleobject.txt";
// 타깃 bucket, bucket 이름에는 반드시 appid가 포함됨
String destBucketName = "examplebucket-1250000000";
// 복사할 타깃 파일
String destKey = "folder/exampleobject.txt";

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
                                                            srcKey, destBucketName, destKey);
copyObjectRequest.setSSECOSKeyManagementParams(new SSECOSKeyManagementParams(kmsKeyId, encryptionContext));
try {
    CopyObjectResult copyObjectResult = cosclient.copyObject(copyObjectRequest);
    String crc64 = copyObjectResult.getCrc64Ecma();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// 클라이언트 종료
cosclient.shutdown();
```

### 고객이 제공한 암호화 키를 사용한 서버 암호화(SSE-C)로 데이터 보호

#### 기능 설명

암호화 키를 사용자가 제공하며, 사용자가 객체 업로드 시 COS가 사용자가 제공한 암호화 키를 사용하여 사용자 데이터에 대해 AES-256 암호화를 진행합니다. SDK는 setHttpProtocol` 및 `setSSECustomerKey` 호출 등의 방법으로 작업을 실행합니다.

> !
>- 해당 암호화로 실행되는 서비스는 HTTPS를 사용해 요청해야 합니다.
>- base64EncodedKey: 사용자가 제공하는 서버 암호화 키의 Base64 인코딩
>- 업로드하는 원본 파일에서 해당 방법을 호출하는 경우 GET(다운로드), HEAD(조회) 사용 시, 원본 객체를 작업할 때도 해당 방법을 호출합니다.


#### 예시 코드

```java
 // 사용자의 개인 정보(secretId, secretKey) 초기화
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
 COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
 // bucket의 리전 설정, COS 리전의 약칭은 https://www.qcloud.com/document/product/436/6224 참조
 ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// https 프로토콜 요청
clientConfig.setHttpProtocol(HttpProtocol.https);
// cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);
// bucket 이름에는 반드시 appid가 포함됨
String bucketName = "examplebucket-1250000000";

String key = "doc/exampleobject.txt";
File localFile = new File("test.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
String base64EncodedKey = "MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=";
// sseCustomerKey: base64 인코딩 키
SSECustomerKey sseCustomerKey = new SSECustomerKey(base64EncodedKey);
putObjectRequest.setSSECustomerKey(sseCustomerKey);
ObjectMetadata objectMetadata = cosclient.getObjectMetadata();
objectMetadata.getHttpExpiresDate();
try {
PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
// putobjectResult는 파일의 etag를 반환하며, 해당 md5 값은 s3 semantics에 따르는 것으로 객체의 md5가 아니고 유일한 표시임
String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
e.printStackTrace();
} catch (CosClientException e) {
e.printStackTrace();
}
// 클라이언트 종료
cosclient.shutdown();
```
