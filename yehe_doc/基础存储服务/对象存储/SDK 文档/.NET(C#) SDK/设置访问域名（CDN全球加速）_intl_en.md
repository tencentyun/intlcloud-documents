## Overview

This document describes how to request the COS service using a non-default endpoint.

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

### Custom origin server domain name

For more information, see [Enabling Custom Origin Domain](https://intl.cloud.tencent.com/document/product/436/31507).

The sample code below shows how to access a COS service using a custom origin server domain name.

#### Sample code

[//]: # (.cssg-snippet-set-custom-domain)
```cs
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetRegion("COS_REGION")  // Sets the default bucket region
  // Set the requested endpoint to “your.domain.com”
  .SetHost("your.domain.com") // Custom endpoint
  .Build();
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/SetCustomDomain.cs).

### Global acceleration endpoint

For more information on global acceleration, see [Overview](https://intl.cloud.tencent.com/document/product/436/33409).

The sample code below shows how to access a COS service using a global acceleration endpoint.

#### Sample code

[//]: # (.cssg-snippet-set-accelerate-domain)
```cs
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetEndpointSuffix("cos.accelerate.myqcloud.com")
  .Build();
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/SetCustomDomain.cs).

### Custom CDN domain name

For more information, see [Enabling Custom CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31506).

The sample code below shows how to access a COS service using a custom CDN acceleration domain name.

#### Sample code

```cs
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetHost("exampledomain.com")
  .Build();
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/SetCustomDomain.cs).

### Default CDN domain name

For more information, see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505).

The sample code below shows how to access a COS service using a default CDN acceleration domain name.

#### Sample code

```cs
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetEndpointSuffix("file.myqcloud.com")
  .Build();
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/SetCustomDomain.cs).
