## Overview

This document provides an overview of APIs and SDK sample codes related to preflight requests for cross-origin access.

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring a preflight request for cross-origin access | Sends a preflight request to check whether a real cross-origin access request can be sent |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Configuring a Preflight Request for Cross-origin Access

#### Feature description
This API is used to get the cross-origin access configuration for a preflight request.

#### Sample code

[//]: # ".cssg-snippet-option-object"
```java
String bucket = "examplebucket-1250000000"; // Bucket name in the format: `BucketName-APPID`
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/BucketCORS.java).

