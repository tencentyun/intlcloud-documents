## Overview

This document describes how to request a COS service using a non-default COS endpoint.

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

### Custom endpoint

For more information, see [Enabling Custom Origin Domain](https://intl.cloud.tencent.com/document/product/436/31507).

The sample code below shows how to access a COS service using a custom endpoint.

#### Sample code

[//]: # ".cssg-snippet-set-custom-domain"
```cs
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetRegion("COS_REGION")  // Set the default bucket region
  // Set the requested endpoint to “your.domain.com”
  .SetHost("your.domain.com") // Custom endpoint
  .Build();
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/SetCustomDomain.cs).

### Global acceleration endpoint

For more information on global acceleration, see [Overview](https://intl.cloud.tencent.com/document/product/436/33409).

The sample code below shows how to access a COS service using a global acceleration endpoint.

#### Sample code

[//]: # ".cssg-snippet-set-accelerate-domain"
```cs
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetEndpointSuffix("cos.accelerate.myqcloud.com")
  .Build();
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/SetCustomDomain.cs).
