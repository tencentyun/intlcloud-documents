## Overview

The Java SDK supports client-side encryption. Files can be encrypted before the upload and decrypted during the download. Client-side encryption is suitable for users who store sensitive data.

The following two types of keys are supported for client-side encryption:
- KMS managed keys: You can provide the ID of your KMS CMK to the SDK. To use this type of keys, the KMS service needs to be activated. For more information, see [Key Management Service](https://www.tencentcloud.com/document/product/1030).
- Customer managed keys: This type of keys (AES symmetric or RSA asymmetric) is provided and managed by you.
>? Symmetric or asymmetric keys mentioned above are to encrypt the randomly generated keys only. Note that files are always encrypted symmetrically using AES-256.
>

## Limits

- User data will not be uploaded to COS unless it is encrypted.
- Client-side encryption may affect the upload speed.
- The SDK uses the serial mode for multipart upload.

## Considerations

The client uses AES-256 internally to encrypt data. By default, earlier versions of JDK6-JDK8 do not support 256-bit encryption. If run, the exception `java.security.InvalidKeyException: Illegal key size or default parameters` will be reported. In this case, we need to supplement Oracle's JCE unlimited strength jurisdiction policy files and deploy them in the JRE environment. Please download the corresponding files according to the JDK version used, and decompress and save them in the `jre/lib/security` directory under `JAVA_HOME`.

- [JDK6 JCE supplementary package](http://www.oracle.com/technetwork/java/javase/downloads/jce-6-download-429243.html)
- [JDK7 JCE supplementary package](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)
- [JDK8 JCE supplementary package](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

## Encryption upon Upload

1. Before each object upload, a symmetric key will be generated randomly and encrypted with the KMS/customer managed key. The encrypted result will then be Base64-encoded and stored in the object metadata.
2. During the upload, the file is encrypted in memory using the AES256 algorithm.

## Decryption upon Download

1. Get the necessary encryption information from the metadata of the file, Base64-decode it, and then decrypt it using the KMS or customer managed key to get the encryption key at upload.
2. Use the resulting key to decrypt the downloaded input stream using AES256.

## Sample Request

#### Sample 1
The following sample uses Tencent Cloud′s KMS service for client-side encryption. For the complete sample code, see [Complete Sample of Client-Side Encryption using KMS](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/KMSEncryptionClientDemo.java).

[//]: # (.cssg-snippet-put-object-cse-c-kms)

```java
// Initialize user authentication information (`secretId` and `secretKey`).
// Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
String secretId = System.getenv("secretId"); // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
String secretKey = System.getenv("secretKey"); // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Set the COS region. For regions and their abbreviations, visit https://intl.cloud.tencent.com/zh/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));
// You are advised to initiate requests over HTTPS to avoid decryption failure caused by altered request headers.
clientConfig.setHttpProtocol(HttpProtocol.https);

// CMK of the KMS service
String cmk = "XXXXXXX";
//// The region needs to be configured separately if the KMS region is different from the region of the COS bucket.
//String kmsRegion = "XXXXX";

// Initiate KMS encryption materials.
KMSEncryptionMaterials encryptionMaterials = new KMSEncryptionMaterials(cmk);
// Use the AES/GCM mode and store the encrypted information in the file metadata.
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
        .withStorageMode(CryptoStorageMode.ObjectMetadata);

//// Specify the KMS region in the encryption configuration if it is different from the region of the COS bucket.
//cryptoConf.setKmsRegion(kmsRegion);

//// You can configure a description for the KMS CMK if needed.
// encryptionMaterials.addDescription("yourDescKey", "yourDescValue");

// Generate an encryption client (EncryptionClient), more specifically COSEncryptionClient. It is a subclass of COSClient, and allows for the use of all APIs supported by COSClient.
// COSEncryptionClient overwrites the COSClient for upload and download logic, and additionally performs encryption. The other operations, however, use the same logic as that of the COSClient.
COSEncryptionClient cosEncryptionClient =
        new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
                new KMSEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
                cryptoConf);

// Upload the file
// Here is an example of PUT Object. For the advanced upload API, all you need to do is pass in the COSEncryptionClient object when generating TransferManager.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File("localFilePath");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
cosEncryptionClient.shutdown();
```

#### Sample 2
The following sample uses symmetric AES-256 to encrypt the randomly generated keys. For the complete sample code, see [Complete Sample of Client-Side Symmetric Encryption](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/SymmetricKeyEncryptionClientDemo.java).

[//]: # (.cssg-snippet-put-object-cse-c-aes)

```java
// Initialize user authentication information (`secretId` and `secretKey`).
// Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
String secretId = System.getenv("secretId"); // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
String secretKey = System.getenv("secretKey"); // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Set the COS region. For regions and their abbreviations, visit https://intl.cloud.tencent.com/zh/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));

// Generate a symmetric key to save as file metadata.
KeyGenerator symKeyGenerator = KeyGenerator.getInstance("AES");
symKeyGenerator.init(256);
SecretKey symKey = symKeyGenerator.generateKey();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(symKey);
// Use AES/GCM mode and store the encrypted information in the file metadata.
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
        .withStorageMode(CryptoStorageMode.ObjectMetadata);

// Generate an encryption client (EncryptionClient), more specifically, COSEncryptionClient. It is a subclass of COSClient, and allows for the use of all APIs supported by COSClient.
// COSEncryptionClient overwrites the COSClient for upload and download logic, and additionally performs encryption. The other operations, however, use the same logic as that of the COSClient.
COSEncryptionClient cosEncryptionClient =
        new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
                new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
                cryptoConf);

// Upload the file
// Here is an example of PUT Object. For the advanced upload API, all you need to do is pass in the COSEncryptionClient object when generating TransferManager.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
cosEncryptionClient.shutdown();
```

#### Sample 3
The following sample uses asymmetric RSA to encrypt the randomly generated keys. For the complete sample code, see [Complete Sample of Client-Side Asymmetric Encryption](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/src/main/java/com/qcloud/cos/demo/AsymmetricKeyEncryptionClientDemo.java).

[//]: # (.cssg-snippet-put-object-cse-c-rsa)
```java
// Initialize user authentication information (`secretId` and `secretKey`).
// Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
String secretId = System.getenv("secretId"); // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
String secretKey = System.getenv("secretKey"); // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// Set the COS region. For regions and their abbreviations, visit https://www.tencentcloud.com/document/product/436/6224.
ClientConfig clientConfig = new ClientConfig(new Region("COS_REGION"));

// Generate an asymmetric key.
KeyPairGenerator keyGenerator = KeyPairGenerator.getInstance("RSA");
SecureRandom srand = new SecureRandom();
keyGenerator.initialize(1024, srand);
KeyPair asymKeyPair = keyGenerator.generateKeyPair();

EncryptionMaterials encryptionMaterials = new EncryptionMaterials(asymKeyPair);
// Use AES/GCM mode and store the encrypted information in the file metadata.
CryptoConfiguration cryptoConf = new CryptoConfiguration(CryptoMode.AuthenticatedEncryption)
        .withStorageMode(CryptoStorageMode.ObjectMetadata);

// Generate an encryption client (EncryptionClient), more specifically COSEncryptionClient. It is a subclass of COSClient, and allows for the use of all APIs supported by COSClient.
// COSEncryptionClient overwrites the COSClient for upload and download logic, and additionally performs encryption. The other operations, however, use the same logic as that of the COSClient.
COSEncryptionClient cosEncryptionClient =
        new COSEncryptionClient(new COSStaticCredentialsProvider(cred),
                new StaticEncryptionMaterialsProvider(encryptionMaterials), clientConfig,
                cryptoConf);

// Upload the file
// Here is an example of putObject. For advanced API upload, use the COSEncryptionClient object when generating TransferManager.
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
File localFile = new File(localFilePath);
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
cosEncryptionClient.putObject(putObjectRequest);
cosEncryptionClient.shutdown();
```
