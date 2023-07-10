## Overview

This document provides an overview of APIs and SDK code samples related to CORS preflight requests.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring a preflight request for cross-origin access | Sends a preflight request to check whether a real cross-origin access request can be sent |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Configuring a Preflight Request for Cross-origin Access

#### Description
This API is used to get the cross-origin access configuration for a preflight request.

#### Sample code

[//]: # (.cssg-snippet-option-object)
```java
// Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
String cosPath = "exampleobject"; // The location identifier of the object in the bucket, i.e., the object key
String origin = "https://cloud.tencent.com";
String accessMethod = "PUT";
OptionObjectRequest optionObjectRequest = new OptionObjectRequest(bucket,
        cosPath, origin,
        accessMethod);
cosXmlService.optionObjectAsync(optionObjectRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest cosXmlRequest, CosXmlResult result) {
        OptionObjectResult optionObjectResult = (OptionObjectResult) result;
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

>? For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketCORS.java).

