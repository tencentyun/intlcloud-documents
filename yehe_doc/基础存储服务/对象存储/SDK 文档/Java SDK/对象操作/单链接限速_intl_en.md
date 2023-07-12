## Overview

This document provides an overview of APIs and SDK code samples related to single-URL speed limits.

>? The speed range is 819200 to 838860800 (in bit/s), that is, 100 KB/s to 100 MB/s. If a value is not within this range, 400 will be returned.
>

### Setting an upload speed limit

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Creating a TransferManager instance" on the current page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";

// Here, a ByteArrayInputStream stream is created as an example. In practice, you should create a stream of the actual InputStream type to upload.
long inputStreamLength = 1024 * 1024;
byte data[] = new byte[inputStreamLength];
InputStream inputStream = new ByteArrayInputStream(data);

// Here, set the upload bandwidth limit (in bit/s) to 10 MB/s.
putObjectRequest.setTrafficLimit(80*1024*1024);

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
shutdownTransferManager(transferManager);
```

### Setting a download speed limit

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Creating a TransferManager instance" on the current page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File downloadFile = new File(localFilePath);

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
// Here, set the download bandwidth limit (in bit/s) to 10 MB/s.
getObjectRequest.setTrafficLimit(80*1024*1024);

try {
    // Return an asynchronous result `Download`. You can synchronously call `waitForCompletion` to wait for the download to end. If successful, `void` is returned; otherwise, an exception will be thrown.
    Download download = transferManager.download(getObjectRequest, downloadFile);
    download.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the TransferManager instance anymore, close it.
// For the detailed code, see "Advanced APIs -> Closing a TransferManager instance" on the current page.
shutdownTransferManager(transferManager);
```
