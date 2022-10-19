## Overview

This document provides an overview of APIs and SDK code samples for object uploads.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading object in whole | Uploads object to bucket. |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading object by using HTML form | Uploads object by using HTML form. |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | 	Appending parts  |	Uploads object by appending parts.   |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries ongoing multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing multipart upload operation | Initializes multipart upload operation. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads object in parts. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying part | Copies object as part. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |


## Advanced APIs (Recommended)

The advanced APIs encapsulate simple APIs via the TransferManager class to provide APIs for easier operations. Internally, a thread pool is used to concurrently accept and process requests from you, so you can choose to execute jobs asynchronously after submitting multiple jobs.

TransferManager instances are concurrency-safe. We recommend you create only one TransferManager instance for a process and then shut it down when it is no longer used to call advanced APIs.


### Feature description

The advanced APIs encapsulate the simple upload and multipart upload APIs and can intelligently select the upload method based on file size. They also support such features as checkpoint restart and upload progress display.

>?
> - A part threshold is used to determine whether to upload in whole or in parts. The threshold is configurable and is 5 MB by default.
> - The part size is configurable and is 1 MB by default.
> - For stream upload, the stream will be uploaded in whole if the stream size is below the part threshold or the `Content-Length` header is not specified.
> - For stream upload, the stream will be uploaded in parts if the stream size is above the part threshold and the `Content-Length` header is specified.
> - For file upload, the file will be uploaded in whole if the file size is below the part threshold or in parts if the file size is above the part threshold.
> - For file upload in parts, multiple parts will be uploaded concurrently with multiple threads.
> - For multipart upload, the advanced upload API provides the feature of getting the upload progress. For more information, see the sample below.
> 

### Creating TransferManager instance

Before using the advanced API, you must create a TransferManager instance first.

```java
// Create a TransferManager instance, which is used to call the advanced API later.
TransferManager createTransferManager() {
    // Create a COSClient client, which is the basic instance for accessing the COS service.
    // For the detailed code, see **Simple Operations** > **Creating COSClient instance** in this document.
    COSClient cosClient = createCOSClient();

    // Set the thread pool size. We recommend you set the size of your thread pool to 16 or 32 to maximize network resource utilization, provided your client and COS networks are sufficient (for example, uploading a file to a COS bucket from a CVM instance in the same region).
    // We recommend you use a smaller value to avoid timeout caused by slow network speed if you are transferring data over a public network with poor bandwidth quality.
    ExecutorService threadPool = Executors.newFixedThreadPool(32);

    // Pass a `threadpool`; otherwise, a single-thread pool will be generated in `TransferManager` by default.
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

The `TransferManagerConfiguration` class is used to record the configuration information of the advanced API. Its main members are as described below:

| Member | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize | Set method | Part size of the multipart upload in bytes. Default value: 5 MB. | long |
| multipartUploadThreshold | Set method | If a file is greater than or equal to this value in bytes, it will be uploaded in concurrent parts. Default value: 5 MB. | long |
| multipartCopyThreshold | Set method | If a file is greater than or equal to this value in bytes, it will be copied in concurrent parts. Default value: 5 GB. | long |
| multipartCopyPartSize | Set method | Part size in bytes for multipart copy. Default value: 100 MB. | long |

### Shutting down TransferManager instance

After confirming that the process no longer uses the TransferManager instance to call the advanced API, be sure to shut it down to avoid resource leakage.

```java
void shutdownTransferManager(TransferManager transferManager) {
    // If the parameter is set to `true`, the COSClient instance in the TransferManager instance will also be shut down at the same time.
    // If the parameter is set to `false`, the COSClient instance in the TransferManager instance will not be shut down.
    transferManager.shutdownNow(true);
}
```

### Uploading local file

The upload source is a local file.

#### Method prototype

```java
// Upload an object.
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Sample request

