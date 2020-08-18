## Overview

This document provides an overview of APIs and SDK code samples related to object deletion.

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Object](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Deleting a Single Object

#### Feature description

This API is used to delete a specified object from a bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-object)
```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];

// Bucket name in the format: `BucketName-APPID`
deleteObjectRequest.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
deleteObjectRequest.object = @"exampleobject";

[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/DeleteObject.m).

**Swift**

[//]: # (.cssg-snippet-delete-object)
```swift
let deleteObject = QCloudDeleteObjectRequest.init();

// Bucket name in the format: `BucketName-APPID`
deleteObject.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
deleteObject.object = "exampleobject";

deleteObject.finishBlock = {(result,error)in
    // `result` returns information such as the etag or custom headers in the response
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteObject(deleteObject);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/DeleteObject.swift).

## Deleting Multiple Objects

#### Feature description

This API is used to delete multiple objects in a single request.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-delete-multi-object)
```objective-c
QCloudDeleteMultipleObjectRequest* delteRequest = [QCloudDeleteMultipleObjectRequest new];
delteRequest.bucket = @"examplebucket-1250000000";

// Single file to be deleted
QCloudDeleteObjectInfo* deletedObject0 = [QCloudDeleteObjectInfo new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
deletedObject0.key = @"exampleobject";

// File set to be deleted
QCloudDeleteInfo* deleteInfo = [QCloudDeleteInfo new];

// Boolean value; Determines whether to enable `Quiet` mode:
// true: enables `Quiet` mode
// false: enables `Verbose` mode
// Default value: false
deleteInfo.quiet = NO;

// The array that stores the information on the objects to be deleted
deleteInfo.objects = @[deletedObject0];

// Encapsulates the information on the multiple objects to be deleted in batches
delteRequest.deleteObjects = deleteInfo;

[delteRequest setFinishBlock:^(QCloudDeleteResult* outputObject,
                               NSError *error) {
    // outputObject returns information such as the Etag or custom headers in the response 
    
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/DeleteObject.m).

**Swift**

[//]: # (.cssg-snippet-delete-multi-object)
```swift
let mutipleDel = QCloudDeleteMultipleObjectRequest.init();

// Bucket name in the format: `BucketName-APPID`
mutipleDel.bucket = "examplebucket-1250000000";

// Single file to be deleted
let info1 = QCloudDeleteObjectInfo.init();

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
info1.key = "exampleobject";

let info2 = QCloudDeleteObjectInfo.init();

// File set to be deleted
let deleteInfos = QCloudDeleteInfo.init();

// The array that stores the information on the objects to be deleted
deleteInfos.objects = [info1,info2];

// Boolean value; Determines whether to enable `Quiet` mode:
// true: enables `Quiet` mode
// false: enables `Verbose` mode
// Default value: false
deleteInfos.quiet = false;

// Encapsulates the information on the multiple objects to be deleted in batches
mutipleDel.deleteObjects = deleteInfos;

mutipleDel.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteMultipleObject(mutipleDel);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/DeleteObject.swift).

