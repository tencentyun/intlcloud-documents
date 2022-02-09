## Overview

This document provides an overview of APIs and SDK code samples related to object uploads.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object | Uploads an object to a bucket. |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using an HTML form | Uploads an object using an HTML form. |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts  | Uploads an object by appending the object by parts.   |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload operation | Initializes a multipart upload operation. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads an object in multiple parts. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |


## Advanced APIs (Recommended)

The advanced APIs encapsulate simple APIs via the TransferManager class to provide APIs for easier operations. Internally, a thread pool is used to concurrently accept and process requests from users, so users can choose to execute tasks asynchronously after submitting multiple tasks.

TransferManager instances are concurrency safe. You are advised to create only one TransferManager instance for a process and then close it when it is no longer used to call advanced APIs.


### Description

The advanced APIs encapsulate the simple upload and multipart upload APIs and can intelligently select the upload method based on file size. They also support features such as checkpoint restart and upload progress display.

>?
> - A part threshold is used to determine whether to use simple upload or multipart upload. The threshold is configurable and is 5 MB by default.
> - The part size is configurable and is 1 MB by default.
> - For stream upload, use simple upload if the object size is below the part threshold or the `Content-Length` header is not specified.
> - For stream upload, use multipart upload if the object size is above the part threshold or the `Content-Length` header is specified.
> - For file upload, use simple upload if the file size is below the part threshold, and use multipart upload if the file size is above the part threshold.
> - For file upload, use multipart upload with concurrent threads.
> - For multipart upload, advanced APIs provides the feature of getting the upload progress. For details, see the sample below.
> 

### Creating a TransferManager instance

Before using the advanced API, you need to create a TransferManager instance.

```java
// Create a TransferManager instance, which is used to call the advanced API later.
TransferManager createTransferManager() {
    // Create a COSClient client, which is the basic instance for accessing the COS service.
    // For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
    COSClient cosClient = createCOSClient();

    // Set the thread pool size. You are advised to the size of your thread pool to 16 or 32 to maximize network resource utilization, provided your client and COS networks are sufficient (for example, by using Tencent Cloud CVM and uploading to COS in the same region).
    // We recommend using a smaller value to avoid timeout due to slow network speed if you are transferring data over a public network with poor bandwidth quality.
    ExecutorService threadPool = Executors.newFixedThreadPool(32);

    // Pass a threadpool. Otherwise, a single-thread pool will be generated in TransferManager by default.
    TransferManager transferManager = new TransferManager(cosClient, threadPool);

    // Set the configuration items of the advanced API.
    // Set the threshold and part size for multipart upload to 5 MB and 1 MB respectively.
    TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
    transferManagerConfiguration.setMultipartUploadThreshold(5*1024*1024);
    transferManagerConfiguration.setMinimumUploadPartSize(1*1024*1024);
    transferManager.setConfiguration(transferManagerConfiguration);

    return transferManager;
}
```

### Parameter description

The `TransferManagerConfiguration` class is used to record the configuration of the advanced API. Its main members are described as follows:

| Member Name | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize | Set method | Part size of the multipart upload in bytes. Default: 5 MB | long |
| multipartUploadThreshold | Set method | If a file is greater than or equal to this value, it will be uploaded in concurrent parts. Unit: byte; default: 5 MB | long |
| multipartCopyThreshold | Set method | If a file is greater than or equal to this value, it will be replicated in concurrent parts. Unit: byte; default: 5 GB | long |
| multipartCopyPartSize | Set method | Part size in bytes for multipart replication. Default: 100 MB | long |

### Closing a TransferManager instance

After confirming that the process does not use the TransferManager instance to call the advanced API anymore, be sure to close it to avoid leaking resources.

```java
void shutdownTransferManager(TransferManager transferManager) {
    // If the parameter is set to `true`, the COSClient instance in the TransferManager instance will also be closed at the same time.
    // If the parameter is set to `false`, the COSClient instance in the TransferManager instance will not be closed.
    transferManager.shutdownNow(true);
}
```

### Uploading a local file

The upload source is a local file.

#### Method prototype

```java
// Upload an object
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Sample request

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Creating a TransferManager instance" on the current page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

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

// After confirming that the process does not use the TransferManager instance anymore, close it.
// For the detailed code, see "Advanced APIs -> Closing a TransferManager instance" on the current page.
shutdownTransferManger(transferManager);
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are described as follows:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | Metadata of a file | ObjectMetadata |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | 

#### Returned values

- Success: returns `Upload`. You can query whether the upload is complete, or wait until the upload is finished.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The UploadResult class records the object upload results requested by calling the waitForUploadResult() method from the Upload class. Its main class members are as follows:

| Member Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| requestId  | Request ID                                                       | String |
| dateStr    | Current server time                                             | String |
| versionId  | Returns the object’s version ID for versioning-enabled buckets. | String |
| crc64Ecma  | CRC64 value computed by the server based on the object content                           | String |

### Uploading a stream type

The upload source is a stream instance of the InputStream type (and its subtypes).

#### Method prototype

```java
// Upload an object
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Sample request

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Creating a TransferManager instance" on the current page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";