```java
// Before using the advanced API, you must make sure that the process contains a TransferManager instance; if not, then create one.
// For the detailed code, see **Advanced API** > **Creating TransferManager instance** in this document.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";
// Local file path.
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

// Set the storage class, which can be STANDARD (default value) or STANDARD_IA. You can also ignore this line as appropriate.
// For more information on storage classes, visit https://cloud.tencent.com/document/product/436/33417.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);

// If you need to set the custom headers of the object, refer to the following code; otherwise, omit the following lines. For more information on custom headers, visit https://cloud.tencent.com/document/product/436/13361.
ObjectMetadata objectMetadata = new ObjectMetadata();

// To set `Content-Type`, `Cache-Control`, `Content-Disposition`, `Content-Encoding`, or `Expires` as a custom header, use `objectMetadata.setHeader()`.
objectMetadata.setHeader(key, value);
// To set a custom header like `x-cos-meta-[custom suffix]`, use:
Map<String, String> userMeta = new HashMap<String, String>();
userMeta.put("x-cos-meta-[custom suffix]", "value");
objectMetadata.setUserMetadata(userMeta);

putObjectRequest.withMetadata(objectMetadata);

try {
    // The advanced API will return an async result `Upload`.
    // You can synchronously call the `waitForUploadResult` method to wait for the upload to complete. If the upload is successful, `UploadResult` will be returned; otherwise, an exception will be reported.
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced API** > **Shutting down TransferManager instance** in this document.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are as described below:

| Request Member | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).  | String |
| key | Constructor or set method | Unique identifier of the object in the bucket. <br>For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | File metadata | ObjectMetadata |
| trafficLimit | Set method | Traffic limit on the uploaded object in bit/s. There is no limit by default. | Int |
|storageClass | Set method | Storage class | String |

#### Returned values

- Success: `Upload` is returned. You can query whether the upload is complete, or wait for the upload to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameter description

The `UploadResult` class records the information of the uploaded object requested by calling the `waitForUploadResult()` method from the `Upload` class. Its main members are as described below:

| Member | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Unique identifier of the object in the bucket. <br/>For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| requestId  | Request ID                                                       | String |
| dateStr    | Current server time                                             | String |
| versionId  | Version ID of the object returned when the bucket has versioning enabled | String |
| crc64Ecma  | CRC64 value computed by the server based on the object content                           | String |

### Uploading stream

The upload source is a stream instance of the `InputStream` type (and its subtypes).

#### Method prototype

```java
// Upload an object.
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Sample request

```java
// Before using the advanced API, you must make sure that the process contains a TransferManager instance; if not, then create one.
// For the detailed code, see **Advanced API** > **Creating TransferManager instance** in this document.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";

// Here, a `ByteArrayInputStream` stream is created as an example. In practice, you should create a stream of the `InputStream` type for upload.
long inputStreamLength = 1024 * 1024;
byte data[] = new byte[inputStreamLength];
InputStream inputStream = new ByteArrayInputStream(data);

ObjectMetadata objectMetadata = new ObjectMetadata();
// If you can get the exact length of the uploaded stream, we recommend you enter `Content-Length`.
// Otherwise, the following line can be omitted, but the advanced API cannot use multipart upload.
objectMetadata.setContentLength(inputStreamLength);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, inputStream, objectMetadata);

// Set the storage class, which can be STANDARD (default value) or STANDARD_IA. You can also ignore this line as appropriate.
// For more information on storage classes, visit https://cloud.tencent.com/document/product/436/33417.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);

try {
    // The advanced API will return an async result `Upload`.
    // You can synchronously call the `waitForUploadResult` method to wait for the upload to complete. If the upload is successful, `UploadResult` will be returned; otherwise, an exception will be reported.
    Upload upload = transferManager.upload(putObjectRequest);
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced API** > **Shutting down TransferManager instance** in this document.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are as described below:

| Request Member | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).  | String |
| key | Constructor or set method | Unique identifier of the object in the bucket. <br>For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | File metadata | ObjectMetadata |
| trafficLimit | Set method | Traffic limit on the uploaded object in bit/s. There is no limit by default. | Int |
|storageClass | Set method | Storage class | String |

#### Returned values

- Success: `Upload` is returned. You can query whether the upload is complete, or wait for the upload to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameter description

The `UploadResult` class records the information of the uploaded object requested by calling the `waitForUploadResult()` method from the `Upload` class. Its main members are as described below:

| Member | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Unique identifier of the object in the bucket. <br/>For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| requestId  | Request ID                                                       | String |
| dateStr    | Current server time                                             | String |
| versionId  | Version ID of the object returned when the bucket has versioning enabled | String |
| crc64Ecma  | CRC64 value computed by the server based on the object content                           | String |

### Displaying the upload progress

>? The upload progress can be displayed only for APIs that use multipart upload.
>

To display the upload progress, you need a function for printing the progress, where the API is called to get the size of the successfully uploaded object and then calculate the current upload progress.

#### Method prototype

```java
// Upload an object.
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Sample request

```java
// You can adjust the following sample code as needed to form your own code.
void showTransferProgress(Transfer transfer) {
    // Here, `Transfer` is the parent class of the async upload result `Upload`.
    System.out.println(transfer.getDescription());

    // Use `transfer.isDone()` to check whether the upload is complete.
    while (transfer.isDone() == false) {
        try {
            // Get the progress every two seconds.
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

    // If the upload is complete, `Completed` will be returned; otherwise, `Failed` will be returned.
    System.out.println(transfer.getState());
}
```

