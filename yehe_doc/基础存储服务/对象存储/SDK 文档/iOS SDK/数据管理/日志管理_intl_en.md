## Overview

This document provides an overview of APIs and SDK code samples related to logging.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting logging | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying logging configuration | Queries the logging configuration of a source bucket |

## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Logging Configuration

#### Description

This API is used to enable logging for a source bucket and store the access logs in a specified destination bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket-logging)
```objective-c
QCloudPutBucketLoggingRequest *request = [QCloudPutBucketLoggingRequest new];

// Status of the logging configuration. If there is no subnode information, logging is disabled
QCloudBucketLoggingStatus *status = [QCloudBucketLoggingStatus new];

// Specific logging configuration; this mainly refers to the destination bucket
QCloudLoggingEnabled *loggingEnabled = [QCloudLoggingEnabled new];

// Destination bucket for storing logs; this can be the source bucket (not recommended) or a bucket in the same region under the same account
loggingEnabled.targetBucket = @"examplebucket-1250000000";

// Specified path in the destination bucket for storing logs
loggingEnabled.targetPrefix = @"mylogs";

status.loggingEnabled = loggingEnabled;
request.bucketLoggingStatus = status;

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
   // `outputObject` contains all the HTTP response headers
   NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketLogging:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLogging.m).

**Swift**

[//]: # (.cssg-snippet-put-bucket-logging)
```swift
let req = QCloudPutBucketLoggingRequest.init();

// Status of the logging configuration. If there is no subnode information, logging is disabled
let status = QCloudBucketLoggingStatus.init();

// Specific logging configuration; this mainly refers to the destination bucket
let loggingEnabled = QCloudLoggingEnabled.init();

// Destination bucket for storing logs; this can be the source bucket (not recommended) or a bucket in the same region under the same account
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
loggingEnabled.targetBucket = "examplebucket-1250000000";

// Specified path in the destination bucket for storing logs
loggingEnabled.targetPrefix = "logs/";

status.loggingEnabled = loggingEnabled;
req.bucketLoggingStatus = status;

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";
req.finishBlock = {(result,error) in
    if let result = result {
        // "result" contains response headers.
    } else {
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().putBucketLogging(req);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLogging.swift).

## Querying Logging Configuration

#### Description

This API is used to query the logging configuration of a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-logging)
```objective-c
QCloudGetBucketLoggingRequest *getReq = [QCloudGetBucketLoggingRequest new];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getReq.bucket = @"examplebucket-1250000000";

[getReq setFinishBlock:^(QCloudBucketLoggingStatus * _Nonnull result,
                         NSError * _Nonnull error) {
    // Logging configuration
    QCloudLoggingEnabled *loggingEnabled = result.loggingEnabled;
}];
[[QCloudCOSXMLService defaultCOSXML]GetBucketLogging:getReq];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketLogging.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-logging)
```swift
let req = QCloudGetBucketLoggingRequest.init();

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";
req.setFinish { (result, error) in
    if let result = result {
        // Logging configuration
        let enabled = result.loggingEnabled
    } else {
        print(error!);
    }
};
QCloudCOSXMLService.defaultCOSXML().getBucketLogging(req);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketLogging.swift).

