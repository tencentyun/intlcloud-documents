## Overview
This document provides an overview of SDK code samples related to generating pre-signed object links.

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Generating a Pre-signed Object Link

#### Sample 1. Generating a pre-signed upload link

[//]: # ".cssg-snippet-get-presign-upload-url"
```java
try {
    String bucket = "examplebucket-1250000000"; // Bucket name
    String cosPath = "exampleobject"; // Location identifier of the object in the bucket.
    String method = "PUT"; // HTTP request method
    PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket
            , cosPath) {
        @Override
        public RequestBodySerializer getRequestBody()
                throws CosXmlClientException {
            // Used to calculate a pre-signed URL for requests like `PUT` that require a request body
            return RequestBodySerializer.string("text/plain",
                    "this is test");
        }
    };
    presignedUrlRequest.setRequestMethod(method);

    String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
}
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectPresignUrl.java).

#### Sample 2. Generating a pre-signed download link

[//]: # ".cssg-snippet-get-presign-download-url"
```java
try {
    String bucket = "examplebucket-1250000000"; // Bucket name
    String cosPath = "exampleobject"; // Location identifier of the object in the bucket.
    String method = "GET"; // HTTP request method
    PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket
            , cosPath);
    presignedUrlRequest.setRequestMethod(method);

    String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest);

} catch (CosXmlClientException e) {
    e.printStackTrace();
}
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectPresignUrl.java).

