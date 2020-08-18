## Overview

This document provides an overview of code samples related to setting server-side encryption for objects.

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Server-side Encryption

You can encrypt uploaded objects in the following ways.

#### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

COS can automatically encrypt your data when entered in IDC and will automatically decrypt it when accessed. Currently, COS supports AES-256 encryption by using a COS master key pair.

You can enable SSE-COS encryption by calling `-(void)setCOSServerSideEncyption` in the iOS SDK.

Objective-C sample code:
```objective-c
[request setCOSServerSideEncyption];
```

Swift sample code:
```swift
request.setCOSServerSideEncyption();
```

#### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

You can enable SSE-C encryption by calling `-(void)setCOSServerSideEncyptionWithCustomerKey:(NSString \*)customerKey` in the SDK for iOS.

> !
>- This type of encryption requires using HTTPS requests.
>- customerKey: the key provided by the user; this key should be a 32-byte string consisting of numbers, letters, and symbols. Chinese characters are not supported.
>- If you used this method when uploading the source file, then it should also be used when downloading, querying, uploading, and copying the source object by using `QCloudCOSXMLDownloadObjectRequest`, `QCloudHeadObjectRequest`, `QCloudCOSXMLUploadObjectRequest`, and `QCloudCOSXMLUploadObjectRequest`, respectively.

Objective-C sample code:
```objective-c
NSString *customKey = @"123456qwertyuioplkjhgfdsazxcvbnm";
[put setCOSServerSideEncyptionWithCustomerKey:customKey];
```

Swift sample code

```swift
let customKey = "123456qwertyuioplkjhgfdsazxcvbnm";
putObject.setCOSServerSideEncyptionWithCustomerKey(customKey);
```
