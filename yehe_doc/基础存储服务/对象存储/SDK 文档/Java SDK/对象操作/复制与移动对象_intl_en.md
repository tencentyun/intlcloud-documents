## Overview

This document provides an overview of APIs and SDK code samples for copying and moving an object.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product//436/10881) | Copying object | Copies object to destination path. |

**Multipart upload operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product//436/7736) | Querying multipart uploads/copies | Queries multipart uploads/copies in progress. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product//436/7746) | Initializing multipart upload/copy operation | Initializes multipart upload/copy operation. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product//436/8287) | Copying part | Copies object as part. |
| [List Parts](https://intl.cloud.tencent.com/document/product//436/7747) | Querying uploaded/copied parts | Queries uploaded/copied parts of multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product//436/7742) | Completing multipart upload/copy | Completes multipart upload/copy. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product//436/7740) | Aborting multipart upload/copy | Aborts multipart upload operation and deletes uploaded/copied parts. |

## Advanced APIs (Recommended)

The advanced APIs encapsulate simple APIs via the TransferManager class to provide APIs for easier operations. Internally, a thread pool is used to concurrently accept and process requests, so you can choose to execute tasks asynchronously after submitting multiple tasks.

TransferManager instances are concurrency safe. We recommend you create only one TransferManager instance for a process and then shut it down when it is no longer used to call advanced APIs.

### Feature description

The advanced APIs encapsulate the APIs for copy in whole and multipart copy and automatically select the copy method based on the file size.

### Creating TransferManager instance

Before using advanced APIs, you must create a TransferManager instance first.

```java
// Create a TransferManager instance, which is used to call advanced APIs later.
TransferManager createTransferManager() {
    // Create a COSClient client, which is the basic instance for accessing the COS service.
    // The COSClient instance created here is based on the information of the destination for copying.
    // For the detailed code, see **Simple Operations** > **Creating COSClient instance** on this page.
    COSClient cosClient = createCOSClient();

    // Set the thread pool size. We recommend you set the size of your thread pool to 16 or 32 to maximize network resource utilization, provided your client and COS networks are sufficient (for example, uploading a file to a COS bucket from a CVM instance in the same region).
    // We recommend you use a smaller value to avoid timeout caused by slow network speed if you are transferring data over a public network with poor bandwidth quality.
    ExecutorService threadPool = Executors.newFixedThreadPool(32);

    // Pass a `threadpool`; otherwise, a single-thread pool will be generated in `TransferManager` by default.
    TransferManager transferManager = new TransferManager(cosClient, threadPool);

    // Set the configuration items of the advanced API.
    // Set the threshold and part size for multipart copy to 5 MB and 1 MB respectively.
    TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
    transferManagerConfiguration.setMultipartCopyThreshold(5*1024*1024);
    transferManagerConfiguration.setMultipartCopyPartSize(1*1024*1024);
    transferManager.setConfiguration(transferManagerConfiguration);

    return transferManager;
}
```

### Parameter description

The `TransferManagerConfiguration` class is used to record the configuration information of advanced APIs. Its main members are as described below:

| Member Name | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize | Set method | Part size of the multipart upload in bytes. Default value: 5 MB. | long |
| multipartUploadThreshold | Set method | If a file is greater than or equal to this value in bytes, it will be uploaded in concurrent parts. Default value: 5 MB. | long |
| multipartCopyThreshold | Set method | If a file is greater than or equal to this value in bytes, it will be copied in concurrent parts. Default value: 5 GB. | long |
| multipartCopyPartSize | Set method | Part size in bytes for multipart copy. Default value: 100 MB. | long |

### Shutting down TransferManager instance

After confirming that the process no longer uses the TransferManager instance to call advanced APIs, be sure to shut it down to avoid resource leakage.

```java
void shutdownTransferManager(TransferManager transferManager) {
    // If the parameter is set to `true`, the COSClient instance in the TransferManager instance will also be shut down at the same time.
    // If the parameter is set to `false`, the COSClient instance in the TransferManager instance will not be shut down.
    transferManager.shutdownNow(true);
}
```

### Intra-region replication

Intra-region replication is possible only when the source and destination objects belong to the same region.

#### Method prototype

```java
// Upload an object.
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### Sample request

```java
// Before using advanced APIs, you must make sure that the process contains a TransferManager instance; if not, then create one.
// For the detailed code, see **Advanced APIs** > **Creating TransferManager instance** on this page.
TransferManager transferManager = createTransferManager();
// Source bucket region.
Region srcBucketRegion = new Region("ap-beijing");
// Enter the source bucket name in the format of `BucketName-APPID`.
String srcBucketName = "srcbucket-1250000000";
// Source file path.
String srcKey = "path/srckey";

// Enter the destination bucket name in the format of `BucketName-APPID`.
String destBucketName = "destbucket-1250000000";
// Destination file path.
String destKey = "path/destkey";

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest);
    // The advanced API returns an asynchronous result `Copy`.
    // You can synchronously call `waitForCopyResult` to wait for the copy to complete. If the copy is successful, `CopyResult` is returned; otherwise, an exception will be reported.
    CopyResult copyResult = copy.waitForCopyResult();
    System.out.println(copyResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced APIs** > **Shutting down TransferManager instance** on this page.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | Object copy request | CopyObjectRequest |

The request members are as described below:

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default value: The value of `region` in `clientconfig`, indicating intra-region replication. | String |
| sourceBucketName  | Source bucket name in the format of `BucketName-APPID` | String |
| sourceKey        | Unique identifier of the source object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324). | String |
| sourceVersionId | Version number of the source file (for source buckets with versioning enabled). Default value: The latest version of the source file. | String |
| destinationBucketName  | Destination bucket name in the format of `BucketName-APPID`. | String |
| destinationKey        | Unique identifier of the destination object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324). | String |
| storageClass | Storage class of the destination file, such as `STANDARD` (default) and `STANDARD_IA`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product//436/30925). | String |