// Here, a ByteArrayInputStream stream is created as an example. In practice, you should create a stream of the actual InputStream type to upload.
long inputStreamLength = 1024 * 1024;
byte data[] = new byte[inputStreamLength];
InputStream inputStream = new ByteArrayInputStream(data);

ObjectMetadata objectMetadata = new ObjectMetadata();
// If you can obtain the exact length of the uploaded stream, you are advised to enter `Content-Length`.
// Otherwise, the following line can be omitted, but the advanced API cannot use multipart upload.
objectMetadata.setContentLength(inputStreamLength);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, inputStream, objectMetadata);

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

// After confirming that the process does not use the TransferManager instance anymore, close it.
// For the detailed code, see "Advanced APIs -> Closing a TransferManager instance" on the current page.
shutdownTransferManger(transferManager);
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are described as follows:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | Metadata of a file | ObjectMetadata |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | 

#### Returned values

- Success: returns `Upload`. You can query whether the upload is complete, or wait until the upload is finished.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The UploadResult class records the object upload results requested by calling the waitForUploadResult() method from the Upload class. Its main class members are as follows:

| Member Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| requestId  | Request ID                                                       | String |
| dateStr    | Current server time                                             | String |
| versionId  | Returns the object’s version ID for versioning-enabled buckets. | String |
| crc64Ecma  | CRC64 value computed by the server based on the object content                           | String |

### Displaying the upload progress

>? The upload progress can be displayed only for APIs that use multipart upload.
>

You need to configure a function to display the upload progress. The function is supposed to call the API to get the object size that has been successfully uploaded and then calculate the current upload progress.

#### Method prototype

```java
// Upload an object
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Sample request

```java
// You can adjust the following sample code as needed to form your own code.
void showTransferProgress(Transfer transfer) {
    // Here, `Transfer` is the parent class of the async upload result `Upload`.
    System.out.println(transfer.getDescription());

    // Use `transfer.isDone()` to check whether the upload is completed.
    while (transfer.isDone() == false) {
        try {
            // Get the progress every 2 seconds.
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            return;
        }

        TransferProgress progress = transfer.getProgress();
        long sofar = progress.getBytesTransferred();
        long total = progress.getTotalBytesToTransfer();
        double pct = progress.getPercentTransferred();
        System.out.printf("upload progress: [%d / %d] = %.02f%%\n", sofar, total, pct);
    }

    // If the upload is completed, `Completed` is returned. If the upload fails, `Failed` is returned.
    System.out.println(transfer.getState());
}
```

The sample code combined with the file upload operation is as follows:

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Creating a TransferManager instance" on the current page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

try {
    // The advanced API will return an asynchronous result `Upload`.
    Upload upload = transferManager.upload(putObjectRequest);
    // Print the upload progress until the upload is completed.
    showTransferProgress();
    // Capture possible exceptions
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the TransferManager instance anymore, close it.
// For the detailed code, see "Advanced APIs -> Closing a TransferManager instance" on the current page.
shutdownTransferManger(transferManager);
```

#### Description of progress obtaining

You can use the `getProgress()` method of the `Upload` class to obtain the `TransferProgress` class, which has the following three methods to obtain the upload progress:

| Method Name | Description | Type |
| ----------------------- | ------------------ | -----   |
| getBytesTransferred     | Obtains the number of bytes uploaded  | long   |
| getTotalBytesToTransfer | Obtains the total number of bytes of the file | long   |
| getPercentTransferred   | Obtains the percentage of the number of bytes uploaded  | double |

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are described as follows:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | Metadata of a file | ObjectMetadata |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | 

#### Returned values

- Success: returns `Upload`. You can query whether the upload is complete, or wait until the upload is finished.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The UploadResult class records the object upload results requested by calling the waitForUploadResult() method from the Upload class. Its main class members are as follows:

| Member Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| requestId  | Request ID                                                       | String |
| dateStr    | Current server time                                             | String |
| versionId  | Returns the object’s version ID for versioning-enabled buckets. | String |
| crc64Ecma  | CRC64 value computed by the server based on the object content                           | String |

### Suspending, resuming, or cancelling an upload

This API can be used to suspend, resume, or cancel an upload task.

> ?
> - A stream upload cannot be suspended, resumed, or cancelled.
> - A simple upload cannot be suspended, resumed, or cancelled.
> - An encryption upload cannot be suspended, resumed, or cancelled.

#### Method prototype

