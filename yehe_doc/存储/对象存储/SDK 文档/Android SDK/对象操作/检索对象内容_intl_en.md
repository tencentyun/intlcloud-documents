## Overview

This document provides an overview of the API and SDK code samples related to extracting object content.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) | Extracting object content | Extracts the content of a specified object (in CSV or JSON format) |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Extracting object content

#### API description 

This API is used by the COS Select feature to extract objects in the following formats:

- CSV: an object is stored in CSV format with its data records separated with a specific delimiter.
- JSON: an object is stored in JSON format, which can be either a JSON file or a JSON list.


>!
> - To use COS Select, you must have the permission to `cos:GetObject`.
> - CSV- or JSON-formatted objects need to be encoded in UTF-8.
> - COS Select can extract CSV- or JSON-formatted objects compressed by gzip or bzip2.
> - COS Select can extract CSV- or JSON-formatted objects encrypted with SSE-COS.

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

>? For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/SelectObject.java).

