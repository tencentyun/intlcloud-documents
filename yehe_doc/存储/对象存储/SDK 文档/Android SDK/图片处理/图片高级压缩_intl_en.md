## Overview

This document provides an overview of APIs and SDK code samples related to advanced image compression.

| API | Operation    |
| ------------------------------------------------------------ | -------- |
| [Advanced image compression](https://intl.cloud.tencent.com/document/product/436/44004) |   Compresses images in a specified bucket   |


## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced Image Compression

### Description

Advanced image compression allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transmission time, loading time, and the use of bandwidth and traffic.

### Sample code: performing advanced image compression upon download

[//]: # (.cssg-snippet-get-object-with-advanced-compress)
```java
String bucket = "examplebucket-1250000000"; // Bucket, formatted as BucketName-APPID
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
String savePath = context.getExternalCacheDir().toString(); // Local path

GetObjectRequest getObjectRequest = new GetObjectRequest(bucket, cosPath,
        savePath);
getObjectRequest.addQuery("imageMogr2/format/tpg", null);

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
>