The sample code combined with the file upload operation is as follows:

```java
// Before using the advanced API, you must make sure that the process contains a TransferManager instance; if not, then create one.
// For the detailed code, see **Advanced API** > **Creating TransferManager instance** in this document.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";
// Local file path.
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

try {
    // The advanced API will return an async result `Upload`.
    Upload upload = transferManager.upload(putObjectRequest);
    // Print the upload progress until the upload is complete.
    showTransferProgress(upload);
    // Capture possible exceptions.
    UploadResult uploadResult = upload.waitForUploadResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced API** > **Shutting down TransferManager instance** in this document.
shutdownTransferManager(transferManager);
```

#### Progress acquisition description

You can use the `getProgress` method of the `Upload` class to get the `TransferProgress` class, which has the following three methods to get the upload progress:

| Method | Description | Type |
| ----------------------- | ------------------ | -----   |
| getBytesTransferred     | Gets the number of uploaded bytes.  | long   |
| getTotalBytesToTransfer | Gets the total number of bytes of the file. | long   |
| getPercentTransferred   | Gets the percentage of the number of uploaded bytes.  | double |

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are as described below:

| Request Member | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).  | String |
| key | Constructor or set method | Unique identifier of the object in the bucket. <br>For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | File metadata | ObjectMetadata |
| trafficLimit | Set method | Traffic limit on the uploaded object in bit/s. There is no limit by default. | Int | No |

#### Returned values

- Success: `Upload` is returned. You can query whether the upload is complete, or wait for the upload to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameter description

The `UploadResult` class records the information of the uploaded object requested by calling the `waitForUploadResult()` method from the `Upload` class. Its main members are as described below:

| Member | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Unique identifier of the object in the bucket. <br/>For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| requestId  | Request ID                                                       | String |
| dateStr    | Current server time                                             | String |
| versionId  | Version ID of the object returned when the bucket has versioning enabled | String |
| crc64Ecma  | CRC64 value computed by the server based on the object content                           | String |

### Pausing, resuming, or canceling upload

This API can be used to pause, resume, or cancel an upload job.

> ?
> - A stream upload cannot be paused, resumed, or canceled.
> - An upload in whole cannot be paused, resumed, or canceled.
> - An encrypted upload cannot be paused, resumed, or canceled.

#### Method prototype

```java
// Upload an object.
public Upload upload(final PutObjectRequest putObjectRequest)
            throws CosServiceException, CosClientException;
```

#### Sample request

```java
// Before using the advanced API, you must make sure that the process contains a TransferManager instance; if not, then create one.
// For the detailed code, see **Advanced API** > **Creating TransferManager instance** in this document.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";
// Local file path.
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

try {
    // The advanced API will return an async result `Upload`.
    Upload upload = transferManager.upload(putObjectRequest);
    // Wait three seconds for part of the file to be uploaded.
    Thread.sleep(3000);
    // Pause the upload and get a `PersistableUpload` instance for resuming the upload later.
    PersistableUpload persistableUpload = upload.pause();
    // Complex pausing and resuming:
    // `PersistableUpload` instance can be used to serialize the file content and store it and then deserialize it to resume the upload.
    // persistableUpload.serialize(out);
    // Resume the upload.
    upload = transferManager.resumeUpload(persistableUpload);
    // Capture possible exceptions.
    UploadResult uploadResult = upload.waitForUploadResult();

    // Or directly cancel the upload.
    // upload.abort();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced API** > **Shutting down TransferManager instance** in this document.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are as described below:

| Request Member | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).  | String |
| key | Constructor or set method | Unique identifier of the object in the bucket. <br>For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| file | Constructor or set method | Local file | File |
| input | Constructor or set method | Input stream | InputStream |
| metadata | Constructor or set method | File metadata | ObjectMetadata |
| trafficLimit | Set method | Traffic limit on the uploaded object in bit/s. There is no limit by default. | Int | No |

#### Returned values

- Success: `Upload` is returned. You can query whether the upload is complete, or wait for the upload to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameter description

The `UploadResult` class records the information of the uploaded object requested by calling the `waitForUploadResult()` method from the `Upload` class. Its main members are as described below:

| Member | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Unique identifier of the object in the bucket. <br/>For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| requestId  | Request ID                                                       | String |
| dateStr    | Current server time                                             | String |
| versionId  | Version ID of the object returned when the bucket has versioning enabled | String |
| crc64Ecma  | CRC64 value computed by the server based on the object content                           | String |

### Uploading local directory

A TransferManager instance encapsulates the feature of reading files from a local directory and uploading them to COS. This feature can upload files without destroying the directory structure. You can also upload files from one directory to another directory.

>? Recursive directory upload is supported. If the uploaded directory is too large, the upload may be slow or blocked for a long time. When you upload a directory recursively, we recommend you upload a directory with a small capacity (for example, 1,024 or fewer files). When you upload a directory with a large capacity, we recommend you split it into multiple small directories for call in batches.
>

#### Method prototype

```java
public MultipleFileUpload uploadDirectory(String bucketName, String virtualDirectoryKeyPrefix,
            File directory, boolean includeSubdirectories);
