## Overview

This document provides an overview of APIs and SDK code samples related to object downloads.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading object | Downloads object. |

## Advanced API (Recommended)

The advanced API allows you to pause, resume (via checkpoint restart), or cancel a download task.

>? When downloading an object, the advanced API directly writes the object into a specified local file. If you need a download stream, see the **Simple Operations** section on this page.
>

### Creating TransferManager instance

Before using the advanced API, you must create a TransferManager instance first.

```java
// Create a TransferManager instance, which is used to call the advanced API later.
TransferManager createTransferManager() {
    // Create a COSClient client, which is the basic instance for accessing the COS service.
    // For the detailed code, see **Simple Operations** -> **Creating COSClient instance** on this page.
    COSClient cosClient = createCOSClient();

    // Set the thread pool size. We recommend you set the size of your thread pool to 16 or 32 to maximize network resource utilization, provided your client and COS networks are sufficient (for example, uploading a file to a COS bucket from a CVM instance in the same region).
    // We recommend you use a smaller value to avoid timeout caused by slow network speed if you are transferring data over a public network with poor bandwidth quality.
    ExecutorService threadPool = Executors.newFixedThreadPool(32);

    // Pass a `threadpool`; otherwise, a single-thread pool will be generated in `TransferManager` by default.
    TransferManager transferManager = new TransferManager(cosClient, threadPool);

    return transferManager;
}
```

### Parameter description

The `TransferManagerConfiguration` class is used to record the configuration information of the advanced API. Its main members are as described below:

| Member Name | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize | `set` method | Part size of the multipart upload in bytes. Default value: 5 MB. | long |
| multipartUploadThreshold | `set` method | If a file is greater than or equal to this value in bytes, it will be uploaded in concurrent parts. Default value: 5 MB. | long |
| multipartCopyThreshold | `set` method | If a file is greater than or equal to this value in bytes, it will be replicated in concurrent parts. Default value: 5 GB. | long |
| multipartCopyPartSize | `set` method | Part size in bytes for multipart replication. Default value: 100 MB. | long |

### Shutting down TransferManager instance

After confirming that the process no longer uses the TransferManager instance to call the advanced API, be sure to shut it down to avoid resource leakage.

```java
void shutdownTransferManager(TransferManager transferManager) {
    // If the parameter is set to `true`, the COSClient instance in the TransferManager instance will also be shut down at the same time.
    // If the parameter is set to `false`, the COSClient instance in the TransferManager instance will not be shut down.
    transferManager.shutdownNow(true);
}
```

### Downloading object

This API is used to download a COS object to a local file.

#### Method prototype

```java
public Download download(final GetObjectRequest getObjectRequest, final File file);
```

#### Sample request

```java
// Before using the advanced API, you must make sure that the process contains a TransferManager instance; if not, then create one.
// For the detailed code, see **Advanced API** -> **Creating TransferManager instance** on this page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// Local file path.
String localFilePath = "/path/to/localFile";
File downloadFile = new File(localFilePath);

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
try {
    // Return an async result `Download`. You can synchronously call `waitForCompletion` to wait for the download to complete. If the download is successful, `void` will be returned; otherwise, an exception will be thrown.
    Download download = transferManager.download(getObjectRequest, downloadFile);
    download.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced API** -> **Shutting down TransferManager instance** on this page.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter  | Description | Type | Default Value |
| ----------------------- | ---------------------------------- | ---------------- | ---------------------------- |
| getObjectRequest | Object download request. | GetObjectRequest | None |
| file | Destination file. | File | None |

The request members are as described below:

| Request Member | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or `set` method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).  | String |
| key | Constructor or `set` method | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| range | `set` method | Download range. | Long[] |
| trafficLimit | `set` method | Traffic limit on the downloaded object in bit/s. There is no limit by default. | int |

#### Returned values

- Success: `Download` is returned. You can query whether the download is complete, or wait for the download to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Downloading object via checkpoint restart

This API is used to download an object by range by using multiple threads at the same time and perform an integrity check after the download is complete. If an abnormal interruption occurs during the download, a range that has been downloaded will not be downloaded again (if the source file has been modified before the restart, it will be downloaded from the beginning).
This API is suitable for downloading large files.

#### Method prototype

```java
public Download download(final GetObjectRequest getObjectRequest, final File file,
        boolean resumableDownload);

public Download download(final GetObjectRequest getObjectRequest, final File file,
        boolean resumableDownload, String resumableTaskFile,
        int multiThreadThreshold, int partSize);
