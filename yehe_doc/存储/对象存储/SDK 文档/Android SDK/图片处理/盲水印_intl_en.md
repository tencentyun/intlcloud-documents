## Overview

This document provides an overview of APIs and SDK code samples related to COS blind watermarking.

| API | Description    |
| ------------------------------------------------------------ | ---------------------------------------- |
| Blind watermarking | Adds blind watermarks to or extracts blind watermarks from local images and uploads them to a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Adding Blind Watermarks

### Description

COS allows you to add a blind watermark when uploading or downloading an object.

### Sample 1. Adding a blind watermark when uploading

[//]: # ".cssg-snippet-put-object-with-watermark"
```java
List<PicOperationRule> rules = new LinkedList<>();
// Add a rule for blind watermarking, and the processed image will be saved in the bucket with a location identifier in the format:
// examplewatermarkobject
rules.add(new PicOperationRule("examplewatermarkobject",
        "watermark/3/type/1/image/aHR0cDovL2V4YW1wbGVzLTEyNTEwMDAw"));
PicOperations picOperations = new PicOperations(true, rules);

PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, srcPath);
putObjectRequest.setPicOperations(picOperations);

// If the upload is successful, you will get 2 images: the original and the processed images
COSXMLUploadTask cosxmlUploadTask = transferManager.upload(putObjectRequest, uploadId);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/PictureOperation.java).

### Sample 2. Adding a blind watermark when downloading

[//]: # ".cssg-snippet-download-object-with-watermark"
```java
GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath, savePathDir, savedFileName);
// Add a text watermark
getObjectRequest.addQuery("watermark/3/type/3/text/dGVuY2VudCBjbG91ZA==", null);

COSXMLDownloadTask cosxmlDownloadTask =
        transferManager.download(applicationContext, getObjectRequest);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/PictureOperation.java).