```java
// Upload an object
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Sample request

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Sample code: Creating a TransferManager instance" on the current page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

try {
    // The advanced API will return an asynchronous result `Upload`.
    Upload upload = transferManager.upload(putObjectRequest);
    // Wait 3 seconds for part of the file to be uploaded.
    Thread.sleep(3000);
    // Suspend the upload and get a PersistableUpload instance for resuming the upload later.
    PersistableUpload persistableUpload = upload.pause();
    // Complex suspension and resuming:
    // A PersistableUpload instance can be used to serialize the file content and store it and then deserialize it to resume the upload.
    // persistableUpload.serialize(out);
    // Resume the upload.
    upload = transferManager.resumeUpload(persistableUpload);
    // Capture possible exceptions
    UploadResult uploadResult = upload.waitForUploadResult();

    // Or directly cancel the upload
    // upload.abort();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the TransferManager instance anymore, close it.
// For the detailed code, see "Advanced APIs -> Sample code: Closing a TransferManager instance" on the current page.
shutdownTransferManger(transferManager);
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are described as follows:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)  | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | Metadata of a file | ObjectMetadata |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | 

#### Returned values

- Success: returns `Upload`. You can query whether the upload is complete, or wait until the upload is finished.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The UploadResult class records the object upload results requested by calling the waitForUploadResult() method from the Upload class. Its main class members are as follows:

| Member Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Unique identifier of the object in the bucket. For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| requestId  | Request ID                                                       | String |
| dateStr    | Current server time                                             | String |
| versionId  | Returns the object’s version ID for versioning-enabled buckets. | String |
| crc64Ecma  | CRC64 value computed by the server based on the object content                           | String |

### Uploading a local directory

A TransferManager instance encapsulates the feature of reading files from a local directory and uploading them to COS. This feature can upload files without destroying the directory structure. You can also upload files from one directory to another directory.

>? Recursive directory upload is supported. If the upload directory is too large, the upload may be slow or blocked for a long time. To upload a directory recursively, you are advised to upload a directory with a small capacity (for example, a directory with more than 1,024 files). If you need to upload large-capacity directories, you are advised to divide them into multiple small directories and call them in batches.
>

#### Method prototype

```java
public MultipleFileUpload uploadDirectory(String bucketName, String virtualDirectoryKeyPrefix,
            File directory, boolean includeSubdirectories);
```

#### Sample request

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Sample code: Creating a TransferManager instance" on the current page.
TransferManager transferManager = createTransferManager();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

// Set the prefix of the directory to upload the objects to. If this parameter is set to “”, objects will be uploaded to the root directory of the bucket.
String cos_path = "/prefix";
// Absolute path of the folder to upload
String dir_path = "/path/to/localdir";
// Whether to upload subdirectories in the folder recursively. If this parameter is set to “true”, objects in subdirectories will also be uploaded with the original directory structure retained.
Boolean recursive = false;

try {
    // Return an asynchronous result “Upload”. You can synchronously call waitForUploadResult to wait for the upload to end. If the upload is successful, UploadResult is returned; otherwise, an exception will be thrown.
    MultipleFileUpload upload = transferManager.uploadDirectory(bucketName, cos_path, new File(dir_path), recursive);

    // You can choose to view the upload progress. For details of the function, see "Advanced APIs -> Uploading files -> Displaying the upload progress" on the current page.
    showTransferProgress(upload);

    // You can also wait for the upload to complete.
    upload.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the TransferManager instance anymore, close it.
// For the detailed code, see "Advanced APIs -> Sample code: Closing a TransferManager instance" on the current page.
shutdownTransferManger(transferManager);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------------- | -------------------- | ---------------- |
| bucketName                | Name of the bucket in COS | GetObjectRequest |
| virtualDirectoryKeyPrefix | Prefix of the objects in COS | String           |
| directory                 | Absolute path of the folder to upload | File             |
| includeSubDirectory       | Whether to upload subdirectories recursively | Boolean          |

#### Returned values

- Success: returns MultipleFileUpload. You can query whether the upload is complete, or wait until the upload is finished.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Simple Operations

Requests for simple operations need to be initiated through COSClient instances. You need to create a COSClient instance before performing simple operations.

COSClient instances are concurrency safe. You are advised to create only one COSClient instance for a process and then close it when it is no longer used to initiate requests.

### Creating a COSClient instance

Before calling the COS API, you need to create a COSClient instance.

```java
// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Set the user identity information.
    // Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
    String secretId = "SECRETID";
    String secretKey = "SECRETKEY";
    COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol, `http` or `https`.
    // For 5.6.53 and earlier versions, HTTPS is recommended.
    // Starting from 5.6.54, HTTPS is used by default.
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // The following settings are optional.

    // Set the read timeout period, which is 30s by default.
    clientConfig.setSocketTimeout(30*1000);
    // Set the connection timeout period, which is 30s by default.
    clientConfig.setConnectionTimeout(30*1000);

    // If necessary, set the HTTP proxy, IP, and port.
    clientConfig.setHttpProxyIp("httpProxyIp");
    clientConfig.setHttpProxyPort(80);

    // Generate a COS client.
    return new COSClient(cred, clientConfig);
}
```

### Creating a COSClient client with a temporary key

If you want to request COS with a temporary key, you need to create a COSClient instance with the temporary key.
This SDK does not generate temporary keys. For how to generate a temporary key, please see [Generating a Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048#cos-sts-sdk).

```java

// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Here, the temporary key information is needed.
    // For how to generate temporary keys, please visit https://intl.cloud.tencent.com/document/product/436/14048.
    String tmpSecretId = "TMPSECRETID";
    String tmpSecretKey = "TMPSECRETKEY";
    String sessionToken = "SESSIONTOKEN";

    COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol, `http` or `https`.
    // For 5.6.53 and earlier versions, HTTPS is recommended.
    // Starting from 5.6.54, HTTPS is used by default.
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // The following settings are optional.

    // Set the read timeout period, which is 30s by default.
    clientConfig.setSocketTimeout(30*1000);
    // Set the connection timeout period, which is 30s by default.
    clientConfig.setConnectionTimeout(30*1000);

    // If necessary, set the HTTP proxy, IP, and port.
    clientConfig.setHttpProxyIp("httpProxyIp");
    clientConfig.setHttpProxyPort(80);

    // Generate a COS client.
    return new COSClient(cred, clientConfig);
}
```

### Uploading a local file

The upload source is a local file.

#### Method prototype

```java
// Method 1. Upload a local file to COS.
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// Method 2. Upload an input stream to COS.
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// Method 3. Encapsulate the two methods above to support more fine-grained parameter control, such as content-type and content-disposition.
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    System.out.println(putObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are described as follows:

| Request Member | Setting Method  | Description                                                     | Type   | Required |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName   | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String         | Yes |
| key | Constructor or set method | Unique identifier of the object in the bucket.<br>For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| file | Constructor or set method | Local file | File | No |
| input | Constructor or set method | Input stream | InputStream | No |
| metadata | Constructor or set method | Metadata of an object | ObjectMetadata | No |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | No |

The `ObjectMetadata` class is used to record the metadata of an object. The main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache expiration time, which is the same value as that of the Expires field in HTTP response header | Date |
| ongoingRestore | Indicates the object is being restored from ARCHIVE | Boolean |
| userMetadata | User-defined metadata prefixed with `x-cos-meta-` | Map&lt;String, String&gt; |
| metadata | Headers other than user-defined metadata | Map&lt;String, String&gt; |
| restoreExpirationTime  | Expiration time for an object copy restored from ARCHIVE | Date |

#### Response description

- Success: returns `PutObjectResult`, including the file ETag.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The PutObjectResult class is used to return result information. Its main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | Request ID | String |
| dateStr  | Current server time | String |
| versionId | Returns the version ID of an object in a version-enabled bucket | String |
| eTag | MD5 checksum of the object returned by PUT Object | String |
| crc64Ecma | CRC64 value computed by the server based on the object content | String |

### Uploading a stream type

The upload source is a stream instance of the InputStream type (and its subtypes).

#### Method prototype

```java
// Method 1. Upload a local file to COS.
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// Method 2. Upload an input stream to COS.
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// Method 3. Encapsulate the two methods above to support more fine-grained parameter control, such as content-type and content-disposition.
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";

// Here, a ByteArrayInputStream stream is created as an example. In practice, you should create a stream of the actual InputStream type to upload.
long inputStreamLength = 1024 * 1024;
byte data[] = new byte[inputStreamLength];
InputStream inputStream = new ByteArrayInputStream(data);

ObjectMetadata objectMetadata = new ObjectMetadata();
// If you can obtain the exact length of the uploaded stream, you are advised to enter `Content-Length`.
// Otherwise, the following line can be omitted, but the advanced API cannot use multipart upload.
objectMetadata.setContentLength(inputStreamLength);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, inputStream, objectMetadata);

try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    System.out.println(putObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are described as follows:

| Request Member | Setting Method   | Description                                                     | Type   | Required |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName   | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String         | Yes |
| key | Constructor or set method | Unique identifier of the object in the bucket.<br>For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| file | Constructor or set method | Local file | File | No |
| input | Constructor or set method | Input stream | InputStream | No |
| metadata | Constructor or set method | Metadata of an object | ObjectMetadata | No |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | No |

The `ObjectMetadata` class is used to record the metadata of an object. The main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache expiration time, which is the same value as that of the Expires field in HTTP response header | Date |
| ongoingRestore | Indicates the object is being restored from ARCHIVE | Boolean |
| userMetadata | User-defined metadata prefixed with `x-cos-meta-` | Map&lt;String, String&gt; |
| metadata | Headers other than user-defined metadata | Map&lt;String, String&gt; |
| restoreExpirationTime  | Expiration time for an object copy restored from ARCHIVE | Date |

#### Response description

- Success: returns `PutObjectResult`, including the file ETag.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The PutObjectResult class is used to return result information. Its main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | Request ID | String |
| dateStr  | Current server time | String |
| versionId | Returns the version ID of an object in a version-enabled bucket | String |
| eTag | MD5 checksum of the object returned by PUT Object | String |
| crc64Ecma | CRC64 value computed by the server based on the object content | String |

### Creating a directory

COS does not have the concept of directories, but you can consider object paths separated with slashes (/) as virtual directories.

>?
> - If you need a directory, you can upload a file to the desired directory, and the directory will be automatically created. For example, if you upload a file like `/dir/example.txt`, the `/dir` directory will be generated automatically. For more information, please see "Uploading local files" on the current page.
> 

If you need a directory with no files, upload an empty stream to a path ending with a slash (/), and then you have a virtual empty directory.

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Specify the path of the directory to be created.
String key = "/example/dir/";

// Here, an empty ByteArrayInputStream is created as an example.
byte data[] = new byte[0];
InputStream inputStream = new ByteArrayInputStream(data);

ObjectMetadata objectMetadata = new ObjectMetadata();
objectMetadata.setContentLength(0);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, inputStream, objectMetadata);

try {
    PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
    System.out.println(putObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

### Appending parts

This API is used to upload an object by appending parts.

#### Method prototype

```java
public AppendObjectResult appendObject(AppendObjectRequest appendObjectRequest)
        throws CosServiceException, CosClientException
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";

// Assume that the contents of these two files need to be appended for upload.
File part1File = new File("/path/to/part1File");
File part2File = new File("/path/to/part2File");

try {
    AppendObjectRequest appendObjectRequest = new AppendObjectRequest(bucketName, key, part1File);
    appendObjectRequest.setPosition(0L);
    AppendObjectResult appendObjectResult = cosclient.appendObject(appendObjectRequest);
    long nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);

    appendObjectRequest = new AppendObjectRequest(bucketName, key, part2File);
    appendObjectRequest.setPosition(nextAppendPosition);
    appendObjectResult = cosclient.appendObject(appendObjectRequest);
    nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
// Shut down the client.
cosclient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| -------------------- | ------------ | ---------------- |
| appendObjectRequest | Request to append upload | AppendObjectRequest |

Members of `AppendObjectRequest`:

| Request Member | Set Method | Description | Type | Required |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName   | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String         | Yes |
| key | Constructor or set method | Unique identifier of the object in the bucket.<br>For example, in the object's access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| localfile | Constructor or set method | Local file | File | No |
| input | Constructor or set method | Input stream | InputStream | No |
| metadata | Constructor or set method | Metadata of an object | ObjectMetadata | No |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded object. The default setting is no limit. | Int | No |
| position | Set method | Start position of the append, in bytes | Long | Yes |

#### Response description

- Success: `AppendObjectResult`
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The `AppendObjectResult` class is used to return results. Its main members are as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| metadata | Headers | ObjectMetadata               |
| nextAppendPosition| Position of the next append | Long |

### Uploading an object using an HTML form

This API is used to upload an object using an HTML form.

#### Constructing the form body for upload

This API is used to construct the form body part at the very beginning according to the form parameters.

```java
String buildPostObjectBody(String boundary, Map<String, String> formFields, String filename, String contentType) {
    StringBuffer stringBuffer = new StringBuffer();
    for(Map.Entry entry: formFields.entrySet()) {
        // Add a boundary line, starting the line with --.
        stringBuffer.append("--").append(boundary).append("\r\n");
        // Field name
        stringBuffer.append("Content-Disposition: form-data; name=\""
                + entry.getKey() + "\"\r\n\r\n");
        // Field value
        stringBuffer.append(entry.getValue() + "\r\n");
    }
    // Add a boundary line, starting the line with --.
    stringBuffer.append("--").append(boundary).append("\r\n");
    // File name
    stringBuffer.append("Content-Disposition: form-data; name=\"file\"; "
            + "filename=\"" + filename + "\"\r\n");
    // File type
    stringBuffer.append("Content-Type: " + contentType + "\r\n\r\n");
    return stringBuffer.toString();
}
```

#### Uploading a local file

```java
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// For more information on COS regions, please visit https://intl.cloud.tencent.com/document/product/436/6224.
String endpoint = "cos.{COS_REGION}.myqcloud.com";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";
// You can log in to the CAM console to view and manage the `SecretId` and `SecretKey` of your project.
String secretId = "AKIDXXXXXXXX";
String seretKey = "1A2Z3YYYYYYYYYY";

String localFilePath = "/path/to/localFile";
String contentType = "image/jpeg";

long startTimestamp = System.currentTimeMillis() / 1000;
long endTimestamp = startTimestamp +  30 * 60;
String endTimestampStr = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss.SSS'Z'").format(endTimestamp * 1000);

String keyTime = startTimestamp + ";" + endTimestamp;
String boundary = "----WebKitFormBoundaryZBPbaoYE2gqeB21N";

// Set the `body` field of the form.
Map<String, String> formFields = new HashMap<>();
formFields.put("q-sign-algorithm", "sha1");
formFields.put("key", key);
formFields.put("q-ak", secretId);
formFields.put("q-key-time", keyTime);

// Construct a policy. For details, visit https://intl.cloud.tencent.com/document/product/436/14690.
String policy = "{\n" +
        "    \"expiration\": \"" + endTimestampStr + "\",\n" +
        "    \"conditions\": [\n" +
        "        { \"bucket\": \"" + bucketName + "\" },\n" +
        "        { \"q-sign-algorithm\": \"sha1\" },\n" +
        "        { \"q-ak\": \"" + secretId + "\" },\n" +
        "        { \"q-sign-time\":\"" + keyTime + "\" }\n" +
        "    ]\n" +
        "}";

// The policy must be Base64 encoded and then placed to the form.
String encodedPolicy = new String(Base64.encodeBase64(policy.getBytes()));
// Set the policy.
formFields.put("policy", encodedPolicy);
// Calculate the signature according to the encoded policy and SecretKey.
COSSigner cosSigner = new COSSigner();
String signature = cosSigner.buildPostObjectSignature(seretKey,
        keyTime, policy);
// Set the signature.
formFields.put("q-signature", signature);

// Construct the body part at the very beginning according to the preceding form parameters.
String formBody = buildPostObjectBody(boundary, formFields,
        localFilePath, contentType);

HttpURLConnection conn = null;
try {
    String urlStr = "http://" + bucketName + "." + endpoint;
    URL url = new URL(urlStr);
    conn = (HttpURLConnection) url.openConnection();
    conn.setRequestMethod("POST");
    conn.setRequestProperty("User-Agent", VersionInfoUtils.getUserAgent());
    conn.setRequestProperty("Content-Type", "multipart/form-data; boundary=" + boundary);
    conn.setDoOutput(true);
    conn.setDoInput(true);

    OutputStream out = new DataOutputStream(conn.getOutputStream());
    // Write to the very beginning of the form.
    out.write(formBody.getBytes());

    // Write the contents of the file to the output stream.
    File file = new File(localFilePath);
    DataInputStream in = new DataInputStream(new FileInputStream(file));
    int readBytes;
    byte[] bytes = new byte[4096];
    while ((readBytes = in.read(bytes)) != -1) {
        out.write(bytes, 0, readBytes);
    }
    in.close();

    // Add the last separator, starting and ending the line with --.
    byte[] endData = ("\r\n--" + boundary + "--\r\n").getBytes();
    out.write(endData);
    out.flush();
    out.close();

    // Read the response header.
    for (Map.Entry<String, List<String>> entries : conn.getHeaderFields().entrySet()) {
        String values = "";
        for (String value : entries.getValue()) {
            values += value + ",";
        }
        if(entries.getKey() == null) {
            System.out.println("reponse line:" +  values );
        } else {
            System.out.println(entries.getKey() + ":" +  values );
        }
    }
} catch (Exception e) {
    e.printStackTrace();
    throw e;
} finally {
    if (conn != null) {
        conn.disconnect();
    }
}
```

## Multipart Operations

When a large file is uploaded, the file is uploaded as a series of parts to address the possible interruptions caused by the long upload time of the large file.

>? If you want the uploaded files or streams to be obtained as a whole, advanced APIs are recommended.
>

### Operation procedures

#### Performing a multipart upload

1. Initialize the multipart upload with `Initiate Multipart Upload` and get the `UploadId`.
2. Use the `UploadId` to upload the parts with `Upload Part - Copy`.
3. Complete the multipart upload with `Complete Multipart Upload`.

#### Resuming a multipart upload

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Use the `UploadId` to list the uploaded parts with `List Parts`.
3. Use the `UploadId` to upload the remaining parts with `Upload Part`.
4. Complete the multipart upload with `Complete Multipart Upload`.

#### Aborting a multipart upload

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Abort the multipart upload and delete the uploaded parts with `Abort Multipart Upload`.

### Initializing a multipart upload

This API is used to initialize a multipart upload and get the corresponding `UploadId` for future operations.

#### Method prototype

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";

InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(bucketName, key);

// During multipart upload, you can specify the metadata of an uploaded file only by initializing the multipart upload.
// Specify desired headers.
ObjectMetadata objectMetadata = new ObjectMetadata();
request.setObjectMetadata(objectMetadata);

try {
    InitiateMultipartUploadResult initResult = cosClient.initiateMultipartUpload(request);
    // Get `UploadId`.
    String uploadId = initResult.getUploadId();
    System.out.println(uploadId);
} catch (CosServiceException e) {
    throw e;
} catch (CosClientException e) {
    throw e;
}
```

#### Parameter description

| Parameter | Description | Type |
| ------------------------------ | ---- | ------------------------------ |
| initiateMultipartUploadRequest | Request | InitiateMultipartUploadRequest |

The request members are described as follows:

| Parameter | Setting Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg`. | String |

#### Response description

- Success: returns `InitiateMultipartUploadResult`, including the `uploadId` that identifies the multipart upload.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Querying multipart uploads

This API (`List Multipart Uploads`) is used to get all ongoing multipart upload tasks to obtain the `UploadId` of a desired multipart upload task.

#### Method prototype

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

// Key of the multipart upload tasks to be queried
String targetKey = "targetKey";

ListMultipartUploadsRequest listMultipartUploadsRequest = new ListMultipartUploadsRequest(bucketName);
// Maximum number of multipart upload tasks listed per request
listMultipartUploadsRequest.setMaxUploads(100);
// Set the target prefix (key) of the multipart upload tasks to be queried.
listMultipartUploadsRequest.setPrefix("targetKey");

MultipartUploadListing multipartUploadListing = null;

boolean found = false;

do {
    multipartUploadListing = cosclient.listMultipartUploads(listMultipartUploadsRequest);
    List<MultipartUpload> multipartUploads = multipartUploadListing.getMultipartUploads();

    for (MultipartUpload mUpload : multipartUploads) {
        if (mUpload.getKey().equals(targetKey)) {
            System.out.println(mUpload.getUploadId());
            found = true;
            break;
        }
    }

    if (found) {
        break;
    }

} while (multipartUploadListing.isTruncated());

if (!found) {
    System.out.printf("do not found upload task with key: %s\n", targetKey);
}
```

#### Parameter description

| Parameter | Description | Type |
| --------------------------- | ---- | --------------------------- |
| listMultipartUploadsRequest | Request | ListMultipartUploadsRequest |

The request members are described as follows:

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| keyMarker | Specifies the key after which the listing should begin | String |
| delimiter | A symbol used to limit the results of a list operation. If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed. If no prefix is specified, the listing will start from the beginning of the path. | String |
| prefix | Specifies that the returned object key must be prefixed with this value. Note that when you use a prefix to query object keys, the returned key will contain the same prefix. | String |
| uploadIdMarker | Specifies the `uploadId` after which the listing should begin | String |
| maxUploads | Sets the maximum number of multipart uploads returned. Valid values: 1-1000 | String |
| encodingType | Encoding type of returned values. Valid value: `url` | String |

#### Response description

- Success: returns `MultipartUploadListing`, including the in-progress multipart uploads.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Uploading parts

This API (`Upload Part`) is used to upload an object in parts.

#### Method prototype

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";
// `UploadId` is the unique identifier of a multipart upload task. You can obtain it by initializing the multipart upload or querying the multipart upload task.
String uploadId = "exampleuploadid";

// An ETag is returned when each part is uploaded. Save the ETags and use them to combine the parts later.
List<PartETag> partETags = new LinkedList<>();

// Upload data. Here, 10 parts (1 MB each) are uploaded.
for (int i = 1; i <= 10; i++) {
    byte data[] = new byte[1024 * 1024];
    // Here, a ByteArrayInputStream stream is created as an example. In practice, you should create a stream of the actual InputStream type to upload.
    long inputStreamLength = 1024 * 1024;
    byte data[] = new byte[inputStreamLength];
    InputStream inputStream = new ByteArrayInputStream(data);

    UploadPartRequest uploadPartRequest = new UploadPartRequest();
    uploadPartRequest.setBucketName(bucketName);
    uploadPartRequest.setKey(key);
    uploadPartRequest.setUploadId(uploadId);
    uploadPartRequest.setInputStream(inputStream(data));
    // Set the part length.
    uploadPartRequest.setPartSize(data.length);
    // Set the part number, which starts from 1.
    uploadPartRequest.setPartNumber(i);

    try {
        UploadPartResult uploadPartResult = cosClient.uploadPart(uploadPartRequest);
        PartETag partETag = uploadPartResult.getPartETag();
        partETags.add(partETag);
    } catch (CosServiceException e) {
        throw e;
    } catch (CosClientException e) {
        throw e;
    }
}

System.out.println(partETags);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | ---- | ----------------- |
| uploadPartRequest | Request | UploadPartRequest |

The request members are described as follows:

| Parameter | Set Method | Description | Type |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName  | Set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg` | String |
| uploadId | Set method | Identifies the `uploadId` of the specified multipart upload | String |
| partNumber | Set method | Number (>= 1) that identifies the specified part | int |
| inputStream | Set method | Input stream to be uploaded in multi-parts | InputStream |
| trafficLimit | Set method | Traffic limits (in bit/s) on the uploaded parts. The default setting is no limit. | Int |

#### Response description

- Success: returns `UploadPartResult`, including the ETags of the uploaded parts.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameters

The `UploadPartResult` class is used to return request results. Its main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| partNumber | Number that identifies the specified part | String                |
| eTag        | Returns the MD5 hash of the uploaded part                   | String |
| crc64Ecma | CRC64 value computed by the server based on the part content | String |

### Querying uploaded parts

This API (`List Parts`) is used to query the uploaded parts of a multipart upload.

#### Method prototype

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";
// `UploadId` is the unique identifier of a multipart upload task. You can obtain it by initializing the multipart upload or querying the multipart upload task.
String uploadId = "exampleuploadid";

// It is used to save information of all uploaded parts.
List<PartETag> partETags = new LinkedList<>();

PartListing partListing = null;
ListPartsRequest listPartsRequest = new ListPartsRequest(bucketName, key, uploadId);
do {
    try {
        partListing = cosClient.listParts(listPartsRequest);
    } catch (CosServiceException e) {
        throw e;
    } catch (CosClientException e) {
        throw e;
    }

    for (PartSummary partSummary : partListing.getParts()) {
        partETags.add(new PartETag(partSummary.getPartNumber(), partSummary.getETag()));
    }

    listPartsRequest.setPartNumberMarker(partListing.getNextPartNumberMarker());
} while (partListing.isTruncated());
```

#### Parameter description

| Parameter  | Set Method | Description | Type |
| ---------------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Object name | String |
| uploadId | Constructor or set method | `uploadId` of the multipart upload to be queried | String |
| maxParts | Set method | Maximum number of entries returned at a time. Default value: `1000` | String |
| partNumberMarker | Set method | By default, entries are listed in UTF-8 binary order, starting from the part number after the marker. | String |
| encodingType | Set method | Encoding type of the returned value | String |

#### Response description

- Success: returns `PartListing`, including the ETag and number of each part as well as the starting marker of the next list.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Completing a multipart upload

This API (`Complete Multipart Upload`) is used to complete the multipart upload of a file.

>? After the multipart upload is completed, the multipart upload task is deleted and the `UploadId` corresponding to the task is no longer valid.
>

#### Method prototype

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";
// `UploadId` is the unique identifier of a multipart upload task. You can obtain it by initializing the multipart upload or querying the multipart upload task.
String uploadId = "exampleuploadid";

// It is used to store the information of the uploaded parts. In actual practice, the content here is obtained from the multipart upload API.
List<PartETag> partETags = new LinkedList<>();

// After the upload is completed, call `complete` to complete the multipart upload.
CompleteMultipartUploadRequest completeMultipartUploadRequest =
        new CompleteMultipartUploadRequest(bucketName, key, uploadId, partETags);
try {
    CompleteMultipartUploadResult completeResult =
            cosClient.completeMultipartUpload(completeMultipartUploadRequest);
    System.out.println(completeResult.getRequestId());
} catch (CosServiceException e) {
    throw e;
} catch (CosClientException e) {
    throw e;
}

// After confirming that the COSClint is not used any more, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Set Method  | Description                                                     | Type   |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg`. | String            |
| uploadId | Constructor or set method | Identifies a specified multipart upload. | String |
| partETags  | Constructor or set method | Identifies the number and ETag returned for an uploaded part. | List&lt;PartETag&gt; |

#### Response description

- Success: returns `CompleteMultipartUploadResult`, including the ETag of the completed object.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Aborting a multipart upload

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts.

>? After a multipart upload is aborted, both the multipart upload task and the uploaded parts are deleted, and the corresponding `UploadId` is no longer valid.
>

#### Method prototype

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// An object key is the unique identifier of an object in a bucket.
String key = "exampleobject";
// `UploadId` is the unique identifier of a multipart upload task. You can obtain it by initializing the multipart upload or querying the multipart upload task.
String uploadId = "exampleuploadid";

AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
try {
    cosClient.abortMultipartUpload(abortMultipartUploadRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// After confirming that the COSClint is not used any more, close it.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Setting Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg`. | String |
| uploadId | Constructor or set method | Identifies a specified multipart upload. | String |

#### Response description

- Success: No value is returned.
- Failure: An error occurs (such as authentication failure), throwing the "CosClientException" or "CosServiceException" exception. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
