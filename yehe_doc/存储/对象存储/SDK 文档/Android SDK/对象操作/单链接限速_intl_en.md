## Overview

This document describes the bandwidth limit on single connection when you call the COS APIs for upload or download.

## Description

This limit should have a value in bit/s ranging from **819200 - 838860800**, i.e. 100 KB/s - 100 MB/s. If this range is exceeded, a 400 error will be returned.

#### Sample 1. Single-connection bandwidth limit when uploading

[//]: # (.cssg-snippet-upload-object-traffic-limit)
```java
TransferConfig transferConfig = new TransferConfig.Builder().build();
// Initialize TransferManager
TransferManager transferManager = new TransferManager(cosXmlService,
        transferConfig);

String bucket = "examplebucket-1250000000"; // Bucket in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e. the object key
String srcPath = new File(context.getCacheDir(), "exampleobject")
        .toString(); // The absolute path of the local file
String uploadId = null; // If there is an uploadId for the initialized multipart upload, assign the value of the uploadId here to resume the upload; otherwise, assign null
String uploadId = null;

PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
// Set the single-connection bandwidth limit in bit/s, e.g. 1 M/s
putObjectRequest.setTrafficLimit(1024 * 1024 * 8);

// Upload the files
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);

// Set the upload progress callback
cosxmlUploadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set the result callback
cosxmlUploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        COSXMLUploadTask.COSXMLUploadTaskResult cOSXMLUploadTaskResult =
                (COSXMLUploadTask.COSXMLUploadTaskResult) result;
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
// Set the status callback where you can view the upload progress
cosxmlUploadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferUploadObject.java).

#### Sample 2. Single-connection bandwidth limit when downloading

[//]: # (.cssg-snippet-download-object-traffic-limit)
```java
//.cssg-snippet-body-start:[transfer-download-object]
// The advanced download API supports checkpoint restart. To do so, a `HEAD` request will be sent first to get file information before download.
// If you are accessing COS using a temporary key or sub-account, please make sure that your access permission list includes HeadObject.

// Initialize `TransferConfig`. The default configuration is used here. To customize it, please see the SDK API documentation.
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

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, savePathDir, savedFileName);
// Set the single-connection bandwidth limit in bit/s, e.g. 1 M/s
getObjectRequest.setTrafficLimit(1024 * 1024 * 8);

Context applicationContext = context.getApplicationContext(); // application
// context
COSXMLDownloadTask cosxmlDownloadTask =
        transferManager.download(applicationContext, getObjectRequest);

// Set the download progress callback
cosxmlDownloadTask.setCosXmlProgressListener(new CosXmlProgressListener() {
    @Override
    public void onProgress(long complete, long target) {
        // todo Do something to update progress...
    }
});
// Set the result callback
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
// Set the status callback where you can view the download progress
cosxmlDownloadTask.setTransferStateListener(new TransferStateListener() {
    @Override
    public void onStateChanged(TransferState state) {
        // todo notify transfer state
    }
});
```

>?For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/TransferDownloadObject.java).

