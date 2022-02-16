## Overview

This document provides an overview of APIs and SDK code samples related to object copy and movement.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to a destination path |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads/copy | Queries in-progress multipart uploads/copy. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload/copy operation | Initializes a multipart upload/copy operation. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded/copied parts | Queries the uploaded/copied parts of a multipart operation. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload/copy | Completes the multipart upload/copy of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload/copy | Aborts a multipart operation and deletes the uploaded/copied parts. |

## Advanced APIs (Recommended)

The advanced APIs encapsulate simple APIs via the TransferManager class to provide APIs for easier operations. Internally, a thread pool is used to concurrently accept and process requests from users, so users can choose to execute tasks asynchronously after submitting multiple tasks.

TransferManager instances are concurrency safe. You are advised to create only one TransferManager instance for a process and then close it when it is no longer used to call advanced APIs.

### Description

The advanced APIs encapsulate the simple copy and multipart copy APIs and automatically choose the copy mode based on the file size.

### Creating a TransferManager instance

Before using the advanced API, you need to create a TransferManager instance.

```java
// Create a TransferManager instance, which is used to call the advanced API later.
TransferManager createTransferManager() {
    // Create a COSClient client, which is the basic instance for accessing the COS service.
    // The COSClient instance created here is based on the information of the destination for copying.
    // For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
    COSClient cosClient = createCOSClient();

    // Set the thread pool size. You are advised to the size of your thread pool to 16 or 32 to maximize network resource utilization, provided your client and COS networks are sufficient (for example, by using Tencent Cloud CVM and uploading to COS in the same region).
    // We recommend using a smaller value to avoid timeout due to slow network speed if you are transferring data over a public network with poor bandwidth quality.
    ExecutorService threadPool = Executors.newFixedThreadPool(32);

    // Pass a threadpool. Otherwise, a single-thread pool will be generated in TransferManager by default.
    TransferManager transferManager = new TransferManager(cosClient, threadPool);

    // Set the configuration items of the advanced API.
    // Set the threshold and part size for multipart xopy to 5 MB and 1 MB respectively.
    TransferManagerConfiguration transferManagerConfiguration = new TransferManagerConfiguration();
    transferManagerConfiguration.setMultipartCopyThreshold(5*1024*1024);
    transferManagerConfiguration.setMultipartCopyPartSize(1*1024*1024);
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

### Intra-region replication

Intra-region replication is possible only when the source and destination objects belong to the same region.

#### Method prototype

```java
// Upload an object
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### Sample request

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Creating a TransferManager instance" on the current page.
TransferManager transferManager = createTransferManager();
// Source bucket region
Region srcBucketRegion = new Region("ap-beijing");
// Source bucket. Enter the bucket name in the format of `BucketName-APPID`.
String srcBucketName = "srcbucket-1250000000";
// Source file path
String srcKey = "path/srckey";

// Destination bucket. Enter the bucket name in the format of `BucketName-APPID`.
String destBucketName = "destbucket-1250000000";
// Destination file path
String destKey = "path/destkey";

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest);
    // The advanced API returns an asynchronous result `copy`.
    // You can synchronously call waitForCopyResult to wait for the replication to end. If the replication is successful, `CopyResult` is returned; otherwise, an exception will be thrown.
    CopyResult copyResult = copy.waitForCopyResult();
    System.out.println(copyResult.getRequestId());
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
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | Object copy request | CopyObjectRequest |

