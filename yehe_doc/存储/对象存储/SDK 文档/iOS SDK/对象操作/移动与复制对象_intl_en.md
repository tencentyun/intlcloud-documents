## Overview


This document provides an overview of APIs and SDK code samples related to object movement.

| API | Operation | Description |
| :----------------------------------------------------------- | :--------------------------- | :--------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes a specified object from a bucket. |




## Moving an Object

Object movement involves copying the source object to the target location and deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS’s Java SDK does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (**object copy** and **object delete**).

For example, if you want to move the `picture.jpg` object to the “doc” directory that is in the same bucket (`mybucket-1250000000`), you can copy the `picture.jpg` to the “doc” directory (making the object key `doc/picture.jpg`) and then delete the source object.

Likewise, if you need to move `picture.jpg` in the `mybucket-1250000000` bucket to another bucket `myanothorbucket-1250000000`, you can copy the object to the `myanothorbucket-1250000000` bucket first and then delete the source object.


#### Sample code

**Objective-C**

[//]: # (.cssg-snippet-move-object)
```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];
    
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
    
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = @"exampleobject";
    
// Source bucket containing the file; the current account needs to have access permission for the bucket, or the bucket should have public-read permission enabled.
request.sourceBucket = @"sourcebucket-1250000000";
    
// Name of the source file
request.sourceObject = @"sourceObject";
    
// APPID of the source file
request.sourceAPPID = @"1250000000";
    
// Source region
request.sourceRegion= @"COS_REGION";
    
[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    // outputObject contains information such as the ETag or custom headers in the response.
    if(!error){
        QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
            
        // Source bucket containing the file; the current account needs to have access permission for the bucket, or the bucket should have public-read permission enabled.
        deleteObjectRequest.bucket = @"sourcebucket-1250000000";
            
        // Name of the source object, which is also the full path of the object in COS. If the object is in a directory, the path should be "dir1/object1".
        deleteObjectRequest.object = @"sourceObject";
            
        [deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
            // `outputObject` contains all the HTTP response headers
            NSDictionary* info = (NSDictionary *) outputObject;
        }];
            
        [[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
    }
}];
    
// Note that for cross-region movement, the region used for `transferManager` must be the region of the destination bucket.
[[QCloudCOSTransferMangerService defaultCOSTransferManager] CopyObject:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MoveObject.m).

**Swift**

[//]: # (.cssg-snippet-transfer-copy-object)
```swift
let copyRequest =  QCloudCOSXMLCopyObjectRequest.init();
        
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
copyRequest.bucket = "examplebucket-1250000000";
                
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
copyRequest.object = "exampleobject";
        
// Source bucket containing the file; the current account needs to have access permission for the bucket, or the bucket should have public-read permission enabled.
// Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
copyRequest.sourceBucket = "sourcebucket-1250000000";
        
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
copyRequest.sourceObject = "sourceObject";
        
// APPID of the source file
copyRequest.sourceAPPID = "1250000000";
        
// Source region
copyRequest.sourceRegion = "COS_REGION";
        
copyRequest.setFinish { (copyResult, error) in
    if let copyResult = copyResult {
        // ETag of the file
        let deleteObject = QCloudDeleteObjectRequest.init();
                
        // Bucket name in the format of BucketName-Appid, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        deleteObject.bucket = "sourcebucket-1250000000";
                
        // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
        deleteObject.object = "sourceObject";
                
        deleteObject.finishBlock = {(result,error)in
            if let result = result {
                    // "result" contains response headers.
            } else {
                  print(error!);
              }
        }
        QCloudCOSXMLService.defaultCOSXML().deleteObject(deleteObject);
    } else {
        print(error!);
    }
            
}
// Note that for cross-region movement, the region used for `transferManager` must be the region of the destination bucket.
QCloudCOSTransferMangerService.defaultCOSTransferManager().copyObject(copyRequest);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferCopyObject.swift).
