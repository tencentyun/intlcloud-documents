## Overview

This document provides an overview of APIs and SDK code samples related to custom endpoints.

| API          | Operation                   | Description                                       |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain | Setting custom endpoint   | Sets a custom endpoint for a bucket |
| GET Bucket domain | Querying custom endpoint   | Queries the custom endpoint of a bucket |

## SDK API References

For parameters and method descriptions of all SDK APIs, see [SDK API References](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Custom Endpoint

#### API description

This API (PUT Bucket domain) is used to configure a custom endpoint for a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-domain)
```objective-c
QCloudPutBucketDomainRequest *req = [QCloudPutBucketDomainRequest new];

// Bucket name in the format of BucketName-APPID
req.bucket = @"examplebucket-1250000000";

QCloudDomainConfiguration *config = [QCloudDomainConfiguration new];
QCloudDomainRule *rule = [QCloudDomainRule new];

// Origin server status
rule.status = QCloudDomainStatueEnabled;
// Endpoint information
rule.name = @"www.baidu.com";

// Replace the existing configuration. If CNAME/TXT is specified as a valid value, the new configuration won’t be delivered until forced verification of the endpoint ownership
rule.replace = QCloudCOSDomainReplaceTypeTxt;
rule.type = QCloudCOSDomainTypeRest;

// An array of rule descriptions
config.rule = [rule];

// Endpoint configuration rule
req.domain  = config;

[request setFinishBlock:^(id outputObject, NSError* error) {
    // outputObject contains all HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
    
}];
[[QCloudCOSXMLService defaultCOSXML]PutBucketDomain:req];
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketDomain.m).

**Swift**

[//]: # (.cssg-snippet-put-bucket-domain)
```swift
let req = QCloudPutBucketDomainRequest.init();

// Bucket name in the format of BucketName-APPID
req.bucket = "examplebucket-1250000000";

let config = QCloudDomainConfiguration.init();
let rule = QCloudDomainRule.init();
rule.status = .enabled;
rule.name = "www.baidu.com";

// Replace the existing configuration. If CNAME/TXT is specified as a valid value, the new configuration won’t be delivered until forced verification of the endpoint ownership
rule.replace = .txt;
rule.type = .rest;

// An array of rule descriptions
config.rules = [rule];

// Endpoint configuration rule
req.domain = config;
req.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketDomain(req);
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketDomain.swift).

#### Error codes

The following describes some frequent special errors that may occur when you make requests using this API.

| Status Code                                 | Description                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict                      | The endpoint record already exists, and no forced overwrite is specified in the request; OR the endpoint record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The endpoint is a domain name without ICP filing in Mainland China                           |

## Querying Custom Endpoint

#### API description

This API (GET Bucket domain) is used to query the custom endpoint of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-domain)
```objective-c
QCloudGetBucketDomainRequest *getReq =  [QCloudGetBucketDomainRequest new];

// Bucket name in the format of BucketName-APPID
getReq.bucket = @"examplebucket-1250000000";

[getReq setFinishBlock:^(QCloudDomainConfiguration * _Nonnull result,
                         NSError * _Nonnull error) {
    // An array of rule descriptions
    NSArray *rules = result.rules;
}];
[[QCloudCOSXMLService defaultCOSXML]GetBucketDomain:getReq];
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketDomain.m).


**Swift**

[//]: # (.cssg-snippet-get-bucket-domain)
```swift
let req = QCloudGetBucketDomainRequest.init();

// Bucket name in the format of BucketName-APPID
req.bucket = "examplebucket-1250000000";

req.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketDomain(req);
```

>?For more samples, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketDomain.swift).


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
<td>Endpoint verification information, which appears as an MD5 checksum of a character string in the format of <code>cos[Region][BucketName-APPID][BucketCreateTime]</code>, where Region is the bucket location, and BucketCreateTime is the bucket creation time in GMT</td>
<td>String</td>
</tr>
</tbody></table>

