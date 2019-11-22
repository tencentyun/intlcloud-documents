## Overview

This document provides an overview of APIs related to basic bucket operations and access control list (ACL) and corresponding SDK sample code.

- It is assumed that you have downloaded, installed, and initialized the SDK as instructed in [Getting Started](https://intl.cloud.tencent.com/document/product/436/11280).
- You are recommended to use Command+F to search for the API you want to query, check the provided descriptions of the API, and then copy the sample code to your project for execution.

> If you want to learn more about the function of the API or the meanings of its parameters, you are recommended to directly view the comments in the code. In Xcode, you can use three-finger tap or Force Touch or hover over a variable and press Control+Command+D to see its interpretation.   

**Basic operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Getting bucket list | Gets the list of all buckets under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| GET Bucket location | Getting bucket region information | Gets the region information of a bucket |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL configuration of a bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Getting bucket ACL | Gets the ACL configuration of a bucket |

## Basic Operations

### Getting Bucket List

#### Feature Description

This API (Bucket list) is used to get the list of all buckets under the specified account.

#### Return Result Descriptions

The result of the request is returned through QCloudListAllMyBucketsResult.

| Parameter Name | Description | Type |
| -------- | ------------------ | ------------------------------ |
| owner    | Information of the bucket owner | QCloudOwner *                  |
| buckets  | Information of all buckets | NSArray&lt;QCloudBucket`*` > * |

QCloudOwner parameter descriptions

| Parameter name | Description | Type |
| ----------- | ------------------ | ---------- |
| displayName | Owner name | NSString * |
| identifier  | Bucket owner ID | NSString * |

QCloudBucket parameter descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ---------- |
| name       | Bucket name                                                | NSString * |
| location   | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224). Examples: ap-beijing, ap-hongkong, eu-frankfurt | NSString * |
| createDate | Bucket creation time in ISO8601 format, such as 2016-11-09T08:46:32.000Z | NSString * |

#### Sample Request

```
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result, NSError* error) {
// Get the return information from the result
}];
[[QCloudCOSXMLService defaultCOSXML] GetService:request];e("CosServerException: " + serverEx.GetInfo());
}
```

### Creating a Bucket

#### Feature Description

This API (Put Bucket) is used to created a bucket.

#### Method Prototype

When you start to use COS, you need to create a bucket under the specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate QCloudPutBucketRequest and enter the required parameters.
2. Call the PutBucket method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the outputObject in the finishBlock of the callback.

#### Parameter Descriptions

#### QCloudPutBucketRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket            | Name of the bucket to be created. For the naming convention, see [Bucket Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312#naming-conventions) | NSString * | Yes |
| accessControlList | Defines the ACL attribute of the bucket. Value range: private, public-read-write, and public-read; default value: private | NSString * | No |
| grantRead         | Grants the grantee read permission in the format of id="OwnerUin"                    | NSString * | No |
| grantWrite        | Grants the grantee write permission in the format of id="OwnerUin"                    | NSString * | No   |
| grantFullControl  | Grants the grantee read/write permission in the format of id="OwnerUin"                    | NSString * | No   |

#### Sample Request

```objective-c
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];
request.bucket = @"examplebucket-1250000000"; //additional actions after finishing
[request setFinishBlock:^(id outputObject, NSError* error) {
// Get the header information returned by the server from the outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucket:request];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.
There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Checking a Bucket and Its Permission

#### Feature Description

- A Head Bucket request can be used to confirm whether a bucket exists and you have permission to access it.
- The permission of Head is the same as that of Read. If the bucket exists, 200 is returned. If you have no permission to access it, 403 is returned. If it does not exist, 404 is returned.   

#### QCloudHeadBucketRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |

#### Examples

```objective-c
QCloudHeadBucketRequest* request = [QCloudHeadBucketRequest new];
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(id outputObject, NSError* error) {
// Get the header information returned by the server from the outputObject
// Set and complete the callback. If there is no error, the bucket can be accessed normally. If there is an error, you can get the specific reason for the failure from the error code and message.
}];
[[QCloudCOSXMLService defaultCOSXML] HeadBucket:request];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Getting Bucket Region Information

#### Feature Description

This API is used to get the region information of a bucket.

#### Method Prototype

Before performing a bucket operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudGetBucketLocationRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudGetBucketLocationRequest and enter the bucket name.    
2. Call the GetBucketLocation method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the outputObject in the finishBlock of the callback.   

#### QCloudGetBucketLocationRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |

#### Return Result Descriptions

 QCloudBucketLocationConstraint parameter descriptions

