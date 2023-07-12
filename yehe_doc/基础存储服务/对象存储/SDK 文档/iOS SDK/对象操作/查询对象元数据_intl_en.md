## Overview

This document provides an overview of APIs and SDK code samples related to querying object metadata.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |

## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Querying Object Metadata

#### Description

This API is used to query the metadata of an object.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-head-object)
```objective-c
QCloudHeadObjectRequest* headerRequest = [QCloudHeadObjectRequest new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
headerRequest.object = @"exampleobject";

// versionId specifies the version ID of an object to query (if versioning is enabled). If versionId is not specified, the latest version will be queried.
headerRequest.versionID = @"versionID";

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
headerRequest.bucket = @"examplebucket-1250000000";

[headerRequest setFinishBlock:^(NSDictionary* result, NSError *error) {
    // "result" contains the request result.
    // Obtain the CRC64 value of the object.
     NSString * crc64 = [[outputObject __originHTTPURLResponse__].allHeaderFields valueForKey:@"x-cos-hash-crc64ecma"];
}];

[[QCloudCOSXMLService defaultCOSXML] HeadObject:headerRequest];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/HeadObject.m).

**Swift**

[//]: # (.cssg-snippet-head-object) 
```swift
let headObject = QCloudHeadObjectRequest.init();

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
headObject.bucket = "examplebucket-1250000000";

// versionId specifies the version ID of an object to query (if versioning is enabled). If versionId is not specified, the latest version will be queried.
headObject.versionID = "versionID";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
headObject.object  = "exampleobject";
headObject.finishBlock =  {(result,error) in
    if let result = result {
        // Obtain the CRC64 value of the object.
        let crc64 = result?.__originHTTPURLResponse__.allHeaderFields["x-cos-hash-crc64ecma"];
       
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().headObject(headObject);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/HeadObject.swift).

