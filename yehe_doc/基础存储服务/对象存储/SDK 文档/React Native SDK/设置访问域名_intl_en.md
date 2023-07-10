## Overview

This document describes how to request the COS service by using a non-default domain name.

## Custom Origin Server Domain Name

For more information, see [Enabling Custom Origin Domain](https://www.tencentcloud.com/document/product/436/31507).

The sample code below shows how to access a COS service using a custom origin server domain name.

#### Sample code

```ts
// The bucket region can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
let region = "ap-beijing"; // Bucket region
let customDomain = "exampledomain.com"; // Custom domain name
// Create a `CosXmlServiceConfig` object and modify the configuration parameters as needed
let cosXmlServiceConfig = {
  region: region,
  isDebuggable: false,
  isHttps: true,
  hostFormat: customDomain // Modify the requested domain name
};
// Register the default COS service
await Cos.registerDefaultService(cosXmlServiceConfig)
```

## Global Acceleration Domain Name

For more information on global acceleration, see [Overview](https://www.tencentcloud.com/document/product/436/33409).

The sample code below shows how to access a COS service using a global acceleration endpoint.

#### Sample code

```ts
// The bucket region can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
let region = "ap-beijing"; // Bucket region
let accelerate = true; // Enable the global acceleration endpoint
// Create a `CosXmlServiceConfig` object and modify the configuration parameters as needed
let cosXmlServiceConfig = {
  region: region,
  isDebuggable: false,
  isHttps: true,
  accelerate: accelerate
};
// Register the default COS service
await Cos.registerDefaultService(cosXmlServiceConfig)
```