```

#### Sample request

```java
// Before using the advanced API, you must make sure that the process contains a TransferManager instance; if not, then create one.
// For the detailed code, see **Advanced API** -> **Creating TransferManager instance** on this page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// Local file path.
String localFilePath = "/path/to/localFile";
File downloadFile = new File(localFilePath);

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
try {
    // Return an async result `Download`. You can synchronously call `waitForCompletion` to wait for the download to complete. If the download is successful, `void` will be returned; otherwise, an exception will be thrown.
    Download download = transferManager.download(getObjectRequest, downloadFile, true);
    download.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced API** -> **Shutting down TransferManager instance** on this page.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter  | Description | Type | Default Value |
| ----------------------- | ---------------------------------- | ---------------- | ---------------------------- |
| getObjectRequest | Object download request. | GetObjectRequest | None |
| file | Destination file. | File | None |
| resumableDownload | Whether to enable checkpoint restart for the download.  | boolean | false |
| resumableTaskFile   | Name of the file that records the checkpoint restart information. | boolean | file.cosresumabletask |
| multiThreadThreshold    | Minimum file size for multi-thread download with checkpoint restart. | int | 20 * 1024 * 1024              |
| partSize | Part size for downloading with checkpoint restart. | int  | 8 * 1024 * 1024  |

The request members are as described below:

| Request Member | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or `set` method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).  | String |
| key | Constructor or `set` method | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| range | `set` method | Download range. | Long[] |
| trafficLimit | `set` method | Traffic limit on the downloaded object in bit/s. There is no limit by default. | int |

#### Returned values

- Success: `Download` is returned. You can query whether the download is complete, or wait for the download to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Displaying download progress

This API is used to display the download progress. You need to configure a function to print the download progress and use it to call the API to get the object size that has been successfully downloaded and then calculate the current download progress.

#### Method prototype

```java
public Download download(final GetObjectRequest getObjectRequest, final File file);
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
// For the detailed code, see **Advanced API** -> **Creating TransferManager instance** on this page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// Local file path.
String localFilePath = "/path/to/localFile";
File downloadFile = new File(localFilePath);

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
try {
    // Return an async result `Download`. You can synchronously call `waitForCompletion` to wait for the download to complete. If the download is successful, `void` will be returned; otherwise, an exception will be thrown.
    Download download = transferManager.download(getObjectRequest, downloadFile);
    // Print the upload progress until the upload is complete.
    showTransferProgress(download);
    // Capture possible exceptions.
    download.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced API** -> **Shutting down TransferManager instance** on this page.
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

| Parameter  | Description | Type | Default Value |
| ----------------------- | ---------------------------------- | ---------------- | ---------------------------- |
| getObjectRequest | Object download request. | GetObjectRequest | None |
| file | Destination file. | File | None |

The request members are as described below:

| Request Member | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or `set` method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).  | String |
| key | Constructor or `set` method | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| range | `set` method | Download range. | Long[] |
| trafficLimit | `set` method | Traffic limit on the downloaded object in bit/s. There is no limit by default. | int |

#### Returned values

- Success: `Download` is returned. You can query whether the download is complete, or wait for the download to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Pausing, resuming, or canceling download

This API can be used to pause, resume, or cancel a download task.

#### Method prototype

```java
public Download download(final GetObjectRequest getObjectRequest, final File file);
```

#### Sample request

```java
// Before using the advanced API, you must make sure that the process contains a TransferManager instance; if not, then create one.
// For the detailed code, see **Advanced API** -> **Creating TransferManager instance** on this page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";
// Local file path.
String localFilePath = "/path/to/localFile";
File downloadFile = new File(localFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);

try {
    // Return an async result `copy`. You can synchronously call `waitForCompletion` to wait for the download to complete. If the download is successful, `void` is returned; otherwise, an exception will be thrown.
    Download download = transferManager.download(getObjectRequest, downloadFile);
    // Wait three seconds for part of the file to be downloaded.
    Thread.sleep(3000L);
    // Pause the download and get a `PersistableUpload` instance for resuming the download later.
    PersistableDownload persistableDownload = download.pause();
    // Complex pausing and resuming:
    // `PersistableDownload` instance can be used to serialize the file content and store it and then deserialize it to resume the upload.
    // persistableDownload.serialize(out);
    // Resume download.
    download = transferManager.resumeDownload(persistableDownload);
    // Capture possible exceptions.
    download.waitForCompletion();

    // Or directly cancel the download.
    // upload.abort();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced API** -> **Shutting down TransferManager instance** on this page.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter  | Description | Type | Default Value |
| ----------------------- | ---------------------------------- | ---------------- | ---------------------------- |
| getObjectRequest | Object download request. | GetObjectRequest | None |
| file | Destination file. | File | None |

The request members are as described below:

| Request Member | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or `set` method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).  | String |
| key | Constructor or `set` method | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| range | `set` method | Download range. | Long[] |
| trafficLimit | `set` method | Traffic limit on the downloaded object in bit/s. There is no limit by default. | int |

