## Overview

This document provides an overview of APIs and SDK code samples for COS inventory.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Creating an inventory job | Creates an inventory job for a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries the inventory jobs of a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job from a bucket |

## SDK API References

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Creating an Inventory Job

#### Feature description

This API (PUT Bucket inventory) is used to create an inventory job for a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-inventory)
```objective-c
QCloudPutBucketInventoryRequest *putReq = [QCloudPutBucketInventoryRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
putReq.bucket= @"examplebucket-1250000000";

// Name of the inventory job
putReq.inventoryID = @"list1";

// You can use XML to set specific configuration information for the inventory job in the request body, including the objects to be analyzed by the inventory job,
// analysis frequency, analysis dimensions, result format, and storage location.
QCloudInventoryConfiguration *config = [QCloudInventoryConfiguration new];

// Inventory name, corresponding to the ID in the request parameter
config.identifier = @"list1";

// Specifies whether inventory is enabled:
// if it is set to true, inventory is enabled;
// if false, no inventories will be generated
config.isEnabled = @"True";

// Information on the storage of the inventory result
QCloudInventoryDestination *des = [QCloudInventoryDestination new];

QCloudInventoryBucketDestination *btDes =[QCloudInventoryBucketDestination new];

// File format of the inventory result. Valid value: CSV
btDes.cs = @"CSV";

// ID of the bucket owner
btDes.account = @"1278687956";

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
btDes.bucket  = @"qcs::cos:ap-guangzhou::examplebucket-1250000000";

// Prefix of the inventory result
btDes.prefix = @"list1";

// Encryption with a COS-managed key
QCloudInventoryEncryption *enc = [QCloudInventoryEncryption new];
enc.ssecos = @"";

// Option to provide server-side encryption for the inventory result
btDes.encryption = enc;

// Information on the bucket where the inventory result is stored after export
des.bucketDestination = btDes;

// Information on the storage of the inventory result
config.destination = des;

// Configure the frequency of the inventory job
QCloudInventorySchedule *sc = [QCloudInventorySchedule new];

// Inventory job frequency. Enumerated values: Daily, Weekly
sc.frequency = @"Daily";
config.schedule = sc;
QCloudInventoryFilter *fileter = [QCloudInventoryFilter new];
fileter.prefix = @"myPrefix";
config.filter = fileter;
config.includedObjectVersions = QCloudCOSIncludedObjectVersionsAll;
QCloudInventoryOptionalFields *fields = [QCloudInventoryOptionalFields new];

fields.field = @[ @"Size",
                  @"LastModifiedDate",
                  @"ETag",
                  @"StorageClass",
                  @"IsMultipartUploaded",
                  @"ReplicationStatus"];

// Set the analysis items that should be included in the inventory result
config.optionalFields = fields;
putReq.inventoryConfiguration = config;
[putReq setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject contains information such as the ETag or custom headers in the response
    NSDictionary * result = (NSDictionary *)outputObject;

}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketInventory:putReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketInventory.m).


**Swift**

[//]: # (.cssg-snippet-put-bucket-inventory)
```swift
let putReq = QCloudPutBucketInventoryRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
putReq.bucket = "examplebucket-1250000000";

// Name of the inventory job
putReq.inventoryID = "list1";

// You can use XML to set specific configuration information for the inventory job in the request body, including the objects to be analyzed by the inventory job,
// analysis frequency, analysis dimensions, result format, and storage location.
let config = QCloudInventoryConfiguration.init();

// Inventory name, corresponding to the ID in the request parameter
config.identifier = "list1";

// Specifies whether inventory is enabled:
// if it is set to true, inventory is enabled;
// if false, no inventories will be generated
config.isEnabled = "True";

// Information on the storage of the inventory result
let des = QCloudInventoryDestination.init();
let btDes = QCloudInventoryBucketDestination.init();

// File format of the inventory result. Valid value: CSV
btDes.cs = "CSV";

// ID of the bucket owner
btDes.account = "1278687956";

// Name of the bucket where the inventory result is stored
btDes.bucket  = "qcs::cos:ap-guangzhou::examplebucket-1250000000";

// Prefix of the inventory result
btDes.prefix = "list1";

// Encryption with a COS-managed key
let enc = QCloudInventoryEncryption.init();
enc.ssecos = "";

// Option to provide server-side encryption for the inventory result
btDes.encryption = enc;

// Information on the bucket where the inventory result is stored after export
des.bucketDestination = btDes;

// Information on the storage of the inventory result
config.destination = des;

// Configure the frequency of the inventory job
let sc = QCloudInventorySchedule.init();

// Inventory job frequency. Enumerated values: Daily, Weekly
sc.frequency = "Daily";
config.schedule = sc;
let fileter = QCloudInventoryFilter.init();
fileter.prefix = "myPrefix";
config.filter = fileter;
config.includedObjectVersions = .all;
let fields = QCloudInventoryOptionalFields.init();
fields.field = [ "Size",
                 "LastModifiedDate",
                 "ETag",
                 "StorageClass",
                 "IsMultipartUploaded",
                 "ReplicationStatus"];
// Set the analysis items that should be included in the inventory result
config.optionalFields = fields;
putReq.inventoryConfiguration = config;

putReq.finishBlock = {(result,error) in
    if let result = result {
        // result contains response headers
    } else{
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().putBucketInventory(putReq);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketInventory.swift).


#### Error codes

The following describes some common errors that may occur when you call this API:

| Error Code | Description | Status Code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You most likely do not have access permission for the bucket | HTTP 403 Forbidden   |

## Querying Inventory Jobs

#### Feature description

This API is used to query the inventory jobs of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-inventory)
```objective-c
QCloudGetBucketInventoryRequest *getReq = [QCloudGetBucketInventoryRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getReq.bucket = @"examplebucket-1250000000";

// Name of the inventory job
getReq.inventoryID = @"list1";
[getReq setFinishBlock:^(QCloudInventoryConfiguration * _Nonnull result,
                         NSError * _Nonnull error) {
    // result contains the inventory information
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketInventory:getReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-inventory)
```swift
let req = QCloudGetBucketInventoryRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";
// Name of the inventory job
req.inventoryID = "list1";
req.setFinish {(result,error) in
    if let result = result {
        // Job information
        let enabled = result.isEnabled
    } else{
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketInventory(req);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift).

## Deleting an Inventory Job

#### Feature description

This API is used to delete a specified inventory job from a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-inventory)
```objective-c
QCloudDeleteBucketInventoryRequest *delReq = [QCloudDeleteBucketInventoryRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
delReq.bucket = @"examplebucket-1250000000";

// Name of the inventory job
delReq.inventoryID = @"list1";
[delReq setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject contains information such as the ETag or custom headers in the response
    NSDictionary * result = (NSDictionary *)outputObject;
    
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketInventory:delReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m).

**Swift**

[//]: # (.cssg-snippet-delete-bucket-inventory)
```swift
let delReq = QCloudDeleteBucketInventoryRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
delReq.bucket = "examplebucket-1250000000";

// Name of the inventory job
delReq.inventoryID = "list1";
delReq.finishBlock = {(result,error) in
    if let result = result {
        // result contains response headers
    } else{
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().deleteBucketInventory(delReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift).