The request members are described as follows:

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default value: the value of "region" in `clientconfig`, meaning intra-region replication | String |
| sourceBucketName  | Source bucket name in the format of `BucketName-APPID` | String |
| sourceKey | Source object key. The object key is the unique identifier of the object in the bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| sourceVersionId | Version ID of the source file (for source buckets with versioning enabled). Default: The latest version of the source file. | String |
| destinationBucketName  | Destination bucket name in the format of `BucketName-APPID` | String |
| destinationKey | Destination object key. The object key is the unique identifier of the object in the bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| storageClass | Storage class for the destination file. For the enumerated values, such as `Standard` (default) and `Standard_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |

#### Returned values

- Success: returns Copy. You can query whether the copy is completed, or wait until the copy finishes synchronously.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Cross-region replication

This API applies to scenarios where the source and destination objects for replication belong to different regions, for example, when you need to replicate an object from the Beijing bucket to the Shanghai bucket.

>? Cross-region replication is not supported between Finance Cloud regions and Public Cloud regions because these regions are not interconnected.
>

#### Method prototype

```java
// Upload an object
public Copy copy(final CopyObjectRequest copyObjectRequest);
```

#### Sample request

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Creating a TransferManager instance" on the current page.
TransferManager transferManager = createTransferManager();
// Source bucket region
Region srcBucketRegion = new Region("ap-beijing");
// Source bucket. Enter the bucket name in the format of `BucketName-APPID`.
String srcBucketName = "srcbucket-1250000000";
// Source file path
String srcKey = "path/srckey";

// Destination bucket. Enter the bucket name in the format of `BucketName-APPID`.
String destBucketName = "destbucket-1250000000";
// Destination file path
String destKey = "path/destkey";

// The COSClient instance created here is based on the information of the replication source.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient srcCOSClient = createCOSClient();

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    Copy copy = transferManager.copy(copyObjectRequest, srcCOSClient, null);
    // The advanced API returns an asynchronous result `copy`.
    // You can synchronously call waitForCopyResult to wait for the replication to end. If the replication is successful, `CopyResult` is returned; otherwise, an exception will be thrown.
    CopyResult copyResult = copy.waitForCopyResult();
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
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | Object copy request | CopyObjectRequest |

The request members are described as follows:

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default value: the value of "region" in `clientconfig`, meaning intra-region replication | String |
| sourceBucketName  | Source bucket name in the format of `BucketName-APPID` | String |
| sourceKey | Source object key. The object key is the unique identifier of the object in the bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| sourceVersionId | Version ID of the source file (for source buckets with versioning enabled). Default: The latest version of the source file. | String |
| destinationBucketName  | Destination bucket name in the format of `BucketName-APPID` | String |
| destinationKey | Destination object key. The object key is the unique identifier of the object in the bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| storageClass | Storage class for the destination file. For the enumerated values, such as `Standard` (default) and `Standard_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |

#### Returned values

- Success: returns Copy. You can query whether the copy is completed, or wait until the copy finishes synchronously.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Moving an object

Object movement involves two steps: copying the source object to the destination location and then deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS’s Java SDK does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (**object copy** and **object delete**).

For example, if you want to move the `picture.jpg` object to the “doc” directory that is in the same bucket (`mybucket-1250000000`), you can copy the `picture.jpg` to the “doc” directory (making the object key `doc/picture.jpg`) and then delete the source object.

Likewise, if you need to move `picture.jpg` in the `mybucket-1250000000` bucket to another bucket `myanothorbucket-1250000000`, you can copy the object to the `myanothorbucket-1250000000` bucket first and then delete the source object.

#### Sample request

```java
// Source bucket region
Region srcBucketRegion = new Region("ap-beijing");
// Source bucket. Enter the bucket name in the format of `BucketName-APPID`.
String srcBucketName = "srcbucket-1250000000";
// Source file path
String srcKey = "path/srckey";

// Destination bucket region
Region destBucketRegion = new Region("ap-shanghai");
// Destination bucket. Enter the bucket name in the format of `BucketName-APPID`.
String destBucketName = "destbucket-1250000000";
// Destination file path
String destKey = "path/destkey";

// For the implementation details, see "Advanced APIs -> Copying objects" on the current page.
copyObject();
// For the implementation details, see "Deleting objects".
deleteObject();
```

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

### Copying objects

This API (`PUT Object-Copy`) is used to copy an object to a destination path.

>? It is recommended to use the advanced API for copying directly.
>

#### Method prototype

```java
public CopyObjectResult copyObject(CopyObjectRequest copyObjectRequest)
            throws CosClientException, CosServiceException
```

#### Sample request

