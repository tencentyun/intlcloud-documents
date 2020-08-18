## Overview

This document provides an overview of APIs and SDK code samples related to restoring an archived object.

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores archived object for access |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Restoring an Archived Object 

#### Feature description

This API is used to restore an archived object for access.

#### Sample code

[//]: # ".cssg-snippet-restore-object"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
String cosPath = "exampleobject"; // Location identifier of the object in the bucket, i.e., the object key
RestoreRequest restoreRequest = new RestoreRequest(bucket, cosPath);
restoreRequest.setExpireDays(5); // Retain for 5 days
restoreRequest.setTier(RestoreConfigure.Tier.Standard); // Standard restoration mode

cosXmlService.restoreObjectAsync(restoreRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        RestoreResult restoreResult = (RestoreResult) result;
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/RestoreObject.java).

