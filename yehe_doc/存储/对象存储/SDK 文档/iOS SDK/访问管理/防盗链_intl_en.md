## Overview

This document provides an overview of APIs and SDK code samples related to bucket referer allowlist or blocklist.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting bucket referer configuration | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying bucket referer configuration | Queries a bucket referer allowlist or blocklist |

## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Bucket Referer Configuration

#### Description  

This API (PUT Bucket referer) is used to set a referer allowlist/blocklist for a bucket.

>! The COS iOS SDK version should be v5.9.6 or higher.
>

#### Sample request
**Objective-C**

[//]: # ".cssg-snippet-put-bucket-referer"
```objective-c
QCloudPutBucketRefererRequest* request = [QCloudPutBucketRefererRequest new];

// Hotlink protection type. Enumerated values: `Black-List`, `White-List`
request.refererType = QCloudBucketRefererTypeBlackList;

// Whether to enable hotlink protection. Enumerated values: `Enabled`, `Disabled`
request.status = QCloudBucketRefererStatusEnabled;

// Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` (default) 
request.configuration = QCloudBucketRefererConfigurationDeny;

// List of domain names in the blocklist/allowlist. Using a prefix to specify multiple domains is supported. Domain names and IPs with ports are supported. A wildcard (*) is supported for second-level or multi-level domains.
request.domainList = @[@"*.com",@"*.qq.com"];

// Bucket name in the format of `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    if (error){
        // Failed to add hotlink protection
    }else{
        // Failed to add hotlink protection
    }

}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketReferer:request];
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReferer.m).
>

**Swift**

[//]: # (.cssg-snippet-put-bucket-referer)
```swift
let request = QCloudPutBucketRefererRequest.init();

// Hotlink protection type. Enumerated values: `Black-List`, `White-List`
request.refererType = QCloudBucketRefererType.blackList;

// Whether to enable hotlink protection. Enumerated values: `Enabled`, `Disabled`
request.status = QCloudBucketRefererStatus.enabled;

// Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` (default) 
request.configuration = QCloudBucketRefererConfiguration.allow;

// List of domain names in the blocklist/allowlist. Using a prefix to specify multiple domains is supported. Domain names and IPs with ports are supported. A wildcard (*) is supported for second-level or multi-level domains.
request.domainList = ["*.com","*.qq.com"];

// Bucket name in the format of `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

request.finishBlock = {(result,error) in
    if (error != nil){
        // Failed to add hotlink protection
    }else{
        // Failed to add hotlink protection
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketReferer(request);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReferer.swift).
>
## Querying Bucket Referer Configuration

#### Description

This API (GET Bucket referer) is used to query the referer allowlist/blocklist of a bucket.

>! The COS iOS SDK version should be v5.9.6 or higher.
>


#### Sample request
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-referer)
```objective-c
QCloudGetBucketRefererRequest* request = [QCloudGetBucketRefererRequest new];

// Bucket name in the format of `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudBucketRefererInfo * outputObject, NSError *error) {
    // Hotlink protection obtained by the `outputObject` request. For field details, see the API documentation or SDK source code.
    // Class of `QCloudBucketRefererInfo`
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketReferer:request];     
```
>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReferer.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-referer)
```swift
let request = QCloudGetBucketRefererRequest.init();

// Bucket name in the format of `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

request.finishBlock = {(result,error) in
    // Hotlink protection obtained by the `outputObject` request. For field details, see the API documentation or SDK source code.
    // Class of `QCloudBucketRefererInfo`
}
QCloudCOSXMLService.defaultCOSXML().getBucketReferer(request);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReferer.swift).
>



