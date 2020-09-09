## Overview

This document describes how to enable server-side encryption when uploading objects. There are three types of keys that can be used for server-side encryption:

* COS-managed key
* KMS-managed key
* Customer-provided key

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

#### Description

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-object-sse)
```objective-c
QCloudCOSXMLUploadObjectRequest *request = [QCloudCOSXMLUploadObjectRequest new];
[request setCOSServerSideEncyption];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PutObjectSSE.m).

**Swift**

[//]: # (.cssg-snippet-put-object-sse)
```swift
request.setCOSServerSideEncyption();
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PutObjectSSE.swift).

### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

#### Description

With this method, the encryption key is provided by the customer. To upload an object, COS will apply AES-256 encryption to the data using the customer-provided encryption key pair.

> !
>- This type of encryption requires using HTTPS requests.
>- You need to provide a 32-byte string as the key, a combination of numbers, letters, and characters, with Chinese characters not supported.
>- If a file was key-encrypted when uploaded, you need to include the same key in your GET (download) or HEAD (query) request for it to succeed.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-object-sse-c)
```objective-c
QCloudCOSXMLUploadObjectRequest *request = [QCloudCOSXMLUploadObjectRequest new];
NSString *customKey = @"123456qwertyuioplkjhgfdsazxcvbnm";
[request setCOSServerSideEncyptionWithCustomerKey:customKey];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PutObjectSSE.m). **Swift**

[//]: # (.cssg-snippet-put-object-sse-c)
```swift
let customKey = "123456qwertyuioplkjhgfdsazxcvbnm";
request.setCOSServerSideEncyptionWithCustomerKey(customKey);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PutObjectSSE.swift).