#### Returned values

- Success: `Download` is returned. You can query whether the download is complete, or wait for the download to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

### Downloading directory

This API is used to download COS objects that have a specified prefix (a virtual directory) to a specified local directory. The downloaded files are in the same directory structure as those in COS.

#### Method prototype

```java
public MultipleFileDownload downloadDirectory(String bucketName, String keyPrefix,
        File destinationDirectory) {
```

#### Sample request

```java
// Before using the advanced API, you must make sure that the process contains a TransferManager instance; if not, then create one.
// For the detailed code, see **Advanced API** -> **Creating TransferManager instance** on this page.
TransferManager transferManager = createTransferManager();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

// Set the prefix of objects to be downloaded (similar to downloading a directory in COS). If this parameter is set to `""`, the entire bucket will be downloaded.
String cos_path = "/prefix";
// Absolute path of the destination folder.
String dir_path = "/to/mydir";

try {
    // Return an async result "download". You can synchronously call `waitForUploadResult` to wait for the download to complete.
    MultipleFileDownload download = transferManager.downloadDirectory(bucketName, cos_path, new File(dir_path));

    // You can view the download progress.
    showTransferProgress(download);

    // You can also wait for the upload to complete.
    download.waitForCompletion();

    System.out.println("download directory done.");
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process no longer uses the TransferManager instance, shut it down.
// For the detailed code, see **Advanced API** -> **Shutting down TransferManager instance** on this page.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter | Description | Type |
| ------------------------- | -------------------- | ---------------- |
| bucketName                | Name of the bucket in COS. | GetObjectRequest |
| keyPrefix                 | Prefix of the objects in COS.  | String           |
| destinationDirectory      | Absolute path of the destination directory. | File             |

#### Returned values

- Success: `MultipleFileUpload` is returned. You can query whether the download is complete, or wait for the download to complete.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

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
    // For more information on COS regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
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
This SDK does not generate temporary keys. For directions on how to generate a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).

```java

// Create a COSClient instance, which is used to initiate requests later.
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
    // For more information on COS regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
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

### Downloading object

This API is used to download an object.

>? The following sample shows how to download an object to a stream. If you want to download an object to a file, use the advanced API described on this page.
>

#### Method prototype

```java
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, you must make sure that the process contains a COSClient instance; if not, then create one.
// For the detailed code, see **Simple Operations** -> **Creating COSClient instance** on this page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, which is the unique identifier of the object in the bucket. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).
String key = "exampleobject";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
COSObjectInputStream cosObjectInput = null;

try {
    COSObject cosObject = cosClient.getObject(getObjectRequest);
    cosObjectInput = cosObject.getObjectContent();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// Process the stream for the download.
// Here, the stream is read directly. You can process it according to the actual situation.
byte[] bytes = null;
try {
    bytes = IOUtils.toByteArray(cosObjectInput);
} catch (IOException e) {
    e.printStackTrace();
} finally {
    // After using the stream, be sure to call `close()`.
    cosObjectInput.close(); 
}

// Do not shut down the COSClient instance before the stream processing is completed.
// After confirming that the process no longer uses the COSClient instance, shut it down.
cosClient.shutdown();
```

#### Parameter description

| Parameter | Description | Type |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | File download request. | GetObjectRequest |
| destinationFile | The file saved locally. | File |

The request members are as described below:

| Request Member | Configuration Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Constructor or `set` method | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| range | `set` method | Download range. | Long[] |
| trafficLimit | `set` method | Traffic limit on the downloaded object in bit/s. There is no limit by default. | Int |


#### Response description

- Success: The `COSObject` class is returned, including the input stream and object attributes.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be thrown. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Response parameter description

The `COSObject` class is used to return request results. Its main members are as described below:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| bucketName |  Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| key | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, its key is `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String |
| metadata | Object metadata.  | ObjectMetadata |
| objectContent | Data stream containing COS object content.  | COSObjectInputStream |
