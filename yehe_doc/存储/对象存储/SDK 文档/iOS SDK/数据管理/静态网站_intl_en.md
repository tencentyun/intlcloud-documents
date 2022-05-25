## Overview

This document provides an overview of APIs and SDK code samples for static website.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website configuration | Configures a static website for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying a static website configuration | Queries the static website configuration of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting a static website configuration | Deletes the static website configuration of a bucket |

## SDK API References

For parameters and method description of all APIs in the SDK, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Static Website Configuration

#### Feature description

This API is used to configure a static website for a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-website)
```objective-c
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
NSString *bucket = @"examplebucket-1250000000";

NSString *indexDocumentSuffix = @"index.html";
NSString *errorDocKey = @"error.html";
NSString *derPro = @"https";
int errorCode = 451;
NSString * replaceKeyPrefixWith = @"404.html";
QCloudPutBucketWebsiteRequest *putReq = [QCloudPutBucketWebsiteRequest new];
putReq.bucket = bucket;

QCloudWebsiteConfiguration *config = [QCloudWebsiteConfiguration new];

QCloudWebsiteIndexDocument *indexDocument = [QCloudWebsiteIndexDocument new];

// Specify the object key suffix of the index document. For example, if index.html is specified, then when the root directory of the bucket is accessed,
// the content of index.html will automatically be returned; when the article/ directory is accessed, the content of article/index.html will automatically be returned.
indexDocument.suffix = indexDocumentSuffix;
// Index document configuration
config.indexDocument = indexDocument;

// Error document configuration
QCloudWebisteErrorDocument *errDocument = [QCloudWebisteErrorDocument new];
errDocument.key = errorDocKey;
// Specify the object key of the general error document. When an error occurs and no error code in the redirect rule is hit for redirect, the content of this object key will be returned
config.errorDocument = errDocument;

// Configuration for redirecting all requests
QCloudWebsiteRedirectAllRequestsTo *redir = [QCloudWebsiteRedirectAllRequestsTo new];
redir.protocol  = derPro;
// Specify the target protocol for redirecting all requests; only HTTPS can be used
config.redirectAllRequestsTo = redir;

// Configuration for a single redirect rule
QCloudWebsiteRoutingRule *rule = [QCloudWebsiteRoutingRule new];

// Conditions for the redirect rule
QCloudWebsiteCondition *contition = [QCloudWebsiteCondition new];
contition.httpErrorCodeReturnedEquals = errorCode;
rule.condition = contition;

// Specific redirect destination of the redirect rule
QCloudWebsiteRedirect *webRe = [QCloudWebsiteRedirect new];
webRe.protocol = derPro;

// Specify the object key of the redirect destination specified in the rule. The prefix part matched in the original request will be replaced.
// This can be set only if the Condition is set to KeyPrefixEquals
webRe.replaceKeyPrefixWith = replaceKeyPrefixWith;
rule.redirect = webRe;

QCloudWebsiteRoutingRules *routingRules = [QCloudWebsiteRoutingRules new];
routingRules.routingRule = @[rule];

// Redirect rule configuration. Up to 100 RoutingRule values can be set
config.rules = routingRules;
putReq.websiteConfiguration  = config;

[putReq setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutBucketWebsite:putReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketWebsite.m).

**Swift**

[//]: # (.cssg-snippet-put-bucket-website)
```swift
let req = QCloudPutBucketWebsiteRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
req.bucket = "examplebucket-1250000000";

let indexDocumentSuffix = "index.html";
let errorDocKey = "error.html";
let errorCode = 451;
let replaceKeyPrefixWith = "404.html";

let config = QCloudWebsiteConfiguration.init();

let indexDocument = QCloudWebsiteIndexDocument.init();

// Specify the object key suffix of the index document. For example, if index.html is specified, then when the root directory of the bucket is accessed,
// the content of index.html will automatically be returned; when the article/ directory is accessed, the content of article/index.html will automatically be returned.
indexDocument.suffix = indexDocumentSuffix;

// Index document configuration
config.indexDocument = indexDocument;

// Error document configuration
let errDocument = QCloudWebisteErrorDocument.init();
errDocument.key = errorDocKey;

// Specify the object key of the general error document. When an error occurs and no error code in the redirect rule is hit for redirect, the content of this object key will be returned
config.errorDocument = errDocument;

// Configuration for redirecting all requests
let redir = QCloudWebsiteRedirectAllRequestsTo.init();

// Specify the target protocol for redirecting all requests; only HTTPS can be used
redir.protocol  = "https";
config.redirectAllRequestsTo = redir;

// Configuration for a single redirect rule
let rule = QCloudWebsiteRoutingRule.init();

// Conditions for the redirect rule
let contition = QCloudWebsiteCondition.init();
contition.httpErrorCodeReturnedEquals = Int32(errorCode);
rule.condition = contition;

// Specific redirect destination of the redirect rule
let webRe = QCloudWebsiteRedirect.init();
webRe.protocol = "https";

// Specify the object key of the redirect destination specified in the rule. The prefix part matched in the original request will be replaced.
// This can be set only if the Condition is set to KeyPrefixEquals
webRe.replaceKeyPrefixWith = replaceKeyPrefixWith;
rule.redirect = webRe;

let routingRules = QCloudWebsiteRoutingRules.init();
routingRules.routingRule = [rule];

// Redirect rule configuration. Up to 100 RoutingRule values can be set
config.rules = routingRules;
req.websiteConfiguration  = config;

req.finishBlock = {(result,error) in
    if let result = result {
        // result contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketWebsite(req);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketWebsite.swift).

## Querying Static Website Configuration

#### Feature description

This API (`GET Bucket website`) is used to query the static website configuration associated with a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-website)
```objective-c
QCloudGetBucketWebsiteRequest *getReq = [QCloudGetBucketWebsiteRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
getReq.bucket = @"examplebucket-1250000000";
[getReq setFinishBlock:^(QCloudWebsiteConfiguration *  result,
                         NSError * error) {
    
    // Set redirect rules. Up to 100 RoutingRule values can be set
    QCloudWebsiteRoutingRules *rules =result.rules;
    
    // Index document
    QCloudWebsiteIndexDocument *indexDocument = result.indexDocument;
    
    // Error document
    QCloudWebisteErrorDocument *errorDocument = result.errorDocument;
   
    // Redirect all requests
    QCloudWebsiteRedirectAllRequestsTo *redirectAllRequestsTo = result.redirectAllRequestsTo;
    
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketWebsite:getReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketWebsite.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-website)
```swift
let req = QCloudGetBucketWebsiteRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
req.bucket = "examplebucket-1250000000";

req.setFinish {(result,error) in
    if let result = result {
        let rules = result.rules
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketWebsite(req);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketWebsite.swift).

## Deleting Static Website Configuration

#### Feature description

This API (`DELETE Bucket website`) is used to delete the static website configuration of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-website)
```objective-c
QCloudDeleteBucketWebsiteRequest *delReq = [QCloudDeleteBucketWebsiteRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
delReq.bucket = @"examplebucket-1250000000";

[delReq setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketWebsite:delReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketWebsite.m).

**Swift**

[//]: # (.cssg-snippet-delete-bucket-website)
```swift
let delReq = QCloudDeleteBucketWebsiteRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
delReq.bucket = "examplebucket-1250000000";

delReq.finishBlock = {(result,error) in
    if let result = result {
        // result contains response headers
    } else {
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().deleteBucketWebsite(delReq);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketWebsite.swift).

