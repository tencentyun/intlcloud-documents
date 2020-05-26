

## Overview

This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Sets static website configuration for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying static website configuration | Queries the static website configuration information of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting static website configuration | Deletes the static website configuration of a bucket |

## Setting Static Website

#### Feature description

This API (PUT Bucket website) is used to configure a static website for a bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudPutBucketWebsiteRequest`
2. Call the `PutBucketWebsite` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `outputObject` in the `finishBlock` of the callback.

#### Sample request

[//]: # (.cssg-snippet-objc-put-bucket-website)

```
NSString *bucket = @"examplebucket-1250000000";
   NSString * regionName = @"ap-chengdu";

   NSString *indexDocumentSuffix = @"index.html";
   NSString *errorDocKey = @"error.html";
   NSString *derPro = @"https";
   int errorCode = 451;
   NSString * replaceKeyPrefixWith = @"404.html";
   QCloudPutBucketWebsiteRequest *putReq = [QCloudPutBucketWebsiteRequest new];
   putReq.bucket = bucket;

   QCloudWebsiteConfiguration *config = [QCloudWebsiteConfiguration new];

   QCloudWebsiteIndexDocument *indexDocument = [QCloudWebsiteIndexDocument new];
   indexDocument.suffix = indexDocumentSuffix;
   config.indexDocument = indexDocument;

   QCloudWebisteErrorDocument *errDocument = [QCloudWebisteErrorDocument new];
   errDocument.key = errorDocKey;
   config.errorDocument = errDocument;


   QCloudWebsiteRedirectAllRequestsTo *redir = [QCloudWebsiteRedirectAllRequestsTo new];
   redir.protocol  = @"https";
   config.redirectAllRequestsTo = redir;


   QCloudWebsiteRoutingRule *rule = [QCloudWebsiteRoutingRule new];
   QCloudWebsiteCondition *contition = [QCloudWebsiteCondition new];
   contition.httpErrorCodeReturnedEquals = errorCode;
   rule.condition = contition;

   QCloudWebsiteRedirect *webRe = [QCloudWebsiteRedirect new];
   webRe.protocol = @"https";
   webRe.replaceKeyPrefixWith = replaceKeyPrefixWith;
   rule.redirect = webRe;

   QCloudWebsiteRoutingRules *routingRules = [QCloudWebsiteRoutingRules new];
   routingRules.routingRule = @[rule];
   config.rules = routingRules;
   putReq.websiteConfiguration  = config;


   [putReq setFinishBlock:^(id outputObject, NSError *error) {

   }];

   [[QCloudCOSXMLService defaultCOSXML] PutBucketWebsite:putReq];
```

Swift sample code:

[//]: # (.cssg-snippet-swift-put-bucket-website)

```
let req = QCloudPutBucketWebsiteRequest.init();
req.bucket = "examplebucket-1250000000";

let indexDocumentSuffix = "index.html";
let errorDocKey = "error.html";
let derPro = "https";
let errorCode = 451;
let replaceKeyPrefixWith = "404.html";

let config = QCloudWebsiteConfiguration.init();

let indexDocument = QCloudWebsiteIndexDocument.init();
indexDocument.suffix = indexDocumentSuffix;
config.indexDocument = indexDocument;

let errDocument = QCloudWebisteErrorDocument.init();
errDocument.key = errorDocKey;
config.errorDocument = errDocument;


let redir = QCloudWebsiteRedirectAllRequestsTo.init();
redir.protocol  = "https";
config.redirectAllRequestsTo = redir;


let rule = QCloudWebsiteRoutingRule.init();
let contition = QCloudWebsiteCondition.init();
contition.httpErrorCodeReturnedEquals = Int32(errorCode);
rule.condition = contition;

let webRe = QCloudWebsiteRedirect.init();
webRe.protocol = "https";
webRe.replaceKeyPrefixWith = replaceKeyPrefixWith;
rule.redirect = webRe;

let routingRules = QCloudWebsiteRoutingRules.init();
routingRules.routingRule = [rule];
config.rules = routingRules;
req.websiteConfiguration  = config;

