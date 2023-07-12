## 소개

본문은 객체를 업로드할 때 서버측 암호화를 활성화하는 방법을 설명합니다. 서버측 암호화에 사용할 수 있는 키는 다음 세 종류:

* COS 호스팅 암호화 키
* 고객 제공 암호화 키
* KMS 호스팅 암호화 키

### COS에서 호스팅하는 암호화 키를 사용한 서버 암호화(SSE-COS)로 데이터 보호

Tencent Cloud COS에서 마스터 키를 호스팅하고 데이터를 관리합니다. COS는 데이터센터에 데이터를 쓸 때 자동으로 암호화하며, 해당 데이터 사용 시 자동으로 복호화합니다. 현재 COS의 마스터 키를 사용한 AES-256 데이터 암호화를 지원합니다.

```java
// 고급 인터페이스를 사용하려면 먼저 이 프로세스에 TransferManager 인스턴스가 있는지 확인하고 없다면 생성합니다.
// 자세한 코드는 객체 업로드 참고: 고급 인터페이스 -> 예시 코드: TransferManager 생성
TransferManager transferManager = createTransferManager();

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 본 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오.
String key = "exampleobject";
// 로컬 파일 경로
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

ObjectMetadata objectMetadata = new ObjectMetadata();
// 암호화 알고리즘을 AES256으로 설정
objectMetadata.setServerSideEncryption(SSEAlgorithm.AES256.getAlgorithm());
putObjectRequest.setMetadata(objectMetadata);

// 서버 암호화 시나리오에서 반환되는 etag는 파일의 md5를 의미하지 않으므로 클라이언트의 md5 인증을 삭제해야 함
// 필요 시 crc64를 획득하여 자체 검증 가능합니다.
System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");

try{
    // 고급 인터페이스는 비동기화 결과 Upload를 반환합니다.
    // waitForUploadResult 메소드를 동기화 호출하여 업로드 완료를 대기할 수 있습니다. 성공 시 UploadResult를 반환하고 실패 시 이상 경고가 발생합니다.
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// 프로세스가 더 이상 transferManager 인스턴스를 사용하지 않음을 확인한 후 비활성화합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> TransferManager 비활성화
shutdownTransferManger(transferManager);
```

### 고객이 제공한 암호화 키를 사용한 서버 암호화(SSE-C)로 데이터 보호

암호화 키는 사용자가 직접 제공하는 것이며, 객체를 업로드할 때 COS는 사용자가 제공한 암호화 키로 사용자의 데이터에 AES-256 암호화를 적용합니다.

> !
>- 해당 암호화로 실행되는 서비스는 HTTPS를 사용해 요청해야 합니다.
>- 숫자, 문자 및 부호의 조합인 32바이트 문자열을 키로 제공해야 하며 중국어는 지원되지 않습니다.
>- 파일이 업로드될 때 키 암호화를 설정한 경우 GET(다운로드) 또는 HEAD(쿼리) 요청에 동일한 키를 포함해야 정상적으로 응답됩니다.

```java
// 고급 인터페이스를 사용하려면 먼저 이 프로세스에 TransferManager 인스턴스가 있는지 확인하고 없다면 생성합니다.
// 자세한 코드는 객체 업로드 참고: 고급 인터페이스 -> 예시 코드: TransferManager 생성
TransferManager transferManager = createTransferManager();

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 본 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오.
String key = "exampleobject";
// 로컬 파일 경로
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

String base64EncodedKey = "MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=";
// sseCustomerKey: base64 코드의 키
SSECustomerKey sseCustomerKey = new SSECustomerKey(base64EncodedKey);
putObjectRequest.setSSECustomerKey(sseCustomerKey);

// 서버 암호화 시나리오에서 반환되는 etag는 파일의 md5를 의미하지 않으므로 클라이언트의 md5 인증을 삭제해야 함
// 필요 시 crc64를 획득하여 자체 검증 가능합니다.
System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");

try{
    // 고급 인터페이스는 비동기화 결과 Upload를 반환합니다.
    // waitForUploadResult 메소드를 동기화 호출하여 업로드 완료를 대기할 수 있습니다. 성공 시 UploadResult를 반환하고 실패 시 이상 경고가 발생합니다.
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// 프로세스가 더 이상 transferManager 인스턴스를 사용하지 않음을 확인한 후 비활성화합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> TransferManager 비활성화
shutdownTransferManger(transferManager);
```

### KMS에서 호스팅하는 암호화 키를 사용한 서버 암호화(SSE-KMS)로 데이터 보호

SSE-KMS 암호화는 KMS가 키를 호스팅하여 관리하는 서버 암호화 방식입니다. KMS는 Tencent Cloud가 선보인 보안 관리형 서비스로서 3rd party가 인증하는 하드웨어 보안 모듈(HSM, Hardware Security Module)로 보안키를 생성하여 보호합니다. KMS로 보안키를 간편하게 생성하고 관리할 수 있어 다양한 애플리케이션과 작업에 필요한 보안키 관리가 편리할 뿐만 아니라 모니터링과 컴플라이언스 니즈를 충족할 수 있습니다. KMS 서비스 활성화 방법은 [서버 암호화 개요](https://intl.cloud.tencent.com/document/product/436/18145)를 참고하십시오.

```java
// 고급 인터페이스를 사용하려면 먼저 이 프로세스에 TransferManager 인스턴스가 있는지 확인하고 없다면 생성합니다.
// 자세한 코드는 객체 업로드 참고: 고급 인터페이스 -> 예시 코드: TransferManager 생성
TransferManager transferManager = createTransferManager();

// 버킷의 이름 생성 형식은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 본 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오.
String key = "exampleobject";
// 로컬 파일 경로
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

// KMS 마스터 키
String kmsKeyId = "your-kms-key-id";
String encryptionContext = Base64.encodeAsString("{\"Ssekmstest\":\"Ssekmstest\"}".getBytes());
SSECOSKeyManagementParams ssecosKeyManagementParams = new SSECOSKeyManagementParams(kmsKeyId, encryptionContext);
putObjectRequest.setSSECOSKeyManagementParams(ssecosKeyManagementParams);

// 서버 암호화 시나리오에서 반환되는 etag는 파일의 md5를 의미하지 않으므로 클라이언트의 md5 인증을 삭제해야 함
// 필요 시 crc64를 획득하여 자체 검증 가능합니다.
System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");

try{
    // 고급 인터페이스는 비동기화 결과 Upload를 반환합니다.
    // waitForUploadResult 메소드를 동기화 호출하여 업로드 완료를 대기할 수 있습니다. 성공 시 UploadResult를 반환하고 실패 시 이상 경고가 발생합니다.
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// 프로세스가 더 이상 transferManager 인스턴스를 사용하지 않음을 확인한 후 비활성화합니다.
// 상세 코드 참고 페이지: 고급 인터페이스 -> TransferManager 비활성화
shutdownTransferManger(transferManager);
```