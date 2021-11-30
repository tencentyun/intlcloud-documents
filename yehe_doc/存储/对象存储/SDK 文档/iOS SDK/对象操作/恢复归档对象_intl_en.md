<!--
 * @Author: your name
 * @Date: 2020-12-07 10:53:33
 * @LastEditTime: 2021-06-08 09:25:29
 * @LastEditors: your name
 * @Description: In User Settings Edit

-->
## Overview

This document provides an overview of APIs and SDK code samples related to restoring an archived object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |

## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Restoring an Archived Object 

#### Description

This API (`POST Object restore`) is used to restore an archived object for access.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-restore-object)
```objective-c
QCloudPostObjectRestoreRequest *req = [QCloudPostObjectRestoreRequest new];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
req.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
req.object = @"exampleobject";

// Set the expiration time of the temporary copy.
req.restoreRequest.days = 10;

// Configuration of the restoration type
req.restoreRequest.CASJobParameters.tier = QCloudCASTierStandard;

[request setFinishBlock:^(id outputObject, NSError* error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PostObjectRestore:req];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/RestoreObject.m).

**Swift**

[//]: # (.cssg-snippet-restore-object)
```swift
let restore = QCloudPostObjectRestoreRequest.init();

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
restore.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
restore.object = "exampleobject";

// Set the expiration time of the temporary copy.
restore.restoreRequest.days = 10;

// Configuration of the restoration type
restore.restoreRequest.casJobParameters.tier = .standard;
restore.finishBlock = {(result,error)in
    if let result = result {
        // "result" contains response headers.
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().postObjectRestore(restore);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/RestoreObject.swift).

