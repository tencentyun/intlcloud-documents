## Overview

This document describes how to request the COS service by using a non-default domain name.

## Custom Origin Server Domain Name

For more information, see [Enabling Custom Origin Server Domains](https://www.tencentcloud.com/document/product/436/31507).

The sample code below shows how to access a COS service using a custom origin server domain name.

#### Sample code

```dart
// The bucket region can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
String region = "ap-beijing"; // Bucket region
String customDomain = "exampledomain.com"; // Custom origin server domain name

// Create a `CosXmlServiceConfig` object and modify the configuration parameters as needed
CosXmlServiceConfig serviceConfig = CosXmlServiceConfig(
    region: region,
    isDebuggable: false,
    isHttps: true,
    hostFormat: customDomain // Modify the requested domain name
);
// Register the default COS service
Cos().registerDefaultService(serviceConfig);
```

## Global Acceleration Domain Name

For more information on global acceleration, see [Overview](https://www.tencentcloud.com/document/product/436/33409).

The sample code below shows how to access a COS service using a global acceleration endpoint.

#### Sample code

```dart
// The bucket region can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
String region = "ap-beijing"; // Bucket region
// Whether to enable global acceleration
bool accelerate = true;
// Create a `CosXmlServiceConfig` object and modify the configuration parameters as needed
CosXmlServiceConfig serviceConfig = CosXmlServiceConfig(
    region: region,
    isDebuggable: false,
    isHttps: true,
    accelerate: accelerate // Use a global acceleration domain name
);
// Register the default COS service
Cos().registerDefaultService(serviceConfig);
```
