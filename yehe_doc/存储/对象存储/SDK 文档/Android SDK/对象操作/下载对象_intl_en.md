## Overview

This document provides an overview of APIs and SDK sample codes related to object download.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (recommended)

### Downloading an object

The advanced version of the GET Object API uses more encapsulated logic to allow you to suspend, resume (via checkpoint restart), or cancel download requests.

#### Sample code:

[//]: # (.cssg-snippet-transfer-download-object)
```java
// The advanced download API supports checkpoint restart. To do so, a `HEAD` request will be sent first to get file information before download.
// If you are using a temporary key or accessing with a sub-account, please make sure that your access permission list includes HeadObject.

// Initialize `TransferConfig`. The default configuration is used here. If you need to customize the configuration, please see the SDK API documentation.
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key
// Local directory path
String savePathDir = context.getExternalCacheDir().toString();
// The file name saved locally. If not specified (null), it will be the same as the COS file name
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

    @Override
    public void onFail(CosXmlRequest request,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
// Set the job status callback where you can view the job progress
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).

#### Sample code 2: Suspending, resuming, or cancelling a download

To suspend a download, use the code below:

[//]: # (.cssg-snippet-transfer-download-object-pause)
```java
cosxmlDownloadTask.pause();;
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

#### Sample code 3: Downloading multiple objects

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
            COSXMLDownloadTask.COSXMLDownloadTaskResult cOSXMLDownloadTaskResult =
                    (COSXMLDownloadTask.COSXMLDownloadTaskResult) result;
        }

        @Override
        public void onFail(CosXmlRequest request,
                           CosXmlClientException clientException,
                           CosXmlServiceException serviceException) {
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

## Simple Operations

### Downloading an object

#### Description

This API is used to download an object to the local file system.

#### Sample code

[//]: # (.cssg-snippet-get-object)
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key
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

    @Override
    public void onFail(CosXmlRequest cosXmlRequest,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/GetObject.java).

