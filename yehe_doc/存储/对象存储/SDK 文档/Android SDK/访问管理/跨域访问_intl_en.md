## Overview

This document provides an overview of APIs and SDK code samples related to cross-origin access.

| API | Operation Name | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting a cross-origin access configuration | Sets the cross-origin access permissions of bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying a cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting a cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a Cross-origin Access Configuration

#### Feature description

This API is used to set the cross-origin access configuration of a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-put-bucket-cors"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
PutBucketCORSRequest putBucketCORSRequest = new PutBucketCORSRequest(bucket);

CORSConfiguration.CORSRule corsRule = new CORSConfiguration.CORSRule();

// Set the rule ID
corsRule.id = "123";
// Allowed origin in the format: `protocol://domain name[:port number]`. The wildcard * is supported
corsRule.allowedOrigin = "https://cloud.tencent.com";
// Set the validity period of the OPTIONS request result 
corsRule.maxAgeSeconds = 5000;

List<String> methods = new LinkedList<>();
methods.add("PUT");
methods.add("POST");
methods.add("GET");
// Allowed HTTP operations such as GET, PUT, HEAD, POST, and DELETE
corsRule.allowedMethod = methods;

List<String> headers = new LinkedList<>();
headers.add("host");
headers.add("content-type");
// Notify the server which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent. The wildcard * is supported
corsRule.allowedHeader = headers;

List<String> exposeHeaders = new LinkedList<>();
exposeHeaders.add("x-cos-meta-1");
// Set custom header information that the browser can receive from the server
corsRule.exposeHeader = exposeHeaders;

putBucketCORSRequest.addCORSRule(corsRule);

cosXmlService.putBucketCORSAsync(putBucketCORSRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketCORSResult putBucketCORSResult = (PutBucketCORSResult) result;
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

## Querying a Cross-origin Access Configuration

#### Feature description

This API is used to query the cross-origin access configuration of a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-cors"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
GetBucketCORSRequest getBucketCORSRequest = new GetBucketCORSRequest(bucket);
cosXmlService.getBucketCORSAsync(getBucketCORSRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketCORSResult getBucketCORSResult = (GetBucketCORSResult) result;
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

## Deleting a Cross-origin Access Configuration

#### Feature description

This API is used to delete the cross-origin access configuration of a specified bucket.

#### Sample code

[//]: # ".cssg-snippet-delete-bucket-cors"
```java
String bucket = "examplebucket-1250000000"; // Format: BucketName-APPID
DeleteBucketCORSRequest deleteBucketCORSRequest =
        new DeleteBucketCORSRequest(bucket);
cosXmlService.deleteBucketCORSAsync(deleteBucketCORSRequest,
        new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketCORSResult deleteBucketCORSResult =
                (DeleteBucketCORSResult) result;
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


