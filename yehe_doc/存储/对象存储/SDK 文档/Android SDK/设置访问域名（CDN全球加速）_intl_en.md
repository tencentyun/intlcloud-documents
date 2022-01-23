## Overview

This document describes how to request the COS service using a non-default endpoint.

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, see [SDK API Reference](https://cos-android-sdk-doc-1253960454.file.myqcloud.com/).

### Default CDN acceleration domain name

For more information, see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505).

The sample code below shows how to access a COS service using a default CDN acceleration domain name.

#### Sample code

[//]: # ".cssg-snippet-set-cdn-domain"
```java
// The bucket region can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, see https://intl.cloud.tencent.com/document/product/436/6224.
String region = "ap-beijing"; // Bucket region
// Default CDN acceleration domain name of the bucket
String cdnDomain = "examplebucket-1250000000.file.myqcloud.com";

CosXmlServiceConfig cosXmlServiceConfig = new CosXmlServiceConfig.Builder()
        .isHttps(true)
        .setRegion(region)
        .setDebuggable(false)
        .setHostFormat(cdnDomain) // Modify the requested domain name
        .addHeader("Host", cdnDomain) // Modify the “Host” filed in the header
        .builder();

// The credentialProvider class is not provided. Instead, you add parameters to the URL when downloading
// for CDN permission verification
CosXmlService cosXmlService = new CosXmlService(context, cosXmlServiceConfig);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/SetCustomDomain.java).

### Custom CDN acceleration domain name

For more information, see [Enabling Custom CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31506).

The sample code below shows how to access a COS service using a custom CDN acceleration domain name.

#### Sample code

[//]: # ".cssg-snippet-set-cdn-custom-domain"
```java
// The bucket region can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, see https://intl.cloud.tencent.com/document/product/436/6224.
String region = "ap-beijing"; // Bucket region
String cdnCustomDomain = "exampledomain.com"; // Custom CDN acceleration domain name

CosXmlServiceConfig cosXmlServiceConfig = new CosXmlServiceConfig.Builder()
        .isHttps(true)
        .setRegion(region)
        .setDebuggable(false)
        .setHostFormat(cdnCustomDomain) // Modify the requested domain name
        .addHeader("Host", cdnCustomDomain) // Modify the “Host” filed in the header
        .builder();
// The credentialProvider class is not provided. Instead, you add parameters to the URL when downloading
// for CDN permission verification
CosXmlService cosXmlService = new CosXmlService(context, cosXmlServiceConfig);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/SetCustomDomain.java).

### Custom origin server domain name

For more information, see [Enabling Custom Origin Domain](https://intl.cloud.tencent.com/document/product/436/31507).

The sample code below shows how to access a COS service using a custom origin server domain name.

#### Sample code

[//]: # ".cssg-snippet-set-custom-domain"
```java
// The bucket region can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, see https://intl.cloud.tencent.com/document/product/436/6224.
String region = "ap-beijing"; // Bucket region
String customDomain = "exampledomain.com"; // Custom origin server domain name

CosXmlServiceConfig cosXmlServiceConfig = new CosXmlServiceConfig.Builder()
        .isHttps(true)
        .setRegion(region)
        .setDebuggable(false)
        .setHostFormat(customDomain) // Modify the requested domain name
        .builder();

CosXmlService cosXmlService = new CosXmlService(context, cosXmlServiceConfig,
        credentialProvider);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/SetCustomDomain.java).

### Global acceleration endpoint

For more information on global acceleration, see [Overview](https://intl.cloud.tencent.com/document/product/436/33409).

The sample code below shows how to access a COS service using a global acceleration endpoint.

#### Sample code

[//]: # ".cssg-snippet-set-accelerate-domain"
```java
// The bucket region can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, see https://intl.cloud.tencent.com/document/product/436/6224.
String region = "ap-beijing"; // Bucket region

CosXmlServiceConfig cosXmlServiceConfig = new CosXmlServiceConfig.Builder()
        .isHttps(true)
        .setRegion(region)
        .setDebuggable(false)
        .setAccelerate(true) // Enable a global acceleration endpoint
        .builder();

CosXmlService cosXmlService = new CosXmlService(context, cosXmlServiceConfig,
        credentialProvider);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Android/app/src/androidTest/java/com/tencent/qcloud/cosxml/cssg/SetCustomDomain.java).
