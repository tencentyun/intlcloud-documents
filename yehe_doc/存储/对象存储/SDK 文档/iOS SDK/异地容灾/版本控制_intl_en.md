## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets a versioning configuration for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning configuration of a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Versioning

#### API description 

This API is used to set a versioning configuration for a specified bucket. Once enabled, versioning can only be suspended but not disabled.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-put-bucket-versioning"
```objective-c
// Enable versioning
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket =@"examplebucket-1250000000";

// Specify the versioning configuration
QCloudBucketVersioningConfiguration* versioningConfiguration =
    [[QCloudBucketVersioningConfiguration alloc] init];

request.configuration = versioningConfiguration;

// Indicate whether versioning is enabled. Enumerated values: QCloudCOSBucketVersioningStatusEnabled,
// QCloudCOSBucketVersioningStatusSuspended
versioningConfiguration.status = QCloudCOSBucketVersioningStatusEnabled;

[request setFinishBlock:^(id outputObject, NSError* error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketVersioning.m).

**Swift**

[//]: # ".cssg-snippet-put-bucket-versioning"
```swift
// Enable versioning
let putBucketVersioning = QCloudPutBucketVersioningRequest.init();

// Bucket name in the format: `BucketName-APPID`
putBucketVersioning.bucket = "examplebucket-1250000000";

// Specify the versioning configuration
let config = QCloudBucketVersioningConfiguration.init();

// Indicate whether versioning is enabled. Enumerated values: Suspended, Enabled
config.status = .enabled;

putBucketVersioning.configuration = config;

putBucketVersioning.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketVersioning(putBucketVersioning);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketVersioning.swift).

## Querying Versioning

#### API description 

This API is used to query the versioning configuration of a specified bucket.

- To get the versioning status of a bucket, you need to have read permission for the bucket.
- There are three versioning statuses: not enabled, enabled, and suspended.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-get-bucket-versioning"
```objective-c
QCloudGetBucketVersioningRequest* request =
                            [[QCloudGetBucketVersioningRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result,
                          NSError* error) {
    // Get the status of multiple versions
    QCloudCOSBucketVersioningStatus * status = result.status;
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketVersioning.m).

**Swift**

[//]: # ".cssg-snippet-get-bucket-versioning"
```swift
let getBucketVersioning = QCloudGetBucketVersioningRequest.init();

// Bucket name in the format: `BucketName-APPID`
getBucketVersioning.bucket = "examplebucket-1250000000";

getBucketVersioning.setFinish { (config, error) in
    if let config = config {
        // Get the status of multiple versions
        let status = config.status
    } else {
        print(error!);
    }
       
}
QCloudCOSXMLService.defaultCOSXML().getBucketVersioning(getBucketVersioning);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketVersioning.swift).