```

#### Sample request

```java
// Before using the advanced API, you must make sure that the process contains a TransferManager instance; if not, then create one.
// For the detailed code, see **Advanced API** > **Creating TransferManager instance** in this document.
TransferManager transferManager = createTransferManager();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

// Set the prefix of the directory to upload the files to. If this parameter is set to `""`, the files will be uploaded to the root directory of the bucket.
String cos_path = "/prefix";
// Absolute path of the folder to be uploaded.
String dir_path = "/path/to/localdir";
// Whether to upload the subdirectories in the directory recursively. If this parameter is set to `true`, the files in the subdirectories will also be uploaded with the original directory structure unchanged.
Boolean recursive = false;

try {
    // Return an async result `Upload`. You can synchronously call `waitForUploadResult` to wait for the upload to complete. If the upload is successful, `UploadResult` will be returned; otherwise, an exception will be reported.
    MultipleFileUpload upload = transferManager.uploadDirectory(bucketName, cos_path, new File(dir_path), recursive);

    // You can choose to view the upload progress. For more information on the function, see **Advanced API** > **Uploading file** > **Displaying the upload progress**.
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

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced API** > **Shutting down TransferManager instance** in this document.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------------- | -------------------- | ---------------- |
| bucketName                | Name of the bucket in COS | GetObjectRequest |
| virtualDirectoryKeyPrefix | Prefix of the objects in COS | String           |
| directory                 | Absolute path of the folder to be uploaded | File             |
| includeSubDirectory       | Whether to upload subdirectories recursively | Boolean          |

#### Returned values

- Success: `MultipleFileUpload` is returned. You can query whether the upload is complete, or wait for the upload to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Simple Operations

Requests for simple operations need to be initiated through `COSClient` instances. You need to create a `COSClient` instance before performing simple operations.

`COSClient` instances are concurrency safe. We recommend you create only one `COSClient` instance for a process and then shut it down when it is no longer used to initiate requests.

### Creating COSClient instance

Before calling the COS API, first create a `COSClient` instance.

```java
// Create a `COSClient` instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Set the user identity information.
    // Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SECRETID` and `SECRETKEY` of your project.
    String secretId = "SECRETID";
    String secretKey = "SECRETKEY";
    COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, visit https://cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol to `http` or `https`.
    // For v5.6.53 or earlier, HTTPS is recommended.
    // For v5.6.54 or later, HTTPS is used by default.
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // The following settings are optional:

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

### Creating COSClient instance with temporary key

If you want to request COS with a temporary key, you need to create a `COSClient` instance with the temporary key.
This SDK does not generate temporary keys. For directions on how to generate a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

```java

// Create a `COSClient` instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Here, the temporary key information is needed.
    // For directions on how to generate a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
    String tmpSecretId = "TMPSECRETID";
    String tmpSecretKey = "TMPSECRETKEY";
    String sessionToken = "SESSIONTOKEN";

    COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, visit https://cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol to `http` or `https`.
    // For v5.6.53 or earlier, HTTPS is recommended.
    // For v5.6.54 or later, HTTPS is used by default.
    clientConfig.setHttpProtocol(HttpProtocol.https);

    // The following settings are optional:

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

### Uploading local file

The upload source is a local file.

#### Method prototype

```java
// Method 1. Upload a local file to COS.
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// Method 2. Upload an input stream to COS.
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// Method 3. Encapsulate the two methods above to support more fine-grained parameter control, such as `content-type` and `content-disposition`.
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, make sure that the process contains a `COSClient` instance; if not, create one.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** in this document.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";
// Local file path.
String localFilePath = "/path/to/localFile";
File localFile = new File(localFilePath);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);

// Set the storage class, which can be STANDARD (default value) or STANDARD_IA. You can also ignore this line as appropriate.
// For more information on storage classes, visit https://cloud.tencent.com/document/product/436/33417.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);

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

// After confirming that the process no longer uses the `COSClient` instance, shut it down.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are as described below:

