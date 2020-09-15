## Overview

This document provides an overview of APIs and SDK code samples related to custom endpoints.

| API | Operation | Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting a custom endpoint | Sets a custom endpoint for a bucket |
| GET Bucket domain    | Querying a custom endpoint | Queries the custom endpoint of a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a Custom Endpoint

#### API description 

This API is used to configure a custom endpoint for a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-domain)
```objective-c
QCloudPutBucketDomainRequest *req = [QCloudPutBucketDomainRequest new];

// Bucket name in the format: `BucketName-APPID`
req.bucket = @"examplebucket-1250000000";

QCloudDomainConfiguration *config = [QCloudDomainConfiguration new];
QCloudDomainRule *rule = [QCloudDomainRule new];

// Status of the endpoint. Valid values: QCloudDomainStatueEnabled and QCloudDomainStatueDisabled
rule.status = QCloudDomainStatueEnabled;
// Endpoint name
rule.name = @"www.baidu.com";

// Replace the existing configuration. If CNAME/TXT is specified as a valid value, the new configuration won’t be delivered until verification of endpoint ownership is complete
rule.replace = QCloudCOSDomainReplaceTypeTxt;
rule.type = QCloudCOSDomainTypeRest;

// An array of rules
config.rule = @[rule];

// Endpoint configuration rule
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

// Bucket name in the format: `BucketName-APPID`
req.bucket = "examplebucket-1250000000";

let config = QCloudDomainConfiguration.init();
let rule = QCloudDomainRule.init();
// Indicate whether the configuration is enabled. Valid values: .enabled, .disabled
rule.status = .enabled;
rule.name = "www.baidu.com";

// Replace the existing configuration. If CNAME/TXT is specified as a valid value, the new configuration won’t be delivered until verification of endpoint ownership is complete
rule.replace = .txt;
rule.type = .rest;

// An array of rules
config.rules = [rule];

// Endpoint configuration rule
req.domain = config;
req.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketDomain(req);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketDomain.swift).

#### Error codes

The following describes some common errors that may occur when making requests using this API.

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The endpoint record already exists, and forced overwrite is not specified in the request; OR the endpoint record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The endpoint is a domain name without ICP filing in the Chinese mainland.                          |

## Querying a Custom Endpoint

#### API description 

This API is used to query the custom endpoint of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-domain)
```objective-c
QCloudGetBucketDomainRequest *getReq =  [QCloudGetBucketDomainRequest new];

// Bucket name in the format: `BucketName-APPID`
getReq.bucket = @"examplebucket-1250000000";

[getReq setFinishBlock:^(QCloudDomainConfiguration * _Nonnull result,
                         NSError * _Nonnull error) {
    // An array of rules
    NSArray *rules = result.rules;
}];
[[QCloudCOSXMLService defaultCOSXML]GetBucketDomain:getReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketDomain.m).


**Swift**

[//]: # (.cssg-snippet-get-bucket-domain)
```swift
let req = QCloudGetBucketDomainRequest.init();

// Bucket name in the format: `BucketName-APPID`
req.bucket = "examplebucket-1250000000";

req.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains information on the endpoint
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketDomain(req);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketDomain.swift).


#### Response parameters

<table>
<thead>
<tr>
<th>Parameter Name</td>
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

