## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning configuration of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning configuration of a bucket |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Versioning

#### Feature description

This API is used to set the versioning configuration of a specified bucket. Once enabled, versioning can only be suspended but not disabled.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-put-bucket-versioning"
```objective-c
// Enable versioning
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket =@"examplebucket-1250000000";

// Specific versioning configuration
QCloudBucketVersioningConfiguration* versioningConfiguration =
    [[QCloudBucketVersioningConfiguration alloc] init];

request.configuration = versioningConfiguration;

// Indicates whether versioning is enabled. Enumerated values: Suspended, Enabled
versioningConfiguration.status = QCloudCOSBucketVersioningStatusEnabled;

[request setFinishBlock:^(id outputObject, NSError* error) {
    
    // You can get the header returned by the server from outputObject
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketVersioning.m).

**Swift**

[//]: # ".cssg-snippet-put-bucket-versioning"
```swift
// Enable versioning
let putBucketVersioning = QCloudPutBucketVersioningRequest.init();

// Bucket name in the format: `BucketName-APPID`
putBucketVersioning.bucket = "examplebucket-1250000000";

// Specific versioning configuration
let config = QCloudBucketVersioningConfiguration.init();

// Indicates whether versioning is enabled. Enumerated values: Suspended, Enabled
config.status = .enabled;

putBucketVersioning.configuration = config;

putBucketVersioning.finishBlock = {(result,error) in
    // You can get the header information returned by the server from `result`
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucketVersioning(putBucketVersioning);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketVersioning.swift).

## Querying Versioning

#### Feature description

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
    
    // `result` contains the versioning status
    result.status;
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/BucketVersioning.m).

**Swift**

[//]: # ".cssg-snippet-get-bucket-versioning"
```swift
let getBucketVersioning = QCloudGetBucketVersioningRequest.init();

// Bucket name in the format: `BucketName-APPID`
getBucketVersioning.bucket = "examplebucket-1250000000";

getBucketVersioning.setFinish { (config, error) in
    if error != nil{
        print(error!);
    }else{
        print(config!);
    }
       
}
QCloudCOSXMLService.defaultCOSXML().getBucketVersioning(getBucketVersioning);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/BucketVersioning.swift).

