## Overview

This document provides an overview of APIs and SDK code samples for downloading an object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://www.tencentcloud.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |

## Advanced APIs (Recommended)

The advanced API allows you to suspend, resume (via checkpoint restart), or cancel download tasks.

>? When downloading an object, the advanced API directly writes the object into a specified local file. If you need a download stream, see the simple operation section on this page.
>

### Creating a TransferManager instance

Before using the advanced API, first create a TransferManager instance.

```java
// Create a TransferManager instance, which is used to call the advanced API later.
TransferManager createTransferManager() {
    // Create a COSClient client, which is the basic instance for accessing the COS service.
    // For the detailed code, see "Simple Operations -> Creating a COSClient instance" on this page.
    COSClient cosClient = createCOSClient();

    // Set the thread pool size. You are advised to set the size of your thread pool to 16 or 32 to maximize network resource utilization if you have sufficient client and COS network resources (for example, by using Tencent Cloud CVM and uploading to COS in the same region).
    // We recommend using a smaller value to avoid timeout due to slow network speed if you are transferring data over a public network with poor bandwidth quality.
    ExecutorService threadPool = Executors.newFixedThreadPool(32);

    // Pass a `threadpool`. Otherwise, a single-thread pool will be generated in `TransferManager` by default.
    TransferManager transferManager = new TransferManager(cosClient, threadPool);

    return transferManager;
}
```

### Parameter description

The `TransferManagerConfiguration` class is used to record the configuration of the advanced API. Its main members are described as follows:

| Member Name | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | -------------- |
| minimumUploadPartSize | `set` method | Part size of the multipart upload in bytes. Default: 5 MB | long |
| multipartUploadThreshold | `set` method | If a file is greater than or equal to this value, it will be uploaded in concurrent parts. Unit: byte; default: 5 MB | long |
| multipartCopyThreshold | `set` method | If a file is greater than or equal to this value, it will be replicated in concurrent parts. Unit: byte; default: 5 GB | long |
| multipartCopyPartSize | `set` method | Part size in bytes for multipart replication. Default: 100 MB | long |

### Closing a TransferManager instance

After confirming that the process does not use the TransferManager instance to call the advanced API anymore, be sure to close it to avoid leaking resources.

```java
void shutdownTransferManager(TransferManager transferManager) {
    // If the parameter is set to `true`, the COSClient instance in the TransferManager instance will also be closed at the same time.
    // If the parameter is set to `false`, the COSClient instance in the TransferManager instance will not be closed.
    transferManager.shutdownNow(true);
}
```

### Downloading an object

This API is used to download a COS object to a local file.

#### Method prototype

```java
public Download download(final GetObjectRequest getObjectRequest, final File file);
```

