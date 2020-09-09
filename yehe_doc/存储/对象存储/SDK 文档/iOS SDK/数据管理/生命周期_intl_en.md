## Overview
This document provides an overview of APIs and SDK code samples related to lifecycle.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle configuration | Sets the lifecycle management configuration for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle configuration | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle configuration | Deletes the lifecycle management configuration of a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Lifecycle Configuration

#### API description 

This API is used to set a lifecycle configuration for a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```objective-c
QCloudPutBucketLifecycleRequest* request = [QCloudPutBucketLifecycleRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";
__block QCloudLifecycleConfiguration* lifecycleConfiguration =
[[QCloudLifecycleConfiguration alloc] init];

// Specify the lifecycle rule
QCloudLifecycleRule* rule = [[QCloudLifecycleRule alloc] init];

// Unique rule ID
rule.identifier = @"identifier";

// Indicate whether the rule is enabled. Enumerated values: Enabled, Disabled
rule.status = QCloudLifecycleStatueEnabled;

// Specify the set of objects to which the rule applies
QCloudLifecycleRuleFilter* filter = [[QCloudLifecycleRuleFilter alloc] init];

// Specify the prefix to filter by. Objects that match the prefix are subject to the rule. You can specify at most one prefix
filter.prefix = "prefix/";

// “filter” specifies the set of objects to which the rule applies
rule.filter = filter;

// Specify when the object transitions to Standard_IA or ARCHIVE storage class
QCloudLifecycleTransition* transition = [[QCloudLifecycleTransition alloc] init];

// Specify the number of days after which the object is last modified that the action in the rule will be performed
transition.days = 100;

// Specify the storage class into which the object transitions. Enumerated values: Standard_IA, ARCHIVE
transition.storageClass = QCloudCOSStorageStandardIA;
rule.transition = transition;
request.lifeCycle = lifecycleConfiguration;

// Specify the lifecycle configuration
request.lifeCycle.rules = @[rule];
[request setFinishBlock:^(id outputObject, NSError* error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutBucketLifecycle:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLifecycle.m).


**Swift**

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```swift
let putBucketLifecycleReq = QCloudPutBucketLifecycleRequest.init();

// Bucket name in the format: `BucketName-APPID`
putBucketLifecycleReq.bucket = "examplebucket-1250000000";

let config = QCloudLifecycleConfiguration.init();

// Specify the lifecycle rule
let rule = QCloudLifecycleRule.init();

// Unique rule ID
rule.identifier = "swift";

// Indicate whether the rule is enabled. Enumerated values: Enabled, Disabled
rule.status = .enabled;

// “filter” specifies the set of objects to which the rule applies
let fileter = QCloudLifecycleRuleFilter.init();

// Specify the prefix to filter by. Objects that match the prefix are subject to the rule. You can specify at most one prefix
fileter.prefix = "0";

// “filter” specifies the set of objects to which the rule applies
rule.filter = fileter;

// Specify when the object transitions to STANDARD_IA or ARCHIVE storage class
let transition = QCloudLifecycleTransition.init();

// Specify the number of days after which the object is last modified that the action in the rule will be performed
transition.days = 100;

// Specify the storage class into which the object transitions. Enumerated values: STANDARD_IA, ARCHIVE
transition.storageClass = .standardIA;

rule.transition = transition;

putBucketLifecycleReq.lifeCycle = config;

// Specify the lifecycle configuration
putBucketLifecycleReq.lifeCycle.rules = [rule];

putBucketLifecycleReq.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketLifecycle(putBucketLifecycleReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift).


## Querying Lifecycle Configuration

#### API description 

This API is used to query the lifecycle management configuration of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```objective-c
QCloudGetBucketLifecycleRequest* request = [QCloudGetBucketLifecycleRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(QCloudLifecycleConfiguration* result,NSError* error) {
    // “result” contains the request results
    // “result.rules” is an array of rules
 
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketLifecycle:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLifecycle.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```swift
let getBucketLifeCycle = QCloudGetBucketLifecycleRequest.init();
getBucketLifeCycle.bucket = "examplebucket-1250000000";
getBucketLifeCycle.setFinish { (config, error) in
    if let config = config {
        // A set of lifecycle rules
        let rules = config.rules
    } else {
        print(error!);
    }
 
};
QCloudCOSXMLService.defaultCOSXML().getBucketLifecycle(getBucketLifeCycle);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift).

## Deleting Lifecycle Configuration

#### API description 

This API is used to delete the lifecycle management configuration from a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```objective-c
QCloudDeleteBucketLifeCycleRequest* request =
[[QCloudDeleteBucketLifeCycleRequest alloc ] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudLifecycleConfiguration* deleteResult, NSError* error) {
    // Return the deletion result
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketLifeCycle:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLifecycle.m).

**Swift**

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```swift
let deleteBucketLifeCycle = QCloudDeleteBucketLifeCycleRequest.init();
deleteBucketLifeCycle.bucket = "examplebucket-1250000000";
deleteBucketLifeCycle.finishBlock = { (result, error) in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
};
QCloudCOSXMLService.defaultCOSXML().deleteBucketLifeCycle(deleteBucketLifeCycle);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift).