#### Returned values

- Success: `Copy` is returned. You can query whether the copy is complete, or wait for the copy to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product//436/31537).

### Cross-region replication

Cross-region replication is possible only when the source and destination objects belong to different regions, for example, when you want to copy an object from the Beijing bucket to the Shanghai bucket.

>? Cross-region replication is not supported between Finance Cloud regions and Public Cloud regions because these regions are not interconnected.
>

#### Method prototype

```java
// Upload an object.
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### Sample request

```java
// The COSClient instance created here is based on the information of the destination for copying.
// Before using advanced APIs, you must make sure that the process contains a TransferManager instance; if not, then create one.
// For the detailed code, see **Advanced APIs** > **Creating TransferManager instance** on this page.
TransferManager transferManager = createTransferManager();
// Source bucket region.
Region srcBucketRegion = new Region("ap-beijing");
// Enter the source bucket name in the format of `BucketName-APPID`.
String srcBucketName = "srcbucket-1250000000";
// Source file path.
String srcKey = "path/srckey";

// Note: The region of the destination bucket is set through the `createTransferManager() -> createCOSClient() -> clientConfig.setRegion(dstRegion)` function when TransferManager/COSClient is created.
// Enter the destination bucket name in the format of `BucketName-APPID`.
String destBucketName = "destbucket-1250000000";
// Destination file path.
String destKey = "path/destkey";

// The COSClient instance created here is based on the information of the source for copying.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** on this page.
COSClient srcCOSClient = createCOSClient();

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
    // The advanced API returns an asynchronous result `Copy`.
    // You can synchronously call `waitForCopyResult` to wait for the copy to complete. If the copy is successful, `CopyResult` is returned; otherwise, an exception will be reported.
    CopyResult copyResult = copy.waitForCopyResult();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced APIs** > **Shutting down TransferManager instance** on this page.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | Object copy request | CopyObjectRequest |

