## Overview

This document provides an overview of APIs related to cross-origin access, lifecycle, versioning, and cross-region replication and corresponding SDK sample code.

- It is assumed that you have downloaded, installed, and initialized the SDK as instructed in [Getting Started](https://intl.cloud.tencent.com/document/product/436/11280).
- You are recommended to use Command+F to search for the API you want to query, check the provided descriptions of the API, and then copy the sample code to your project for execution.

>  If you want to learn more about the function of the API or the meanings of its parameters, you are recommended to directly view the comments in the code. In Xcode, you can use three-finger tap or Force Touch or hover over a variable and press Control+Command+D to see its interpretation.   

**Cross-origin access**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning feature of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rule of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rule of a bucket |

## Cross-origin Access

### Setting Cross-origin Access Configuration

#### Method Prototype

Before setting the cross-origin resource sharing (CORS) for a bucket, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudPutBucketCORSRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudPutBucketCORSRequest, set the bucket, and load the required CORS into QCloudCORSRule. If there are multiple sets of CORS settings, you can put multiple QCloudCORSRules into one NSArray and then place the array in the request in the rules attribute of QCloudCORSConfiguration.    
2. Call the PutBucketCORS method in the QCloudCOSXMLService object to initiate a request.    
3. Check whether the setting succeeded in the finishBlock of the callback (i.e., whether error is empty) and perform some additions actions after successful setting.   

#### QCloudPutBucketCORSRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------------------------- | ---- |
| bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| corsConfiguration | Specific parameter where CORS is encapsulated                                       | QCloudCORSConfiguration * | Yes   |

QCloudCORSConfiguration parameter descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------ | -------------------------------- | ---- |
| rules    | Array that stores the CORS. The array content is the QCloudCORSRule instance | NSArray&lt;QCloudCORSRule`*` > * | Yes   |

QCloudCORSRule parameter descriptions

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ---------------------------- | ---- |
| identifier | Configures the rule ID | NSString * | No |
| allowedMethod | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | NSArray &lt;NSString`*`> * | Yes |
| allowedOrigin | Allowed origin in the format of protocol://domain name[:port number], such as `http://www.qq.com`. Wildcard \* is supported | NSString * | Yes |
| allowedHeader | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard * is supported | NSArray &lt;NSString `*` > * | Yes   |
| maxAgeSeconds | Sets the validity period of the result of the OPTIONS request | int | Yes |
| exposeHeader | Sets custom header information from the server that the browser can receive | NSString * | Yes |

#### Examples

```objective-c
QCloudPutBucketCORSRequest* putCORS = [QCloudPutBucketCORSRequest new];
QCloudCORSConfiguration* cors = [QCloudCORSConfiguration new];

QCloudCORSRule* rule = [QCloudCORSRule new];
rule.identifier = @"sdk";
rule.allowedHeader = @[@"origin",@"host",@"accept",@"content-type",@"authorization"];
rule.exposeHeader = @"ETag";
rule.allowedMethod = @[@"GET",@"PUT",@"POST", @"DELETE", @"HEAD"];
rule.maxAgeSeconds = 3600;
rule.allowedOrigin = @"*";
cors.rules = @[rule];
putCORS.corsConfiguration = cors;
putCORS.bucket = @"examplebucket-1250000000";
[putCORS setFinishBlock:^(id outputObject, NSError *error) {
// Get the header information returned by the server from the outputObject
    if (!error) {
      //success
  }
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketCORS:putCORS];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying Cross-origin Access Configuration

#### Method Prototype

Before querying cross-origin access configuration, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudGetBucketCORSRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:

1. Instantiate QCloudGetBucketCORSRequest and enter the name of the bucket for which to get the CORS.
2. Call the GetBucketCORS method in the QCloudCOSXMLService object to initiate a request.
3. Get the result from finishBlock of the callback. The result is encapsulated in the QCloudCORSConfiguration object, where the rules attribute is an array that contains a set of QCloudCORSRules, and the specific CORS settings are encapsulated in the QCloudCORSRule objects.

#### QCloudGetBucketCORSRequest Request Parameter Descriptions

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ---------- |
| bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * |

#### Return Result Descriptions

 QCloudCORSConfiguration parameter descriptions

| Parameter Name | Description | Type |
| -------- | -------- | -------------------------------- |
| rules    | Rule set | NSArray&lt;QCloudCORSRule`*` > * |

QCloudCORSRule parameter descriptions

| Parameter Name | Description | Type |
| ------------- | ------------------------------------------------------------ | ---------------------------- |
| identifier    | Configures the rule ID                                                | NSString *                   |
| allowedMethod | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | NSArray &lt;NSString`*`> * |
| allowedOrigin | Allowed origin in the format of protocol://domain name[:port number], such as `http://www.qq.com`. Wildcard \* is supported | NSString * |
| allowedHeader | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard * is supported | NSArray &lt;NSString `*` > * |
| maxAgeSeconds | Sets the validity period of the result of the OPTIONS request | int |
| exposeHeader | Sets custom header information from the server that the browser can receive | NSString * |

#### Examples

```objective-c
QCloudGetBucketCORSRequest* corsReqeust = [QCloudGetBucketCORSRequest new];
corsReqeust.bucket = @"examplebucket-1250000000";

[corsReqeust setFinishBlock:^(QCloudCORSConfiguration * _Nonnull result, NSError * _Nonnull error) {
// CORS settings are encapsulated in the result
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketCORS:corsReqeust];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting Cross-origin Access Configuration

#### Method Prototype

Before performing a bucket operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudDeleteBucketCORSRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudDeleteBucketCORSRequest and enter the required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the outputObject in the finishBlock of the callback.   

#### QCloudDeleteBucketCORSRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |

#### Examples

```objective-c
QCloudDeleteBucketCORSRequest* deleteCORS = [QCloudDeleteBucketCORSRequest new];
deleteCORS.bucket = @"examplebucket-1250000000";
[deleteCORS setFinishBlock:^(id outputObject, NSError *error) {
   // Get the header information returned by the server from the outputObject
   //success if error == nil
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketCORS:deleteCORS];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Lifecycle

### Setting Lifecycle

#### Feature Description

COS allows you to manage the lifecycle of objects in buckets through lifecycle configuration that contains one or more rule sets that will be applied to a set of object rules (where each rule defines an operation for COS).
These operations include the following two types:

- Transition: This defines when an object should transition to another storage class. For example, you can choose to transition an object to the STANDARD_IA (IA for infrequent access) storage class 30 days after creation.
- Expiration: This specifies the expiration time of an object. COS automatically deletes expired objects.
  The Put Bucket Lifecycle API is used to create a new lifecycle configuration for a bucket. If the bucket has already been configured with lifecycle, using this API to create a new configuration will overwrite the existing configuration.

#### QCloudPutBucketLifecycleRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ----------------------------- | ---- |
| bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString* | Yes   |
| lifeCycle | Sets the lifecycle configuration for the bucket                               | QCloudLifecycleConfiguration* | Yes   |

QCloudLifecycleConfiguration parameter descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------ | ------------------------------- | ---- |
| rules    | Array of rule sets | NSArray<QCloudLifecycleRule*> * | Yes   |

 QCloudLifecycleRule parameter descriptions

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------ | --------------------------------------------- | ---- |
| identifier                     | Uniquely identifies a rule; up to 255 characters              | NSString*                                     | No   |
| filter                         | Describes the set of objects subject to the rule                  | QCloudLifecycleRuleFilter*                    | Yes   |
| status                         | Specifies whether a rule is enabled. Enumerated values: Enabled, Disabled            | QCloudLifecycleStatue                         | Yes   |
| abortIncompleteMultipartUpload | Sets the maximum amount of time allowed for a multipart upload to keep running                      | QCloudLifecycleAbortIncompleteMultipartUpload | No   |
| transition                     | Transition attribute of a rule, specifying when an object should transition to Standard_IA or ARCHIVE storage class   | QCloudLifecycleTransition*                    | No   |
| expiration                     | Expiration attribute of a rule                                           | QCloudLifecycleExpiration*                    | No   |
| noncurrentVersionExpiration    | Specifies when a non-current version object should expire                             | QCloudLifecycleExpiration*                    | No   |
| noncurrentVersionTransition    | Specifies when a non-current version object should transition to STANDARD_IA or ARCHIVE storage class | QCloudNoncurrentVersionExpiration*            | No  |

QCloudLifecycleTransition parameter descriptions

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | --------------------- | ---- |
| days | Specifies the number of days after the last modified date of an object that should elapse before the action corresponding to a rule is performed. If it is Transition, a valid value of this field is a non-negative integer; if it is Expiration, a valid value of this field is a positive integer. A maximum of 3,650 days is supported | int | No|
| transitionDate | Specifies when the action corresponding to a rule should be performed                                 | NSString *            | No   |
| storageClass   | Specifies the transitioned storage class of an object. Enumerated values: STANDARD_IA, ARCHIVE | QCloudCOSStorageClass | Yes   |

#### Examples

```objective-c
QCloudPutBucketLifecycleRequest* request = [QCloudPutBucketLifecycleRequest new];
request.bucket = @"examplebucket-1250000000";
__block QCloudLifecycleConfiguration* configuration = [[QCloudLifecycleConfiguration alloc] init];
QCloudLifecycleRule* rule = [[QCloudLifecycleRule alloc] init];
rule.identifier = @"identifier";
rule.status = QCloudLifecycleStatueEnabled;
QCloudLifecycleRuleFilter* filter = [[QCloudLifecycleRuleFilter alloc] init];
filter.prefix = @"0";
rule.filter = filter;

QCloudLifecycleTransition* transition = [[QCloudLifecycleTransition alloc] init];
transition.days = 100;
transition.storageClass = QCloudCOSStorageStandarIA;
rule.transition = transition;
request.lifeCycle = configuration;
request.lifeCycle.rules = @[rule];
[request setFinishBlock:^(id outputObject, NSError* error) {
   // Get the header information returned by the server from the outputObject
   // Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketLifecycle:request];

```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying Lifecycle

#### Feature Description

This API is used to get the lifecycle of the specified bucket.

#### QCloudGetBucketLifecycleRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | --------- | ---- |
| bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString* | Yes   |

#### Return Result Descriptions

Same as the return result of QCloudLifecycleConfiguration of the Put Bucket Lifecycle API.

#### Examples

```objective-c
QCloudGetBucketLifecycleRequest* request = [QCloudGetBucketLifecycleRequest new];
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(QCloudLifecycleConfiguration* result,NSError* error) {
    // Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketLifecycle:request];

```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting Lifecycle

#### Feature Description

This API is used to delete the lifecycle of the specified bucket.

#### QCloudDeleteBucketLifeCycleRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | --------- | ---- |
| bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString* | Yes   |

#### Method Prototype

The steps to delete the lifecycle configuration of a bucket in the COS SDK for iOS are as follows:

1. Instantiate QCloudDeleteBucketLifeCycleRequest and enter the required parameters.
2. Call the DeleteBucketLifeCycle method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the QCloudLifecycleConfiguration in the finishBlock of the callback.

#### Examples

```objective-c
  QCloudDeleteBucketLifeCycleRequest* request = [[QCloudDeleteBucketLifeCycleRequest alloc ] init];
  request.bucket = @"examplebucket-1250000000";
  [request setFinishBlock:^(QCloudLifecycleConfiguration* deleteResult, NSError* deleteError) {

  }];
  [[QCloudCOSXMLService defaultCOSXML] DeleteBucketLifeCycle:request];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Versioning

### Setting Versioning

#### Feature Description

This API is used to set the versioning feature of the specified bucket.

#### Method Prototype

1. Instantiate QCloudPutBucketVersioningRequest and enter the required parameters.
2. Call the PutBucketVersioning method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the outputObject in the finishBlock of the callback.

#### Sample Request

**Enable versioning**

```objective-c
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];
request.bucket =@"examplebucket-1250000000";
QCloudBucketVersioningConfiguration* configuration = [[QCloudBucketVersioningConfiguration alloc] init];
request.configuration = configuration;
configuration.status = QCloudCOSBucketVersioningStatusEnabled;
[request setFinishBlock:^(id outputObject, NSError* error) {
// Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];

```

**Suspend versioning**

```objective-c
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
QCloudBucketVersioningConfiguration* configuration = [[QCloudBucketVersioningConfiguration alloc] init];
request.configuration = configuration;
configuration.status = QCloudCOSBucketVersioningStatusSuspended;
[request setFinishBlock:^(id outputObject, NSError* error) {
// Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------- | ------------------------------------------------------------ | ------------------------------------- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | NSString *                         |
| configuration | Versioning policy                                                 | QCloudBucketVersioningConfiguration * |

QCloudBucketVersioningConfigurationcan parameter descriptions

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------------------------------- |
| status | Indicates whether versioning is enabled. Enumerated values: QCloudCOSBucketVersioningStatusSuspended, QCloudCOSBucketVersioningStatusEnabled | QCloudCOSBucketVersioningStatus |

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying Versioning

#### Feature Description

This API is used to query the versioning information of the specified bucket.

#### Method Prototype

1. Instantiate QCloudGetBucketVersioningRequest and enter the required parameters.
2. Call the GetBucketVersioning method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the QCloudBucketVersioningConfiguration in the finishBlock of the callback.

#### Sample Request

```objective-c
CloudGetBucketVersioningRequest* request = [[QCloudGetBucketVersioningRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result, NSError* error) {
// Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ---------- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | NSString *                         |

#### Return Result Descriptions

The return result is stored in the instance of QCloudBucketVersioningConfiguration with the same parameter descriptions as those of QCloudPutBucketVersioningRequest.

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Cross-region Replication

### Setting Cross-region Replication

#### Feature Description

This API is used to set the cross-region replication rule of the specified bucket.

#### Method Prototype

1. Instantiate QCloudPutBucketReplicationRequest and enter the required parameters.
2. Call the PutBucketRelication method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the outputObject in the finishBlock of the callback.

#### Sample Request

```objective-c
QCloudPutBucketReplicationRequest* request = [[QCloudPutBucketReplicationRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
QCloudBucketReplicationConfiguation* configuration = [[QCloudBucketReplicationConfiguation alloc] init];
configuration.role = [NSString identifierStringWithID:@"uin" :@"uin"];
QCloudBucketReplicationRule* rule = [[QCloudBucketReplicationRule alloc] init];

rule.identifier = @"identifier";
rule.status = QCloudQCloudCOSXMLStatusEnabled;

QCloudBucketReplicationDestination* destination = [[QCloudBucketReplicationDestination alloc] init];
NSString* destinationBucket = @"destinationBucket";
NSString* region = @"destinationRegion"
destination.bucket = [NSString stringWithFormat:@"qcs:id/0:cos:%@:appid/%@:%@",@"region",@"appid",@"destinationBucket"];
rule.destination = destination;
configuration.rule = @[rule];
request.configuation = configuration;
[request setFinishBlock:^(id outputObject, NSError* error) {
// Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketRelication:request];
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------------------------------------- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | NSString *                         |
| configuration | Cross-region replication rule                                               | QCloudBucketReplicationConfiguation * |

QCloudBucketReplicationConfiguation parameter descriptions

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | --------------------------------------------- |
| role     | Initiator ID in the format of id="OwnerUin"                        | NSString *                                    |
| rule     | Specific configuration information of up to 1,000 rules. All rules must point to the same destination bucket | NSArray&lt;QCloudBucketReplicationRule`*` > * |

QCloudBucketReplicationRule parameter descriptions

| Parameter Name | Description | Type |
| ----------- | ------------------------------------------------------------ | ------------------------------------ |
| status | Specifies whether a rule is enabled. Value range: QCloudCOSXMLStatusEnabled, QCloudCOSXMLStatusDisabled | QCloudCOSXMLStatus |
| identifier  | Identifies the name of a specific rule                                     | NSString *                           |
| prefix | Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. The prefix matching root directory is empty | NSString * |
| destination | Destination bucket information                                               | QCloudBucketReplicationDestination * |

QCloudBucketReplicationDestination parameter descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| bucket       | Resource ID. Note that this is different from the bucket ID <br>Format: `qcs:id/0:cos:[region]:appid/[AppId]:[bucketname]` | NSString *                                                   |
| storageClass | Storage class of an object. Enumerated values: STANDARD (QCloudCOSStorageStandard), STANDARD_IA (QCloudCOSStorageStandardIA). Default value: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageStandard<br>QCloudCOSStorageStandardIA<br>QCloudCOSStorageARCHIVE |

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying Cross-region Replication

#### Feature Description

This API is used to query the cross-region replication rule of the specified bucket.

#### Method Prototype

1. Instantiate QCloudGetBucketReplicationRequest and enter the required parameters.
2. Call the GetBucketReplication method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the QCloudBucketReplicationConfiguation in the finishBlock of the callback.

#### Sample Request

```objective-c
QCloudGetBucketReplicationRequest* request = [[QCloudGetBucketReplicationRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(QCloudBucketReplicationConfiguation* result, NSError* error) {
// Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketReplication:request];
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ---------- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | NSString *                         |

#### Return Result Descriptions

The return result is stored in the instance of QCloudBucketReplicationConfiguation with the same parameter descriptions as those of QCloudPutBucketReplicationRequest.

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting Cross-region Replication

#### Feature Description

This API is used to delete the cross-region replication rule of the specified bucket.

#### Method Prototype

1. Instantiate QCloudDeleteBucketReplicationRequest and enter the required parameters.
2. Call the DeleteBucketReplication method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the outputObject in the finishBlock of the callback.

#### Sample Request

```objective-c
QCloudDeleteBucketReplicationRequest* request = [[QCloudDeleteBucketReplicationRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(id outputObject, NSError* error) {

}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketReplication:request];
```

#### Parameter Descriptions

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ---------- |
| bucket  | Bucket name in the format of BucketName-APPID. For more information, see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | NSString *                         |

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).
