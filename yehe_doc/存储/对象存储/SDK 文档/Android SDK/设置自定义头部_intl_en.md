## Overview

This document describes how to include custom headers in a request using the SDK.

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

#### Description

COS allows object upload requests to include custom headers that  specify user-defined metadata. These headers start with `x-cos-meta-`, end with a custom suffix, and are saved as part of the object metadata.

If you have activated the Tencent Cloud CI service, you can specify the `Pic-Operations` header to enable automatic image processing. For detailed API instructions, see [Persistence Processing](https://intl.cloud.tencent.com/document/product/1045/33695).

#### Sample code

[//]: # ".cssg-snippet-set-custom-headers"
```java
// The bucket region can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, see https://intl.cloud.tencent.com/document/product/436/6224.
String region = "ap-beijing"; // Bucket region
String commonHeaderKey = "commonexamplekey"; // Key of the custom common header
String commonHeaderValue = "commonexamplevalue"; // Value of the custom common header
String requestHeaderKey = "requestexamplekey"; // Key of the custom request header
String requestHeaderValue = "requestexamplevalue"; // Value of the custom request header

CosXmlServiceConfig cosXmlServiceConfig = new CosXmlServiceConfig.Builder()
        .isHttps(true)
        .setRegion(region)
        .setDebuggable(false)
        // Add a custom common header to each request
        .addHeader(commonHeaderKey, commonHeaderValue)
        .builder();

CosXmlService cosXmlService = new CosXmlService(context, cosXmlServiceConfig,
        credentialProvider);

// Add a custom header with higher priority than common headers to a single request
HeadObjectRequest headObjectRequest = new HeadObjectRequest(bucket, cosPath);
try {
    headObjectRequest.setRequestHeaders(requestHeaderKey, requestHeaderValue, false);
} catch (CosXmlClientException e) {
    e.printStackTrace();
}

// Initiate a request
cosXmlService.headObjectAsync(headObjectRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        HeadObjectResult headObjectResult = (HeadObjectResult) result;
    }

    @Override
    public void onFail(CosXmlRequest request, CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        if (clientException != null) {
            clientException.printStackTrace();
        } else {
            serviceException.printStackTrace();
        }
    }
});
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/SetCustomHeaders.java).