The request members are as described below:

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default value: The value of `region` in `clientconfig`, indicating intra-region replication. | String |
| sourceBucketName  | Source bucket name in the format of `BucketName-APPID` | String |
| sourceKey        | Unique identifier of the source object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324). | String |
| sourceVersionId | Version number of the source file (for source buckets with versioning enabled). Default value: The latest version of the source file. | String |
| destinationBucketName  | Destination bucket name in the format of `BucketName-APPID`. | String |
| destinationKey        | Unique identifier of the destination object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324). | String |
| storageClass | Storage class of the destination file, such as `STANDARD` (default) and `STANDARD_IA`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product//436/30925). | String |

#### Returned values

- Success: `Copy` is returned. You can query whether the copy is complete, or wait for the copy to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product//436/31537).

### Moving object

Object movement involves two steps: copying the source object to the destination location and then deleting the source object.

As COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS's Java SDK does not provide a standalone API to change object identifiers. However, you can still move an object through a combination of basic operations (**object copy** and **object delete**).

For example, if you want to move the `picture.jpg` object to the `doc` directory that is in the same bucket (`mybucket-1250000000`), you can copy the `picture.jpg` object to the `doc` directory first (making the object key `doc/picture.jpg`) and then delete the source object.

Similarly, if you want to move the `picture.jpg` object in the `mybucket-1250000000` bucket to another bucket `myanothorbucket-1250000000`, you can copy the object to the `myanothorbucket-1250000000` bucket first and then delete the source object.

#### Sample request

```java
// Source bucket region.
Region srcBucketRegion = new Region("ap-beijing");
// Enter the source bucket name in the format of `BucketName-APPID`.
String srcBucketName = "srcbucket-1250000000";
// Source file path.
String srcKey = "path/srckey";

// Destination bucket region.
Region destBucketRegion = new Region("ap-shanghai");
// Enter the destination bucket name in the format of `BucketName-APPID`.
String destBucketName = "destbucket-1250000000";
// Destination file path.
String destKey = "path/destkey";

// For the implementation details, see **Advanced APIs** > **Copying object** on this page.
copyObject();
// For the implementation details, see **Deleting object**.
deleteObject();
```

## Simple Operations

Requests for simple operations need to be initiated through `COSClient` instances. You need to create a `COSClient` instance before performing simple operations.

`COSClient` instances are concurrency safe. We recommend you create only one COSClient instance for a process and then shut it down when it is no longer used to initiate requests.

### Creating COSClient instance

Before calling the COS API, you must create a COSClient instance first.

```java
// Create a COSClient instance, which is used to initiate requests later.
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
    // For 5.6.53 and earlier versions, HTTPS is recommended.
    // Starting from 5.6.54, HTTPS is used by default.
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

If you want to request COS with a temporary key, you need to create a COSClient instance with the temporary key.
This SDK does not generate temporary keys. For how to generate a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product//436/14048).

```java

// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Here, the temporary key information is needed.
    // For directions on how to generate a temporary key, visit https://intl.cloud.tencent.com/document/product//436/14048.
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
    // For 5.6.53 and earlier versions, HTTPS is recommended.
    // Starting from 5.6.54, HTTPS is used by default.
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

### Copying object

This API (`PUT Object-Copy`) is used to copy an object to a destination path.

>? We recommend you use the advanced API for copying directly.
>

#### Method prototype

```java
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
            throws CosClientException, CosServiceException
```

#### Sample request

