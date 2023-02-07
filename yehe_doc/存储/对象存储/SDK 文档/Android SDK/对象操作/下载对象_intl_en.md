## Overview

This document provides an overview of APIs and SDK code samples for downloading an object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Downloading an object

The advanced version of the GET Object API uses more encapsulated logic to allow you to suspend, resume (via checkpoint restart), or cancel download requests.

#### Sample 1. Downloading an object

[//]: # (.cssg-snippet-transfer-download-object)
```java
// The advanced download API supports checkpoint restart. Therefore, a HEAD request will be sent before the download to obtain the file information.
// If you are using a temporary key or accessing with a sub-account, ensure that your permission list includes HeadObject.

// Initialize TransferConfig. The default configuration is used here. To customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
// Path of the local directory
String savePathDir = context.getExternalCacheDir().toString();
// File name saved locally. If not specified (null), it will be the same as the COS file name
String savedFileName = "exampleobject";

Context applicationContext = context.getApplicationContext(); // application
// context
COSXMLDownloadTask cosxmlDownloadTask =
        transferManager.download(applicationContext,
                bucket, cosPath, savePathDir, savedFileName);

// Set the download progress callback
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set the response callback
cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLDownloadTask.COSXMLDownloadTaskResult downloadTaskResult =
                (COSXMLDownloadTask.COSXMLDownloadTaskResult) result;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest request,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
// Set the job status callback to view the job progress
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).

#### Sample 2. Suspending, resuming, or cancelling a download

To suspend a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-pause)
```java
cosxmlDownloadTask.pause();
```

To resume a suspended download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-resume)
```java
cosxmlDownloadTask.resume();
```

To cancel a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-cancel)
```java
cosxmlDownloadTask.cancel();
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).

#### Sample 3. Setting checkpoint restart for download

[//]: # (.cssg-snippet-transfer-download-resumable)
```java
// Initialize TransferConfig. The default configuration is used here. To customize the configuration, please see the SDK API documentation.
// TransferManager supports checkpoint restart for download. You only need to ensure the consistency of parameters `bucket`, `cosPath`, `savePathDir`, and `savedFileName`.
// Then the SDK will resume the download from where interrupted.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
// Path of the local directory
String savePathDir = context.getExternalCacheDir().toString();
// File name saved locally. If not specified (null), it will be the same as the COS file name
String savedFileName = "exampleobject";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, savePathDir, savedFileName);

Context applicationContext = context.getApplicationContext(); // application
// context
COSXMLDownloadTask cosxmlDownloadTask =
        transferManager.download(applicationContext, getObjectRequest);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).

#### Sample 4. Batch download

[//]: # (.cssg-snippet-transfer-batch-download-objects)
```java
// The location of the object in the bucket, i.e., the object key
String[] cosPaths = new String[] {
        "exampleobject1",
        "exampleobject2",
        "exampleobject3",
};

for (String cosPath : cosPaths) {

    COSXMLDownloadTask cosxmlDownloadTask =
            transferManager.download(applicationContext,
                    bucket, cosPath, savePathDir, savedFileName);
    // Set the response callback
    cosxmlDownloadTask.setCosXmlResultListener(new CosXmlResultListener() {
        @Override
        public void onSuccess(CosXmlRequest request, CosXmlResult result) {
            COSXMLDownloadTask.COSXMLDownloadTaskResult downloadResult =
                    (COSXMLDownloadTask.COSXMLDownloadTaskResult) result;
        }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest request,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
            if (clientException != null) {
                clientException.printStackTrace();
            } else {
                serviceException.printStackTrace();
            }
        }
    });
}
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).

#### Sample 5. Creating a directory

[//]: # (.cssg-snippet-transfer-download-directory)
```java
boolean isTruncated = true;
String marker = null;
try {
    while (isTruncated) {
        GetBucketRequest getBucketRequest = new GetBucketRequest(region, bucket, directoryPath);
        // Configure pagination
        getBucketRequest.setMarker(marker);
        // Configure not to query subdirectories
        getBucketRequest.setDelimiter("/");
        GetBucketResult getBucketResult = cosXmlService.getBucket(getBucketRequest);
        // Batch download
        for (ListBucket.Contents content : getBucketResult.listBucket.contentsList) {
            GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, content.key, savePathDir);
            transferManager.download(context,getObjectRequest);
        }
        isTruncated = getBucketResult.listBucket.isTruncated;
        marker = getBucketResult.listBucket.nextMarker;
    }
} catch (CosXmlServiceException serviceException) {
    serviceException.printStackTrace();
} catch (CosXmlClientException clientException) {
    clientException.printStackTrace();
}
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).

#### Sample 6. Downloading files anonymously (downloading public files without passing in the key)

[//]: # (.cssg-snippet-transfer-download-resumable)
```java
// Initialize TransferConfig. The default configuration is used here. To customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
CosXmlServiceConfig cosXmlServiceConfig = new CosXmlServiceConfig.Builder()
        .setRegion("ap-guangzhou")
        .builder();
// The `CosXmlService` generated by anonymous download does not require passing in the key generator.
CosXmlService cosXmlService = new CosXmlService(context, cosXmlServiceConfig);
TransferManager transferManager = new TransferManager(cosXmlService, transferConfig);
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
// Path of the local directory
String savePathDir = context.getExternalCacheDir().toString();
// The filename saved locally. If not specified (null), it will be the same as the COS filename.
String savedFileName = "exampleobject";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, savePathDir, savedFileName);

Context applicationContext = context.getApplicationContext(); // application
// context
COSXMLDownloadTask cosxmlDownloadTask =
        transferManager.download(applicationContext, getObjectRequest);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).

## Simple Operations

### Downloading an object

#### Feature description

This API is used to download an object to the local file system.

#### Sample code

[//]: # (.cssg-snippet-get-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
String savePath = context.getExternalCacheDir().toString(); // Local path

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath,
        savePath);
getObjectRequest.setProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long progress, long max) {
        // todo Do something to update progress...
    }
});

cosXmlService.getObjectAsync(getObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest,
                          CosXmlResult cosXmlResult) {
        GetObjectResult getObjectResult = (GetObjectResult) cosXmlResult;
    }

    // If you use the Kotlin language to call this, please note that the exception in the callback method is nullable; otherwise, the onFail method will not be called back, that is:
    // clientException is of type CosXmlClientException? and serviceException is of type CosXmlServiceException?
    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       @Nullable CosXmlClientException clientException,
                       @Nullable CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/GetObject.java).

