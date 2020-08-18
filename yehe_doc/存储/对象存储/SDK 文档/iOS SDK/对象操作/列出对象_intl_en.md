## Overview

This document provides an overview of APIs and SDK code samples related to listing objects.

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://cloud.tencent.com/document/product/436/35521) | Querying a list of objects and their version history | Queries some or all objects in a bucket and their version history |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Querying an Object List

#### Feature description

This API is used to query some or all objects in a bucket.

#### Sample 1. Getting the first page of data
**Objective-C**

[//]: # (.cssg-snippet-get-bucket)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Maximum number of entries returned at a time. Default value: 1,000
request.maxKeys = 100;

// Prefix match, which is used to specify the address prefix of the returned files
request.prefix = @"dir1/";

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // `result` contains the request result
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    if (result.isTruncated) {
        // The data is truncated, and the next page of data needs to be pulled
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/ListObjects.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket)
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
getBucketReq.bucket = "examplebucket-1250000000";

// Maximum number of entries returned at a time. Default value: 1,000
getBucketReq.maxKeys = 100;

// Prefix match
getBucketReq.prefix = "dir/";

getBucketReq.setFinish { (result, error) in
    // `result` contains the request result
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    
    if error != nil{
        print(error!);
    } else if let isTruncated = result?.isTruncated {
        if (isTruncated) {
            // The data is truncated, and the next page of data needs to be requested
            self.prevPageResult = result;
        }
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/ListObjects.swift).

#### Sample 2. Requesting the next page of data
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-next-page)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// `prevPageResult` is the result returned on the previous page
// Paging parameter. By default, entries are listed in UTF-8 binary order starting with the marker
request.marker = prevPageResult.nextMarker;

// Maximum number of entries returned at a time. Default value: 1,000
request.maxKeys = 100;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // `result` contains the request result
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    if (result.isTruncated) {
        // The data is truncated, and the next page of data needs to be pulled
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/ListObjects.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-next-page)
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
getBucketReq.bucket = "examplebucket-1250000000";

// Paging parameter. By default, entries are listed in UTF-8 binary order starting with the marker
if let result = self.prevPageResult {
    getBucketReq.marker = result.marker
}

// Maximum number of entries returned at a time. Default value: 1,000
getBucketReq.maxKeys = 100;
// Prefix match
getBucketReq.prefix = "dir/";

getBucketReq.setFinish { (result, error) in
    // `result` contains the request result
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    
    if error != nil{
        print(error!);
    } else if let isTruncated = result?.isTruncated {
        if (isTruncated) {
            // The data is truncated, and the next page of data needs to be requested
            self.prevPageResult = result;
        }
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/ListObjects.swift).

#### Sample 3. Getting an object list and subdirectories
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Maximum number of entries returned at a time. Default value: 1,000
request.maxKeys = 100;

// Prefix match, which is used to specify the address prefix of the returned files
request.prefix = @"dir1/";

// The delimiter is a symbol. If the prefix exists, identical paths between the prefix and delimiter will be grouped together and
// defined as a common prefix, and then all common prefixes will be listed; otherwise, the listing will start from the beginning of the path
// delimiter: path separator, which is always `/`
request.delimiter = @"/";

// `prevPageResult` is the result returned on the previous page
// Paging parameter. By default, entries are listed in UTF-8 binary order starting with the marker
request.marker = prevPageResult.nextMarker;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // `result` contains the request result
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    if (result.isTruncated) {
        // The data is truncated, and the next page of data needs to be pulled
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/ListObjects.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
getBucketReq.bucket = "examplebucket-1250000000";

// Maximum number of entries returned at a time. Default value: 1,000
getBucketReq.maxKeys = 100;

// Prefix match, which is used to specify the address prefix of the returned files
getBucketReq.prefix = "dir/";

// The delimiter is a symbol. If the prefix exists, identical paths between the prefix and delimiter will be grouped together and
// defined as a common prefix, and then all common prefixes will be listed; otherwise, the listing will start from the beginning of the path
// delimiter: path separator, which is always `/`
getBucketReq.delimiter = "/";

// Paging parameter. By default, entries are listed in UTF-8 binary order starting with the marker
if let result = self.prevPageResult {
    getBucketReq.marker = result.marker
}

getBucketReq.setFinish { (result, error) in
    // `result` contains the request result
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    
    if error != nil{
        print(error!);
    } else if let isTruncated = result?.isTruncated {
        if (isTruncated) {
            // The data is truncated, and the next page of data needs to be requested
            self.prevPageResult = result;
        }
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/ListObjects.swift).

## Querying an Object Version List

#### Feature description

This API is used to query some or all objects in a versioning-enabled bucket.

#### Sample. Getting the object version list’s first page of data
**Objective-C**

[//]: # (.cssg-snippet-list-objects-versioning)
```objective-c
QCloudListObjectVersionsRequest* listObjectVersionsRequest = [[QCloudListObjectVersionsRequest alloc] init];

// Bucket name
listObjectVersionsRequest.bucket = @"bucketname";

// Number of requested data entries per page. Default value: 1000.
listObjectVersionsRequest.maxKeys = 100;

// Total number of entries that have been requested
listObjectVersionsRequest.marker = prevPageResult.versionIDMarkder;

[listObjectVersionsRequest setFinishBlock:^(QCloudListVersionsResult * _Nonnull result,
                                            NSError * _Nonnull error) {
    
    // Deleted files
    NSArray<QCloudDeleteMarker*> *deleteMarker = result.deleteMarker;
    
    // Number of object version entries
    NSArray<QCloudVersionContent*> *versionContent = result.versionContent;
    
    if (result.isTruncated) {
        // The data is truncated, and the next page of data needs to be pulled
        self->prevPageResult = result;
    }

    
}];

[[QCloudCOSXMLService defaultCOSXML] ListObjectVersions:listObjectVersionsRequest];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/ListObjectsVersioning.m).

**Swift**

[//]: # (.cssg-snippet-list-objects-versioning)
```swift
let listObjectVersionsRequest :QCloudListObjectVersionsRequest = QCloudListObjectVersionsRequest();

// Bucket name in the format: `BucketName-APPID`
listObjectVersionsRequest.bucket = "examplebucket-1250000000";

// Number of data entries requested at a time
listObjectVersionsRequest.maxKeys = 100;

listObjectVersionsRequest.setFinish { (result, error) in
    
    // result.deleteMarker; // Deleted file
    // result.versionContent;   Number of object version entries
}

QCloudCOSXMLService.defaultCOSXML().listObjectVersions(listObjectVersionsRequest);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/ListObjectsVersioning.swift).