```java
// Source bucket region.
Region srcBucketRegion = new Region("ap-beijing");
// Enter the source bucket name in the format of `BucketName-APPID`.
String srcBucketName = "srcbucket-1250000000";
// Source file path.
String srcKey = "path/srckey";

// Destination bucket region.
Region destBucketRegion = new Region("ap-beijing");
// Enter the destination bucket name in the format of `BucketName-APPID`.
String destBucketName = "destbucket-1250000000";
// Destination file path.
String destKey = "path/destkey";

// Before using the COS API, you must make sure that the process contains a COSClient instance; if not, then create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see **Upload in Whole** > **Creating COSClient instance** on this page.
COSClient cosClient = createCOSClient();

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    CopyObjectResult copyObjectResult = cosClient.copyObject(copyObjectRequest);
    System.out.println(copyObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the COSClient instance, shut it down.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

The request members are as described below:

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default value: The value of `region` in `clientConfig`, indicating intra-region replication. | String |
| sourceBucketName | Source bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product//436/13312). | String |
| sourceKey        | Unique identifier of the source object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324). | String |
| sourceVersionId | Version number of the source file (for source buckets with versioning enabled). Default value: The latest version of the source file. | String |
| destinationBucketName | Destination bucket name in the format of `BucketName-APPID`, which can contain letters, numbers, and hyphens. | String |
| destinationKey        | Unique identifier of the destination object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324). | String |
| storageClass | Storage class of the destination file, such as `STANDARD` (default) and `STANDARD_IA`. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product//436/30925). | String |

#### Response description

- Success: `CopyObjectResult` is returned, which contains the `Etag` and other information of the new file.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product//436/31537).

## Multipart Upload Operations

When a large file is copied, the file is copied in a series of parts to eliminate the possible interruptions caused by the long upload time of the large file.

>? We recommend you use the advanced API for copying directly.
>

### Directions

#### Performing multipart copy

1. Initialize the multipart copy with `Initiate Multipart Upload` to get the `UploadId`.
2. Use the `UploadId` to copy the parts with `Upload Part`.
3. Complete the multipart copy with `Complete Multipart Upload`.

#### Resuming multipart copy

1. If you did not record the `UploadId` of the multipart copy, you can query the multipart copy job with `List Multipart Uploads` to get the `UploadId` of the file.
2. Use the `UploadId` to list the copied parts with `List Parts`.
3. Use the `UploadId` to copy the remaining parts with `Upload Part`.
4. Complete the multipart copy with `Complete Multipart Upload`.

#### Aborting multipart copy

1. If you did not record the `UploadId` of the multipart copy, you can query the multipart copy job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Abort the multipart copy and delete the copied parts with `Abort Multipart Upload`.

### Initializing multipart copy

This API is used to initialize a multipart copy and get the `UploadId` for subsequent operations.

#### Method prototype

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, you must make sure that the process contains a COSClient instance; if not, then create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** on this page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324).
String key = "exampleobject";

InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(bucketName, key);

// During multipart copy, you can specify the metadata of a copied file only by initializing the multipart copy.
// Specify the desired headers.
ObjectMetadata objectMetadata = new ObjectMetadata();
request.setObjectMetadata(objectMetadata);

try {
    InitiateMultipartUploadResult initResult = cosClient.initiateMultipartUpload(request);
    // Get `uploadid`.
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
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product//436/13312). | String |
| key | Constructor or set method | Path (i.e., [object key](https://intl.cloud.tencent.com/document/product//436/13324)) to upload the part to, such as  `folder/picture.jpg`. | String |

#### Response description

- Success: `InitiateMultipartUploadResult` is returned, which contains the `uploadId` that identifies the multipart upload.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product//436/31537).

### Querying multipart copy

This API (`List Multipart Uploads`) is used to get all multipart copy jobs in progress and get the `uploadId` of a desired multipart copy job.

#### Method prototype

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### Sample request

```java
// Before using the COS API, you must make sure that the process contains a COSClient instance; if not, then create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** on this page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

// Key of the multipart copy jobs to be queried.
String targetKey = "targetKey";

