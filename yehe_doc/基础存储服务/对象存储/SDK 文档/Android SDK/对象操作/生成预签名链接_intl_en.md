## Overview

This document provides an overview of SDK code samples related to generating pre-signed object URLs.

>?
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 


## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Generating a Pre-Signed Object URL

#### Sample code 1. Generating a pre-signed upload URL

[//]: # (.cssg-snippet-get-presign-upload-url)
```java
try {
    String bucket = "examplebucket-1250000000"; //Bucket name
    String cosPath = "exampleobject"; // Location identifier of the object in the bucket
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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectPresignUrl.java).
>

#### Sample code 2. Generating a pre-signed download URL

[//]: # (.cssg-snippet-get-presign-download-url)
```java
try {
    String bucket = "examplebucket-1250000000"; //Bucket name
    String cosPath = "exampleobject"; // Location identifier of the object in the bucket
    String method = "GET"; // HTTP request method
    PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket
            , cosPath);
    presignedUrlRequest.setRequestMethod(method);

    String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest);

} catch (CosXmlClientException e) {
    e.printStackTrace();
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectPresignUrl.java).
>

