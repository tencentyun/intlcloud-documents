## Overview

This document provides an overview of APIs and SDK code samples related to object deletion.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes an object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Deleting an Object

#### Description

This API (`DELETE Object`) is used to delete a specified object.

#### Sample code 1: deleting a single object
**Objective-C**

[//]: # (.cssg-snippet-delete-object)
```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
deleteObjectRequest.bucket = @"examplebucket-1250000000";


// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
deleteObjectRequest.object = @"exampleobject";

[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m).

**Swift**

[//]: # (.cssg-snippet-delete-object)
```swift
let deleteObject = QCloudDeleteObjectRequest.init();

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
deleteObject.bucket = "examplebucket-1250000000";


// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
deleteObject.object = "exampleobject";

deleteObject.finishBlock = {(result,error)in
    if let result = result {
        // "result" contains response headers.
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteObject(deleteObject);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift).


#### Sample code 2: deleting an object
**Objective-C**

[//]: # (.cssg-snippet-delete-dir)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// Maximum number of objects to return at a time. Default value: 1000
request.maxKeys = 100;

// Name of the directory to delete, prefixed with a slash (/)
request.prefix = @"prefix";

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    if(!error){
        NSMutableArray *deleteInfosArr = [NSMutableArray array];
        for (QCloudBucketContents *content in result.contents) {
            QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
            delteRequest.bucket = request.bucket;

            QCloudDeleteObjectInfo *object = [QCloudDeleteObjectInfo new];
            object.key = content.key;
            [deleteInfosArr addObject:object];
        }
            
        QCloudDeleteInfo *deleteInfos = [QCloudDeleteInfo new];
        deleteInfos.objects = [deleteInfosArr copy];
          
        QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
        delteRequest.bucket = @"examplebucket-1250000000";
        delteRequest.deleteObjects = deleteInfos;
        [delteRequest setFinishBlock:^(QCloudDeleteResult *outputObject, NSError *error) {
            NSLog(@"outputObject = %@",outputObject);
        }];

        [[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];
            
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m).

**Swift**

[//]: # (.cssg-snippet-delete-dir)
```swift
let getBucketReq = QCloudGetBucketRequest.init();
        
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";
        
// Maximum number of objects to return at a time. Default value: 1000
getBucketReq.maxKeys = 100;
        
// Name of the directory to delete, prefixed with a slash (/)
getBucketReq.prefix = "dir/";
        
getBucketReq.setFinish { (result, error) in
    if let result = result {
        let contents = result.contents;
        let infos = NSMutableArray.init();
        for content in contents {
            let info = QCloudDeleteObjectInfo.init();
            info.key = content.key;
            infos.add(info);
        }
        let mutipleDel = QCloudDeleteMultipleObjectRequest.init();
        // File set to be deleted
        let deleteInfos = QCloudDeleteInfo.init();
        // Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        mutipleDel.bucket = "examplebucket-1250000000";
                
        deleteInfos.objects = infos as! [QCloudDeleteObjectInfo];
                
        // Boolean value. Determines whether to enable the `Quiet` mode:
        // true: enable the `Quiet` mode
        // false: enable the `Verbose` mode
        // Default value: false
        deleteInfos.quiet = false;
                
        // Encapsulates the information on the multiple objects to be deleted in batches
        mutipleDel.deleteObjects = deleteInfos;
                
        mutipleDel.setFinish { (result, error) in
            if let result = result {
                let deleted = result.deletedObjects
                let failed = result.deletedFailedObjects
            } else {
                print(error!);
            }
        }
        QCloudCOSXMLService.defaultCOSXML().deleteMultipleObject(mutipleDel);
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift).

## Deleting Multiple Objects

#### Description

The API (DELETE Multiple Objects) is used to delete multiple objects.

#### Sample code 1: deleting multiple objects

**Objective-C**

[//]: # (.cssg-snippet-delete-multi-object)
```objective-c
QCloudDeleteMultipleObjectRequest* delteRequest = [QCloudDeleteMultipleObjectRequest new];
delteRequest.bucket = @"examplebucket-1250000000";

// Single file to be deleted
QCloudDeleteObjectInfo* deletedObject0 = [QCloudDeleteObjectInfo new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
deletedObject0.key = @"exampleobject";

// File set to be deleted
QCloudDeleteInfo* deleteInfo = [QCloudDeleteInfo new];

// Boolean value. Determines whether to enable the `Quiet` mode:
// true: enable the `Quiet` mode
// false: enable the `Verbose` mode
// Default value: false
deleteInfo.quiet = NO;

// Array that stores the information on the objects to be deleted
deleteInfo.objects = @[deletedObject0];

// Encapsulates the information on the multiple objects to be deleted in batches
delteRequest.deleteObjects = deleteInfo;

[delteRequest setFinishBlock:^(QCloudDeleteResult* outputObject,
                               NSError *error) {
    // outputObject contains information such as the ETag or custom headers in the response.
    
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m).

**Swift**

[//]: # (.cssg-snippet-delete-multi-object)
```swift
let mutipleDel = QCloudDeleteMultipleObjectRequest.init();

// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
mutipleDel.bucket = "examplebucket-1250000000";

// Single file to be deleted
let info1 = QCloudDeleteObjectInfo.init();

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
info1.key = "exampleobject";

let info2 = QCloudDeleteObjectInfo.init();

// File set to be deleted
let deleteInfos = QCloudDeleteInfo.init();

// Array that stores the information on the objects to be deleted
deleteInfos.objects = [info1,info2];

// Boolean value. Determines whether to enable the `Quiet` mode:
// true: enable the `Quiet` mode
// false: enable the `Verbose` mode
// Default value: false
deleteInfos.quiet = false;

// Encapsulates the information on the multiple objects to be deleted in batches
mutipleDel.deleteObjects = deleteInfos;

mutipleDel.setFinish { (result, error) in
    if let result = result {
        let deleted = result.deletedObjects
        let failed = result.deletedFailedObjects
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().deleteMultipleObject(mutipleDel);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift).

#### Sample code 2: deleting objects with a specified prefix
**Objective-C**

[//]: # (.cssg-snippet-delete-dir)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// Maximum number of objects to return at a time. Default value: 1000
request.maxKeys = 100;

//To delete files with a specified prefix, `prefix` should be the prefix of the files to delete
request.prefix = @"prefix";

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    if(!error){
        NSMutableArray *deleteInfosArr = [NSMutableArray array];
        for (QCloudBucketContents *content in result.contents) {
            QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
            delteRequest.bucket = request.bucket;

            QCloudDeleteObjectInfo *object = [QCloudDeleteObjectInfo new];
            object.key = content.key;
            [deleteInfosArr addObject:object];
        }
            
        QCloudDeleteInfo *deleteInfos = [QCloudDeleteInfo new];
        deleteInfos.objects = [deleteInfosArr copy];
          
        QCloudDeleteMultipleObjectRequest *delteRequest = [QCloudDeleteMultipleObjectRequest new];
        delteRequest.bucket = @"examplebucket-1250000000";
        delteRequest.deleteObjects = deleteInfos;
        [delteRequest setFinishBlock:^(QCloudDeleteResult *outputObject, NSError *error) {
            NSLog(@"outputObject = %@",outputObject);
        }];

        [[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];
            
    }
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DeleteObject.m).

**Swift**

[//]: # (.cssg-snippet-delete-dir)
```swift
let getBucketReq = QCloudGetBucketRequest.init();
        
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
getBucketReq.bucket = "examplebucket-1250000000";
        
// Maximum number of objects to return at a time. Default value: 1000
getBucketReq.maxKeys = 100;
        
//To delete files with a specified prefix, `prefix` should be the prefix of the files to delete
getBucketReq.prefix = "dir/";

        
getBucketReq.setFinish { (result, error) in
    if let result = result {
        let contents = result.contents;
        let infos = NSMutableArray.init();
        for content in contents {
            let info = QCloudDeleteObjectInfo.init();
            info.key = content.key;
            infos.add(info);
        }
        let mutipleDel = QCloudDeleteMultipleObjectRequest.init();
        // File set to be deleted
        let deleteInfos = QCloudDeleteInfo.init();
        // Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        mutipleDel.bucket = "examplebucket-1250000000";
                
        deleteInfos.objects = infos as! [QCloudDeleteObjectInfo];
                
        // Boolean value. Determines whether to enable the `Quiet` mode:
        // true: enable the `Quiet` mode
        // false: enable the `Verbose` mode
        // Default value: false
        deleteInfos.quiet = false;
                
        // Encapsulates the information on the multiple objects to be deleted in batches
        mutipleDel.deleteObjects = deleteInfos;
                
        mutipleDel.setFinish { (result, error) in
            if let result = result {
                let deleted = result.deletedObjects
                let failed = result.deletedFailedObjects
            } else {
                print(error!);
            }
        }
        QCloudCOSXMLService.defaultCOSXML().deleteMultipleObject(mutipleDel);
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DeleteObject.swift).

