## 개요

Java SDK는 클라이언트 암호화를 지원합니다. 파일을 암호화한 후 업로드하고, 다운로드 시 복호화하여 중요 데이터를 저장하는 클라이언트에 적합합니다.

클라이언트 암호화는 다음 두 가지 방식을 지원합니다.
- KMS 서비스 호스팅 키: KMS 서비스의 사용자 마스터 키 ID(CMK ID)를 SDK에 제공하기만 하면 됩니다. 이 방식을 사용하려면 KMS 서비스를 활성화해야 합니다. KMS 서비스 정보에 대한 자세한 내용은 [Tencent Cloud Key Management Service](https://intl.cloud.tencent.com/document/product/1030)를 참고하십시오.
- 사용자 보관 키: 사용자가 암호화 키를 제공하고 보관합니다. 대칭 AES 및 비대칭 RSA 암호화를 지원합니다.
>? 대칭과 비대칭은 매번 생성되는 임의 키를 암호화할 때만 사용하며, 파일 데이터 암호화에는 항상 AES256 대칭 암호화를 사용합니다.
>

## 주의 사항

- 사용자 데이터를 암호화하기 전에는 Tencent Cloud Cloud Object Storage(COS)에 업로드하지 않습니다.
- 클라이언트 암호화는 일부 업로드 속도를 소모합니다.
- SDK 내부의 멀티파트 업로드는 직렬 방식으로 업로드합니다.

## 준비 사항

클라이언트 암호화는 내부 데이터 암호화에 AES256을 사용합니다. 기본적으로 JDK6~JDK8 초기 버전은 256비트 암호화를 지원하지 않으며, 실행 시 `java.security.InvalidKeyException: Illegal key size or default parameters`와 같은 이상 경고가 뜹니다. 이 경우 정책적 제한이 없는 Oracle의 JCE 권한 파일을 JRE 환경에 배포해야 합니다. 현재 사용 중인 JDK 버전에 따라 해당하는 파일을 각각 다운로드하여 압축을 해제한 후 JAVA_HOME의 `jre/lib/security` 디렉터리에 저장하십시오.

- [JDK6 JCE 보충 패키지](https://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)
- [JDK7 JCE 보충 패키지](https://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
- [JDK8 JCE 보충 패키지](https://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

## 업로드 암호화 프로세스

1. 파일 객체를 업로드하기 전에 무작위로 대칭 암호화 키를 생성합니다. 무작위로 생성한 키는 KMS 서비스(또는 사용자가 제공한 키)를 통해 암호화되며, 암호화된 결과는 객체의 메타데이터에 base64로 인코딩되어 저장됩니다.
2. 파일 객체를 업로드합니다. 업로드 시 메모리에서 AES256 알고리즘을 사용해 암호화합니다.

## 다운로드 복호화 프로세스

1. 파일 메타데이터에서 암호화에 필요한 정보를 가져와 Base64로 디코딩 후 KMS 서비스(또는 사용자가 제공한 키)로 복호화하여 암호화된 데이터의 키를 얻습니다.
2. 키 쌍을 사용해 입력 스트림을 다운로드하고 AES256을 사용해 복호화하여 복호화된 파일 입력 스트림을 얻습니다.

## 요청 예시

#### 예시 1
Tencent Cloud KMS 서비스를 사용해 암호화하고, 암호화 클라이언트를 생성하는 예시입니다. 전체 예시 코드는 [KMS 암호화 클라이언트의 암호화 전체 예시](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/KMSEncryptionClientDemo.java)를 참고하십시오.

[//]: # (.cssg-snippet-put-object-cse-c-kms)

```java
// 사용자의 개인 정보(secretId, secretKey) 초기화
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 버킷 리전 설정, COS 리전의 약칭은 https://www..com/document/product/436/6224 참고
ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));
// 요청 헤더가 조작되어 데이터를 암호화하지 못하는 문제를 방지하기 위해, 요청 시 https 프로토콜만 사용할 것을 권장
clientConfig.setHttpProtocol(HttpProtocol.https);

// KMS 서비스의 마스터 키
String cmk = "XXXXXXX";
//// KMS 서비스 리전과 COS 버킷 리전이 동일하지 않은 경우 단독 설정 필요
//String kmsRegion = "XXXXX";

// KMS 암호화 자료 초기화
KMSEncryptionMaterials encryptionMaterials = new KMSEncryptionMaterials(cmk);
// AES/GCM 모드를 사용하여 암호화 정보를 파일 메타 정보에 저장
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
        .withStorageMode(CryptoStorageMode.ObjectMetadata);

//// KMS 서비스 리전과 COS 리전이 동일하지 않은 경우 암호화 설정에서 KMS 서비스 리전 지정
//cryptoConf.setKmsRegion(kmsRegion);

//// 필요한 경우 KMS 서비스의 cmk에 해당 설명 정보 설정 가능
// encryptionMaterials.addDescription("yourDescKey", "yourDescValue");

// 암호화된 클라이언트 EncryptionClient를 생성합니다. COSEncryptionClient는 COSClient의 서브 유형으로, COSClient가 지원하는 모든 인터페이스를 지원합니다.
// EncryptionClient는 COSClient의 업로드/다운로드 로직을 덮어쓰기 하며 내부적으로 암호화 작업을 실행합니다. 다른 작업 실행 로직은 COSClient와 동일합니다.
COSEncryptionClient cosEncryptionClient =
        new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
                new KMSEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
                cryptoConf);

// 파일 업로드
// putObject의 예시, 고급 API 업로드는 TransferManager 생성 시 COSEncryptionClient 객체를 전송할 때만 사용
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File("localFilePath");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
cosEncryptionClient.shutdown();
```

#### 예시 2
대칭 AES256을 사용하여 매번 생성되는 임의 키를 암호화하는 예시입니다. 전체 예시 코드는 [클라이언트 대칭 키 암호화 전체 예시](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/SymmetricKeyEncryptionClientDemo.java)를 참고하십시오.

[//]: # (.cssg-snippet-put-object-cse-c-aes)

```java
// 사용자의 개인 정보(secretId, secretKey) 초기화
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 버킷 리전 설정, COS 리전의 약칭은 https://www..com/document/product/436/6224 참고
ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));

// 대칭 키 생성, 생성된 대칭 키는 파일에 저장 가능
KeyGenerator symKeyGenerator = KeyGenerator.getInstance("AES");
symKeyGenerator.init(256);
SecretKey symKey = symKeyGenerator.generateKey();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(symKey);
// AES/GCM 모드를 사용하여 암호화 정보를 파일 메타데이터에 저장
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
        .withStorageMode(CryptoStorageMode.ObjectMetadata);

// 암호화된 클라이언트 EncryptionClient를 생성합니다. COSEncryptionClient는 COSClient의 서브 유형으로, COSClient가 지원하는 모든 인터페이스를 지원합니다.
// EncryptionClient는 COSClient의 업로드/다운로드 로직을 덮어쓰기 하며 내부적으로 암호화 작업을 실행합니다. 다른 작업 실행 로직은 COSClient와 동일합니다.
COSEncryptionClient cosEncryptionClient =
        new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
                new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
                cryptoConf);

// 파일 업로드
// putObject의 예시, 고급 API 업로드는 TransferManager 생성 시 COSEncryptionClient 객체를 전송할 때만 사용
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
cosEncryptionClient.shutdown();
```

#### 예시 3
비대칭 RSA를 사용하여 매번 생성되는 임의 키를 암호화하는 예시입니다. 전체 예시 코드는 [클라이언트 비대칭 키 암호화 전체 예시](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/AsymmetricKeyEncryptionClientDemo.java)를 참고하십시오.

[//]: # (.cssg-snippet-put-object-cse-c-rsa)
```java
// 사용자의 개인 정보(secretId, secretKey) 초기화
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 버킷 리전 설정, COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참고
ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));

// 비대칭 키 생성
KeyPairGenerator keyGenerator = KeyPairGenerator.getInstance("RSA");
SecureRandom srand = new SecureRandom();
keyGenerator.initialize(1024, srand);
KeyPair asymKeyPair = keyGenerator.generateKeyPair();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(asymKeyPair);
// AES/GCM 모드를 사용하여 암호화 정보를 파일 메타데이터에 저장
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
        .withStorageMode(CryptoStorageMode.ObjectMetadata);

// 암호화된 클라이언트 EncryptionClient를 생성합니다. COSEncryptionClient는 COSClient의 서브 유형으로, COSClient가 지원하는 모든 인터페이스를 지원합니다.
// EncryptionClient는 COSClient의 업로드/다운로드 로직을 덮어쓰기 하며 내부적으로 암호화 작업을 실행합니다. 다른 작업 실행 로직은 COSClient와 동일합니다.
COSEncryptionClient cosEncryptionClient =
        new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
                new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
                cryptoConf);

// 파일 업로드
// putObject의 예시, 고급 API 업로드는 TransferManager 생성 시 COSEncryptionClient 객체를 전송할 때만 사용
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
cosEncryptionClient.shutdown();
```
