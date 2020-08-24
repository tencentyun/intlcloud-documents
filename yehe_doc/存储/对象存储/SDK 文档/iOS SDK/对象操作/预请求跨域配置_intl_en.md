## Overview

This document provides an overview of APIs and SDK sample codes related to preflight requests for cross-origin access.

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring a preflight request for cross-origin access | Sends a preflight request to check whether a real cross-origin access request can be sent |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Configuring a Preflight Request for Cross-origin Access

#### Feature description
This API is used to get the cross-origin access configuration for a preflight request.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-option-object)
```objective-c
QCloudOptionsObjectRequest* request = [[QCloudOptionsObjectRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket =@"examplebucket-1250000000";

// Simulates the origin domain name from which the request for cross-origin access is sent
request.origin = @"http://cloud.tencent.com";
request.accessControlRequestMethod = @"GET";
request.accessControlRequestHeaders = @"host";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // outputObject returns information such as the Etag or custom headers
    NSDictionary* info = (NSDictionary *) outputObject;
    
}];

[[QCloudCOSXMLService defaultCOSXML] OptionsObject:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/BucketCORS.m).

**Swift**

[//]: # (.cssg-snippet-option-object)
```swift
let optionsObject = QCloudOptionsObjectRequest.init();

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
optionsObject.object = "exampleobject";

// Simulates the origin domain name from which the request for cross-origin access is sent
optionsObject.origin = "http://www.qcloud.com";
optionsObject.accessControlRequestMethod = "GET";
optionsObject.accessControlRequestHeaders = "origin";

// Bucket name in the format: `BucketName-APPID`
optionsObject.bucket = "examplebucket-1250000000";

optionsObject.finishBlock = {(result,error) in
    
    // `result` returns information such as the etag or custom headers in the response
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().optionsObject(optionsObject);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/BucketCORS.swift).

