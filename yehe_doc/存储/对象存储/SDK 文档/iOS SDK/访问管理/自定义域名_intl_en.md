## Overview

This document provides an overview of APIs and SDK code samples for custom domains.

| API | Operation | Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting a custom domain | Sets a custom domain for a bucket |
| GET Bucket domain    | Querying a custom domain | Queries the custom domain of a bucket |

## SDK API References

For parameters and method description of all APIs in the SDK, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Custom Domains

#### Feature description

This API is used to set a custom domain for a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-domain)
```objective-c
QCloudPutBucketDomainRequest *req = [QCloudPutBucketDomainRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
req.bucket = @"examplebucket-1250000000";

QCloudDomainConfiguration *config = [QCloudDomainConfiguration new];
QCloudDomainRule *rule = [QCloudDomainRule new];

// Origin server status. Valid values: QCloudDomainStatueEnabled; QCloudDomainStatueDisabled
rule.status = QCloudDomainStatueEnabled;
// Domain information
rule.name = @"www.baidu.com";

// Replace the existing configuration. If CNAME/TXT is specified as a valid value, the new configuration won’t be delivered until verification of endpoint ownership is complete
rule.replace = QCloudCOSDomainReplaceTypeTxt;
rule.type = QCloudCOSDomainTypeRest;

// Array of rule descriptions
config.rule = @[rule];

// Domain configuration rule
req.domain  = config;

[request setFinishBlock:^(id outputObject, NSError* error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
    
}];
[[QCloudCOSXMLService defaultCOSXML]PutBucketDomain:req];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketDomain.m).

**Swift**

[//]: # (.cssg-snippet-put-bucket-domain)
```swift
let req = QCloudPutBucketDomainRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";

let config = QCloudDomainConfiguration.init();
let rule = QCloudDomainRule.init();
// Indicate whether the rule is enabled. Valid values: .enabled; .disabled
rule.status = .enabled;
rule.name = "www.baidu.com";

// Replace the existing configuration. If CNAME/TXT is specified as a valid value, the new configuration won’t be delivered until verification of endpoint ownership is complete
rule.replace = .txt;
rule.type = .rest;

// Array of rule descriptions
config.rules = [rule];

// Domain configuration rule
req.domain  = config;
req.finishBlock = {(result,error) in
    if let result = result {
        // result contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketDomain(req);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketDomain.swift).

#### Error codes

The following describes some common errors that may occur when you call this API:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The domain record already exists, and forced overwrite is not specified in the request; OR the domain record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The domain does not have an ICP filing in the Chinese mainland                          |

## Querying a Custom Domain

#### Feature description

This API is used to query the custom domain set for a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-domain)
```objective-c
QCloudGetBucketDomainRequest *getReq =  [QCloudGetBucketDomainRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getReq.bucket = @"examplebucket-1250000000";

[getReq setFinishBlock:^(QCloudDomainConfiguration * _Nonnull result,
                         NSError * _Nonnull error) {
    // Array of rule descriptions
    NSArray *rules = result.rules;
}];
[[QCloudCOSXMLService defaultCOSXML]GetBucketDomain:getReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketDomain.m).


**Swift**

[//]: # (.cssg-snippet-get-bucket-domain)
```swift
let req = QCloudGetBucketDomainRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";

req.finishBlock = {(result,error) in
    if let result = result {
        // result contains origin server information
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketDomain(req);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketDomain.swift).


#### Response parameters

<table>
<thead>
<tr>
<th>Parameter Name</th>
<th>Description</th>
<th>Type</th>
</tr>
</thead>
<tbody><tr>
<td nowrap="nowrap">x-cos-domain-txt-verification</td>
<td>Endpoint verification information. This field is an MD5 checksum of a character string in the format: <code>cos[Region][BucketName-APPID][BucketCreateTime]</code>, where `Region` is the bucket region and `BucketCreateTime` is the time the bucket was created in GMT format</td>
<td>String</td>
</tr>
</tbody></table>