| Request Member | Configuration Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  | Description                                                     | Type   | Required |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| key | Constructor or set method | Unique identifier of the object in the bucket. <br>For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| file | Constructor or set method | Local file | File | No |
| input | Constructor or set method | Input stream | InputStream | No |
| metadata | Constructor or set method | Object metadata | ObjectMetadata | No |
| trafficLimit | Set method | Traffic limit on the uploaded object in bit/s. There is no limit by default. | Int | No |
|storageClass | Set method | Storage class | String | No |

The `ObjectMetadata` class is used to record the metadata of an object. Its main members are as described below:

| Member | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache expiration time, which has the same value as the `Expires` field in the HTTP response header | Date |
| ongoingRestore | Indicates that the object is being restored from the ARCHIVE storage class | Boolean |
| userMetadata | Custom metadata prefixed with `x-cos-meta-` | Map&lt;String, String&gt; |
| metadata | Headers other than custom metadata | Map&lt;String, String&gt; |
| restoreExpirationTime  | Expiration time for an object copy restored from ARCHIVE | Date |

#### Response description

- Success: `PutObjectResult` is returned, including the file `eTag`.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameter description

The `PutObjectResult` class is used to return the result information. Its main members are as described below:

| Member | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | Request ID | String |
| dateStr  | Current server time | String |
| versionId | Version ID of the object returned when the bucket has versioning enabled | String |
| eTag        | The object's MD5 value returned by the simple upload API, such as `09cba091df696af91549de27b8e7d0f6`. **Note: Although the value of the `ETag` response header has double quotation marks, the value of the parsed `eTag` string here doesn't.* * | String |
| crc64Ecma | CRC64 value computed by the server based on the object content | String |

### Uploading stream

The upload source is a stream instance of the `InputStream` type (and its subtypes).

#### Method prototype

```java
// Method 1. Upload a local file to COS.
public PutObjectResult putObject(String bucketName, String key, File file)
            throws CosClientException, CosServiceException;
// Method 2. Upload an input stream to COS.
public PutObjectResult putObject(String bucketName, String key, InputStream input, ObjectMetadata metadata)
            throws CosClientException, CosServiceException;
// Method 3. Encapsulate the two methods above to support more fine-grained parameter control, such as `content-type` and `content-disposition`.
public PutObjectResult putObject(PutObjectRequest putObjectRequest)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, make sure that the process contains a `COSClient` instance; if not, create one.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** in this document.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";

// Here, a `ByteArrayInputStream` stream is created as an example. In practice, you should create a stream of the `InputStream` type for upload.
long inputStreamLength = 1024 * 1024;
byte data[] = new byte[inputStreamLength];
InputStream inputStream = new ByteArrayInputStream(data);

ObjectMetadata objectMetadata = new ObjectMetadata();
// If you can get the exact length of the uploaded stream, we recommend you enter `Content-Length`.
// Otherwise, the following line can be omitted, but the advanced API cannot use multipart upload.
objectMetadata.setContentLength(inputStreamLength);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, inputStream, objectMetadata);

// Set the storage class, which can be STANDARD (default value) or STANDARD_IA. You can also ignore this line as appropriate.
// For more information on storage classes, visit https://cloud.tencent.com/document/product/436/33417.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);

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

// After confirming that the process no longer uses the `COSClient` instance, shut it down.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | ------------ | ---------------- |
| putObjectRequest | File upload request | PutObjectRequest |

The request members are as described below:

| Request Member | Configuration Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  | Description                                                     | Type   | Required |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| key | Constructor or set method | Unique identifier of the object in the bucket. <br>For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| file | Constructor or set method | Local file | File | No |
| input | Constructor or set method | Input stream | InputStream | No |
| metadata | Constructor or set method | Object metadata | ObjectMetadata | No |
| trafficLimit | Set method | Traffic limit on the uploaded object in bit/s. There is no limit by default. | Int | No |
|storageClass | Set method | Storage class | String | No |

The `ObjectMetadata` class is used to record the metadata of an object. Its main members are as described below:

| Member | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| httpExpiresDate | Cache expiration time, which has the same value as the `Expires` field in the HTTP response header | Date |
| ongoingRestore | Indicates that the object is being restored from the ARCHIVE storage class | Boolean |
| userMetadata | Custom metadata prefixed with `x-cos-meta-` | Map&lt;String, String&gt; |
| metadata | Headers other than custom metadata | Map&lt;String, String&gt; |
| restoreExpirationTime  | Expiration time for an object copy restored from ARCHIVE | Date |

#### Response description

- Success: `PutObjectResult` is returned, including the file `eTag`.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameter description

The `PutObjectResult` class is used to return the result information. Its main members are as described below:

| Member | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| requestId | Request ID | String |
| dateStr  | Current server time | String |
| versionId | Version ID of the object returned when the bucket has versioning enabled | String |
| eTag        | The object's MD5 value returned by the simple upload API, such as `09cba091df696af91549de27b8e7d0f6`. **Note: Although the value of the `ETag` response header has double quotation marks, the value of the parsed `eTag` string here doesn't.* * | String |
| crc64Ecma | CRC64 value computed by the server based on the object content | String |

### Creating directory

COS does not have the concept of directory itself, but you can consider object paths separated with slashes (/) as virtual directories.

>?
> - If you need a directory, you can upload a file to the desired directory, and the directory will be automatically created. For example, if you upload a file like `/dir/example.txt`, the `/dir` directory will be generated automatically. For more information, see "Uploading local file" in this document.
> 

If you need a directory with no files, you can upload an empty stream to a path ending with a slash (/), and then you will have a virtual directory.

```java
// Before using the COS API, make sure that the process contains a `COSClient` instance; if not, create one.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** in this document.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Specify the path of the directory to be created.
String key = "/example/dir/";

