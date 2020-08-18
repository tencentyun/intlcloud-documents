## Overview

This document provides an overview of APIs and SDK code samples related to restoring an archived object.

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores archived object for access |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Restoring an Archived Object 

#### Feature description

This API is used to retrieve an archived object for access.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-restore-object)
```objective-c
QCloudPostObjectRestoreRequest *req = [QCloudPostObjectRestoreRequest new];

// Bucket name in the format: `BucketName-APPID`
req.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
req.object = @"exampleobject";

// Set the expiration time of the temporary copy
req.restoreRequest.days  = 10;

// Configuration of the restoration type
req.restoreRequest.CASJobParameters.tier =QCloudCASTierStandard;

[req setFinishBlock:^(id outputObject, NSError *error) {
    
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
    
}];

[[QCloudCOSXMLService defaultCOSXML] PostObjectRestore:req];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/RestoreObject.m).

**Swift**

[//]: # (.cssg-snippet-restore-object)
```swift
let restore = QCloudPostObjectRestoreRequest.init();

// Bucket name in the format: `BucketName-APPID`
restore.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
restore.object = "exampleobject";

// Set the expiration time of the temporary copy
restore.restoreRequest.days = 10;

// Configuration of the restoration type
restore.restoreRequest.casJobParameters.tier = .standard;
restore.finishBlock = {(result,error)in
    if error != nil{
        print(error!)
    }else{
        // `result` returns information such as the etag or custom headers in the response
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().postObjectRestore(restore);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/RestoreObject.swift).

