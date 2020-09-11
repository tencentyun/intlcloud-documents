## Overview

This document describes how to include custom headers in a request using the SDK.

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

#### Description

COS allows object upload requests to include custom headers that specify user-defined metadata. These headers start with `x-cos-meta-`, end with a custom suffix, and are saved as part of the object metadata.

If you have activated the Tencent Cloud CI service, you can specify the `Pic-Operations` header to enable automatic image processing. For detailed API instructions, see [Persistence Processing](https://intl.cloud.tencent.com/document/product/1045/33695).

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-set-custom-headers)
```objective-c
request.customHeaders[@"custom-key"] = @"custom-value";
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/SetCustomHeaders.m).

**Swift**

[//]: # (.cssg-snippet-set-custom-headers)
```swift
request.customHeaders["custom-key"] = "custom-value";
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/SetCustomHeaders.swift).

