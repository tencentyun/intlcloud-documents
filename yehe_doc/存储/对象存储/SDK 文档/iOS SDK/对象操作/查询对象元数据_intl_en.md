## Overview

This document provides an overview of APIs and SDK code samples related to querying object metadata.

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Querying Object Metadata

#### Feature description

This API is used to query the metadata of an object.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-head-object"
```objective-c
QCloudHeadObjectRequest* headerRequest = [QCloudHeadObjectRequest new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
headerRequest.object = @"exampleobject";

// Specify the `versionId` of the object if versioning is enabled; if this parameter is not specified, the latest version will be queried
headerRequest.versionID = @"versionID";

// Bucket name in the format: `BucketName-APPID`
headerRequest.bucket = @"examplebucket-1250000000";

[headerRequest setFinishBlock:^(NSDictionary* result, NSError *error) {
    // `result` contains the request result

}];

[[QCloudCOSXMLService defaultCOSXML] HeadObject:headerRequest];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/HeadObject.m).

**Swift**

[//]: # ".cssg-snippet-head-object"
```swift
let headObject = QCloudHeadObjectRequest.init();

// Bucket name in the format: `BucketName-APPID`
headObject.bucket = "examplebucket-1250000000";

// Specify the `versionId` of the object if versioning is enabled; if this parameter is not specified, the latest version will be queried
headObject.versionID = "versionID";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
headObject.object  = "exampleobject";
headObject.finishBlock =  {(result,error) in
    if let result = result {
        // "result" contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().headObject(headObject);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/HeadObject.swift).

