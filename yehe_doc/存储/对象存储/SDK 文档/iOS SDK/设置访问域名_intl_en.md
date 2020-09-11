## Overview

This document describes how to request COS service using a domain/endpoint other than default COS endpoints.

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Default CDN Acceleration Domain Name

For more information, see [Enabling Default CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31505).

The sample code below shows how to access COS service using a default CDN acceleration domain name.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-set-cdn-domain)
```objective-c
QCloudCOSXMLEndPoint *endpoint = [[QCloudCOSXMLEndPoint alloc] init];
endpoint.suffix = @"file.myqcloud.com";
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/SetCustomDomain.m).

**Swift**

[//]: # (.cssg-snippet-set-cdn-domain)
```swift
let endpoint = QCloudCOSXMLEndPoint();
endpoint.suffix = "file.myqcloud.com";
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/SetCustomDomain.swift).

## Custom CDN Acceleration Domain Name

For more information, see [Enabling Custom CDN Acceleration Domain Names](https://intl.cloud.tencent.com/document/product/436/31506).

The sample code below shows how to access COS service using a custom CDN acceleration domain name.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-set-cdn-custom-domain)
```objective-c
QCloudCOSXMLEndPoint *endpoint = [[QCloudCOSXMLEndPoint alloc] initWithLiteralURL:[NSURL URLWithString:@"exampledomain.com"]];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/SetCustomDomain.m).

**Swift**

[//]: # (.cssg-snippet-set-cdn-custom-domain)
```swift
let endpoint = QCloudCOSXMLEndPoint.init(literalURL: NSURL.init(string: "exampledomain.com") as URL?);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/SetCustomDomain.swift).

## Custom Endpoint

For more information, see [Enabling Custom Endpoints](https://intl.cloud.tencent.com/document/product/436/31507).

The sample code below shows how to access COS service using a custom endpoint.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-set-custom-domain)
```objective-c
NSString *customDomain = @"exampledomain.com"; // Custom endpoint
QCloudCOSXMLEndPoint *endpoint = [[QCloudCOSXMLEndPoint alloc] initWithLiteralURL:[NSURL URLWithString:customDomain]];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/SetCustomDomain.m).

**Swift**

[//]: # (.cssg-snippet-set-custom-domain)
```swift
let endpoint = QCloudCOSXMLEndPoint.init(literalURL: NSURL.init(string: "exampledomain.com") as URL?);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/SetCustomDomain.swift).

## Global Acceleration Endpoint

For more information on global acceleration, see [Overview](https://intl.cloud.tencent.com/document/product/436/33409).

The sample code below shows how to access COS service using a global acceleration endpoint.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-set-accelerate-domain)
```objective-c
QCloudCOSXMLEndPoint *endpoint = [[QCloudCOSXMLEndPoint alloc]init];
endpoint.suffix = @"cos.accelerate.myqcloud.com";
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/SetCustomDomain.m).
**Swift**

[//]: # (.cssg-snippet-set-accelerate-domain)
```swift
let endpoint = QCloudCOSXMLEndPoint();
endpoint.suffix = "cos.accelerate.myqcloud.com";
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/SetCustomDomain.swift).
