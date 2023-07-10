<!--
 * @Author: your name
 * @Date: 2020-12-07 10:53:33
 * @LastEditTime: 2021-06-08 09:27:54
 * @LastEditors: your name
 * @Description: In User Settings Edit
-->
## Overview

This document provides an overview of APIs and SDK code samples related to CORS preflight requests.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring a preflight request for cross-origin access | Sends a preflight request to check whether a real cross-origin access request can be sent |

## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Configuring a Preflight Request for Cross-origin Access

#### Description
This API is used to get the cross-origin access configuration for a preflight request.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-option-object)
```objective-c
QCloudOptionsObjectRequest* request = [[QCloudOptionsObjectRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket =@"examplebucket-1250000000";

// Set the origin domain, request method, and host for the CORS pre-flight request.
request.origin = @"http://cloud.tencent.com";
request.accessControlRequestMethod = @"GET";
request.accessControlRequestHeaders = @"host";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // outputObject contains information such as the ETag or custom headers in the response.
    NSDictionary* info = (NSDictionary *) outputObject;
    
}];

[[QCloudCOSXMLService defaultCOSXML] OptionsObject:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m).

**Swift**

[//]: # (.cssg-snippet-option-object)
```swift
let optionsObject = QCloudOptionsObjectRequest.init();

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
optionsObject.object = "exampleobject";

// Set the origin domain, request method, and headers for the CORS pre-flight request.
optionsObject.origin = "http://www.qcloud.com";
optionsObject.accessControlRequestMethod = "GET";
optionsObject.accessControlRequestHeaders = "origin";

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
optionsObject.bucket = "examplebucket-1250000000";

optionsObject.finishBlock = {(result,error) in
    if let result = result {
        // You can get the header information returned by the server from `result`
    }
}
QCloudCOSXMLService.defaultCOSXML().optionsObject(optionsObject);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift).

