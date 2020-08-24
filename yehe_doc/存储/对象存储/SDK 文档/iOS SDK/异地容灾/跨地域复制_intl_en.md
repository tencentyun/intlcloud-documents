## Overview

This document provides an overview of APIs and SDK code samples related to cross-region replication.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication rules | Sets the cross-region replication rules of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication rules | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication rules | Deletes the cross-region replication rules of a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Cross-region Replication Rules

#### Feature description

This API is used to set the cross-region replication rules of a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-replication)
```objective-c
QCloudPutBucketReplicationRequest* request = [[QCloudPutBucketReplicationRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// All cross-region replication configuration information
QCloudBucketReplicationConfiguation* replConfiguration =
                            [[QCloudBucketReplicationConfiguation alloc] init];

// Initiator ID
replConfiguration.role = @"qcs::cam::uin/100000000001:uin/100000000001";

// Specific configuration information
QCloudBucketReplicationRule* rule = [[QCloudBucketReplicationRule alloc] init];

// Name of the specific rule
rule.identifier = @"identifier";
rule.status = QCloudCOSXMLStatusEnabled;

// Resource ID
QCloudBucketReplicationDestination* destination = [[QCloudBucketReplicationDestination alloc] init];
NSString* destinationBucket = @"destinationbucket-1250000000";

// Destination bucket region
NSString* region = @"ap-beijing";
destination.bucket = [NSString stringWithFormat:@"qcs::cos:%@::%@",region,destinationBucket];

// Destination bucket information
rule.destination = destination;

// Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. The prefix matching root directory is empty
rule.prefix = @"prefix1";
replConfiguration.rule = @[rule];
request.configuation = replConfiguration;

[request setFinishBlock:^(id outputObject, NSError* error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
    
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketRelication:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReplication.m).

**Swift**

[//]: # (.cssg-snippet-put-bucket-replication)
```swift
let putBucketReplication = QCloudPutBucketReplicationRequest.init();

// Bucket name in the format: `BucketName-APPID`
putBucketReplication.bucket = "examplebucket-1250000000";

// All cross-region replication configuration information
let config = QCloudBucketReplicationConfiguation.init();
config.role = "qcs::cam::uin/100000000001:uin/100000000001";

// Initiator ID
let rule = QCloudBucketReplicationRule.init();
 
// Name of the specific rule
rule.identifier = "swift";
rule.status = .enabled;

// Resource ID
let destination = QCloudBucketReplicationDestination.init();
let destinationBucket = "destinationbucket-1250000000";
let region = "ap-beijing";
destination.bucket = "qcs::cos:\(region)::\(destinationBucket)";

// Destination bucket information
rule.destination = destination;

// Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. The prefix matching root directory is empty
rule.prefix = "a";

config.rule = [rule];

putBucketReplication.configuation = config;

putBucketReplication.finishBlock = {(result,error) in
    // You can get the header information returned by the server from `result`
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketRelication(putBucketReplication);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReplication.swift).

## Querying Cross-region Replication Rules

#### Feature description

This API is used to query the cross-region replication rules of a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-replication)
```objective-c
QCloudGetBucketReplicationRequest* request = [[QCloudGetBucketReplicationRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudBucketReplicationConfiguation* result,
                          NSError* error) {
    // Specific configuration information. A maximum of 1,000 policies are supported. All policies must point to the same destination bucket
    NSArray *rules = result.rule;
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketReplication:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReplication.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-replication)
```swift
let getBucketReplication = QCloudGetBucketReplicationRequest.init();
getBucketReplication.bucket = "examplebucket-1250000000";
getBucketReplication.setFinish { (config, error) in
    if error != nil{
        print(error!);
    }else{
        print(config!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucketReplication(getBucketReplication);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReplication.swift).

## Deleting Cross-region Replication Rules

#### Feature description

This API is used to delete the cross-region replication rules of a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-replication)
```objective-c
QCloudDeleteBucketReplicationRequest* request =
                        [[QCloudDeleteBucketReplicationRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
    
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketReplication:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketReplication.m).

**Swift**

[//]: # (.cssg-snippet-delete-bucket-replication)
```swift
let deleteBucketReplication = QCloudDeleteBucketReplicationRequest.init();
deleteBucketReplication.bucket = "examplebucket-1250000000";
deleteBucketReplication.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteBucketReplication(deleteBucketReplication);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketReplication.swift).

