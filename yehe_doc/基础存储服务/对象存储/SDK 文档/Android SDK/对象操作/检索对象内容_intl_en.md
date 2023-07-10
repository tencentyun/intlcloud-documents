## Overview

This document provides an overview of APIs and SDK code samples related to object content extraction.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) | Extracting object content | Extracts the content of a specified object (in CSV or JSON format) |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Extracting Object Content

#### Description

COS Select supports extracting content from objects in the following formats:

- CSV: The object’s data records are separated by a specific delimiter.
- JSON: either a JSON file or a JSON list

>!
> - To use COS Select, you must have the permission on `cos:GetObject`.
> - CSV and JSON objects need to be encoded in UTF-8.
> - COS Select supports extracting CSV and JSON objects compressed by gzip or bzip2.
> - COS Select supports extracting CSV and JSON objects encrypted with SSE-COS.
> 

#### Sample code

[//]: # (.cssg-snippet-select-object)
```java
String bucket = "examplebucket-1250000000";
// The object must be in JSON or CSV format
String cosPath = "exampleobject";
final String expression = "Select * from COSObject";

SelectObjectContentRequest selectObjectContentRequest = new SelectObjectContentRequest(
        bucket, cosPath, expression, true,
        new InputSerialization(CompressionType.NONE, new JSONInput(JSONType.DOCUMENT)),
        new OutputSerialization(new JSONOutput(","))
);

// Set the result callback which may work repeatedly
selectObjectContentRequest.setSelectObjectContentProgressListener(new SelectObjectContentListener() {
    @Override
    public void onProcess(SelectObjectContentEvent event) {

    }
});
cosXmlService.selectObjectContentAsync(selectObjectContentRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        SelectObjectContentResult selectObjectContentResult =
                (SelectObjectContentResult) result;
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

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/SelectObject.java).
>

