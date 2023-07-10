## Overview


This document provides an overview of APIs and SDK code samples for copying and moving objects.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path. |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes a specified object from a bucket. |

**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads/copy | Queries in-progress multipart uploads/copy. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload/copy operation | Initializes a multipart upload/copy operation. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded/copied parts | Queries the uploaded/copied parts of a multipart operation. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload/copy | Completes the multipart upload/copy of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload/copy | Aborts a multipart operation and deletes the uploaded/copied parts. |


## SDK API References

For parameters and method description of all APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Copying objects

The advanced APIs encapsulate async requests for the simple copy and multipart copy APIs and support pausing, resuming, and canceling copy requests.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-transfer-copy-object"
```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
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
    // You can get the information such as the ETag or custom headers in the response from outputObject.
}];

// Note that for cross-region replication, the region used for `transferManager` must be the region of the destination bucket
[[QCloudCOSTransferMangerService defaultCOSTransferManager] CopyObject:request];

// Cancel the copy
// To cancel the copy operation, call `cancel`
[request cancel];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferCopyObject.m).

**Swift**

[//]: # ".cssg-snippet-transfer-copy-object"
```swift
let copyRequest =  QCloudCOSXMLCopyObjectRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
copyRequest.bucket = "examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
copyRequest.object = "exampleobject";

// Source bucket containing the file; the current account needs to have access permission for the bucket, or the bucket should have public-read permission enabled.
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
copyRequest.sourceBucket = "sourcebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
copyRequest.sourceObject = "sourceObject";

// APPID of the source file
copyRequest.sourceAPPID = "1250000000";

// Source region
copyRequest.sourceRegion = "COS_REGION";

copyRequest.setFinish { (copyResult, error) in
    if let copyResult = copyResult {
        // ETag of the file
        let eTag = copyResult.eTag
    } else {
        print(error!);
    }
    
}
// Note that for cross-region replication, the region used for `transferManager` must be the region of the destination bucket
QCloudCOSTransferMangerService.defaultCOSTransferManager().copyObject(copyRequest);

// Cancel the copy
// To cancel the copy operation, call `cancel`
copyRequest.cancel();
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferCopyObject.swift).


### Moving an object

Object movement involves copying the source object to the target location and deleting the source object.

Since COS uses the bucket name (`Bucket`) and object key (`ObjectKey`) to identify objects, moving an object will change the object identifier. Currently, COS’s Java SDK does not provide a standalone API to change object identifiers. However, you can still move the object with a combination of basic operations (**object copy** and **object delete**).

For example, if you want to move the `picture.jpg` object to the “doc” directory that is in the same bucket (`mybucket-1250000000`), you can copy the `picture.jpg` to the “doc” directory (making the object key `doc/picture.jpg`) and then delete the source object.

Likewise, if you need to move `picture.jpg` in the `mybucket-1250000000` bucket to another bucket `myanothorbucket-1250000000`, you can copy the object to the `myanothorbucket-1250000000` bucket first and then delete the source object.


#### Sample code

**Objective-C**

