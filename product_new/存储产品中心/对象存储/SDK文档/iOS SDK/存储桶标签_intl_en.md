

## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting a bucket tag | Sets a tag for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting a bucket tag | Deletes a specified bucket tag |

## Setting Bucket Tag

#### Feature description

This API (PUT Bucket tagging) is used to set a tag for an existing bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudPutBucketTaggingRequest`
2. Call the `PutBucketTagging` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `outputObject` in the `finishBlock` of the callback.

#### Sample request

[//]: # (.cssg-snippet-objc-put-bucket-tagging)

```
QCloudPutBucketTaggingRequest *putReq = [QCloudPutBucketTaggingRequest new];
putReq.bucket = @"examplebucket-1250000000";

QCloudBucketTagging *taggings = [QCloudBucketTagging new];
QCloudBucketTag *tag1 = [QCloudBucketTag new];
QCloudBucketTagSet *tagSet = [QCloudBucketTagSet new];
taggings.tagSet = tagSet;
tag1.key = @"age";
tag1.value = @"20";
QCloudBucketTag *tag2 = [QCloudBucketTag new];
tag2.key = @"name";
tag2.value = @"karis";
tagSet.tag = @[tag1,tag2];
putReq.taggings = taggings;

[putReq setFinishBlock:^(id outputObject, NSError *error) {

}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketTagging:putReq];
```

Swift sample code:

[//]: # (.cssg-snippet-swift-put-bucket-tagging)

```
let req = QCloudPutBucketTaggingRequest.init();
req.bucket = "examplebucket-1250000000";
let taggings = QCloudBucketTagging.init();
let tagSet = QCloudBucketTagSet.init();
taggings.tagSet = tagSet;
let tag1 = QCloudBucketTag.init();
tag1.key = "age";
tag1.value = "20";

let tag2 = QCloudBucketTag.init();
tag2.key = "name";
tag2.value = "karis";
tagSet.tag = [tag1,tag2];
req.taggings = taggings;
req.finishBlock = {(result,error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketTagging(req);
```

#### Parameter description

#### `QCloudPutBucketTaggingRequest` request parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | --------------------- | -------- |
| bucket  | Bucket for which to set a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) |  NSString * | Yes |
| taggings | Tag set                                                     | QCloudBucketTagging * | Yes       |

#### `QCloudBucketTagging` parameter description

| Parameter Name | Description | Type | Required |
| -------- | ---------- | -------------------- | -------- |
| tagSet   | Tag set | QCloudBucketTagSet * | Yes       |

#### `QCloudBucketTagSet` parameter description

| Parameter Name | Description | Type | Required |
| -------- | -------------------------- | --------------------------- | -------- |
| tag      | Tag set. Up to 10 tags are supported | NSArray<QCloudBucketTag*> * | Yes       |

#### `QCloudBucketTag` parameter description

| Parameter Name | Description | Type | Required |
| -------- | -------- | ---------- | -------- |
| key      | Tag key | NSString * | Yes       |
| value    | Tag value | NSString * | Yes       |

#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Querying Bucket Tag

#### Feature description

This API (GET Bucket tagging) is used to query the existing tags of a specified bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudGetBucketTaggingRequest`
2. Call the `GetBucketTagging` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `result` in the `finishBlock` of the callback.



#### Sample request

[//]: # (.cssg-snippet-objc-get-bucket-tagging)

```
QCloudGetBucketTaggingRequest *getReq = [QCloudGetBucketTaggingRequest new];
       getReq.bucket = @"examplebucket-1250000000";
       [getReq setFinishBlock:^(QCloudBucketTagging * result, NSError * error) {
       }];
       [[QCloudCOSXMLService defaultCOSXML] GetBucketTagging:getReq];
```

Swift sample code:

[//]: # (.cssg-snippet-swift-get-bucket-tagging)

```
let req = QCloudGetBucketTaggingRequest.init();
req.bucket = "examplebucket-1250000000";
req.setFinish { (result, error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
};
QCloudCOSXMLService.defaultCOSXML().getBucketTagging(req);
```

#### Parameter description

#### `QCloudGetBucketTaggingRequest` request parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | -------- |
| bucket  | Bucket for which to query a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) |  NSString * | Yes |

#### Returned result description

#### `QCloudBucketTagging` parameter description

| Parameter Name | Description | Type |
| -------- | ---------- | -------------------- |
| tagSet   | Tag set | QCloudBucketTagSet * |

#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).



## Deleting Bucket Tag

#### Feature description

This API (DELETE Bucket tagging) is used to delete an existing tag of a specified bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudDeleteBucketTaggingRequest`
2. Call the `DeleteBucketTagging` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `outputObject` in the `finishBlock` of the callback.



#### Sample request

[//]: # (.cssg-snippet-objc-delete-bucket-tagging)

```
QCloudDeleteBucketTaggingRequest *delReq = [QCloudDeleteBucketTaggingRequest new];
delReq.bucket =  @"examplebucket-1250000000";
[delReq setFinishBlock:^(id outputObject, NSError *error) {

}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketTagging:delReq];
```

Swift sample code:

[//]: # (.cssg-snippet-swift-delete-bucket-tagging)

```
let req = QCloudDeleteBucketTaggingRequest.init();
req.bucket = "examplebucket-1250000000";
req.finishBlock =  { (result, error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
};
QCloudCOSXMLService.defaultCOSXML().deleteBucketTagging(req);
```

#### Parameter description

#### `QCloudDeleteBucketTaggingRequest` request parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | -------- |
| bucket  | Bucket for which to delete a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) |  NSString * | Yes |

#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).
