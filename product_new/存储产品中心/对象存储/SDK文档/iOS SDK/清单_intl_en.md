

## Overview

This document provides an overview of APIs and SDK code samples related to inventory.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Setting an inventory job | Sets an inventory job in a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries inventory jobs for a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job of a bucket |

## Setting Inventory Job

#### Feature description

This API (PUT Bucket inventory) is used to create an inventory job in a bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudPutBucketInventoryRequest`
2. Call the `PutBucketInventory` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `outputObject` in the `finishBlock` of the callback.

#### Sample request

[//]: # (.cssg-snippet-objc-put-bucket-inventory)

```
QCloudPutBucketInventoryRequest *putReq = [QCloudPutBucketInventoryRequest new];
   putReq.bucket= @"examplebucket-1250000000";
   putReq.inventoryID = @"list1";
   QCloudInventoryConfiguration *config = [QCloudInventoryConfiguration new];
   config.identifier = @"list1";
   config.isEnabled = @"True";
   QCloudInventoryDestination *des = [QCloudInventoryDestination new];
   QCloudInventoryBucketDestination *btDes =[QCloudInventoryBucketDestination new];
   btDes.cs = @"CSV";
   btDes.account = @"1278687956";
   btDes.bucket  = @"qcs::cos:ap-guangzhou::examplebucket-1250000000";
   btDes.prefix = @"list1";
   QCloudInventoryEncryption *enc = [QCloudInventoryEncryption new];
   enc.ssecos = @"";
   btDes.encryption = enc;
   des.bucketDestination = btDes;
   config.destination = des;
   QCloudInventorySchedule *sc = [QCloudInventorySchedule new];
   sc.frequency = @"Daily";
   config.schedule = sc;
   QCloudInventoryFilter *fileter = [QCloudInventoryFilter new];
   fileter.prefix = @"myPrefix";
   config.filter = fileter;
   config.includedObjectVersions = QCloudCOSIncludedObjectVersionsAll;
   QCloudInventoryOptionalFields *fields = [QCloudInventoryOptionalFields new];
   fields.field = @[ @"Size",@"LastModifiedDate",@"ETag",@"StorageClass",@"IsMultipartUploaded",@"ReplicationStatus"];
   config.optionalFields = fields;
   putReq.inventoryConfiguration = config;
   [putReq setFinishBlock:^(id outputObject, NSError *error) {


   }];
   [[QCloudCOSXMLService defaultCOSXML] PutBucketInventory:putReq];
```

Swift sample code:

[//]: # (.cssg-snippet-swift-put-bucket-inventory)

```
let putReq = QCloudPutBucketInventoryRequest.init();
putReq.bucket = "examplebucket-1250000000";
putReq.inventoryID = "list1";
let config = QCloudInventoryConfiguration.init();
config.identifier = "list1";
config.isEnabled = "True";
let des = QCloudInventoryDestination.init();
let btDes = QCloudInventoryBucketDestination.init();
btDes.cs = "CSV";
btDes.account = "1278687956";
btDes.bucket  = "qcs::cos:ap-guangzhou::examplebucket-1250000000";
btDes.prefix = "list1";
let enc = QCloudInventoryEncryption.init();
enc.ssecos = "";
btDes.encryption = enc;
des.bucketDestination = btDes;
config.destination = des;
let sc = QCloudInventorySchedule.init();
sc.frequency = "Daily";
config.schedule = sc;
let fileter = QCloudInventoryFilter.init();
fileter.prefix = "myPrefix";
config.filter = fileter;
config.includedObjectVersions = .all;
let fields = QCloudInventoryOptionalFields.init();
fields.field = [ "Size","LastModifiedDate","ETag","StorageClass","IsMultipartUploaded","ReplicationStatus"];
config.optionalFields = fields;
putReq.inventoryConfiguration = config;

