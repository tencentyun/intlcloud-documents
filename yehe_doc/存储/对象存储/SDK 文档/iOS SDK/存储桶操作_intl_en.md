## Introduction

This document provides an overview of APIs and SDK code samples related to basic operations on buckets and bucket access control list (ACL).

- We assume you have completed SDK download, installation, and initialization as described in [Getting Started](https://intl.cloud.tencent.com/document/product/436/8629).
We recommend you use Control+F to find the desired API, view our API description, copy the examples and run them in your project.

>If you need more features, or do not understand what the returned parameters mean, we recommend you view the comments in the code using three finger drag, Force-touch, or hovering over the variable and pressing Control+Command+D.   

**Basic Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a bucket |

## Basic Operations

### Querying the bucket list

#### Feature

This API is used to query the list of all buckets under the specified account.

#### Returned Result

#### Parameters of returned result QCloudListAllMyBucketsResult

| Parameter Name | Description | Type |
| -------- | ------------------ | ------------------------------ |
| owner | Bucket owner information | QCloudOwner * |
| buckets | All bucket information | NSArray&lt;QCloudBucket`*`>* |

QCloudOwner parameter description

| Parameter Name | Description | Type |
| ----------- | ------------------ | ---------- |
| - - - DisplayName | Part owner name | String |
| ID | ID of the bucket owner | string |

QCloudBucket parameter description

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ---------- |
| Name | Bucket name | string |
| x-cos-bucket-region | Bucket region such as `ap-beijing`, `ap-hongkong`, and `eu-frankfurt`. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | Enum |
| CreationDate | Time when the bucket was created, in ISO8601 format, such as 2016-11-09T08:46:32.000Z | string |

#### Request Example

Objective-C code sample:

[//]: # (.cssg-snippet-objc-get-service)
```objective-c
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result, NSError* error) {
    // Get the returned information from result
}];
[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-get-service)
```swift
let getServiceReq = QCloudGetServiceRequest.init();
getServiceReq.setFinish{(result,error) in
    if result == nil {
        print(error!);
    } else {
        // Get the returned information from result
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().getService(getServiceReq);
```

### Creating a bucket

#### Feature

This API (PUT Bucket) is used to create a bucket under a specified account.

#### Method Prototype

Before using COS, you need to create a bucket under the specific account for use and management of objects, and define the region of the bucket. The creator of the bucket is the owner of the bucket by default. The bucket access permission is Private Read/Write by default if not otherwise specified upon creation. Specific steps are as follows:    

1. Instantiate QCloudPutBucketRequest and enter the required parameters.
2. Call the PutBucket method in the QCloudCOSXMLService object to initiate a request.
3. Obtain specific content from outputObject in finishBlock of callback.

#### Parameter Description

#### QCloudPutBucketRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Name of the bucket to be created. For naming rules, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | NSString* | Yes |
| accessControlList | Defines the ACL attribute of a bucket. Valid values: private, public-read-write, public-read; Default: private | NSString * | No |
| GrantRead | Grants the grantee Read access in the format of `id="[OwnerUin]"` | String | No |
| GrantWrite | Grants the grantee Write access in the format of `id="[OwnerUin]"` | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |

#### Request Example


Objective-C code sample:

[//]: # (.cssg-snippet-objc-put-bucket)
```objective-c
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];
request.bucket = @"examplebucket-1250000000"; //additional actions after finishing
[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-put-bucket)
```swift
let putBucketReq = QCloudPutBucketRequest.init();
putBucketReq.bucket = "examplebucket-1250000000";
putBucketReq.finishBlock = {(result,error) in
    if error != nil {
        print(error!);
    } else {
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().putBucket(putBucketReq);
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.
Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

### Retrieving information on a bucket and its permission

#### Feature

This API is used to verify whether a bucket exists and whether you have the permission to access it. The permission requirements for HEAD Bucket are the same as those for GET Bucket. 200 is returned if the bucket exists; 403 is returned if you do not have access to the bucket; 404 is returned if the bucket does not exist.   

#### QCloudHeadBucketRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-head-bucket)
```objective-c
QCloudHeadBucketRequest* request = [QCloudHeadBucketRequest new];
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-head-bucket)
```swift
let headBucketReq = QCloudHeadBucketRequest.init();
headBucketReq.bucket = "examplebucket-1250000000";
headBucketReq.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print( result!);
    }}
QCloudCOSXMLService.defaultCOSXML().headBucket(headBucketReq);
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting a bucket

#### Feature

This API is used to delete the empty bucket under the specified account.

#### Method Prototype

The steps to delete a bucket in COS iOS SDK are as follows:

1. Instantiate QCloudDeleteBucketCORSRequest and enter the required parameters.
2. Call the GetBucket method in the QCloudCOSXMLService object to initiate a request.
3. Obtain specific content from outputObject in finishBlock of callback.

#### Parameter Description

#### QCloudDeleteBucketCORSRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Name of the bucket to be deleted, can be viewed in [COS Console](https://console.cloud.tencent.com/cos5/bucket), naming format is BucketName-APPID<br>such as examplebucket-1250000000. Note: bucket is required to be empty before deletion | NSString* | Yes |

#### Request Example


Objective-C code sample:

[//]: # (.cssg-snippet-objc-delete-bucket)
```objective-c
QCloudDeleteBucketRequest* request = [[QCloudDeleteBucketRequest alloc ] init];
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-delete-bucket)
```swift
let deleteBucketReq = QCloudDeleteBucketRequest.init();
deleteBucketReq.bucket = "examplebucket-1250000000";
deleteBucketReq.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().deleteBucket(deleteBucketReq);
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

## ACL

### Setting bucket ACL

#### Feature

This API (PUT Bucket acl) is used to set the access control list (ACL) for a specified bucket.

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before bucket operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudPutBucketACLRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudPutBucketACLRequest, enter the bucket to be set, and then enter corresponding parameters according to the permission type of the bucket.    
2. Call the PutBucketACL method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the setting result (successful or failed) from finishBlock of callback, and perform some additional operations if the setting is successful.   

#### QCloudPutBucketACLRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| accessControlList | Defines the ACL attribute of a bucket. Valid values: private, public-read-write, public-read; Default: private | NSString * | No |
| GrantRead | Grants the grantee Read access in the format of `id="[OwnerUin]"` | String | No |
| GrantWrite | Grants the grantee Write access in the format of `id="[OwnerUin]"` | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-put-bucket-acl)
```objective-c
QCloudPutBucketACLRequest* putACL = [QCloudPutBucketACLRequest new];
NSString* appID = @"1131975903";// Grant a new account ID
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@", appID,
    ### APPID
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];
putACL.grantFullControl = grantString;
String bucket = "examplebucket-1250000000";
[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] PutBucketACL:putACL];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-put-bucket-acl)
```swift
let putBucketACLReq = QCloudPutBucketACLRequest.init();
putBucketACLReq.bucket = "examplebucket-1250000000";
let appTD = "1131975903";// Grant a new account ID
let ownerIdentifier = "qcs::cam::uin/\(appTD):uin/\(appTD)";
let grantString = "id=\"\(ownerIdentifier)\"";
putBucketACLReq.grantWrite = grantString;
putBucketACLReq.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().putBucketACL(putBucketACLReq);
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying bucket ACL

#### Feature

This API (GET Bucket acl) is used to query the access control list (ACL) of a bucket.

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before bucket operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudGetBucketACLRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudGetBucketACLRequest and enter the bucket whose ACL is to be obtained.    
2. Call the GetBucketACL method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content from QCloudACLPolicy in finishBlock of callback.    

#### QCloudGetBucketACLRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |

#### Returned Result

#### Parameters of returned result QCloudACLPolicy

| Parameter Name | Description | Type |
| ----------- | ------------------------------------------------------------ | ---------- |
| displayName | Bucket owner information | NSString * |
| - - ID | Bucket owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String | No |

QCloudACLOwner parameters

| Parameter Name | Description | Type |
| ----------------- | -------------------- | ------------------------- |
| owner | Bucket owner information | QCloudACLOwner * |
| accessControlList | Information of the authorized user and permissions | QCloudAccessControlList * |

QCloudAccessControlList parameters

| Parameter Name | Description | Type |
| --------- | ---------------------- | -------------------------------- |
| ACLGrants | An array to store information about grantees | NSArray&lt;QCloudACLGrant`*`>* |

#### Samples

Objective-C code sample:

[//]: # (.cssg-snippet-objc-get-bucket-acl)
```objective-c
QCloudGetBucketACLRequest* getBucketACl = [QCloudGetBucketACLRequest new];
getBucketACl.bucket = @"examplebucket-1250000000";
[getBucketACl setFinishBlock:^(QCloudACLPolicy * _Nonnull result, NSError * _Nonnull error) {
    QCloudACLPolicy contains Bucket ACL information.
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketACL:getBucketACl];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-get-bucket-acl)
```swift
let getBucketACLReq = QCloudGetBucketACLRequest.init();
getBucketACLReq.bucket = "examplebucket-1250000000";
getBucketACLReq.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().getBucketACL(getBucketACLReq)
```
#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
- For SDK-defined custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For solutions regarding these error codes, refer to [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610).