// Create an empty `ByteArrayInputStream` as an example.
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

// After confirming that the process no longer uses the `COSClient` instance, shut it down.
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
// Before using the COS API, make sure that the process contains a `COSClient` instance; if not, create one.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** in this document.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";

// Suppose the contents of these two files need to be appended for upload.
File part1File = new File("/path/to/part1File");
File part2File = new File("/path/to/part2File");

try {
    AppendObjectRequest appendObjectRequest = new AppendObjectRequest(bucketName, key, part1File);
    appendObjectRequest.setPosition(0L);
    AppendObjectResult appendObjectResult = cosClient.appendObject(appendObjectRequest);
    long nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);

    appendObjectRequest = new AppendObjectRequest(bucketName, key, part2File);
    appendObjectRequest.setPosition(nextAppendPosition);
    appendObjectResult = cosClient.appendObject(appendObjectRequest);
    nextAppendPosition = appendObjectResult.getNextAppendPosition();
    System.out.println(nextAppendPosition);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
// Shut down the client.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| -------------------- | ------------ | ---------------- |
| appendObjectRequest | Request to append object parts | AppendObjectRequest |

The members of `AppendObjectRequest` are as described below:

| Request Member | Configuration Method | Description | Type | Required |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |---|
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| key | Constructor or set method | Unique identifier of the object in the bucket. <br>For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| localfile | Constructor or set method | Local file | File | No |
| input | Constructor or set method | Input stream | InputStream | No |
| metadata | Constructor or set method | Object metadata | ObjectMetadata | No |
| trafficLimit | Set method | Traffic limit on the uploaded object in bit/s. There is no limit by default. | Int | No |
| position | Set method | Starting position of the append in bytes | Long | Yes |

#### Response description

- Success: `AppendObjectResult`.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameter description

The `AppendObjectResult` class is used to return the result information. Its main members are as described below:

| Member | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| metadata | Response header | ObjectMetadata               |
| nextAppendPosition| Position of the next append | Long |

### Uploading object by using HTML form

This API is used to upload an object by using an HTML form.

#### Constructing form body for upload

This API is used to construct the form body part at the very beginning according to the form parameters.

```java
String buildPostObjectBody(String boundary, Map<String, String> formFields, String filename, String contentType) {
    StringBuffer stringBuffer = new StringBuffer();
    for(Map.Entry entry: formFields.entrySet()) {
        // Add a boundary line starting with `--`.
        stringBuffer.append("--").append(boundary).append("\r\n");
        // Field name
        stringBuffer.append("Content-Disposition: form-data; name=\""
                + entry.getKey() + "\"\r\n\r\n");
        // Field value
        stringBuffer.append(entry.getValue() + "\r\n");
    }
    // Add a boundary line starting with `--`.
    stringBuffer.append("--").append(boundary).append("\r\n");
    // Filename
    stringBuffer.append("Content-Disposition: form-data; name=\"file\"; "
            + "filename=\"" + filename + "\"\r\n");
    // File type
    stringBuffer.append("Content-Type: " + contentType + "\r\n\r\n");
    return stringBuffer.toString();
}
```

#### Uploading local file

