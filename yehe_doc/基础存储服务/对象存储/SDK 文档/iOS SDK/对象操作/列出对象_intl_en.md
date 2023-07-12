## Overview

This document provides an overview of APIs and SDK code samples for listing objects.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | Querying objects and their version history | Queries some or all the objects in a bucket and their version history. |

## SDK API References

For parameters and method description of all APIs in the SDK, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Querying an Object List

#### Feature description

This API is used to query some or all the objects in a bucket.

#### Sample 1. Getting the first page of data
**Objective-C**

[//]: # (.cssg-snippet-get-bucket)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// Maximum number of objects to return at a time. Default value: 1000
request.maxKeys = 100;

// Prefix match, which is used to specify the address prefix of the returned files
request.prefix = @"dir1/";

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // result contains the request result
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    if (result.isTruncated) {
        // The data is truncated, and the next page of data needs to be pulled
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjects.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket)
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";

// Maximum number of objects to return at a time. Default value: 1000
getBucketReq.maxKeys = 100;

// Prefix match
getBucketReq.prefix = "dir/";

getBucketReq.setFinish { (result, error) in
    if let result = result {
        // Object list
        let contents = result.contents
        
        if (result.isTruncated) {
            // The data is truncated, and the next page of data needs to be requested
            self.prevPageResult = result;
        }
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ListObjects.swift).

#### Sample 2. Requesting the next page of data
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-next-page)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// prevPageResult is the result returned on the previous page
// Paging parameter. By default, entries are listed in UTF-8 binary order starting with the marker
request.marker = prevPageResult.nextMarker;

// Maximum number of objects to return at a time. Default value: 1000
request.maxKeys = 100;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // result contains the request result.
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    if (result.isTruncated) {
        // The data is truncated, and the next page of data needs to be pulled
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjects.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-next-page)
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";

// Paging parameter. By default, entries are listed in UTF-8 binary order starting with the marker
if let result = self.prevPageResult {
    getBucketReq.marker = result.marker
}

// Maximum number of objects to return at a time. Default value: 1000
getBucketReq.maxKeys = 100;
// Prefix match
getBucketReq.prefix = "dir/";

getBucketReq.setFinish { (result, error) in
    if let result = result {
        // Object list
        let contents = result.contents
        
        if (result.isTruncated) {
            // The data is truncated, and the next page of data needs to be requested
            self.prevPageResult = result;
        }
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ListObjects.swift).

#### Sample 3. Getting an object list and subdirectories
**Objective-C**

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// Maximum number of objects to return at a time. Default value: 1000
request.maxKeys = 100;

// Prefix match, which is used to specify the address prefix of the returned files
request.prefix = @"dir1/";

// The delimiter is a symbol. If the Prefix exists, identical paths between the Prefix and delimiter will be grouped together, 
// which is defined as Common Prefix. Then, all common prefixes are listed. If there is no Prefix, the listing starts from the beginning of the path.
// delimiter: path separator, which is fixed to `/`
request.delimiter = @"/";

// prevPageResult is the result returned on the previous page.
// Paging parameter. By default, entries are listed in UTF-8 binary order starting with the marker
request.marker = prevPageResult.nextMarker;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // result contains the request result
    // `QCloudListBucketResult.contents` is the array of files in the bucket
    // `QCloudListBucketResult.commonPrefixes` is the array of folders in the bucket
    if (result.isTruncated) {
        // The data is truncated, and the next page of data needs to be pulled.
        self->prevPageResult = result;
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjects.m).

**Swift**

[//]: # (.cssg-snippet-get-bucket-with-delimiter)
```swift
let getBucketReq = QCloudGetBucketRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";

// Maximum number of objects to return at a time. Default value: 1000
getBucketReq.maxKeys = 100;

// Prefix match, which is used to specify the address prefix of the returned files
getBucketReq.prefix = "dir/";

// The delimiter is a symbol. If the Prefix exists, identical paths between the Prefix and delimiter will be grouped together, 
// which is defined as Common Prefix. Then, all common prefixes are listed. If there is no Prefix, the listing starts from the beginning of the path.
// delimiter: path separator, which is always `/`
getBucketReq.delimiter = "/";

// Paging parameter. By default, entries are listed in UTF-8 binary order starting with the marker
if let result = self.prevPageResult {
    getBucketReq.marker = result.marker
}

getBucketReq.setFinish { (result, error) in
    if let result = result {
        // Object list
        let contents = result.contents
        
        if (result.isTruncated) {
            // The data is truncated, and the next page of data needs to be requested
            self.prevPageResult = result;
        }
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ListObjects.swift).

## Querying an Object Version List

#### Feature description

This API is used to query some or all objects in a versioning-enabled bucket.

#### Sample code: Getting the first page of data from an object version

[//]: # (.cssg-snippet-list-objects-versioning)
```objective-c
QCloudListObjectVersionsRequest* listObjectVersionsRequest = [[QCloudListObjectVersionsRequest alloc] init];

// Bucket Name
listObjectVersionsRequest.bucket = @"bucketname";

// Number of requested data entries per page. Default value: 1000.
listObjectVersionsRequest.maxKeys = 100;

// List the unrequested entries from the current key
listObjectVersionsRequest.keyMarker = prevPageResult.nextKeyMarker;
// List the unrequested entries from an object version in the current key
listObjectVersionsRequest.versionIdMarker = prevPageResult.nextVersionIDMarkder;
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjectsVersioning.m).