req.finishBlock = {(result,error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }

}
QCloudCOSXMLService.defaultCOSXML().putBucketWebsite(req);
```

#### Parameter description

#### `QCloudPutBucketWebsiteRequest` request parameter description

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ---------------------------- | -------- |
| bucket | Bucket for which to set a static website in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | NSString *                   | Yes |
| websiteConfiguration | Sets the configuration information of static website                                       | QCloudWebsiteConfiguration * | Yes       |

#### `QCloudWebsiteConfiguration` parameter description

| Parameter Name | Description | Type | Required |
| --------------------- | ---------------------------------------- | ------------------------------------ | -------- |
| rules                 | Sets redirect rules. Up to 100 `RoutingRule` can be set | QCloudWebsiteRoutingRules *          | Yes       |
| indexDocument         | Index document                                 | QCloudWebsiteIndexDocument *         | Yes       |
| errorDocument         | Error document                                 | QCloudWebisteErrorDocument *         | No       |
| redirectAllRequestsTo | Redirects all requests                           | QCloudWebsiteRedirectAllRequestsTo * | No       |

#### `QCloudWebsiteRoutingRules` parameter description

| Parameter Name | Description | Type | Required |
| ----------- | ---------------------------------------------------- | ------------------------------------ | -------- |
| routingRule | Sets a single redirect rule, including prefix match-triggered and error code-triggered redirect | NSArray<QCloudWebsiteRoutingRule*> * | No       |

#### `QCloudWebsiteIndexDocument` parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------ | ---------- | -------- |
| suffix   | Specifies the index document | NSString * | Yes       |

#### `QCloudWebisteErrorDocument` parameter description

| Parameter Name | Description | Type | Required |
| -------- | ---------------- | ---------- | -------- |
| key      | Specifies the common return for errors | NSString * | No       |

#### `QCloudWebsiteRedirectAllRequestsTo` parameter description

| Parameter Name | Description | Type | Required |
| -------- | -------------------------------------- | --------- | -------- |
| protocol | RedirectAllRequestsTo | Specifies the protocol for global redirect, which can only be `https` | NSString* | No       |



#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Querying Static Website Configuration

#### Feature description

This API (GET Bucket website) is used to query the configuration information of a static website associated with a bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudGetBucketWebsiteRequest`
2. Call the `GetBucketWebsite` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `result` in the `finishBlock` of the callback.



#### Sample request

[//]: # (.cssg-snippet-objc-get-bucket-website)

```
QCloudGetBucketWebsiteRequest *getReq = [QCloudGetBucketWebsiteRequest new];
getReq.bucket = @"examplebucket-1250000000";
[getReq setFinishBlock:^(QCloudWebsiteConfiguration *  result, NSError * error) {

}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketWebsite:getReq];

```

Swift sample code:

[//]: # (.cssg-snippet-swift-get-bucket-website)

```
let req = QCloudGetBucketWebsiteRequest.init();
req.bucket = "examplebucket-1250000000";

req.setFinish {(result,error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketWebsite(req);
```

#### Parameter description

#### `QCloudGetBucketWebsiteRequest` request parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | -------- |
| bucket | Bucket for which to query static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | NSString *                   | Yes |

#### Returned result description

#### `QCloudWebsiteConfiguration` parameter description

| Parameter Name | Description | Type |
| --------------------- | ----------------------------------------- | ------------------------------------ |
| rules                 | Sets redirect rules. Up to 100 `RoutingRule` can be set | QCloudWebsiteRoutingRules *          |
| errorDocument         | Error document                                  | QCloudWebisteErrorDocument *         |
| redirectAllRequestsTo | Redirects all requests                           | QCloudWebsiteRedirectAllRequestsTo * |



#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).



## Deleting Static Website Configuration

#### Feature description

This API (DELETE Bucket website) is used to delete the static website configuration of a bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudDeleteBucketWebsiteRequest`
2. Call the `DeleteBucketWebsite` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `outputObject` in the `finishBlock` of the callback.

#### Sample request

[//]: # (.cssg-snippet-objc-delete-bucket-website)

```
QCloudDeleteBucketWebsiteRequest *delReq = [QCloudDeleteBucketWebsiteRequest new];
delReq.bucket = "examplebucket-1250000000";
[delReq setFinishBlock:^(id outputObject, NSError *error) {

}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketWebsite:delReq];

```

Swift sample code:

[//]: # (.cssg-snippet-swift-delete-bucket-website)

```
let delReq = QCloudDeleteBucketWebsiteRequest.init();
delReq.bucket = "examplebucket-1250000000";
delReq.finishBlock = {(result,error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
}

QCloudCOSXMLService.defaultCOSXML().deleteBucketWebsite(delReq);
```

#### Parameter description

#### `QCloudDeleteBucketWebsiteRequest` request parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | -------- |
| bucket | Bucket for which to delete static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | NSString *                   | Yes |

#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).