[//]: #	".cssg-snippet-move-object"
```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];
    
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
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
    // You can get the information such as the ETag or custom headers in the response from outputObject
    if(!error){
        QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
            
        // Source bucket containing the file; the current account needs to have access permission for the bucket, or the bucket should have public-read permission enabled.
        deleteObjectRequest.bucket = @"sourcebucket-1250000000";
            
        // Name of the source object, which is also the full path of the object in COS. If the object is in a directory, the path should be "dir1/object1".
        deleteObjectRequest.object = @"sourceObject";
            
        [deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
            // `outputObject` contains all the `HTTP` response headers
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

[//]: # ".cssg-snippet-transfer-copy-object"
```swift
let copyRequest =  QCloudCOSXMLCopyObjectRequest.init();
        
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
copyRequest.bucket = "examplebucket-1250000000";
                
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
copyRequest.object = "exampleobject";
        
// Source bucket containing the file; the current account needs to have access permission for the bucket, or the bucket should have public-read permission enabled.
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
copyRequest.sourceBucket = "sourcebucket-1250000000";
        
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
copyRequest.sourceObject = "sourceObject";
        
// `APPID` of the source file
copyRequest.sourceAPPID = "1250000000";
        
// Source region
copyRequest.sourceRegion = "COS_REGION";
        
copyRequest.setFinish { (copyResult, error) in
    if let copyResult = copyResult {
        // `ETag` of the file
        let deleteObject = QCloudDeleteObjectRequest.init();
                
        // Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        deleteObject.bucket = "sourcebucket-1250000000";
                
        // Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
        deleteObject.object = "sourceObject";
                
        deleteObject.finishBlock = {(result,error)in
            if let result = result {
                    // result contains response headers
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


## Simple Operations


### Copying an object (modifying object attributes)

This API (`PUT Object-Copy`) is used to copy an object to a destination path.

#### Sample 1. Copying an object with its attributes preserved
**Objective-C**

[//]: # ".cssg-snippet-copy-object"

```objective-c
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";
// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as Copy, the user-defined metadata in the Header will be ignored and the object will be copied directly.
// If it is specified as Replaced, the metadata will be modified based on the Header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as Replaced.
request.metadataDirective = @"Copy";
// Define the ACL attribute of Object. Valid values: private; public-read; default.
// Default value: default (i.e., the object will inherit the bucket's permissions)
// Note: If you do not need ACL for the object, please use default
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
request.accessControlList = @"default";
// Path of the source object
request.objectCopySource =
@"sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";
// Specify the `versionID` of the source file. This parameter is only returned for buckets whose versioning is enabled or suspended
request.versionID = @"objectVersion1";
[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    // result contains the request result.
 
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/CopyObject.m).

**Swift**

[//]: # ".cssg-snippet-copy-object"
```swift
let putObjectCopy = QCloudPutObjectCopyRequest.init();
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
putObjectCopy.bucket = "examplebucket-1250000000";
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
putObjectCopy.object = "exampleobject";
// Path of the source object
putObjectCopy.objectCopySource = "sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";
// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as Copy, the user-defined metadata in the Header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as `Replaced`
putObjectCopy.metadataDirective = "Copy";
// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions)
// Note: If you do not need ACL for the object, please use default
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
putObjectCopy.accessControlList = "default";
// Specify the versionID of the source file. This parameter is only returned for buckets whose versioning is enabled or suspended
putObjectCopy.versionID = "versionID";
putObjectCopy.setFinish { (result, error) in
    if let result = result {
        let eTag = result.eTag
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putObjectCopy(putObjectCopy);
```


>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/CopyObject.swift).

#### Sample 2. Copying an object while replacing its attributes
**Objective-C**

[//]: # ".cssg-snippet-copy-object-replaced"
```objective-c
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";
// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as Copy, the user-defined metadata in the Header will be ignored and the object will be copied directly.
// If it is specified as Replaced, the metadata will be modified based on the Header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as Replaced
request.metadataDirective = @"Replaced";
// Modify the metadata
[request.customHeaders setValue:@"newValue" forKey:@"x-cos-meta-*"];
// Storage class. For enumerated values, see **Storage Class Overview**, such as 
// `STANDARD_IA` and `ARCHIVE`. For the enumerated values, please see the Storage Class documentation. This header will be returned only if the storage class of the file is not `STANDARD`.
// Modify the storage class
[request.customHeaders setValue:@"newValue" forKey:@"x-cos-storage-class"];
// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions)
// Note: If you do not need ACL for the object, please use default
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
// Modify the ACL
request.accessControlList = @"private";
// Path of the source object
request.objectCopySource =
    @"sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// Specify the versionID of the source file. This parameter is only returned for buckets whose versioning is enabled or suspended
request.versionID = @"objectVersion1";

[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    // result contains the request result.
    
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/CopyObject.m).

**Swift**

[//]: # ".cssg-snippet-copy-object-replaced"


```swift
let request : QCloudPutObjectCopyRequest  = QCloudPutObjectCopyRequest();
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = "examplebucket-1250000000";
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = "exampleobject";
// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as Copy, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as Replaced, the metadata will be modified based on the Header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as Replaced.
request.metadataDirective = "Replaced";
// Modify the metadata
request.customHeaders.setValue("newValue", forKey: "x-cos-meta-*");
// Storage class. For enumerated values, see **Storage Class Overview**, such as
// `STANDARD_IA` and `ARCHIVE`. For the enumerated values, please see the Storage Class documentation. This header will be returned only if the storage class of the file is not `STANDARD`.
// Modify the storage class
request.customHeaders.setValue("newValue", forKey: "x-cos-storage-class");
// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions)
// Note: If you do not need ACL for the object, please use default
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
// Modify the ACL
request.accessControlList = "Source file ACL";
// Path of the source object
request.objectCopySource = "sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";
// Specify the versionID of the source file. This parameter is only returned for buckets whose versioning is enabled or suspended
request.versionID = "versionID";
request.setFinish { (result, error) in
    if let result = result {
        let eTag = result.eTag
    } else {
        print(error!);
    }
       
}
QCloudCOSXMLService.defaultCOSXML().putObjectCopy(request);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/CopyObject.swift).

#### Sample 3. Modifying object metadata
**Objective-C**

[//]: # ".cssg-snippet-modify-object-metadata"

```objective-c
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";
// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as Copy, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as Replaced, the metadata will be modified based on the Header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as Replaced
request.metadataDirective = @"Replaced";
// Custom object header
[request.customHeaders setValue:@"newValue" forKey:@"x-cos-meta-*"];
// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions)
// Note: If you do not need ACL for the object, please use default
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
request.accessControlList = @"default";
// Path of the source object
request.objectCopySource =
    @"examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    // result contains the request result
    
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```


>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ModifyObjectProperty.m).

**Swift**

[//]: # ".cssg-snippet-modify-object-metadata"
```swift
let request : QCloudPutObjectCopyRequest  = QCloudPutObjectCopyRequest();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = "examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = "exampleobject";

// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as Copy, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as Replaced, the metadata will be modified based on the Header information. If the destination path is the same as the source path
// (i.e., you want to modify the metadata), it must be set to `Replaced`.
request.metadataDirective = "Replaced";

// Custom object header
request.customHeaders.setValue("newValue", forKey: "x-cos-meta-*")

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions)
// Note: If you do not need ACL for the object, please use default
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
request.accessControlList = "default";

// Path of the source object
request.objectCopySource =
    "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

request.setFinish { (result, error) in
    if let result = result {
        // ETag of the destination object
        let eTag = result.eTag
    } else {
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().putObjectCopy(request);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ModifyObjectProperty.swift).

#### Sample 4. Modifying the storage class of an object
**Objective-C**

[//]: # ".cssg-snippet-modify-object-storage-class"
```objective-c
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

// Storage class. For enumerated values, see **Storage Class Overview**, such as
// `STANDARD_IA` and `ARCHIVE`. For the enumerated values, please see the Storage Class documentation. This header will be returned only if the storage class of the file is not `STANDARD`.
[request.customHeaders setValue:@"ARCHIVE" forKey:@"x-cos-storage-class"];

// Path of the source object
request.objectCopySource =
    @"examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

// Specify the versionID of the source file. This parameter is only returned for buckets whose versioning is enabled or suspended
request.versionID = @"";

[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    // result contains the request result.
   
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ModifyObjectProperty.m).

**Swift**

[//]: # ".cssg-snippet-modify-object-storage-class"
```swift
let request : QCloudPutObjectCopyRequest  = QCloudPutObjectCopyRequest();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = "examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = "exampleobject";

// Storage class. For enumerated values, see **Storage Class Overview**, such as
// `STANDARD_IA` and `ARCHIVE`. For the enumerated values, please see the Storage Class documentation. This header will be returned only if the storage class of the file is not `STANDARD`.
request.customHeaders.setValue("newValue", forKey: "x-cos-storage-class");
// Path of the source object
request.objectCopySource =
    "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

request.setFinish { (result, error) in
    if let result = result {
        // ETag of the destination object
        let eTag = result.eTag
    } else {
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().putObjectCopy(request);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ModifyObjectProperty.swift).

## Multipart Operations

This section describes how to perform a multipart copy. There are similarities between the multipart copy and the multipart upload in terms of APIs and usage.

#### Performing a multipart copy

1. Initialize parts with `Initiate Multipart Upload` and get the `UploadId`.
2. Use the `UploadId` to copy the parts with `Upload Part - Copy`.
3. Complete the multipart copy with `Complete Multipart Upload`.

#### Performing a multipart copy

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart copy job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Use the `UploadId` to list the copied parts with `List Parts`.
3. Use the `UploadId` to copy the remaining parts with `Upload Part - Copy`.
4. Complete the multipart copy with `Complete Multipart Upload`.

#### Aborting a multipart copy

1. If you did not record the `UploadId` of the multipart copy, you can query the multipart copy job with `List Multipart Upload` to get the `UploadId`.
2. Abort the multipart copy and delete the copied parts with `Abort Multipart Upload`.

### Querying multipart copies

#### Feature description

This API (`List Multipart Uploads`) is used to query in-progress multipart copies in a specified bucket, which is the same as the API for querying a multipart upload.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-list-multi-upload"
```objective-c
QCloudListBucketMultipartUploadsRequest* uploads = [QCloudListBucketMultipartUploadsRequest new];
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
uploads.bucket = @"examplebucket-1250000000";
// Set the maximum number of parts to return. Value range: 1–1000
uploads.maxUploads = 100;
[uploads setFinishBlock:^(QCloudListMultipartUploadsResult* result,
                          NSError *error) {
    // You can get the information on in-progress multipart uploads from result
    // Object in the ongoing multipart copy
    NSArray<QCloudListMultipartUploadContent*> *uploads = result.uploads;
}];
[[QCloudCOSXMLService defaultCOSXML] ListBucketMultipartUploads:uploads];
```


>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # ".cssg-snippet-list-multi-upload"
```swift
let listParts = QCloudListBucketMultipartUploadsRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
listParts.bucket = "examplebucket-1250000000";

// Set the maximum number of parts to return. Value range: 1–1000
listParts.maxUploads = 100;

listParts.setFinish { (result, error) in
    if let result = result {
        // List all the unfinished multipart copy
        let uploads = result.uploads;
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().listBucketMultipartUploads(listParts);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Initializing a multipart copy

#### Feature description

This API is used to initialize a multipart copy operation and get its `uploadId`, which is the same as the API for initializing a multipart upload.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-init-multi-upload"
``` objective-c
QCloudInitiateMultipartUploadRequest* initRequest = [QCloudInitiateMultipartUploadRequest new];
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
initRequest.bucket = @"examplebucket-1250000000";
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
initRequest.object = @"exampleobject";
// This will be returned as object metadata
initRequest.cacheControl = @"cacheControl";
initRequest.contentDisposition = @"contentDisposition";
// Define the ACL attribute of the object. Valid values: private (default), public-read-write, public-read
initRequest.accessControlList = @"public";
// Grant read permission.
initRequest.grantRead = @"grantRead";
// Grant full permissions to the grantee.
initRequest.grantFullControl = @"grantFullControl";
[initRequest setFinishBlock:^(QCloudInitiateMultipartUploadResult* outputObject,
                              NSError *error) {
    // Get the uploadId of the multipart copy. This ID is required for the subsequent copy. Please save it for future use.
    self->uploadId = outputObject.uploadId;
    
}];

[[QCloudCOSXMLService defaultCOSXML] InitiateMultipartUpload:initRequest];
```



>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # ".cssg-snippet-init-multi-upload"
```swift
let initRequest = QCloudInitiateMultipartUploadRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
initRequest.bucket = "examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
initRequest.object = "exampleobject";

initRequest.setFinish { (result, error) in
    if let result = result {
          // Get the uploadId of the multipart copy. This ID is required for the subsequent copy. Please save it for future use.
        self.uploadId = result.uploadId;
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().initiateMultipartUpload(initRequest);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/MultiPartsUploadObject.swift).


### Copying an object part

#### Feature description

This API (`Upload Part-Copy`) is used to copy an object as a part.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-upload-part-copy"
```objective-c
QCloudUploadPartCopyRequest* request = [[QCloudUploadPartCopyRequest alloc] init];

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

// URL path of the source file. A previous version can be specified by using the versionID subresource.
request.source = @"sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// The Initiate Multipart Copy request returns an upload ID that uniquely identifies the copy.
request.uploadID = uploadId;

// Number that identifies the part
request.partNumber = 1;

[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    QCloudMultipartInfo *part = [QCloudMultipartInfo new];
    
    // Get the ETag of the copied part
    part.eTag = result.eTag;
    part.partNumber = @"1";
    // Save it for completing the copying
    self.parts=@[part];
}];

[[QCloudCOSXMLService defaultCOSXML]UploadPartCopy:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MultiPartsCopyObject.m).

**Swift**

[//]: # ".cssg-snippet-upload-part-copy"
```swift
let req = QCloudUploadPartCopyRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
req.object = "exampleobject";

// URL path of the source file. A previous version can be specified by using the versionID subresource.
req.source = "sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";
// The Initiate Multipart Copy request returns an upload ID that uniquely identifies the copy.
if let uploadId = self.uploadId {
    req.uploadID = uploadId;
}

// Number that identifies the part
req.partNumber = 1;
req.setFinish { (result, error) in
    if let result = result {
        let mutipartInfo = QCloudMultipartInfo.init();
        // Get the ETag of the copied part
        mutipartInfo.eTag = result.eTag;
        mutipartInfo.partNumber = "1";
        // Save it for completing the copying
        self.parts = [mutipartInfo];
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().uploadPartCopy(req);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/MultiPartsCopyObject.swift).

### Querying copied parts

#### Feature description

This API (`List Parts`) is used to query the copied part under a specified copy, which is the same as the API for querying uploaded parts.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-list-parts"
```objective-c
QCloudListMultipartRequest* request = [QCloudListMultipartRequest new];

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
request.object = @"exampleobject";

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";

// The Initiate Multipart Copy request returns an upload ID that uniquely identifies the copy.
request.uploadId = uploadId;

[request setFinishBlock:^(QCloudListPartsResult * _Nonnull result,
                          NSError * _Nonnull error) {
    
    // Get the copied part information from result
    // Information on each part
    NSArray<QCloudMultipartUploadPart*> *parts = result.parts;
}];

[[QCloudCOSXMLService defaultCOSXML] ListMultipart:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # ".cssg-snippet-list-parts"
```swift
let req = QCloudListMultipartRequest.init();

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
req.object = "exampleobject";

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
req.bucket = "examplebucket-1250000000";

// The Initiate Multipart Copy request returns an upload ID that uniquely identifies the copy.
if let uploadId = self.uploadId {
    req.uploadId = uploadId;
}
req.setFinish { (result, error) in
    if let result = result {
        // All uploaded parts
        let parts = result.parts
    } else {
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().listMultipart(req);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Completing a multipart copy

#### Feature description

This API (`Complete Multipart Upload`) is used to complete the multipart copy of a file, which is the same as the API for completing a multipart upload.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-complete-multi-upload"

```objective-c
QCloudCompleteMultipartUploadRequest *completeRequst = [QCloudCompleteMultipartUploadRequest new];
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
completeRequst.object = @"exampleobject";
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
completeRequst.bucket = @"examplebucket-1250000000";
// `uploadId` of the multipart copy to be queried. This ID can be obtained from `QCloudInitiateMultipartUploadResult`, i.e. the result of the multipart copy initialization request.
completeRequst.uploadId = uploadId;
// Copied part information
QCloudCompleteMultipartUploadInfo *partInfo = [QCloudCompleteMultipartUploadInfo new];
NSMutableArray * parts = [self.parts mutableCopy];
// Sort the copied parts.
[parts sortUsingComparator:^NSComparisonResult(QCloudMultipartInfo*  _Nonnull obj1,
                                               QCloudMultipartInfo*  _Nonnull obj2) {
    int a = obj1.partNumber.intValue;
    int b = obj2.partNumber.intValue;
    
    if (a < b) {
        return NSOrderedAscending;
    } else {
        return NSOrderedDescending;
    }
}];
partInfo.parts = [parts copy];
completeRequst.parts = partInfo;

[completeRequst setFinishBlock:^(QCloudUploadObjectResult * _Nonnull result,
                                 NSError * _Nonnull error) {
    // Get the copy result from result
}];

[[QCloudCOSXMLService defaultCOSXML] CompleteMultipartUpload:completeRequst];
```


>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # ".cssg-snippet-complete-multi-upload"
```swift
let  complete = QCloudCompleteMultipartUploadRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
complete.bucket = "examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
complete.object = "exampleobject";

// `uploadId` of the multipart copy to be queried. This ID can be obtained from
// `QCloudInitiateMultipartUploadResult`, i.e., the result of the multipart copy initialization request
complete.uploadId = "exampleUploadId";
if let uploadId = self.uploadId {
    complete.uploadId = uploadId;
}

// Copied part information
let completeInfo = QCloudCompleteMultipartUploadInfo.init();
if self.parts == nil {
    print ("parts that have not completed yet");
    return;
}
if self.parts != nil {
    completeInfo.parts = self.parts ?? [];
}

complete.parts = completeInfo;
complete.setFinish { (result, error) in
   // Get the copy result from result
}
QCloudCOSXMLService.defaultCOSXML().completeMultipartUpload(complete);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Aborting a multipart copy

#### Feature description

This API (`Abort Multipart Upload`) is used to abort a multipart copy and delete the copied parts, which is the same as the API for aborting a multipart upload.

#### Sample code
**Objective-C**

[//]: # ".cssg-snippet-abort-multi-upload"
```objective-c
QCloudAbortMultipfartUploadRequest *abortRequest = [QCloudAbortMultipfartUploadRequest new];
// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
abortRequest.object = @"exampleobject";
// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
abortRequest.bucket = @"examplebucket-1250000000";
// uploadId of the multipart copy to be aborted
// This ID can be obtained from `QCloudInitiateMultipartUploadResult`, i.e. the result of the multipart copy initialization request
abortRequest.uploadId = @"exampleUploadId";
[abortRequest setFinishBlock:^(id outputObject, NSError *error) {
    // You can get the information such as the ETag or custom headers in the response from outputObject
    NSDictionary * result = (NSDictionary *)outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML]AbortMultipfartUpload:abortRequest];
```


>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/AbortMultiPartsUpload.m).

**Swift**

[//]: # ".cssg-snippet-abort-multi-upload"
```swift
let abort = QCloudAbortMultipfartUploadRequest.init();

// Bucket name in the format of BucketName-APPID, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
abort.bucket = "examplebucket-1250000000";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "video/xxx/movie.mp4"
abort.object = "exampleobject";

// uploadId of the multipart copy to be queried. This ID can be obtained from
// `QCloudInitiateMultipartUploadResult`, i.e., the result of the multipart copy initialization request
abort.uploadId = self.uploadId!;

abort.finishBlock = {(result,error)in
    if let result = result {
        // You can get the header information returned by the server from result
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().abortMultipfartUpload(abort);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/AbortMultiPartsUpload.swift).