```java
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// For more information on COS regions, visit https://cloud.tencent.com/document/product/436/6224.
String endpoint = "cos.{COS_REGION}.myqcloud.com";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";
// The `SECRETID` and `SECRETKEY` can be viewed and managed in the CAM console.
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

// Construct a policy. For more information, visit https://intl.cloud.tencent.com/document/product/436/14690.
String policy = "{\n" +
        "    \"expiration\": \"" + endTimestampStr + "\",\n" +
        "    \"conditions\": [\n" +
        "        { \"bucket\": \"" + bucketName + "\" },\n" +
        "        { \"q-sign-algorithm\": \"sha1\" },\n" +
        "        { \"q-ak\": \"" + secretId + "\" },\n" +
        "        { \"q-sign-time\":\"" + keyTime + "\" }\n" +
        "    ]\n" +
        "}";

// The policy needs to be Base64-encoded before being placed to the form.
String encodedPolicy = new String(Base64.encodeBase64(policy.getBytes()));
// Set the policy.
formFields.put("policy", encodedPolicy);
// Calculate the signature according to the encoded policy and `secretKey`.
COSSigner cosSigner = new COSSigner();
String signature = cosSigner.buildPostObjectSignature(seretKey,
        keyTime, policy);
// Set the signature.
formFields.put("q-signature", signature);

// Construct the body part at the very beginning according to the form parameters above.
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

    // Write the file content to the output stream.
    File file = new File(localFilePath);
    DataInputStream in = new DataInputStream(new FileInputStream(file));
    int readBytes;
    byte[] bytes = new byte[4096];
    while ((readBytes = in.read(bytes)) != -1) {
        out.write(bytes, 0, readBytes);
    }
    in.close();

    // Add the last separator starting and ending with `--`.
    byte[] endData = ("\r\n--" + boundary + "--\r\n").getBytes();
    out.write(endData);
    out.flush();
    out.close();

    // Read the response headers.
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

>? If you want the uploaded file or stream to be obtained as a whole, advanced APIs are recommended.
>

### Directions

#### Performing multipart upload

1. Initialize the multipart upload with `Initiate Multipart Upload` to get the `UploadId`.
2. Use the `UploadId` to upload the parts with `Upload Part`.
3. Complete the multipart upload with `Complete Multipart Upload`.

#### Resuming multipart upload

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the file.
2. Use the `UploadId` to list the uploaded parts with `List Parts`.
3. Use the `UploadId` to upload the remaining parts with `Upload Part`.
4. Complete the multipart upload with `Complete Multipart Upload`.

#### Aborting multipart upload

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the file.
2. Abort the multipart upload and delete the uploaded parts with `Abort Multipart Upload`.

### Initializing multipart upload

This API is used to initialize a multipart upload to get the `uploadId` for subsequent operations.

#### Method prototype

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, make sure that the process contains a `COSClient` instance; if not, create one.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** in this document.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";

InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(bucketName, key);

// During a multipart upload, you can specify the metadata of an uploaded file only by initializing the multipart upload.
// Specify the desired headers.
ObjectMetadata objectMetadata = new ObjectMetadata();
request.setObjectMetadata(objectMetadata);

try {
    InitiateMultipartUploadResult initResult = cosClient.initiateMultipartUpload(request);
    // Get the `uploadid`.
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

The request members are as described below:

| Parameter | Configuration Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Constructor or set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg` | String |

#### Response description

- Success: `InitiateMultipartUploadResult` is returned, including the `uploadId` that identifies the multipart upload.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Querying multipart uploads

This API (`List Multipart Uploads`) is used to get all ongoing multipart upload jobs to find the `uploadId` of the desired multipart upload job.

#### Method prototype

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### Sample request

```java
// Before using the COS API, make sure that the process contains a `COSClient` instance; if not, create one.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** in this document.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

// Key of the multipart upload jobs to be queried
String targetKey = "targetKey";

ListMultipartUploadsRequest listMultipartUploadsRequest = new ListMultipartUploadsRequest(bucketName);
// Maximum number of multipart upload jobs that can be listed per request
listMultipartUploadsRequest.setMaxUploads(100);
// Set the target prefix (key) of the multipart upload jobs to be queried.
listMultipartUploadsRequest.setPrefix("targetKey");

MultipartUploadListing multipartUploadListing = null;

boolean found = false;

do {
    multipartUploadListing = cosClient.listMultipartUploads(listMultipartUploadsRequest);
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

The request members are as described below:

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| bucketName |  Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| keyMarker | Specifies the key after which the listing should begin | String |
| delimiter | A symbol. If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed. If no prefix is specified, the listing will start from the beginning of the path. | String |
| prefix | Specifies that the returned object key must be prefixed with this value. Note that when you use a prefix to query object keys, the returned key will contain the same prefix. | String |
| uploadIdMarker | The `UploadId` after which the listing should begin | String |
| maxUploads | The maximum number of multipart uploads that can be returned. Value range: 1–1000. | String |
| encodingType | Encoding type of the returned value. Valid value: `url`. | String |

#### Response description

- Success: `MultipartUploadListing` is returned, including the information of the ongoing multipart uploads.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Uploading parts

This API (`Upload Part`) is used to upload an object in parts.

#### Method prototype

```java
public UploadPartResult uploadPart(UploadPartRequest uploadPartRequest) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, make sure that the process contains a `COSClient` instance; if not, create one.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** in this document.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";
// `uploadId` is the unique identifier of a multipart upload job, which can be obtained by initializing the multipart upload or querying the multipart upload job.
String uploadId = "exampleuploadid";

