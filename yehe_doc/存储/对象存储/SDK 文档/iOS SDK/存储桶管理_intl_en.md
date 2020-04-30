## Introduction

This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycle, version control, and cross-region replication.

- We assume you have completed SDK download, installation, and initialization as described in [Getting Started](https://intl.cloud.tencent.com/document/product/436/8629).
We recommend you use Control+F to find the desired API, view our API description, copy the examples and run them in your project.

>If you need more features, or do not understand what the returned parameters mean, we recommend you view the comments in the code using three finger drag, Force-touch, or hovering over the variable and pressing Control+Command+D.   

**Cross-origin Access**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets cross-origin access permissions for a bucket |
| [GET Bucket cors](https://cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management for a bucket |
| [GET Bucket lifecycle](https://cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management  configuration of a bucket |
| [DELETE Bucket lifecycle](https://cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning configuration for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region Replication**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets cross-region replication rules for a bucket |
| [GET Bucket replication](https://cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |

## Cross-Origin Access

### Setting cross-origin configuration

#### Method Prototype

Before performing the CORS operation of configuring the bucket, you need to import the header file QCloudCOSXML/QCloudCOSXML.h. Before import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/8629#step1). First generate a QCloudPutBucketCORSRequest instance, enter additional restrictions as required, and then get the approved content. Detailed steps are as follows:    

1. Instantiate QCloudPutBucketCORSRequest, configure the bucket, and put the required CORS into QCloudCORSRule. If there are multiple CORS configurations, you can place multiple QCloudCORSRule in an NSArray, put the array into QCloudCORSConfiguration's rules attribute, and then into the request.    
2. Call the PutBucketCORS method in the QCloudCOSXMLService object to initiate the request.    
3. Obtain the setting result (error is empty or not) from finishBlock of callback, and perform additional operations if the setting is successful.   

#### QCloudPutBucketCORSRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------------------------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString* | Yes |
| corsConfiguration | Specific parameter that encapsulates CORS | QCloudCORSConfiguration * | Yes |

#### QCloudCORSConfiguration parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------ | -------------------------------- | ---- |
| rules | The array containing CORS. It is a QCloudCORSRule instance. | NSArray&lt;QCloudCORSRule`*` > * |

#### QCloudCORSRule parameters

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ---------------------------- | ---- |
| identifier | ID of the configuration rule | NSString* |
| allowedMethod | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | NSArray &lt;NSString`*`>* |
| AllowedOrigins | String | | Allowed source origins. Wildcard `*` is supported. Format: `Protocol://domain name[:port]`, Example: `http://www.qq.com` | Yes |
| allowedHeader | It is used to notify the server about which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent. The wildcard "*" is supported. | NSArray&lt;NSString `*`>* | No |
| maxAgeSeconds | Configures the valid period of the results obtained by OPTIONS request | int |
| exposeHeader | Configures the custom header information that can be received by the browser from the server | NSString* |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-put-bucket-cors)
```objective-c
QCloudPutBucketCORSRequest* putCORS = [QCloudPutBucketCORSRequest new];
QCloudCORSConfiguration* cors = [QCloudCORSConfiguration new];

QCloudCORSRule* rule = [QCloudCORSRule new];
rule.identifier = @"sdk";
rule.allowedHeader = @[@"origin",@"host",@"accept",@"content-type",@"authorization"];
rule.exposeHeader = @"ETag";
"AllowedMethod": ["GET", "POST", "PUT", "DELETE", "HEAD"],
rule.maxAgeSeconds = 3600;
rule.allowedOrigin = @"http://cloud.tencent.com";
cors.rules = @[rule];
putCORS.corsConfiguration = cors;
putCORS.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] PutBucketCORS:putCORS];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-put-bucket-cors)
```swift
let putBucketCorsReq = QCloudPutBucketCORSRequest.init();

let corsConfig = QCloudCORSConfiguration.init();

let rule = QCloudCORSRule.init();
rule.identifier = "swift-sdk";
rule.allowedHeader = ["origin","host","accept","content-type","authorization"];
rule.exposeHeader = "Etag";
"AllowedMethod": ["GET", "POST", "PUT", "DELETE", "HEAD"],
rule.maxAgeSeconds = 3600;
rule.allowedOrigin = "*";

corsConfig.rules = [rule];

putBucketCorsReq.corsConfiguration = corsConfig;
putBucketCorsReq.bucket = "examplebucket-1250000000";
putBucketCorsReq.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}

QCloudCOSXMLService.defaultCOSXML().putBucketCORS(putBucketCorsReq);
```

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, please refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

### Query cross-origin configuration

#### Method Prototype

Before performing the operation of querying cross-domain configuration, you need to import the header file QCloudCOSXML/QCloudCOSXML.h. Before import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/8629#step1). First generate a QCloudPutBucketCORSRequest, enter the instance request and additional restrictions as required, and then get the approved content. Detailed steps are as follows:

1. Instantiate QCloudGetBucketCORSRequest and enter the bucket whose CORS is to be obtained.
2. Call the GetBucketCORS method in the QCloudCOSXMLService object to initiate a request.
3. Obtain the result from finishBlock of callback. The result is encapsulated in the QCloudCORSConfiguration object whose "rules" attribute is an array containing a set of QCloudCORSRule. The specific CORS configurations are encapsulated in the QCloudCORSRule object.

#### QCloudGetBucketACLRequest parameters

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ---------- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString* | Yes |

#### Returned Result

 #### QCloudCORSConfiguration parameters

| Parameter Name | Description | Type |
| -------- | -------- | -------------------------------- |
| rules | Rule Set | NSArray&lt;QCloudCORSRule`*`>* |

#### QCloudCORSRule parameters

| Parameter Name | Description | Type |
| ------------- | ------------------------------------------------------------ | ---------------------------- |
| identifier | ID of the configuration rule | NSString* |
| allowedMethod | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | NSArray &lt;NSString`*`>* |
| allowedOrigin | Allowed access source. The wildcard "*" is supported. Format: protocol://domain name[:port], for example, `http://www.qq.com` | NSString* |
| allowedHeader | It is used to notify the server about which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent. The wildcard "*" is supported. | NSArray &lt;NSString `*`>* |
| maxAgeSeconds | Configures the valid period of the results obtained by OPTIONS request | int |
| exposeHeader | Configures the custom header information that can be received by the browser from the server | NSString* |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-get-bucket-cors)
```objective-c
QCloudGetBucketCORSRequest* corsReqeust = [QCloudGetBucketCORSRequest new];
corsReqeust.bucket = @"examplebucket-1250000000";

[corsReqeust setFinishBlock:^(QCloudCORSConfiguration * _Nonnull result, NSError * _Nonnull error) {
    // CORS is encapsulated in result
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-get-bucket-cors)
```swift
let  getBucketCorsRes = QCloudGetBucketCORSRequest.init();
getBucketCorsRes.bucket = "examplebucket-1250000000";
getBucketCorsRes.setFinish { (corsConfig, error) in
    if error != nil{
        print(error!);
    else
        print(corsConfig!);
    }}
QCloudCOSXMLService.defaultCOSXML().getBucketCORS(getBucketCorsRes);
```

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, please refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

### Delete cross-origin configuration

#### Method Prototype

Before performing the bucket operation, you need to import the header file QCloudCOSXML/QCloudCOSXML.h. Before import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/8629#step1). First generate a QCloudPutBucketCORSRequest instance, enter additional restrictions as required, and then get the approved content. Detailed steps are as follows:    

1. Instantiate QCloudDeleteBucketCORSRequest and enter the required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content in finishBlock callback.   

#### QCloudDeleteBucketCORSRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString* | Yes |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-delete-bucket-cors)
```objective-c
QCloudDeleteBucketCORSRequest* deleteCORS = [QCloudDeleteBucketCORSRequest new];
deleteCORS.bucket = @"examplebucket-1250000000";
[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    // You can get the header information returned by the server from outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-delete-bucket-cors)
```swift
let deleteBucketCorsRequest = QCloudDeleteBucketCORSRequest.init();
deleteBucketCorsRequest.bucket = "examplebucket-1250000000";
deleteBucketCorsRequest.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().deleteBucketCORS(deleteBucketCorsRequest);
```

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, please refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

## Lifecycle

### Setting the lifecycle

#### Feature

COS allows you to manage the lifecycle of objects in buckets through lifecycle configuration that contains one or more rule sets that will be applied to a set of objects. Each rule defines an operation for COS.
There are two types of operations:

- Transition: Specify the time when an object is transitioned into another storage class. For example, you can choose to transition an object into STANDARD_IA (applicable to infrequent access) storage class 30 days after its creation.
- Expiration: Specify the expiration time of an Object. COS will automatically delete objects that have expired.
  Put Bucket Lifecycle is used to create a new lifecycle configuration for a Bucket. If the Bucket has been configured with a lifecycle, you can use this API to create a new configuration which will overwrite the existing one.

#### QCloudPutBucketLifecycleRequest parameters

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ----------------------------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString* | Yes |
| lifeCycle | Lifecycle configuration | QCloudLifecycleConfiguration* | Yes |

#### QCloudLifecycleConfiguration parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------ | ------------------------------- | ---- |
| rules | An array of rule description sets | NSArray<QCloudLifecycleRule*>* | Yes |

 #### QCloudLifecycleRule parameters

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------ | --------------------------------------------- | ---- |
| identifier | Uniquely identifies a rule. Its length cannot exceed 255 characters. | NSString* | Yes |
| filter | Describes the collection of Objects affected by rules | QCloudLifecycleRuleFilter* |
| status | Indicates whether the rule is enabled. Enumerated values: Enabled, Disabled. | QCloudLifecycleStatue | Yes |
| abortIncompleteMultipartUpload | Sets the maximum length of time allowed for a continuous multipart upload | QCloudLifecycleAbortIncompleteMultipartUpload | No |
| transition | Rule transition attribute, which indicates when an object is transited to Standard_IA etc. | QCloudLifecycleTransition* | No |
| expiration | Rule expiration attribute | QCloudLifecycleExpiration* | No |
| noncurrentVersionExpiration | Indicates when objects of non-current version expire | QCloudLifecycleExpiration* | No |
| noncurrentVersionTransition | Indicates when objects of non-current version are transited to STANDARD_IA etc. | QCloudNoncurrentVersionExpiration* | No |

QCloudLifecycleTransition parameter description

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | --------------------- | ---- |
|Days | LifecycleConfiguration.Rule.Transition <br>or Expiration | Specifies the number of days between the last modified date of an object and the date when the operation corresponding to a rule is performed. If the operation is `Transition`, a valid value of this field should be a non-negative integer; if it is `Expiration`, a valid value of this field should be a positive integer. Maximum: 3,650 days | Integer | No |
| transitionDate | Specifies when to execute on the action corresponding to the rule | NSString* | No |
| storageClass | Specifies the storage type to which the Object is transitioned into. Enumerated values: STANDARD_IA, ARCHIVE | QCloudCOSStorageClass | Yes |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-put-bucket-lifecycle)
```objective-c
QCloudPutBucketLifecycleRequest* request = [QCloudPutBucketLifecycleRequest new];
request.bucket = @"examplebucket-1250000000";
__block QCloudLifecycleConfiguration* lifecycleConfiguration = [[QCloudLifecycleConfiguration
    alloc] init];
QCloudLifecycleRule* rule = [[QCloudLifecycleRule alloc] init];
rule.identifier = @"identifier";
rule.status = QCloudLifecycleStatueEnabled;
QCloudLifecycleRuleFilter* filter = [[QCloudLifecycleRuleFilter alloc] init];
filter.prefix = @"0";
rule.filter = filter;

QCloudLifecycleTransition* transition = [[QCloudLifecycleTransition alloc] init];
transition.days = 100;
transition.storageClass = QCloudCOSStorageStandardIA;
rule.transition = transition;
request.lifeCycle = lifecycleConfiguration;
request.lifeCycle.rules = @[rule];
[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-put-bucket-lifecycle)
```swift
let putBucketLifecycleReq = QCloudPutBucketLifecycleRequest.init();
putBucketLifecycleReq.bucket = "examplebucket-1250000000";

let config = QCloudLifecycleConfiguration.init();

let rule = QCloudLifecycleRule.init();
rule.identifier = "swift";
rule.status = .enabled;

let fileter = QCloudLifecycleRuleFilter.init();
fileter.prefix = "0";

rule.filter = fileter;

let transition = QCloudLifecycleTransition.init();
transition.days = 100;
transition.storageClass = .standardIA;

rule.transition = transition;

putBucketLifecycleReq.lifeCycle = config;
putBucketLifecycleReq.lifeCycle.rules = [rule];

putBucketLifecycleReq.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().putBucketLifecycle(putBucketLifecycleReq);
```

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, please refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying the lifecycle

#### Feature

This API is used to get the lifecycle of the specified bucket.

#### QCloudGetBucketLifecycleRequest request parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | --------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString* | Yes |

#### Returned Result

Same with QCloudLifecycleConfiguration in the API Put Bucket Lifecycle.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-get-bucket-lifecycle)
```objective-c
* Operations on bucket lifecycle, such as PQCloudutBucketLifecycleRequest, and QCloudGetBucketLifecycleRequest.
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result, NSError* error) {
    // You can get the returned information from result
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-get-bucket-lifecycle)
```swift
let getBucketLifeCycle = QCloudGetBucketLifecycleRequest.init();
getBucketLifeCycle.bucket = "examplebucket-1250000000";
getBucketLifeCycle.setFinish { (config, error) in
    if error != nil{
        print(error!);
    }else{
        print(config!);
    }};
QCloudCOSXMLService.defaultCOSXML().getBucketLifecycle(getBucketLifeCycle);
```

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, please refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting the lifecycle

#### Feature

This API is used to delete the lifecycle of the specified bucket.

#### QCloudDeleteBucketLifeCycleRequest request parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | --------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString* | Yes |

#### Method Prototype

The detailed steps to delete the lifecycle configuration of a bucket in COS iOS SDK are as follows:

1. Instantiate QCloudDeleteBucketCORSRequest and enter the required parameters.
2. Call the PutBucketACL method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the QCloudLifecycleConfiguration in finishBlock callback.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-delete-bucket-lifecycle)
```objective-c
QCloudDeleteBucketLifeCycleRequest* request = [[QCloudDeleteBucketLifeCycleRequest alloc ] init];
String bucket = "examplebucket-1250000000";
[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result, NSError* error) {
    // error returns the delete result
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-delete-bucket-lifecycle)
```swift
let deleteBucketLifeCycle = QCloudDeleteBucketLifeCycleRequest.init();
deleteBucketLifeCycle.bucket = "examplebucket-1250000000";
deleteBucketLifeCycle.finishBlock = { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }};
QCloudCOSXMLService.defaultCOSXML().deleteBucketLifeCycle(deleteBucketLifeCycle);
```

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, please refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

## Versioning

### Setting Versioning

#### Feature

This API (PUT Bucket versioning) is used to set versioning for a bucket.

#### Method Prototype

1. Instantiate QCloudPutBucketRequest and enter the required parameters.
2. Call the `PutBucketVersioning` method of `QCloudCOSXMLService` to initiate a request.
3. Obtain specific content from outputObject in finishBlock of callback.

#### Request Example

**Enable Versioning**

Objective-C code sample:

[//]: # (.cssg-snippet-objc-put-bucket-versioning)
```objective-c
// Enabling Versioning
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];
String bucket = "examplebucket-1250000000";
| configuration | Version control details | QCloudBucketVersioningConfiguration* | Yes |
    #### QCloudBucketVersioningConfiguration parameters
