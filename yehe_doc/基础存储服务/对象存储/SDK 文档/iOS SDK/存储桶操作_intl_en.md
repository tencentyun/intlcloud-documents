## Overview

This document provides an overview of APIs and SDK code samples for basic bucket operations.


| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and whether you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket from a specified account |

## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Querying a Bucket List

#### Feature description

This API (GET Service (List Buckets)) is used to query the list of all buckets under a specified account.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-get-service)
```objective-c
// Method for getting the list of all storage spaces under an account
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result,
                          NSError* error) {
    
    //Get the returned information from result
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
// Method for getting the list of all storage spaces under an account
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

#### Feature description

This API (`PUT Bucket`) is used to create a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-bucket)
```objective-c
// Create a bucket
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];

// Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
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

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
putBucketReq.bucket = "examplebucket-1250000000";
putBucketReq.finishBlock = {(result,error) in
    // You can get the header information returned by the server from result
    if error != nil {
        print(error!);
    } else {
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucket(putBucketReq);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PutBucket.swift).

## Checking a Bucket and Its Permissions

#### Feature description

This API is used to check whether a bucket exists and whether you have permission to access it.

- If the bucket exists and you have permission to read it, HTTP status code 200 will be returned.
- If you do not have permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-head-bucket)
```objective-c
QCloudHeadBucketRequest* request = [QCloudHeadBucketRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the header information returned by the server from outputObject
    NSDictionary * result = (NSDictionary *)outputObject;

}];
[[QCloudCOSXMLService defaultCOSXML] HeadBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/HeadBucket.m).


**Swift**

[//]: # (.cssg-snippet-head-bucket)
```swift
let headBucketReq = QCloudHeadBucketRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
headBucketReq.bucket = "examplebucket-1250000000";

headBucketReq.finishBlock = {(result,error) in
    if let result = result {
        // result contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().headBucket(headBucketReq);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/HeadBucket.swift).

## Checking whether a bucket exists

#### Feature description

You can check whether a bucket exists by using the shortcut API provided by the SDK.


#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-head-bucket)
```objective-c
  // Bucket name in the format of BucketName-APPID
  [[QCloudCOSXMLService defaultCOSXML] doesBucketExist: @"examplebucket-1250000000"];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/HeadBucket.m).


**Swift**

[//]: # (.cssg-snippet-head-bucket)
```swift
     // Bucket name in the format of BucketName-APPID
   QCloudCOSXMLService.defaultCOSXML().doesBucketExist("examplebucket-1250000000");
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/HeadBucket.swift).


## Deleting a Bucket

#### Feature description

This API is used to delete a specified bucket.

>! Before deleting a bucket, please make sure that all the data and incomplete multipart uploads in the bucket have been deleted; otherwise, the bucket cannot be deleted.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-bucket)
```objective-c
QCloudDeleteBucketRequest* request = [[QCloudDeleteBucketRequest alloc ] init];

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject,NSError*error) {
    // You can get the header information returned by the server from outputObject
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteBucket.m).

**Swift**

[//]: # (.cssg-snippet-delete-bucket)
```swift
let deleteBucketReq = QCloudDeleteBucketRequest.init();

// Bucket name in the format of BucketName-APPID
deleteBucketReq.bucket = "examplebucket-1250000000";

deleteBucketReq.finishBlock = {(result,error) in
    if let result = result {
        // result contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteBucket(deleteBucketReq);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteBucket.swift).

