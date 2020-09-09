## Overview

This document provides an overview of APIs and SDK code samples related to listing objects.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying a list of objects and their version history | Queries some or all objects in a bucket as well as their version history |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Querying an Object List

#### API description

This API is used to query some or all objects in a bucket.

#### Sample 1. Getting the first page of objects
**Objective-C**

[//]: # ".cssg-snippet-get-bucket"
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// The maximum number of objects returned at a time; the default value is 1,000
request.maxKeys = 100;

// Prefix to match, which is used to specify the URL prefix of returned objects
request.prefix = @"dir1/";

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    //“result” contains the request result
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    if (result.isTruncated) {
        // Indicate the listing is truncated, and you need to request subsequent pages
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjects.m).

**Swift**

[//]: # ".cssg-snippet-get-bucket"
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
getBucketReq.bucket = "examplebucket-1250000000";

// The maximum number of objects returned at a time; the default value is 1,000
getBucketReq.maxKeys = 100;

// Prefix to match
getBucketReq.prefix = "dir/";

getBucketReq.setFinish { (result, error) in
    if let result = result {
        // A list of objects
        let contents = result.contents
        
        if (result.isTruncated) {
            // Indicate the listing is truncated, and you need to request subsequent pages
            self.prevPageResult = result;
        }
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ListObjects.swift).

#### Sample 2. Requesting the next page of objects
**Objective-C**

[//]: # ".cssg-snippet-get-bucket-next-page"
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// `prevPageResult` contains the result returned on the previous page
// Specify pagination parameters. By default, objects are listed in UTF-8 binary order starting from the object after the marker
request.marker = prevPageResult.nextMarker;

// The maximum number of objects returned at a time; the default value is 1,000
request.maxKeys = 100;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    //“result” contains the request result
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    if (result.isTruncated) {
        // Indicate the listing is truncated, and you need to request subsequent pages
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjects.m).

**Swift**

[//]: # ".cssg-snippet-get-bucket-next-page"
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
getBucketReq.bucket = "examplebucket-1250000000";

// Specify pagination parameters. By default, objects are listed in UTF-8 binary order starting from the object after the marker
if let result = self.prevPageResult {
    getBucketReq.marker = result.marker
}

// The maximum number of objects returned at a time; the default value is 1,000
getBucketReq.maxKeys = 100;
// Prefix to match
getBucketReq.prefix = "dir/";

getBucketReq.setFinish { (result, error) in
    if let result = result {
        // A list of objects
        let contents = result.contents
        
        if (result.isTruncated) {
            // Indicate the listing is truncated, and you need to request subsequent pages
            self.prevPageResult = result;
        }
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ListObjects.swift).

#### Sample 3. Getting an object list and subdirectories
**Objective-C**

[//]: # ".cssg-snippet-get-bucket-with-delimiter"
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// The maximum number of objects returned at a time; the default value is 1,000
request.maxKeys = 100;

// Prefix to match, which is used to specify the URL prefix of returned objects
request.prefix = @"dir1/";

// “delimiter” is a symbol. If “prefix” is specified, identical paths between “prefix” and “delimiter” will be grouped together and
// defined as a “Common Prefix”. Then, all common prefixes are listed. If “prefix” is not specified, the listing starts from the beginning of the path
// delimiter: path separator, which is always `/`
request.delimiter = @"/";

// `prevPageResult` is the result returned on the previous page
// Specify pagination parameters. By default, objects are listed in UTF-8 binary order starting from the object after the marker
request.marker = prevPageResult.nextMarker;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    //“result” contains the request result
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    if (result.isTruncated) {
        // Indicate the listing is truncated, and you need to request subsequent pages
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjects.m).

**Swift**

[//]: # ".cssg-snippet-get-bucket-with-delimiter"
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// Bucket name in the format: `BucketName-APPID`
getBucketReq.bucket = "examplebucket-1250000000";

// The maximum number of objects returned at a time; the default value is 1,000
getBucketReq.maxKeys = 100;

// Prefix to match, which is used to specify the URL prefix of returned objects
getBucketReq.prefix = "dir/";

// “delimiter” is a symbol. If “prefix” is specified, identical paths between “prefix” and “delimiter” will be grouped together and
// defined as a “Common Prefix”. Then, all common prefixes are listed. If “prefix” is not specified, the listing starts from the beginning of the path
// delimiter: path separator, which is always `/`
getBucketReq.delimiter = "/";

// Specify pagination parameters. By default, objects are listed in UTF-8 binary order starting from the object after the marker
if let result = self.prevPageResult {
    getBucketReq.marker = result.marker
}

getBucketReq.setFinish { (result, error) in
    if let result = result {
        // A list of objects
        let contents = result.contents
        
        if (result.isTruncated) {
            // Indicate the listing is truncated, and you need to request subsequent pages
            self.prevPageResult = result;
        }
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ListObjects.swift).

## Querying an Object Version List

#### API description 

This API is used to query some or all objects in a versioning-enabled bucket.

#### Sample. Getting the first page of object versions

[//]: # ".cssg-snippet-list-objects-versioning"
```objective-c
QCloudListObjectVersionsRequest* listObjectVersionsRequest = [[QCloudListObjectVersionsRequest alloc] init];

// Bucket name
listObjectVersionsRequest.bucket = @"bucketname";

// Maximum number of entries returned per page. Default value: 1000
listObjectVersionsRequest.maxKeys = 100;

// Specify the key after which remaining entries are to be listed
listObjectVersionsRequest.keyMarker = prevPageResult.nextKeyMarker;
// Specify the version ID after which remaining entries are to be listed
listObjectVersionsRequest.versionIdMarker = prevPageResult.nextVersionIDMarkder;
[listObjectVersionsRequest setFinishBlock:^(QCloudListVersionsResult * _Nonnull result,
                                            NSError * _Nonnull error) {
    
    // Deleted objects
    NSArray<QCloudDeleteMarker*> *deleteMarker = result.deleteMarker;
    
    // List object versions
    NSArray<QCloudVersionContent*> *versionContent = result.versionContent;
    
    if (result.isTruncated) {
        // Indicate the listing is truncated, and you need to request subsequent pages
        self->prevPageResult = result;
    }

    
}];

[[QCloudCOSXMLService defaultCOSXML] ListObjectVersions:listObjectVersionsRequest];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjectsVersioning.m).