request.configuration = configuration;
configuration.status = QCloudCOSBucketVersioningStatusEnabled;

[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-put-bucket-versioning)
```swift
let putBucketVersioning = QCloudPutBucketVersioningRequest.init();
putBucketVersioning.bucket = "examplebucket-1250000000";

let config = QCloudBucketVersioningConfiguration.init();
config.status = .enabled;

putBucketVersioning.configuration = config;

putBucketVersioning.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().putBucketVersioning(putBucketVersioning);
```

#### Parameter Description

| Parameter Name | Description | Type |
| ------------- | ------------------------------------------------------------ | ------------------------------------- |
| bucket | Bucket naming format is BucketName-APPID. For details, please refer to [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | NSString* |
| configuration | Version control details | QCloudBucketVersioningConfiguration* | Yes |

#### QCloudBucketVersioningConfiguration parameters

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------------------------------- |
| status | Indicates whether the version is enabled. Enumerated value is QCloudCOSBucketVersioningStatusSuspended\QCloudCOSBucketVersioningStatusEnabled | QCloudCOSBucketVersioningStatus |

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, please refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying Versioning

#### Feature

This API (GET Bucket versioning) is used to query the versioning configuration of a bucket.

#### Method Prototype

1. Instantiate QCloudGetBucketRequest and enter the required parameters.
2. Call the `GetBucketVersioning` method of `QCloudCOSXMLService` to initiate a request.
3. Get the specific content from the QCloudBucketVersioningConfiguration in finishBlock callback.

#### Request Example

Objective-C code sample:

[//]: # (.cssg-snippet-objc-get-bucket-versioning)
```objective-c
QCloudGetBucketVersioningRequest* request = [[QCloudGetBucketVersioningRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result, NSError* error) {
    // You can get the returned information from result
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-get-bucket-versioning)
```swift
let getBucketVersioning = QCloudGetBucketVersioningRequest.init();
getBucketVersioning.bucket = "examplebucket-1250000000";
getBucketVersioning.setFinish { (config, error) in
    if error != nil{
        print(error!);
    }else{
        print(config!);
    }}
QCloudCOSXMLService.defaultCOSXML().getBucketVersioning(getBucketVersioning);
```

#### Parameter Description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ---------- |
| bucket | Bucket naming format is BucketName-APPID. For details, please refer to [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | NSString* |

#### Returned Result

The returned result is stored in the QCloudBucketVersioningConfiguration instance, and the parameter description is the same as that for QCloudPutBucketVersioningRequest.

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, please refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

## Cross-region Replication

### Setting cross-region replication

#### Feature

This API (PUT Bucket replication) is used to set cross-region replication rules for a bucket.

#### Method Prototype

1. Instantiate QCloudPutBucketRequest and enter the required parameters.
2. Call the GetBucketLocation method in the QCloudCOSXMLService object to initiate a request.
3. Obtain specific content from outputObject in finishBlock of callback.

#### Request Example


Objective-C code sample:

[//]: # (.cssg-snippet-objc-put-bucket-replication)
```objective-c
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];
String bucket = "examplebucket-1250000000";
QCloudBucketReplicationConfiguation* replConfiguration = [[QCloudBucketReplicationConfiguation
    alloc] init];
replConfiguration.role = @"qcs::cam::uin/100000000001:uin/100000000001";
QCloudBucketReplicationRule* rule = [[QCloudBucketReplicationRule alloc] init];

rule.identifier = @"identifier";
rule.status = QCloudCOSXMLStatusEnabled;

QCloudBucketReplicationDestination* destination = [[QCloudBucketReplicationDestination alloc] init];
NSString* destinationBucket = @"destinationbucket-1250000000";
NSString* region = @"ap-beijing";
destination.bucket = [NSString stringWithFormat:@"qcs::cos:%@::%@",region,destinationBucket];
rule.destination = destination;
rule.prefix = @"a";
replConfiguration.rule = @[rule];
request.configuation = replConfiguration;

[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-put-bucket-replication)
```swift
let putBucketReplication = QCloudPutBucketReplicationRequest.init();
putBucketReplication.bucket = "examplebucket-1250000000";

let config = QCloudBucketReplicationConfiguation.init();
Role: "qcs::cam::uin/100000000001:uin/100000000001",

let rule = QCloudBucketReplicationRule.init();
rule.identifier = "swift";
rule.status = .enabled;

| destination | Destination bucket information | QCloudBucketReplicationDestination* |
let destinationBucket = "destinationbucket-1250000000";
region = ap-beijing
destination.bucket = "qcs::cos:\(region)::\(destinationBucket)";
rule.destination = destination;
rule.prefix = "a";

config.rule = [rule];

putBucketReplication.configuation = config;

putBucketReplication.finishBlock = {(result,error) in
        if error != nil{
            print(error!);
        }else{
            print(result!);
        }}
QCloudCOSXMLService.defaultCOSXML().putBucketRelication(putBucketReplication);
```

#### Parameter Description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------------------------------------- |
| bucket | Bucket naming format is BucketName-APPID. For details, please refer to [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | NSString* |
| configuration | Describes all the cross-origin configuration | QCloudBucketReplicationConfiguration* | Yes |

#### Parameters of returned result QCloudBucketReplicationConfiguration

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | --------------------------------------------- |
| role | Initiator ID, format is: header information of id = "OwnerUin" | NSString* |
| rule | Specific configuration information, up to 1000 is supported, all policies can only point to one destination bucket | NSArray&lt;QCloudBucketReplicationRule`*`>* |

#### QCloudBucketReplicationRule parameters

| Parameter Name | Description | Type |
| ----------- | ------------------------------------------------------------ | ------------------------------------ |
| status | Indicates whether the rule takes effect, possible values (QCloudCOSXMLStatusEnabled、QCloudCOSXMLStatusDisabled) | QCloudCOSXMLStatus |
| identifier |  Indicates the name of a specific Rule | NSString* |
| prefix | Prefix match policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned. | NSString* |
| destination | Destination bucket information | QCloudBucketReplicationDestination* |

QCloudBucketReplicationDestination parameter description

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| bucket | Resource identifier. Note it is different from the bucket<br>format is:`qcs::cos:[region]:appid/[AppId]:[bucketname]` | NSString* |
| storageClass | Used to label the specific Rule name | QCloudCOSStorageStandard<br>QCloudCOSStorageStandardIA<br>QCloudCOSStorageARCHIVE |

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, please refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying cross-region replication

#### Feature

This API (GET Bucket replication) is used to query the cross-region replication rules of a specified bucket.

#### Method Prototype

1. Instantiate QCloudGetBucketRequest and enter the required parameters.
2. Call the GetBucketLocation method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the QCloudBucketReplicationConfiguation in finishBlock callback.

#### Request Example


Objective-C code sample:

[//]: # (.cssg-snippet-objc-get-bucket-replication)
```objective-c
QCloudGetBucketVersioningRequest* request = [[QCloudGetBucketVersioningRequest alloc] init];
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result, NSError* error) {
    // You can get the returned information from result
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-get-bucket-replication)
```swift
let getBucketReplication = QCloudGetBucketReplicationRequest.init();
getBucketReplication.bucket = "examplebucket-1250000000";
getBucketReplication.setFinish { (config, error) in
    if error != nil{
        print(error!);
    }else{
        print(config!);
    }}
QCloudCOSXMLService.defaultCOSXML().getBucketReplication(getBucketReplication);
```
#### Parameter Description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ---------- |
| bucket | Bucket naming format is BucketName-APPID. For details, please refer to [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | NSString* |

#### Returned Result

The returned result is stored in the QCloudBucketReplicationConfiguation instance. The parameter details are the same as that for QCloudPutBucketReplicationRequest.

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, please refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

## Deleting cross-region replication

#### Feature

This API (DELETE Bucket replication) is used to delete the cross-region replication rules of a bucket.

#### Method Prototype

1. Instantiate QCloudDeleteBucketCORSRequest and enter the required parameters.
2. Call the GetBucketLocation method in the QCloudCOSXMLService object to initiate a request.
3. Obtain specific content from outputObject in finishBlock of callback.

#### Request Example


Objective-C code sample:

[//]: # (.cssg-snippet-objc-delete-bucket-replication)
```objective-c
QCloudDeleteBucketReplicationRequest* request = [[QCloudDeleteBucketReplicationRequest alloc] init];
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-delete-bucket-replication)
```swift
let deleteBucketReplication = QCloudDeleteBucketReplicationRequest.init();
deleteBucketReplication.bucket = "examplebucket-1250000000";
deleteBucketReplication.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().deleteBucketReplication(deleteBucketReplication);
```

#### Parameter Description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ---------- |
| bucket | Bucket naming format is BucketName-APPID. For details, please refer to [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | NSString* |

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, please refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).