```java
// Source bucket region
Region srcBucketRegion = new Region("ap-beijing");
// Source bucket. Enter the bucket name in the format of `BucketName-APPID`.
String srcBucketName = "srcbucket-1250000000";
// Source file path
String srcKey = "path/srckey";

// Destination bucket region
Region destBucketRegion = new Region("ap-beijing");
// Destination bucket. Enter the bucket name in the format of `BucketName-APPID`.
String destBucketName = "destbucket-1250000000";
// Destination file path
String destKey = "path/destkey";

// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see "Simple Upload -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    CopyObjectResult copyObjectResult = cosclient.copyObject(copyObjectRequest);
    System.out.println(copyObjectResult.getRequestId());
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the COSClient instance anymore, close it.
cosclient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------ | ----------------- |
| copyObjectRequest | File copy request | CopyObjectRequest |

The request members are described as follows:

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| sourceBucketRegion | Region of the source bucket. Default: same as the `region` value in the current clientConfig, which represents intra-region replication | String |
| sourceBucketName | Source bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| sourceKey | Source object key. An object key is the unique identifier of an object in a bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| sourceVersionId | Version ID of the source file (for source buckets with versioning enabled). Default: The latest version of the source file. | String |
| destinationBucketName | Destination bucket name in the format of `BucketName-APPID`. It should contain letters, numbers, and hyphens. | String |
| destinationKey | Destination object key. An object key is the unique identifier of an object in a bucket. For example, in the object’s access endpoint `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is `doc/picture.jpg`. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| storageClass | Storage class for the destination file. For the enumerated values, such as `Standard` (default) and `Standard_IA`, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String |

#### Response description

- Success: returns `CopyObjectResult`, including the ETag and other information on the new file.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

## Multipart Operations

When a large file is copied, the file is copied as a series of parts to address the possible interruptions caused by the long upload time of the large file.

>? It is recommended to use the advanced API for copying directly.
>

### Operation procedures

#### Performing a multipart copy

1. Initialize parts with `Initiate Multipart Upload` and get the `UploadId`.
2. Use the `UploadId` to copy the parts with `Upload Part`.
3. Complete the multipart copy with `Complete Multipart Upload`.

#### Resuming a multipart copy

1. If you did not record the `UploadId` of the multipart copy, you can query the multipart copy job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Use the `UploadId` to list the copied parts with `List Parts`.
3. Use the `UploadId` to copy the remaining parts with `Upload Part`.
4. Complete the multipart copy with `Complete Multipart Upload`.

#### Multipart copy abortion process

1. If you did not record the `UploadId` of the multipart copy, you can query the multipart copy job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Abort the multipart copy and delete the copied parts with `Abort Multipart Upload`.

### Initializing a multipart copy

This API is used to initialize a multipart copy and get the corresponding `UploadId` for future operations.

#### Method prototype

```java
public InitiateMultipartUploadResult initiateMultipartUpload(
    InitiateMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";

InitiateMultipartUploadRequest request = new InitiateMultipartUploadRequest(bucketName, key);

// During multipart copy, you can specify the metadata of a copied file only by initializing the multipart copy.
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

### Querying multipart copies

This API (`List Multipart Uploads`) is used to get all ongoing multipart copy tasks to obtain the `UploadId` of a desired multipart copy task.

#### Method prototype

```java
public MultipartUploadListing listMultipartUploads(
            ListMultipartUploadsRequest listMultipartUploadsRequest)
            throws CosClientException, CosServiceException
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

// Key of the multipart copy tasks to be queried
String targetKey = "targetKey";

ListMultipartUploadsRequest listMultipartUploadsRequest = new ListMultipartUploadsRequest(bucketName);
// Maximum number of multipart upload tasks listed per request
listMultipartUploadsRequest.setMaxUploads(100);
// Set the target prefix (key) of the multipart copy tasks to be queried.
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

### Copying an object part

This API (`Upload Part - Copy`) is used to copy an object by parts.

#### Method prototype

