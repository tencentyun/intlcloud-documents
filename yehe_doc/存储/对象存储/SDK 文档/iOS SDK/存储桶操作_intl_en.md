## Overview

This document provides an overview of APIs and SDK code samples related to basic bucket operations.


| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates bucket under a specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under a specified account |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Querying a Bucket List

#### API description

This API is used to query the list of all buckets under a specified account.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-service)
```objective-c
// Specify the request method for a list of all buckets under an account
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result,
                          NSError* error) {
    
    // “result” returns a list of buckets
    NSArray<QCloudBucket*> *buckets = result.buckets;
    
    // Bucket owner
    QCloudOwner *owner = result.owner;
}];
[[QCloudCOSXMLService defaultCOSXML] GetService:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/GetService.m).

**Swift**

[//]: # (.cssg-snippet-get-service)
```swift
// Specify the request method for a list of all buckets under an account
let getServiceReq = QCloudGetServiceRequest.init();
getServiceReq.setFinish{(result,error) in
    if let result = result {
        let buckets = result.buckets
        let owner = result.owner
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getService(getServiceReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/GetService.swift).

## Creating a Bucket

#### API Description

This API is used to create a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket)
```objective-c
// Create a bucket
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // “outputObject” obtains headers returned by the browser
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PutBucket.m).

**Swift**

[//]: # (.cssg-snippet-put-bucket)
```swift
// Create a bucket
let putBucketReq = QCloudPutBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
putBucketReq.bucket = "examplebucket-1250000000";
putBucketReq.finishBlock = {(result,error) in
    // “result” obtains headers returned by the browser
    if error != nil {
        print(error!);
    } else {
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucket(putBucketReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PutBucket.swift).

## Checking a Bucket and Its Permissions

#### API Description

This API is used to check whether a bucket exists and whether you have the permission to access it. Possible scenarios are outlined below:

- If the bucket exists and you have permission to read it, HTTP status code 200 will be returned.
- If you do not have permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-head-bucket)
```objective-c
QCloudHeadBucketRequest* request = [QCloudHeadBucketRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // “outputObject” obtains headers returned by the browser
    NSDictionary * result = (NSDictionary *)outputObject;

}];
[[QCloudCOSXMLService defaultCOSXML] HeadBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/HeadBucket.m).


**Swift**

[//]: # (.cssg-snippet-head-bucket)
```swift
let headBucketReq = QCloudHeadBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
headBucketReq.bucket = "examplebucket-1250000000";

headBucketReq.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().headBucket(headBucketReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/HeadBucket.swift).


## Deleting a Bucket

#### API Description

This API is used to delete a specified bucket.

>! Before deleting a bucket, please make sure that all the data and incomplete multipart uploads in the bucket have been cleared; otherwise, the bucket cannot be deleted.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket)
```objective-c
QCloudDeleteBucketRequest* request = [[QCloudDeleteBucketRequest alloc ] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject,NSError*error) {
    // “outputObject” obtains headers returned by the browser
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteBucket.m).

**Swift**

[//]: # (.cssg-snippet-delete-bucket)
```swift
let deleteBucketReq = QCloudDeleteBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
deleteBucketReq.bucket = "examplebucket-1250000000";

deleteBucketReq.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteBucket(deleteBucketReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteBucket.swift).

