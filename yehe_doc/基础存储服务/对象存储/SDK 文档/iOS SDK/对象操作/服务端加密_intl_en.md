## Overview

This document describes how to enable server-side encryption when uploading objects. There are three types of keys that can be used for server-side encryption:

* COS-managed key
* Customer-provided key
* KMS-managed key


## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PutObjectSSE.m).

**Swift**

[//]: # (.cssg-snippet-put-object-sse)
```swift
request.setCOSServerSideEncyption();
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PutObjectSSE.swift).

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

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PutObjectSSE.m).
>

**Swift**

[//]: # (.cssg-snippet-put-object-sse-c)
```swift
let customKey = "123456qwertyuioplkjhgfdsazxcvbnm";
request.setCOSServerSideEncyptionWithCustomerKey(customKey);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PutObjectSSE.swift).
>

### Using server-side encryption with KMS-managed encryption keys (SSE-KMS) to protect data

#### Description

SSE-KMS encryption is server-side encryption using keys managed by KMS, a Tencent Cloud security management service. KMS is designed to generate and protect your keys using third party–certified hardware security modules (HSM). It allows you to easily create and manage keys for use in multiple applications and services, while meeting regulatory and compliance requirements. For information on how to activate KMS service, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-object-sse-kms)
```objective-c
QCloudCOSXMLUploadObjectRequest *request = [QCloudCOSXMLUploadObjectRequest new];
NSString *customKey = @"123456qwertyuioplkjhgfdsazxcvbnm";
NSString *arrJsonStr = @"{\"key\":\"value\"}";
[request setCOSServerSideEncyptionWithKMSCustomKey:customKey jsonStr:arrJsonStr];
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PutObjectSSE.m).
>

**Swift**

[//]: # (.cssg-snippet-put-object-sse-kms)
```swift
let customKey = "123456qwertyuioplkjhgfdsazxcvbnm";
let arrJsonStr = "{\"key\":\"value\"}";
self.advancedRequest?.setCOSServerSideEncyptionWithKMSCustomKey(customKey, jsonStr: arrJsonStr);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PutObjectSSE.swift).
>