ListMultipartUploadsRequest listMultipartUploadsRequest = new ListMultipartUploadsRequest(bucketName);
// Maximum number of multipart upload jobs that can be listed per request.
listMultipartUploadsRequest.setMaxUploads(100);
// Set the target prefix (key) of the multipart copy jobs to be queried.
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
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product//436/13312). | String |
| keyMarker | Specifies the key where the list starts | String |
| delimiter | A symbol used to limit the results of a listing operation. If a prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed. If no prefix is specified, the listing will start from the beginning of the path. | String |
| prefix | Specifies that returned object keys must be prefixed with the value of this parameter. Note that if you use this parameter, returned keys will contain the prefix. | String |
| uploadIdMarker | Specifies the `uploadId` where the list starts | String |
| maxUploads | Sets the maximum number of multipart uploads that can be returned at a time. Value range: 1–1000. | String |
| encodingType | Encoding type of the returned value. Valid value: url. | String |

#### Response description

- Success: `MultipartUploadListing` is returned, which contains the information of the multipart uploads in progress.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product//436/31537).

### Copying object part

This API (`Upload Part - Copy`) is used to copy an object by parts.

#### Method prototype

```java
public CopyPartResult copyPart(CopyPartRequest copyPartRequest) throws CosClientException, CosServiceException
```

#### Sample request

```java
// Before using the COS API, you must make sure that the process contains a COSClient instance; if not, then create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** on this page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324).
String key = "exampleobject";
// `uploadId` is the unique identifier of a multipart copy job. It can be obtained by initializing the multipart copy or querying the multipart copy job.
String uploadId = "exampleuploadid";

// Source bucket region.
Region srcBucketRegion = new Region("ap-beijing");
// Enter the source bucket name in the format of `BucketName-APPID`.
String srcBucketName = "srcbucket-1250000000";
// Source file path.
String srcKey = "path/srckey";

// Destination bucket region.
Region destBucketRegion = new Region("ap-beijing");
// Enter the destination bucket name in the format of `BucketName-APPID`.
String destBucketName = "destbucket-1250000000";
// Destination file path.
String destKey = "path/destkey";

CopyPartRequest copyPartRequest = new CopyPartRequest();
copyPartRequest.setSourceBucketRegion(srcBucketRegion);
copyPartRequest.setSourceBucketName(srcBucketName);
copyPartRequest.setSourceKey(srcKey);

// Specify the scope of data in the source file to be copied (similar to `content-range`).
copyPartRequest.setFirstByte(0L);
copyPartRequest.setLastByte(1048575L);

copyPartRequest.setDestinationBucketName(destBucketName);
copyPartRequest.setDestinationKey(destKey);

// Set the part number for the current copy, which starts from 1.
copyPartRequest.setPartNumber(1);
copyPartRequest.setUploadId(uploadId);

try {
    CopyPartResult copyPartResult = cosClient.copyPart(copyPartRequest);
    PartETag partETag = copyPartResult.getPartETag();
    System.out.println(partETag);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```

#### Parameter description

| Parameter | Description | Type |
| --------------- | ---- | --------------- |
| copyPartRequest | Request | CopyPartRequest |

The request members are as described below:

| Parameter | Configuration Method | Description | Type |
| --------------------- | -------- | ------------------------------------------------------------ | ------ |
| destinationBucketName | Set method | Destination bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product//436/13312). | String |
| destinationKey | Set method | Name of the destination object (i.e., [object key](https://intl.cloud.tencent.com/document/product//436/13324)) to store the replicated part, such as `folder/picture.jpg`. | String |
| uploadId | Set method | ID that identifies the specified multipart upload | String |
| partNumber | Set method | Number (≥1) that identifies the specified part | int |
| sourceBucketRegion | Set method | Region of the source bucket | Region |
| sourceBucketName | Set method | Source bucket name | String |
| sourceKey | Set method | Name/Path (i.e., [object key](https://intl.cloud.tencent.com/document/product//436/13324)) of the source object before the replication, such as `folder/picture.jpg`. | String |
| firstByte | Set method | First byte offset of the source object | Long |
| lastByte | Set method | Last byte offset of the source object | Long |

#### Response description

- Success: `CopyPartResult` is returned, which contains the `ETag` of the part.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product//436/31537).

### Querying copied parts

This API (`List Parts`) is used to query the copied parts of a multipart copy.

#### Method prototype

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, you must make sure that the process contains a COSClient instance; if not, then create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** on this page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324).
String key = "exampleobject";
// `uploadId` is the unique identifier of a multipart copy job. It can be obtained by initializing the multipart copy or querying the multipart copy job.
String uploadId = "exampleuploadid";

// It is used to store the information of the copied parts.
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
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product//436/13312). | String |
| key | Constructor or set method | Object name | String |
| uploadId | Constructor or set method | `uploadId` of the multipart upload to be queried | String |
| maxParts | Set method | Maximum number of entries that can be returned at a time. Default value: 1000. | String |
| partNumberMarker | Set method | The marker after which the returned list begins. By default, entries are listed in UTF-8 binary order. | String |
| encodingType | Set method | Encoding type of the returned value. | String |

#### Response description

- Success: `PartListing` is returned, which contains the `ETag` and number of each part as well as the starting marker of the next list.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product//436/31537).

### Completing multipart copy

This API (`Complete Multipart Upload`) is used to complete a multipart copy.

>? After the multipart copy is complete, the multipart copy job will be deleted, and the `UploadId` of the job will no longer be valid.
>

#### Method prototype

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, you must make sure that the process contains a COSClient instance; if not, then create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** on this page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324).
String key = "exampleobject";
// `uploadId` is the unique identifier of a multipart copy job. It can be obtained by initializing the multipart copy or querying the multipart copy job.
String uploadId = "exampleuploadid";

// It is used to store the information of the uploaded parts and is obtained from the multipart upload API.
List<PartETag> partETags = new LinkedList<>();

// Call `complete` to complete the multipart copy after the multipart upload is complete.
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

// After confirming that the COSClient instance is no longer used, shut it down.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Configuration Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product//436/13312). | String |
| key | Constructor or set method | Path (i.e., [object key](https://intl.cloud.tencent.com/document/product//436/13324)) to upload the part to, such as  `folder/picture.jpg`. | String |
| uploadId | Constructor or set method | ID that identifies the specified multipart upload | String |
| partETags  | Constructor or set method | Number that identifies the specified part and `eTag` returned for it | List&lt;PartETag&gt; |

#### Response description

- Success: `CompleteMultipartUploadResult` is returned, which contains the `eTag` of the completed object.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product//436/31537).

### Aborting multipart copy

This API (`Abort Multipart Upload`) is used to abort a multipart copy and delete the copied parts.

>? After a multipart copy is aborted, both the multipart copy job and the copied parts will be deleted, and the `UploadId` will no longer be valid.
>

#### Method prototype

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, you must make sure that the process contains a COSClient instance; if not, then create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see **Simple Operations** > **Creating COSClient instance** on this page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product//436/13324).
String key = "exampleobject";
// `uploadId` is the unique identifier of a multipart copy job. It can be obtained by initializing the multipart copy or querying the multipart copy job.
String uploadId = "exampleuploadid";

AbortMultipartUploadRequest abortMultipartUploadRequest = new AbortMultipartUploadRequest(bucketName, key, uploadId);
try {
    cosClient.abortMultipartUpload(abortMultipartUploadRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// After confirming that the COSClient instance is no longer used, shut it down.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Configuration Method | Description | Type |
| ---------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product//436/13312). | String |
| key | Constructor or set method | Path (i.e., [object key](https://intl.cloud.tencent.com/document/product//436/13324)) to upload the part to, such as  `folder/picture.jpg`. | String |
| uploadId | Constructor or set method | ID that identifies the specified multipart upload | String |

#### Response description

- Success: No value is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product//436/31537).