```java
public CopyPartResult copyPart(CopyPartRequest copyPartRequest) throws CosClientException, CosServiceException
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// `UploadId` is the unique identifier of a multipart copy task. You can obtain it by initializing the multipart copy or querying the multipart copy task.
String uploadId = "exampleuploadid";

// Source bucket region
Region srcBucketRegion = new Region("ap-beijing");
// Source bucket. Enter the bucket name in the format of `BucketName-APPID`.
String srcBucketName = "srcbucket-1250000000";
// Source file path
String srcKey = "path/srckey";

// Destination bucket region
Region destBucketRegion = new Region("ap-beijing");
// Destination bucket. Enter the bucket name in the format of `BucketName-APPID`.
String destBucketName = "destbucket-1250000000";
// Destination file path
String destKey = "path/destkey";

CopyPartRequest copyPartRequest = new CopyPartRequest();
copyPartRequest.setSourceBucketRegion(srcBucketRegion);
copyPartRequest.setSourceBucketName(srcBucketName);
copyPartRequest.setSourceKey(srcKey);

// Specify the range of data of the source file to be copied (similar to `content-range`).
copyPartRequest.setFirstByte(0L);
copyPartRequest.setLastByte(1048575L);

copyPartRequest.setDestinationBucketName(destBucketName);
copyPartRequest.setDestinationKey(destKey);

// Set the part number for the current copy, which starts from 1.
copyPartRequest.setPartNumber(1);
copyPartRequest.setUploadId(uploadId);

try {
    CopyPartResult copyPartResult = cosclient.copyPart(copyPartRequest);
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

The request members are described as follows:

| Parameter | Set Method | Description | Type |
| --------------------- | -------- | ------------------------------------------------------------ | ------ |
| destinationBucketName | Set method | Destination bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| destinationKey | Set method | Name of the destination object (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to store the replicated part, for example, `folder/picture.jpg` | String |
| uploadId | Set method | Identifies the `uploadId` of the specified multipart upload | String |
| partNumber | Set method | Number (>= 1) that identifies the specified part | int |
| sourceBucketRegion | Set method | Region of the source bucket | Region |
| sourceBucketName | Set method | Source bucket name | String |
| sourceKey | Set method | Name/Path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) of the source object before the replication, for example, `folder/picture.jpg` | String |
| firstByte | Set method | First byte offset of the source object | Long |
| lastByte | Set method | Last byte offset of the source object | Long |

#### Response description

- Success: returns `CopyPartResult`, including the ETag of the part.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Querying copied parts

This API (`List Parts`) is used to query the copied parts of a multipart copy.

#### Method prototype

```java
public PartListing listParts(ListPartsRequest request)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// `UploadId` is the unique identifier of a multipart copy task. You can obtain it by initializing the multipart copy or querying the multipart copy task.
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

| Parameter  | Set Method | Description | Type |
| ---------------- | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Object name | String |
| uploadId | Constructor or set method | `uploadId` of the multipart upload to be queried | String |
| maxParts | Set method | Maximum number of entries returned at a time. Default value: `1000` | String |
| partNumberMarker | Set method | By default, entries are listed in UTF-8 binary order, starting from the part number after the marker. | String |
| encodingType | Set method | Encoding type of the returned value | String |

#### Response description

- Success: returns `PartListing`, including the ETag and number of each part as well as the starting marker of the next list.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Completing a multipart copy

This API (`Complete Multipart Upload`) is used to complete the multipart copy of a file.

>? After the multipart copy is completed, the multipart copy task is deleted and the `UploadId` corresponding to the task is no longer valid.
>

#### Method prototype

```java
public CompleteMultipartUploadResult completeMultipartUpload(CompleteMultipartUploadRequest request) throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// `UploadId` is the unique identifier of a multipart copy task. You can obtain it by initializing the multipart copy or querying the multipart copy task.
String uploadId = "exampleuploadid";

// It is used to store the information of the uploaded parts. In actual practice, the content here is obtained from the multipart upload API.
List<PartETag> partETags = new LinkedList<>();

// After the multipart upload is completed, call `complete` to complete the multipart copy.
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

| Parameter | Set Method &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ---------- | ------------------- | ------------------------------------------------------------ | ----------------- |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| key | Constructor or set method | Specifies the path (i.e., [object key](https://intl.cloud.tencent.com/document/product/436/13324)) to upload the part to, for example, `folder/picture.jpg`. | String            |
| uploadId | Constructor or set method | Identifies a specified multipart upload. | String |
| partETags  | Constructor or set method | Identifies the number and ETag returned for an uploaded part. | List&lt;PartETag&gt; |

#### Response description

- Success: returns `CompleteMultipartUploadResult`, including the ETag of the completed object.
- Failure: if an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, please see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Aborting a multipart copy

This API (`Abort Multipart Upload`) is used to abort a multipart copy and delete the copied parts.

>? After a multipart copy is aborted, both the multipart copy task and the copied parts are deleted, and the corresponding `UploadId` is no longer valid.
>

#### Method prototype

```java
public void abortMultipartUpload(AbortMultipartUploadRequest request)  throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// The COSClient instance created here is based on the information of the destination for copying.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// `UploadId` is the unique identifier of a multipart copy task. You can obtain it by initializing the multipart copy or querying the multipart copy task.
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
