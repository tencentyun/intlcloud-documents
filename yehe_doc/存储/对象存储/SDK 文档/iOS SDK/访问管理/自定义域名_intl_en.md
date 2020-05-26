

## Overview

This document provides an overview of APIs and SDK code samples related to custom domain name.

| API | Operation Name | Operation Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting custom domain name | Sets custom domain name information for a bucket |
| GET Bucket domain | Querying custom domain name | Queries the custom domain name information of a bucket |

## Setting Custom Domain Name

#### Feature description

This API (PUT Bucket domain) is used to configure a custom domain name for a bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudPutBucketDomainRequest`
2. Call the `PutBucketDomain` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `outputObject` in the `finishBlock` of the callback.

#### Sample request

[//]: # (.cssg-snippet-objc-put-bucket-domain)

```
QCloudPutBucketDomainRequest *req = [QCloudPutBucketDomainRequest new];
    req.bucket = @"examplebucket-1250000000";
    QCloudDomainConfiguration *config = [QCloudDomainConfiguration new];
    QCloudDomainRule *rule = [QCloudDomainRule new];
    rule.status = QCloudDomainStatueEnabled;
    rule.name = @"www.baidu.com";
    rule.replace = QCloudCOSDomainReplaceTypeTxt;
    rule.type = QCloudCOSDomainTypeRest;
    config.rules = @[rule];
    req.domain  = config;
    [req setFinishBlock:^(id outputObject, NSError *error) {

    }];
      [[QCloudCOSXMLService defaultCOSXML]PutBucketDomain:req];

```

Swift sample code:

[//]: # (.cssg-snippet-swift-put-bucket-domain)

```
let req = QCloudPutBucketDomainRequest.init();
req.bucket = "examplebucket-1250000000";

let config = QCloudDomainConfiguration.init();
let rule = QCloudDomainRule.init();
rule.status = .enabled;
rule.name = "www.baidu.com";
rule.replace = .txt;
rule.type = .rest;
config.rules = [rule];
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

#### Parameter description

#### `QCloudPutBucketDomainRequest` request parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | --------------------------- | -------- |
| bucket   | Bucket for which to set a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | NSString *                  | Yes       |
| domain   | Domain name configuration rule                                               | QCloudDomainConfiguration * | Yes       |

#### `QCloudDomainConfiguration` parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------ | ----------------------------- | -------- |
| rules    | Rule set array | NSArray<QCloudDomainRule*>  * | Yes       |

#### `QCloudDomainRule` parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | -------------------------- | -------- |
| name     | Custom domain name. Valid values: letter, digit, dot                      | NSString *                 | Yes       |
| status   | Domain name status. Valid values: ENABLED/DISABLED                   | QCloudDomainStatue         | Yes       |
| type     | Type of bound origin server. Valid values: REST/WEBSITE                           | QCloudCOSDomainType        | Yes       |
| replace  | Overwrites existing configuration. Valid values: CNAME/TXT. If this parameter is entered, the configuration will be distributed after the domain name ownership is forcibly verified | QCloudCOSDomainReplaceType | Yes       |

#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Querying Custom Domain Name

#### Feature description

This API (GET Bucket domain) is used to query the custom domain name information of a bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudGetBucketDomainRequest`
2. Call the `GetBucketDomain` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `result` in the `finishBlock` of the callback.

#### Sample request

[//]: # (.cssg-snippet-objc-get-bucket-domain)

```
QCloudGetBucketDomainRequest *getReq =  [QCloudGetBucketDomainRequest new];
getReq.bucket = @"examplebucket-1250000000";
[getReq setFinishBlock:^(QCloudDomainConfiguration * _Nonnull result, NSError * _Nonnull error) {

}];
[[QCloudCOSXMLService defaultCOSXML]GetBucketDomain:getReq];

```

Swift sample code:

[//]: # (.cssg-snippet-swift-get-bucket-domain)

```
let req = QCloudGetBucketDomainRequest.init();
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

#### Parameter description

#### `QCloudGetBucketTaggingRequest` request parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | --------------------------- | -------- |
| bucket   | Bucket for which to query a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | NSString *                  | Yes       |
| domain   | Domain name configuration rule                                               | QCloudDomainConfiguration * | Yes       |



#### Return parameter description

#### `QCloudDomainConfiguration` parameter description

| Parameter Name | Description | Type |
| -------- | ------------------ | ----------------------------- |
| rules    | Rule set array | NSArray<QCloudDomainRule*>  * |

#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).