putReq.finishBlock = {(result,error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
}

QCloudCOSXMLService.defaultCOSXML().putBucketInventory(putReq);

```

#### Parameter description

#### `QCloudPutBucketInventoryRequest` request parameter description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | ------------------------------ | -------- |
| bucket  | Bucket for which to set an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) |  NSString * | Yes |
| inventoryID        | Inventory job name. Default value: None. Valid characters: a-z, A-Z, 0-9, -, _, .             | NSString * | Yes |
| inventoryConfiguration | Indicates the status of the logging configuration                                       | QCloudInventoryConfiguration * | Yes       |

#### `QCloudInventoryConfiguration` parameter description

| Parameter Name | Description | Type | Required |
| ---------------------- | ------------------------------------------------------------ | --------------------------------- | -------- |
| identifier             | Inventory name, corresponding to the ID in the request parameter                           | NSString *                        | Yes       |
| isEnabled              | Inventory status flag: <br><li>If this is set to `True`, the inventory is enabled; <br><li>if `False`, no inventories will be generated | NSString *                        | Yes       |
| includedObjectVersions | Whether to include object versions in the inventory <br><li>If this is set to `All`, the inventory will include all object versions and add `VersionId`, `IsLatest`, and `DeleteMarker` fields <br><li>If `Current`, no object version information will be included in the inventory | QCloudCOSIncludedObjectVersions * | Yes       |
| destination            | Describes the information of the inventory result storage                                   | QCloudInventoryDestination *      | Yes       |
| schedule               | Filters the objects to be analyzed. The inventory feature will analyze the objects that match the prefix set in `Filter` | QCloudInventorySchedule *         | Yes       |
| filter                 | Describes the information of the inventory result storage                                       | QCloudInventoryFilter *           | No       |
| optionalFields         | Name of the analysis items that can be optionally included in the inventory result. Valid values: Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, ReplicationStatus | QCloudInventoryOptionalFields *   | No       |



#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

#### Error code description

Some frequent special errors that may occur with this request are listed below:

| Error code | Description | Status code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You probably do not have access to the bucket. | HTTP 403 Forbidden |

## Querying Inventory Job

#### Feature description

This API (GET Bucket inventory) is used to query the inventory job information in a bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudGetBucketInventoryRequest`
2. Call the `GetBucketInventory` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `result` in the `finishBlock` of the callback.

#### Sample request

[//]: # (.cssg-snippet-objc-get-bucket-inventory)

```
QCloudGetBucketInventoryRequest *getReq = [QCloudGetBucketInventoryRequest new];
getReq.bucket = @"examplebucket-1250000000";
getReq.inventoryID = @"list1";
[getReq setFinishBlock:^(QCloudInventoryConfiguration * _Nonnull result, NSError * _Nonnull error) {

}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketInventory:getReq];

```

Swift sample code:

[//]: # (.cssg-snippet-swift-get-bucket-inventory)

```
let req = QCloudGetBucketInventoryRequest.init();
req.bucket = "examplebucket-1250000000";
req.inventoryID = "list1";
req.setFinish {(result,error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketInventory(req);

```

#### Parameter description

#### `QCloudGetBucketInventoryRequest` request parameter description

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ---------- | -------- |
| bucket  | Bucket for which to query an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) |  NSString * | Yes |
| inventoryID        | Inventory job name. Default value: None. Valid characters: a-z, A-Z, 0-9, -, _, .             | NSString * | Yes |

#### Returned result description

#### `QCloudInventoryConfiguration` parameter description

| Parameter Name | Description | Type |
| ---------------------- | ------------------------------------------------------------ | --------------------------------- |
| identifier             | Inventory name, corresponding to the ID in the request parameter                           | NSString *                        |
| isEnabled              | Inventory status flag: <br><li>If this is set to `True`, the inventory is enabled; <br><li>if `False`, no inventories will be generated | NSString *                        |
| includedObjectVersions | Whether to include object versions in the inventory <br><li>If this is set to `All`, the inventory will include all object versions and add `VersionId`, `IsLatest`, and `DeleteMarker` fields <br><li>If `Current`, no object version information will be included in the inventory | QCloudCOSIncludedObjectVersions * |
| destination            | Describes the information of the inventory result storage                                   | QCloudInventoryDestination *      |
| schedule               | Filters the objects to be analyzed. The inventory feature will analyze the objects that match the prefix set in `Filter` | QCloudInventorySchedule *         |
| filter                 | Describes the information of the inventory result storage                                       | QCloudInventoryFilter *           |
| optionalFields         | Name of the analysis items that can be optionally included in the inventory result. Valid values: Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, ReplicationStatus | QCloudInventoryOptionalFields *   |

#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).



## Deleting Inventory Job

#### Feature description

This API (DELETE Bucket inventory) is used to delete a specified inventory job of a bucket.

#### Method prototype

When you start to use COS, you need to create a bucket under a specified account for object use and management and specify the region where the bucket resides. The user who creates a bucket is considered the owner of the bucket by default. If you do not specify the access permission when creating a bucket, the bucket has private read/write ("private") permission. The steps are as follows:    

1. Instantiate `QCloudDeleteBucketInventoryRequest`
2. Call the `DeleteBucketInventory` method in the `QCloudCOSXMLService` object to initiate a request.
3. Get the specific content from the `outputObject` in the `finishBlock` of the callback.

#### Sample request

[//]: # (.cssg-snippet-objc-delete-bucket-inventory)

```
QCloudDeleteBucketInventoryRequest *delReq = [QCloudDeleteBucketInventoryRequest new];
delReq.bucket = @"examplebucket-1250000000";
delReq.inventoryID = @"list1";
[delReq setFinishBlock:^(id outputObject, NSError *error) {

}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketInventory:delReq];

```

Swift sample code:

[//]: # (.cssg-snippet-swift-delete-bucket-inventory)

```
let delReq = QCloudDeleteBucketInventoryRequest.init();
delReq.bucket = "examplebucket-1250000000";
delReq.inventoryID = "list1";
delReq.finishBlock = {(result,error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
}

QCloudCOSXMLService.defaultCOSXML().deleteBucketInventory(delReq);

```

#### Parameter description

#### `QCloudDeleteBucketInventoryRequest` request parameter description

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ---------- | -------- |
| bucket  | Bucket for which to delete an inventory job in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) |  NSString * | Yes |
| inventoryID        | Inventory job name. Default value: None. Valid characters: a-z, A-Z, 0-9, -, _, .             | NSString * | Yes |

#### Returned error code description

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, please see the definitions in the `NSURLError.h` header of the `Foundation` framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, please see [API Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, please see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

