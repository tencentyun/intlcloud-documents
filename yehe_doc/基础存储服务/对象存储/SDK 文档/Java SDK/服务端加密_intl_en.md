## Overview


This document provides an overview of APIs and SDK code samples related to server-side encryption.


| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33459) | Setting bucket encryption | Sets the default encryption configuration for a bucket |
| [GET Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33460) | Querying bucket encryption configuration | Queries the default encryption configuration of a bucket |
| [DELETE Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33461) | Deleting bucket encryption configuration | Deletes the default encryption configuration of a bucket |



### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

#### Feature description

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.


#### Sample code

You can call the `setServerSideEncryption`, `setMetadata`, and other methods in the SDK. The sample code is as follows:


```java
 // Initialize user authentication information (`secretId` and `secretKey`).
// Log in to the CAM console to check and manage the `SecretId` and `SecretKey` of your project.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
 COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
 // Set the bucket region. For abbreviations of COS regions, see https://cloud.tencent.com/document/product/436/6224
 ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain "appid".
String bucketName = "examplebucket-1250000000";

String key = "doc/exampleobject.txt";
File localFile = new File("test.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
ObjectMetadata objectMetadata = new ObjectMetadata();
// Set the encryption algorithm to AES-256.
objectMetadata.setServerSideEncryption(SSEAlgorithm.AES256.getAlgorithm());
putObjectRequest.setMetadata(objectMetadata);
try {
    PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
    // "putobjectResult" will return ETag, an MD5 checksum that uniquely identifies the object, and is different from the MD5 checksum of the object according to the semantics of S3.
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
// Shut down the client.
cosclient.shutdown();
```

### Using server-side encryption with KMS-managed encryption keys (SSE-KMS) to protect data


#### Feature description
SSE-KMS is server-side encryption with a key managed by Tencent Cloud Key Management System (KMS). You can use the default key or create a key. For more information about keys, please see [Creating a Key](https://intl.cloud.tencent.com/document/product/1030/31971). For more information about SSE-KMS, please see the **SSE-KMS Encryption** section in [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

#### Sample code

Sample 1: Using KMS encryption for objects uploaded with simple upload

```java
COSCredentials cred = new BasicCOSCredentials("SECRET_ID", "SECRET_KEY");
// 2. Set the bucket region. For abbreviations of COS regions, please see https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// Use the HTTPS protocol.
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain "appid".
String bucketName = "examplebucket-1250000000";

String key = "doc/exampleobject.txt";
File localFile = new File("/test.log");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
String kmsKeyId = "your-kms-key-id";
String encryptionContext = Base64.encodeAsString("{\"Ssekmstest\":\"Ssekmstest\"}".getBytes());
SSECOSKeyManagementParams ssecosKeyManagementParams = new SSECOSKeyManagementParams(kmsKeyId, encryptionContext);
putObjectRequest.setSSECOSKeyManagementParams(ssecosKeyManagementParams);
// For server-side encryption scenarios, the returned ETag is not the MD5 value of the file. Therefore, MD5 verification on the client should be removed.
// You can obtain the CRC64 value for verification as needed.
System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");
try {
    PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
    // "putobjectResult" will return ETag.
    String etag = putObjectResult.getETag();
    String crc64 = putObjectResult.getCrc64Ecma();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// Shut down the client.
cosclient.shutdown();
```

Sample 2: Using KMS encryption for objects uploaded with multipart upload

```java
COSCredentials cred = new BasicCOSCredentials("SECRET_ID", "SECRET_KEY");
// 2. Set the bucket region. For abbreviations of COS regions, please see https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// Use the HTTPS protocol.
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain "appid".
String bucketName = "examplebucket-1250000000";

String key = "doc/exampleobject.txt";
String kmsKeyId = "your-kms-key-id";
String encryptionContext = Base64.encodeAsString("{\"Ssekmstest\":\"Ssekmstest\"}".getBytes());
InitiateMultipartUploadRequest initiateMultipartUploadRequest = new InitiateMultipartUploadRequest(bucketName, key);
SSECOSKeyManagementParams ssecosKeyManagementParams = new SSECOSKeyManagementParams(kmsKeyId, encryptionContext);
// For server-side encryption scenarios, the returned ETag is not the MD5 value of the file. Therefore, MD5 verification on the client should be removed.
// You can obtain the CRC64 value for verification as needed.
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
        // Set the input stream of the part data source.
        uploadPartRequest.setInputStream(new ByteArrayInputStream(data));
        // Set the part length.
        uploadPartRequest.setPartSize(data.length); // Set the data length.
        uploadPartRequest.setPartNumber(i + 1);     // Assume that part number is 10.

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

// Shut down the client.
cosclient.shutdown();
```

Sample 3: Using KMS encryption for destination objects of a copy operation

```java
COSCredentials cred = new BasicCOSCredentials("SECRET_ID", "SECRET_KEY");
// 2. Set the bucket region. For abbreviations of COS regions, please see https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// Use the HTTPS protocol.
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3. Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain "appid".

String kmsKeyId = "your-kms-key-id";
String encryptionContext = Base64.encodeAsString("{\"Ssekmstest\":\"Ssekmstest\"}".getBytes());

// Region of the source bucket. Cross-region replication is supported.
Region srcBucketRegion = new Region("ap-guangzhou");
// Source bucket. The bucket name must contain "appid".
String srcBucketName = "examplebucket-1250000000";
// The source file to copy
String srcKey = "doc/exampleobject.txt";
// Destination bucket. The bucket name must contain "appid".
String destBucketName = "examplebucket-1250000000";
// The destination file of the copy operation
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

// Shut down the client.
cosclient.shutdown();
```

### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

#### Feature description

Users can provide a key for the encryption. In this way, the key will be used to AES-256 encrypt objects during the upload. You can call the `setHttpProtocol`, `setSSECustomerKey`, and other methods in the SDK for implementation.

> !
>- This type of encryption requires using HTTPS requests.
>- base64EncodedKey: the Base64-encoded key for server-side encryption provided by the customer
>- If this encryption method was used when you uploaded the source file, you should also use it when you GET (download) or HEAD (query) this file.


#### Sample code

```java
 // Initialize user authentication information (`secretId` and `secretKey`).
// Log in to the CAM console to check and manage the `SecretId` and `SecretKey` of your project.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
 COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
 // Set the bucket region. For abbreviations of COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224
 ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// The HTTPS protocol is required.
clientConfig.setHttpProtocol(HttpProtocol.https);
// Generate the COS client.
COSClient cosclient = new COSClient(cred, clientConfig);
// The bucket name must contain "appid".
String bucketName = "examplebucket-1250000000";

String key = "doc/exampleobject.txt";
File localFile = new File("test.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
String base64EncodedKey = "MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=";
// "sseCustomerKey" is a Base64-encoded key.
SSECustomerKey sseCustomerKey = new SSECustomerKey(base64EncodedKey);
putObjectRequest.setSSECustomerKey(sseCustomerKey);
ObjectMetadata objectMetadata = cosclient.getObjectMetadata();
objectMetadata.getHttpExpiresDate();
try {
PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
// "putobjectResult" will return ETag, an MD5 checksum that uniquely identifies the object, and is different from the MD5 checksum of the object according to the semantics of S3.
String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
e.printStackTrace();
} catch (CosClientException e) {
e.printStackTrace();
}
// Shut down the client.
cosclient.shutdown();
```
