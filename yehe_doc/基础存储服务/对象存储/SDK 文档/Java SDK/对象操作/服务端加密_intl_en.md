## Overview

This document describes how to enable server-side encryption when uploading objects. There are three types of keys that can be used for server-side encryption:

* COS-managed key
* Customer-provided key
* KMS-managed key

### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced API -> Sample Code: Creating TransferManager" in "Uploading Objects".
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

ObjectMetadata objectMetadata = new ObjectMetadata();
// Set the encryption algorithm to AES-256.
objectMetadata.setServerSideEncryption(SSEAlgorithm.AES256.getAlgorithm());
putObjectRequest.setMetadata(objectMetadata);

// For server-side encryption scenarios, the returned ETag is not the MD5 value of the file. Therefore, MD5 verification on the client should be removed.
// You can obtain the CRC64 value for verification as needed.
System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");

try {
    // The advanced API will return an asynchronous result `Upload`.
    // You can call the `waitForUploadResult` method to wait for the upload to complete. If the upload is successful, `UploadResult` is returned. If the upload fails, an exception is returned.
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the TransferManager anymore, close it.
// For the detailed code, see "Advanced APIs -> Closing TransferManager" on the current page.
shutdownTransferManager(transferManager);
```

### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

With this method, the encryption key is provided by the customer. To upload an object, COS will apply AES-256 encryption to the data using the customer-provided encryption key pair.

> !
>- This type of encryption requires using HTTPS requests.
>- You need to provide a 32-byte string as the key, a combination of numbers, letters, and characters, with Chinese characters not supported.
>- If a file was key-encrypted when uploaded, you need to include the same key in your GET (download) or HEAD (query) request for it to succeed.

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced API -> Sample Code: Creating TransferManager" in "Uploading Objects".
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

String base64EncodedKey = "MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=";
// "sseCustomerKey" is a Base64-encoded key.
SSECustomerKey sseCustomerKey = new SSECustomerKey(base64EncodedKey);
putObjectRequest.setSSECustomerKey(sseCustomerKey);

// For server-side encryption scenarios, the returned ETag is not the MD5 value of the file. Therefore, MD5 verification on the client should be removed.
// You can obtain the CRC64 value for verification as needed.
System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");

try {
    // The advanced API will return an asynchronous result `Upload`.
    // You can call the `waitForUploadResult` method to wait for the upload to complete. If the upload is successful, `UploadResult` is returned. If the upload fails, an exception is returned.
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the TransferManager anymore, close it.
// For the detailed code, see "Advanced APIs -> Closing TransferManager" on the current page.
shutdownTransferManager(transferManager);
```

### Using server-side encryption with KMS-managed encryption keys (SSE-KMS) to protect data

SSE-KMS encryption is server-side encryption using keys managed by KMS, a Tencent Cloud security management service. KMS is designed to generate and protect your keys using third-party-certified hardware security modules (HSM). It allows you to easily create and manage keys for use in multiple applications and services, while meeting regulatory and compliance requirements. For information on how to activate KMS service, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced API -> Sample Code: Creating TransferManager" in "Uploading Objects".
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

// KMS CMK
String kmsKeyId = "your-kms-key-id";
String encryptionContext = Base64.encodeAsString("{\"Ssekmstest\":\"Ssekmstest\"}".getBytes());
SSECOSKeyManagementParams ssecosKeyManagementParams = new SSECOSKeyManagementParams(kmsKeyId, encryptionContext);
putObjectRequest.setSSECOSKeyManagementParams(ssecosKeyManagementParams);

// For server-side encryption scenarios, the returned ETag is not the MD5 value of the file. Therefore, MD5 verification on the client should be removed.
// You can obtain the CRC64 value for verification as needed.
System.setProperty(SkipMd5CheckStrategy.DISABLE_PUT_OBJECT_MD5_VALIDATION_PROPERTY, "true");

try {
    // The advanced API will return an asynchronous result `Upload`.
    // You can call the `waitForUploadResult` method to wait for the upload to complete. If the upload is successful, `UploadResult` is returned. If the upload fails, an exception is returned.
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the TransferManager anymore, close it.
// For the detailed code, see "Advanced APIs -> Closing TransferManager" on the current page.
shutdownTransferManager(transferManager);
```
