## Overview

This document provides an overview of APIs and SDK code samples related to basic bucket operations.


| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under a specified account |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Querying a Bucket List

#### Feature description

This API is used to query the list of all buckets under a specified account.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-get-service"
```objective-c
// Method for getting the list of all storage spaces under an account
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result,
                          NSError* error) {
    
    // Get the returned information (bucket list) from `result`
    NSArray<QCloudBucket*> *buckets = result.buckets;
    
    // Bucket owner
    QCloudOwner *owner = result.owner;
}];
[[QCloudCOSXMLService defaultCOSXML] GetService:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/GetService.m).

**Swift**

[//]: # ".cssg-snippet-get-service"
```swift
// Method for getting the list of all storage spaces under an account
let getServiceReq = QCloudGetServiceRequest.init();
getServiceReq.setFinish{(result,error) in
    if result == nil {
        print(error!);
    } else {
        
        // Get the returned information from `result`
        // result?.owner ;  bucket owner
        // result?.buckets; bucket list
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getService(getServiceReq);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/GetService.swift).

## Creating a Bucket

#### Feature description

This API is used to create a bucket.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-put-bucket"
```objective-c
// Create a bucket
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the headers returned by the server from outputObject
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucket:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/PutBucket.m).

**Swift**

[//]: # ".cssg-snippet-put-bucket"
```swift
// Create a bucket
let putBucketReq = QCloudPutBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
putBucketReq.bucket = "examplebucket-1250000000";
putBucketReq.finishBlock = {(result,error) in
    // You can get the header information returned by the server from `result`
    if error != nil {
        print(error!);
    } else {
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putBucket(putBucketReq);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/PutBucket.swift).

## Checking a Bucket and Its Permissions

#### Feature description

This API is used to check whether a bucket exists and whether you have the permission to access it. Possible scenarios are outlined below:

- If the bucket exists and you have the permission to read it, HTTP status code 200 will be returned.
- If you do not have the permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-head-bucket"
```objective-c
QCloudHeadBucketRequest* request = [QCloudHeadBucketRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get the headers returned by the server from outputObject
    NSDictionary * result = (NSDictionary *)outputObject;

    
    // x-cos-bucket-region: bucket region. For the enumerated values, please see Regions and Access Domain Names
    // Examples: ap-beijing, ap-hongkong, eu-frankfurt

}];
[[QCloudCOSXMLService defaultCOSXML] HeadBucket:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/HeadBucket.m).


**Swift**

[//]: # ".cssg-snippet-head-bucket"
```swift
let headBucketReq = QCloudHeadBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
headBucketReq.bucket = "examplebucket-1250000000";

headBucketReq.finishBlock = {(result,error) in
    
    // You can get the header information returned by the server from `result`
    if error != nil{
        print(error!);
    }else{
        print( result!);
    }

    
    // x-cos-bucket-region: bucket region. For the enumerated values, please see Regions and Access Domain Names
    // Examples: ap-beijing, ap-hongkong, eu-frankfurt
}
QCloudCOSXMLService.defaultCOSXML().headBucket(headBucketReq);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/HeadBucket.swift).


## Deleting a Bucket

#### Feature description

This API is used to delete a specified bucket.

>! Before deleting a bucket, please make sure that all the data and incomplete multipart uploads in the bucket have been deleted; otherwise, the bucket cannot be deleted.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-delete-bucket"
```objective-c
QCloudDeleteBucketRequest* request = [[QCloudDeleteBucketRequest alloc ] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject,NSError*error) {
    
    // You can get the headers returned by the server from outputObject
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucket:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/DeleteBucket.m).

**Swift**

[//]: # ".cssg-snippet-delete-bucket"
```swift
let deleteBucketReq = QCloudDeleteBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
deleteBucketReq.bucket = "examplebucket-1250000000";

deleteBucketReq.finishBlock = {(result,error) in
    // You can get the header information returned by the server from `result`
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteBucket(deleteBucketReq);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/DeleteBucket.swift).