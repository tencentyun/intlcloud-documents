## Overview
This document provides an overview of APIs and SDK code samples related to lifecycles.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle configuration | Sets lifecycle for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting a lifecycle configuration | Deletes the lifecycle configuration of a bucket |

## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting a Lifecycle Configuration

#### Description

This API is used to set the lifecycle configuration of a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```objective-c
QCloudPutBucketLifecycleRequest* request = [QCloudPutBucketLifecycleRequest new];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
__block QCloudLifecycleConfiguration* lifecycleConfiguration =
[[QCloudLifecycleConfiguration alloc] init];

// Rule description
QCloudLifecycleRule* rule = [[QCloudLifecycleRule alloc] init];

// Unique rule ID
rule.identifier = @"identifier";

// Indicates whether the rule is enabled. Enumerated values: Enabled, Disabled
rule.status = QCloudLifecycleStatueEnabled;

// Describes the set of objects subject to the rule
QCloudLifecycleRuleFilter* filter = [[QCloudLifecycleRuleFilter alloc] init];

// Specifies the prefix to which the rule applies. Objects that match the prefix are subject to the rule. You can specify at most one prefix
filter.prefix = @"prefix1";

// Describes the set of objects subject to the rule
rule.filter = filter;

// Transition attribute of the rule, specifying when an object should transition to Standard_IA or ARCHIVE storage class
QCloudLifecycleTransition* transition = [[QCloudLifecycleTransition alloc] init];

// Specifies the number of days after which the object is last modified that the action in the rule will be performed
transition.days = 100;

// Specifies the transitioned storage class of object. Enumerated values: Standard_IA, ARCHIVE
transition.storageClass = QCloudCOSStorageStandardIA;
rule.transition = transition;
request.lifeCycle = lifecycleConfiguration;

// Lifecycle configuration
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

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
putBucketLifecycleReq.bucket = "examplebucket-1250000000";

let config = QCloudLifecycleConfiguration.init();

// Rule description
let rule = QCloudLifecycleRule.init();

// Unique rule ID
rule.identifier = "swift";

// Indicates whether the rule is enabled. Enumerated values: Enabled, Disabled
rule.status = .enabled;

// Describes the set of objects subject to the rule
let fileter = QCloudLifecycleRuleFilter.init();

// Specifies the prefix to which the rule applies. Objects that match the prefix are subject to the rule. You can specify at most one prefix
fileter.prefix = "0";

// Describes the set of objects subject to the rule
rule.filter = fileter;

// Transition attribute of the rule, specifying when an object should transition to Standard_IA or ARCHIVE storage class
let transition = QCloudLifecycleTransition.init();

// Specifies the number of days after which the object is last modified that the action in the rule will be performed
transition.days = 100;

// Specifies the transitioned storage class of object. Enumerated values: Standard_IA, ARCHIVE
transition.storageClass = .standardIA;

rule.transition = transition;

putBucketLifecycleReq.lifeCycle = config;

// Lifecycle configuration
putBucketLifecycleReq.lifeCycle.rules = [rule];

putBucketLifecycleReq.finishBlock = {(result,error) in
    if let result = result {
        // "result" contains response headers.
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketLifecycle(putBucketLifecycleReq);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift).


## Querying a Lifecycle Configuration

#### Description

This API is used to query the lifecycle management configuration of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```objective-c
QCloudGetBucketLifecycleRequest* request = [QCloudGetBucketLifecycleRequest new];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(QCloudLifecycleConfiguration* result,NSError* error) {
    // You can get the returned information from result
    // `result.rules` is the array of rule descriptions
 
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
        // Lifecycle rule
        let rules = config.rules
    } else {
        print(error!);
    }
 
};
QCloudCOSXMLService.defaultCOSXML().getBucketLifecycle(getBucketLifeCycle);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift).

## Deleting a Lifecycle Configuration

#### Description

This API is used to delete the lifecycle management configuration of a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```objective-c
QCloudDeleteBucketLifeCycleRequest* request =
[[QCloudDeleteBucketLifeCycleRequest alloc ] init];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudLifecycleConfiguration* deleteResult, NSError* error) {
    // Returns the deletion result
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
        // "result" contains response headers.
    } else {
        print(error!);
    }
};
QCloudCOSXMLService.defaultCOSXML().deleteBucketLifeCycle(deleteBucketLifeCycle);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLifecycle.swift).