#### Sample request

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Creating a TransferManager instance" on this page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://www.tencentcloud.com/document/product/436/13324).
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File downloadFile = new File(localFilePath);

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
try {
    // Return an asynchronous result `Download`. You can synchronously call `waitForCompletion` to wait for the download to end. If successful, `void` is returned; otherwise, an exception will be reported.
    Download download = transferManager.download(getObjectRequest, downloadFile);
    download.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the TransferManager anymore, close it.
// For the detailed code, see "Advanced APIs -> Closing a TransferManager instance" on this page.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter  | Description | Type | Default Value |
| ----------------------- | ---------------------------------- | ---------------- | ---------------------------- |
| getObjectRequest | Object download request | GetObjectRequest | No |
| file | Destination file | File | No |

Description of the `Request` member:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or `set` method | Bucket name in the format of `BucketName-APPID`. For details, see the bucket naming conventions section in [Bucket Overview](https://www.tencentcloud.com/document/product/436/13312).  | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://www.tencentcloud.com/document/product/436/13324) | String |
| range | `set` method | Download range | Long[] |
| trafficLimit | `set` method | Traffic limits (in bit/s) on the downloaded object. There is no limit by default. | int |

#### Returned values

- Success: returns `Download`. You can query whether the download is complete, or wait until the download is finished.
-Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/31537).

### Downloading an object (checkpoint restart)

In this API, an object is downloaded by ranges using multiple threads at the same time, and an integrity check is performed after the download is completed. If there is an exceptional interruption during the download, a range that has been downloaded will not be downloaded again (if the source file has been modified before the restart, it will be downloaded from the beginning).
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
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Creating a TransferManager instance" on this page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://www.tencentcloud.com/document/product/436/13324).
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File downloadFile = new File(localFilePath);

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
try {
    // Return an asynchronous result `Download`. You can synchronously call `waitForCompletion` to wait for the download to end. If successful, `void` is returned; otherwise, an exception will be reported.
    Download download = transferManager.download(getObjectRequest, downloadFile, true);
    download.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the TransferManager anymore, close it.
// For the detailed code, see "Advanced APIs -> Closing a TransferManager instance" on this page.
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter  | Description | Type | Default Value |
| ----------------------- | ---------------------------------- | ---------------- | ---------------------------- |
| getObjectRequest | Object download request | GetObjectRequest | No |
| file | Destination file | File | No |
| resumableDownload | Whether to enable checkpoint restart for the download  | boolean | false |
| resumableTaskFile   | Name of the file that records the checkpoint restart information | String | file.cosresumabletask |
| multiThreadThreshold    | Minimum file size to use multi-thread download with checkpoint restart | int | 20 * 1024 * 1024              |
| partSize | Part size for downloading with checkpoint restart | int  | 8 * 1024 * 1024  |

Description of the `Request` member:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or `set` method | Bucket name in the format of `BucketName-APPID`. For details, see the bucket naming conventions section in [Bucket Overview](https://www.tencentcloud.com/document/product/436/13312).  | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://www.tencentcloud.com/document/product/436/13324) | String |
| range | `set` method | Download range | Long[] |
| trafficLimit | `set` method | Traffic limits (in bit/s) on the downloaded object. There is no limit by default. | int |

#### Returned values

- Success: returns `Download`. You can query whether the download is complete, or wait until the download is finished.
-Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/31537).

### Displaying the download progress

You need to configure a function to display the download progress. The function is supposed to call the API to get the object size that has been successfully downloaded and then calculate the current download progress.

#### Method prototype

```java
public Download download(final GetObjectRequest getObjectRequest, final File file);
```

#### Sample request

```java
// You can adjust the following sample code as needed to form your own code.
void showTransferProgress(Transfer transfer) {
    System.out.println(transfer.getDescription());

    // Use `transfer.isDone()` to check whether the download is completed.
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

    // If the upload is completed, `Completed` is returned. If the upload fails, `Failed` is returned.
    System.out.println(transfer.getState());
}
```

The sample code for the file download operation is as follows:

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Creating a TransferManager instance" on this page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://www.tencentcloud.com/document/product/436/13324).
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File downloadFile = new File(localFilePath);

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
try {
    // Return an asynchronous result `Download`. You can synchronously call `waitForCompletion` to wait for the download to end. If successful, `void` is returned; otherwise, an exception will be reported.
    Download download = transferManager.download(getObjectRequest, downloadFile);
    // Print the download progress until the download is complete.
    showTransferProgress(download);
    // Possible exceptions are captured here.
    download.waitForCompletion();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the TransferManager anymore, close it.
// For the detailed code, see "Advanced APIs -> Closing a TransferManager instance" on this page.
shutdownTransferManager(transferManager);
```

#### Description of progress obtaining

You can use the `getProgress` method of the `download` class to obtain the `TransferProgress` class, which has the following three methods to obtain the download progress:

| Method Name | Description | Type |
| ----------------------- |-------------| -----   |
| getBytesTransferred     | Obtains the number of bytes downloaded | long   |
| getTotalBytesToTransfer | Obtains the total number of bytes of the file | long   |
| getPercentTransferred   | Obtains the percentage of the number of bytes downloaded | double |

#### Parameter description

| Parameter  | Description | Type | Default Value |
| ----------------------- | ---------------------------------- | ---------------- | ---------------------------- |
| getObjectRequest | Object download request | GetObjectRequest | No |
| file | Destination file | File | No |

Description of the `Request` member:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or `set` method | Bucket name in the format of `BucketName-APPID`. For details, see the bucket naming conventions section in [Bucket Overview](https://www.tencentcloud.com/document/product/436/13312).  | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://www.tencentcloud.com/document/product/436/13324) | String |
| range | `set` method | Download range | Long[] |
| trafficLimit | `set` method | Traffic limits (in bit/s) on the downloaded object. There is no limit by default. | int |

#### Returned values

- Success: returns `Download`. You can query whether the download is complete, or wait until the download is finished.
-Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/31537).

### Suspending, resuming, or cancelling a download

This API can be used to suspend, resume, or cancel a download task.

#### Method prototype

```java
public Download download(final GetObjectRequest getObjectRequest, final File file);
```

#### Sample request

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Sample code: Creating a TransferManager instance" on this page.
TransferManager transferManager = createTransferManager();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://www.tencentcloud.com/document/product/436/13324).
String key = "exampleobject";
// Local file path
String localFilePath = "/path/to/localFile";
File downloadFile = new File(localFilePath);
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);

try {
    // Return an async result `copy`. You can synchronously call `waitForCompletion` to wait for the `download` to end. If successful, `void` is returned; otherwise, an exception will be reported.
    Download download = transferManager.download(getObjectRequest, downloadFile);
    // Wait 3 seconds for part of the file to be downloaded.
    Thread.sleep(3000L);
    // Suspend the download and get a `PersistableUpload` instance for resuming the download later.
    PersistableDownload persistableDownload = download.pause();
    // Complex suspension and resuming:
    // `PersistableDownload` instance can be used to serialize the file content and store it and then deserialize it to resume the download.
    // persistableDownload.serialize(out);
    // Resume download
    download = transferManager.resumeDownload(persistableDownload);
    // Capture possible exceptions
    download.waitForCompletion();

    // Or directly cancel the download
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
shutdownTransferManager(transferManager);
```

#### Parameter description

| Parameter  | Description | Type | Default Value |
| ----------------------- | ---------------------------------- | ---------------- | ---------------------------- |
| getObjectRequest | Object download request | GetObjectRequest | No |
| file | Destination file | File | No |

Description of the `Request` member:

| Request Member | Set Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or `set` method | Bucket name in the format of `BucketName-APPID`. For details, see the bucket naming conventions section in [Bucket Overview](https://www.tencentcloud.com/document/product/436/13312).  | String |
| key | Constructor or set method |The object key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [ObjectKey](https://www.tencentcloud.com/document/product/436/13324) | String |
| range | `set` method | Download range | Long[] |
| trafficLimit | `set` method | Traffic limits (in bit/s) on the downloaded object. There is no limit by default. | int |

#### Returned values

- Success: returns `Download`. You can query whether the download is complete, or wait until the download is finished.
-Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/31537).

### Downloading a directory

This API is used to download COS objects that have a specified prefix (a virtual directory) to a specified local directory. The downloaded files are in the same directory structure as in COS.

#### Method prototype

```java
public MultipleFileDownload downloadDirectory(String bucketName, String keyPrefix,
        File destinationDirectory) {
```

#### Sample request

```java
// Before using the advanced API, ensure that the process contains a TransferManager instance. If such an instance does not exist, create one.
// For the detailed code, see "Advanced APIs -> Sample code: Creating a TransferManager instance" on this page.
TransferManager transferManager = createTransferManager();
// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";

// Set the prefix of objects to download (similar to downloading a directory in COS). If this parameter is set to "", the entire bucket will be downloaded.
String cos_path = "/prefix";
// Absolute path of the destination folder
String dir_path = "/to/mydir";

try {
    // Return an asynchronous result `download`. You can synchronously call `waitForUploadResult` to wait for the download to end.
    MultipleFileDownload download = transferManager.downloadDirectory(bucketName, cos_path, new File(dir_path));

    // You can view the download progress.
    showTransferProgress(download);

    // You can also wait for the download to complete.
    download.waitForCompletion();

    System.out.println("download directory done.");
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
} catch (InterruptedException e) {
    e.printStackTrace();
}

// After confirming that the process does not use the TransferManager instance anymore, close it.
// For the detailed code, see "Advanced APIs -> Sample code: Closing a TransferManager instance" on the current page.
shutdownTransferManager(transferManager);
```

#### Parameters

| Parameter | Description | Type |
| ------------------------- | -------------------- | ---------------- |
| bucketName                | Name of the bucket in COS | GetObjectRequest |
| keyPrefix                 | Prefix of the objects in COS  | String           |
| destinationDirectory      | Absolute path of the destination directory | File             |

#### Returned values

- Success: returns MultipleFileUpload. You can query whether the download is complete, or wait until the download is finished.
-Failure: an error (such as authentication failure) occurs, with a CosClientException or CosServiceException exception. For details, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/31537).

## Simple Operations

Requests for simple operations need to be initiated through `COSClient` instances. You need to create a `COSClient` instance before performing simple operations.

`COSClient` instances are concurrency-safe. You are advised to create only one COSClient instance for a process and then close it when it is no longer used to initiate requests.

### Creating a COSClient instance

Before calling the COS API, first create a COSClient instance.

```java
// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Set the user identity information.
    // Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) to view and manage the `SecretId` and `SecretKey` of your project.
    SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
    SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
    COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, visit https://cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol to `HTTP` or `HTTPS`.
    // For v5.6.53 or earlier, HTTPS is recommended.
    // For v5.6.54 or later, HTTPS is used by default.
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

### Creating a COSClient instance with a temporary key

If you want to request COS with a temporary key, you need to create a COSClient instance with the temporary key.
This SDK does not generate temporary keys. For details on how to generate a temporary key, see [Generating and Using Temporary Keys](https://www.tencentcloud.com/document/product/436/14048).

```java

// Create a COSClient instance, which is used to initiate requests later.
COSClient createCOSClient() {
    // Here, the temporary key information is needed.
    // For details on how to generate temporary keys, visit https://www.tencentcloud.com/document/product/436/14048.
    String tmpSecretId = "TMPSECRETID";
    String tmpSecretKey = "TMPSECRETKEY";
    String sessionToken = "SESSIONTOKEN";

    COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);

    // `ClientConfig` contains the COS client configuration for subsequent COS requests.
    ClientConfig clientConfig = new ClientConfig();

    // Set the bucket region.
    // For more information on COS regions, visit https://cloud.tencent.com/document/product/436/6224.
    clientConfig.setRegion(new Region("COS_REGION"));

    // Set the request protocol to `HTTP` or `HTTPS`.
    // For v5.6.53 or earlier, HTTPS is recommended.
    // For v5.6.54 or later, HTTPS is used by default.
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

### Downloading an object

This API (`GET Object`) is used to download an object to the local host.

>? The following sample shows how to download an object to a stream. If you want to download an object to a file, use the advanced API described on the current page.
>

#### Method prototype

```java
public COSObject getObject(GetObjectRequest getObjectRequest)
            throws CosClientException, CosServiceException;
```

#### Sample request

```java
// Before using the COS API, ensure that the process contains a COSClient instance. If such an instance does not exist, create one.
// For the detailed code, see "Simple Operations -> Creating a COSClient instance" on the current page.
COSClient cosClient = createCOSClient();

// Enter the bucket name in the format of `BucketName-APPID`.
String bucketName = "examplebucket-1250000000";
// Object key, the unique ID of an object in a bucket. For more information, please see [Object Key](https://www.tencentcloud.com/document/product/436/13324).
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

// Do not close the COSClient instance before the stream processing is completed.
// After confirming that the process does not use the COSClient instance anymore, close it.
cosClient.shutdown();
```

#### Parameters

| Parameter | Description | Type |
| ---------------- | -------------- | ---------------- |
| getObjectRequest | File download request | GetObjectRequest |
| destinationFile | The file saved locally | File |

Description of the `Request` member:

| Request Member | Setting Method | Description | Type |
| ------------ | ------------------- | ------------------------------------------------------------ | ------ |
| bucketName | Constructor or set method | Bucket naming format is BucketName-APPID. For details, see [Naming Conventions](https://www.tencentcloud.com/document/product/436/13312) | String |
| key | Constructor or set method | Object key, the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is `doc/picture.jpg`. For more information, see [ObjectKey](https://www.tencentcloud.com/document/product/436/13324) | String |
| range | `set` method | Download range | Long[] |
| trafficLimit | `set` method | Traffic limits (in bit/s) on the downloaded object. The default setting is no limit. | Int |


#### Response description

- Success: returns the `COSObject` class, including the input stream and object attributes.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://www.tencentcloud.com/document/product/436/31537).

#### Response parameters

The `COSObject` class is used to return request results. Its main members are described as follows:

| Member Name | Description | Type |
| --------------- | --------------------------------------------------- | ------------------- |
| bucketName |  Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://www.tencentcloud.com/document/product/436/13312) | String |
| key | The object key is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/do/picture.jpg`, the object key is doc/picture.jpg. For details, see [ObjectKey](https://www.tencentcloud.com/document/product/436/13324) | String |
| metadata | Object metadata  | ObjectMetadata |
| objectContent | Data stream containing COS object content  | COSObjectInputStream |
