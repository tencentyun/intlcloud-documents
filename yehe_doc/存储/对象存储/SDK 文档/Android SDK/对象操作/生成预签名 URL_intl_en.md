## Overview

This document provides an overview of SDK code samples related to generating pre-signed object URLs.

>?
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 


## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

## Generating a Pre-Signed Object URL

#### Sample code 1. Generating a pre-signed upload URL

[//]: # (.cssg-snippet-get-presign-upload-url)
```java
try {
     // Bucket name
    String bucket = "examplebucket-1250000000";
    // Object key, the unique location ID of an object in a bucket. For more information, see [Object Key](https://www.tencentcloud.com/document/product/436/13324).
    // Note: The key does not need to be encoded.
    String cosPath = "exampleobject";
    // HTTP request method
    String method = "PUT";
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
    // Set the signature validity period to be 60s. Note that here is the signature validity period. You need to ensure the key validity period by yourself.
    presignedUrlRequest.setSignKeyTime(60);
    // Set not to sign `Host`
    presignedUrlRequest.addNoSignHeader("Host");
    String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectPresignUrl.java).

#### Sample code 2. Generating a pre-signed download URL

[//]: # (.cssg-snippet-get-presign-download-url)
```java
try {
    // Bucket name
    String bucket = "examplebucket-1250000000"; 
    // Object key, the unique location ID of an object in a bucket. For more information, see [Object Key](https://www.tencentcloud.com/document/product/436/13324).
    // Note: The key does not need to be encoded.
    String cosPath = "exampleobject";
    // HTTP request method
    String method = "GET"; 
    PresignedUrlRequest presignedUrlRequest = new PresignedUrlRequest(bucket
            , cosPath);
    presignedUrlRequest.setRequestMethod(method);

    // Set the signature validity period to be 60s. Note that here is the signature validity period. You need to ensure the key validity period by yourself.
    presignedUrlRequest.setSignKeyTime(60);
    // Set not to sign `Host`
    presignedUrlRequest.addNoSignHeader("Host");

    String urlWithSign = cosXmlService.getPresignedURL(presignedUrlRequest);

} catch (CosXmlClientException e) {
    e.printStackTrace();
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/ObjectPresignUrl.java).

