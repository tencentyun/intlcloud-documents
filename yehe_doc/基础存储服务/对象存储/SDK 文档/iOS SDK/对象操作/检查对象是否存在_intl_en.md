## Overview

This document provides an overview of the API and sample code for quickly checking whether an object exists in a bucket. The sample code actually calls the [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) COS API and is a simplified version of the API.

In addition to checking whether an object exists, `HEAD Object` returns object metadata. To view the SDK API that contains the full functionality of `HEAD Object`, please see [Querying Object Metadata](https://intl.cloud.tencent.com/document/product/436/37688).

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |

## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Querying Object Metadata

#### Description

This API is used to check whether an object exists in a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-object-exist)
```objective-c

// Bucket name in the format of `BucketName-APPID`
NSString *bucket = @"examplebucket-1250000000";
// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
NSString *object = @"exampleobject";
[[QCloudCOSXMLService defaultCOSXML] doesObjectExistWithBucket:bucket object:object];
```
>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/HeadObject.m).

**Swift**

[//]: # (.cssg-snippet-head-object) 
```swift
// Bucket name in the format of `BucketName-APPID`
let bucket = "examplebucket-1250000000";
// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
let object  = "exampleobject";

QCloudCOSXMLService.defaultCOSXML().doesObjectExist(withBucket: bucket, object: object);

```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/HeadObject.swift).