| Parameter Name | Description | Type |
| ------------------ | -------------------- | --------- |
| locationConstraint | Describes the bucket region | NSString* |

#### Examples

```objective-c
QCloudGetBucketLocationRequest* locationReq = [QCloudGetBucketLocationRequest new];
locationReq.bucket = @"examplebucket-1250000000";
 __block QCloudBucketLocationConstraint* location;
[locationReq setFinishBlock:^(QCloudBucketLocationConstraint * _Nonnull result, NSError * _Nonnull error) {
       location = result;
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketLocation:locationReq];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.
There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting a Bucket

#### Feature Description

This API is used to delete the specified bucket.

#### Method Prototype

The steps to delete a bucket in the COS SDK for iOS are as follows:

1. Instantiate QCloudDeleteBucketRequest and enter the required parameters.
2. Call the DeleteBucket method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the outputObject in the finishBlock of the callback.

#### Parameter Descriptions

#### QCloudDeleteBucketRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Name of the bucket to be deleted in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket). Note that the bucket should be emptied before it can be deleted | NSString * | Yes   |

#### Sample Request

```objective-c
QCloudDeleteBucketRequest* request = [[QCloudDeleteBucketRequest alloc ] init];
request.bucket = @"examplebucket-1250000000";  // Bucket name in the format of BucketName-APPID
[request setFinishBlock:^(id outputObject,NSError*error) {
//additional actions after finishing
// Get the header information returned by the server from the outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucket:request];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## ACL

### Setting Bucket ACL

#### Method Prototype

Before performing a bucket operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudPutBucketACLRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudPutBucketACLRequest and enter the name of the bucket to be set and corresponding parameter according to the permission type of the set value.    
2. Call the PutBucketACL method in the QCloudCOSXMLService object to initiate a request.    
3. Check whether the setting succeeded in the outputObject of the finishBlock of the callback and perform some additions actions after successful setting.   

#### QCloudPutBucketACLRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| accessControlList | Defines the ACL attribute of the bucket. Value range: private, public-read-write, and public-read; default value: private | NSString * | No |
| grantRead         | Grants the grantee read permission in the format of id="OwnerUin"                    | NSString * | No |
| grantWrite        | Grants the grantee write permission in the format of id="OwnerUin"                    | NSString * | No   |
| grantFullControl  | Grants the grantee read/write permission in the format of id="OwnerUin"                    | NSString * | No   |

#### Examples

```objective-c
QCloudPutBucketACLRequest* putACL = [QCloudPutBucketACLRequest new];
NSString* appID = @“1250000000”;// Your AppID
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@", appID, appID];
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];
putACL.grantFullControl = grantString;
putACL.bucket = @“examplebucket-1250000000”;
[putACL setFinishBlock:^(id outputObject, NSError *error) {
//error occucs if error != nil
// Get the header information returned by the server from the outputObject
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketACL:putACL];

```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Getting Bucket ACL

#### Method Prototype

Before performing a bucket operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudGetBucketACLRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudGetBucketACLRequest and enter the name of the bucket for which to get the ACL.    
2. Call the GetBucketACL method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the QCloudACLPolicy in the finishBlock of the callback.    

#### QCloudGetBucketACLRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |

#### Return Result Descriptions

QCloudACLPolicy parameter descriptions

| Parameter Name | Description | Type |
| ----------- | ------------------------------------------------------------ | ---------- |
| displayName | Information of the bucket owner                                           | NSString * |
| identifier  | Bucket owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. If the account is a root account, `<OwnerUin>` and `<SubUin>` have the same value | NSString * |

QCloudACLOwner parameter descriptions

| Parameter Name | Description | Type |
| ----------------- | -------------------- | ------------------------- |
| owner    | Information of the bucket owner | QCloudACLOwner *          |
| accessControlList | Information of the grantee and permission | QCloudAccessControlList * |

QCloudAccessControlList parameter descriptions

| Parameter Name | Description | Type |
| --------- | ---------------------- | -------------------------------- |
| ACLGrants | Array used to store the grantee information | NSArray&lt;QCloudACLGrant`*` > * |

#### Examples

```objective-c
QCloudGetBucketACLRequest* getBucketACl   = [QCloudGetBucketACLRequest new];
getBucketACl.bucket = @"testbucket-123456789";
[getBucketACl setFinishBlock:^(QCloudACLPolicy * _Nonnull result, NSError * _Nonnull error) {
   // QCloudACLPolicy contains the ACL information of the bucket
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketACL:getBucketACl];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).