// An ETag will be returned after each part is uploaded. It can be saved and used to combine the parts later.
List<PartETag> partETags = new LinkedList<>();

// Upload data. Here, ten parts (1 MB each) are uploaded.
for (int i = 1; i <= 10; i++) {
    byte data[] = new byte[1024 * 1024];
    // Here, a `ByteArrayInputStream` stream is created as an example. In practice, you should create a stream of the `InputStream` type for upload.
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
    // Set the part number, starting from 1.
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

The request members are as described below:

| Parameter | Configuration Method | Description | Type |
| ----------- | -------- | ------------------------------------------------------------ | ----------- |
| bucketName | Set method  | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg` | String |
| uploadId | Set method | Identifies the specified multipart upload | String |
| partNumber | Set method | Number (≥1) that identifies the specified part | int |
| inputStream | Set method | Input stream to be uploaded in parts | InputStream |
| trafficLimit | Set method | Traffic limit on the uploaded parts in bit/s. There is no limit by default. | Int |

#### Response description

- Success: `UploadPartResult` is returned, including the ETags of the uploaded parts.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameter description

The `UploadPartResult` class is used to return the result information. Its main members are as described below:

| Member | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| partNumber | Number that identifies the specified part | String                |
| eTag        | MD5 checksum of the uploaded part                   | String |
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
// Before using the COS API, make sure that the process contains a `COSClient` instance; if not, create one.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** in this document.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";
// `uploadId` is the unique identifier of a multipart upload job, which can be obtained by initializing the multipart upload or querying the multipart upload job.
String uploadId = "exampleuploadid";

// It is used to save the information of all uploaded parts.
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

| Parameter  | Configuration Method | Description | Type |
| ---------------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Constructor or set method | Object name | String |
| uploadId | Constructor or set method | `uploadId` of the multipart upload to be queried | String |
| maxParts | Set method | Maximum number of entries that can be returned at a time. Default value: `1000`. | String |
| partNumberMarker | Set method | By default, entries are listed in UTF-8 binary order, starting from the part number after the marker. | String |
| encodingType | Set method | Encoding type of the returned value | String |

#### Response description

- Success: `PartListing` is returned, including the ETag and number of each part as well as the starting marker of the next listing.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Completing multipart upload

This API (`Complete Multipart Upload`) is used to complete the multipart upload of a file.

>? After the multipart upload is completed, the multipart upload job will be deleted, and the `UploadId` will be no longer valid.
>

#### Method prototype

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, make sure that the process contains a `COSClient` instance; if not, create one.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** in this document.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";
// `uploadId` is the unique identifier of a multipart upload job, which can be obtained by initializing the multipart upload or querying the multipart upload job.
String uploadId = "exampleuploadid";

// It is used to store the information of the uploaded parts, which can be obtained from the multipart upload API.
List<PartETag> partETags = new LinkedList<>();

// After the multipart upload is completed, call `complete` to complete the upload.
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

// After confirming that the COSClient instance will be no longer used, shut it down.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Configuration Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Constructor or set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg`. | String |
| uploadId | Constructor or set method | Identifies the specified multipart upload | String |
| partETags  | Constructor or set method | Identifies the number and ETag returned for an uploaded part | List&lt;PartETag&gt; |

#### Response description

- Success: `CompleteMultipartUploadResult` is returned, including the ETag of the completed object.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Aborting multipart upload

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts.

>? After a multipart upload is aborted, both the multipart upload job and the uploaded parts will be deleted, and the `UploadId` will be no longer valid.
>

#### Method prototype

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, make sure that the process contains a `COSClient` instance; if not, create one.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** in this document.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket.
String key = "exampleobject";
// `uploadId` is the unique identifier of a multipart upload job, which can be obtained by initializing the multipart upload or querying the multipart upload job.
String uploadId = "exampleuploadid";

AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
try {
    cosClient.abortMultipartUpload(abortMultipartUploadRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// After confirming that the COSClient instance will be no longer used, shut it down.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Configuration Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Constructor or set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg` | String |
| uploadId | Constructor or set method | Identifies the specified multipart upload | String |

#### Response description

- Success: No value is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
