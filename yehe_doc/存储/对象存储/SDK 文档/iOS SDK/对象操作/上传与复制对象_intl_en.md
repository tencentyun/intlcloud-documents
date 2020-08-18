## Overview

This document provides an overview of APIs and SDK code samples related to object upload and replication.


**Simple operations**

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using a form | Uploads an object using a form request |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |

**Multipart upload operations**

| API | Operation Name | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart upload operations | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload operation | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in multiple parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload operation | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload operation | Aborts multipart a upload operation and deletes the uploaded parts |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (Recommended)

### Uploading an object

The advanced APIs encapsulate the simple upload and multipart upload APIs and can intelligently select the upload method based on file size. They also support checkpoint restart for resuming interrupted operations.

#### Sample 1. Uploading a local file
**Objective-C**

[//]: # (.cssg-snippet-transfer-upload-file)
```objective-c
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
// Local file path
NSURL* url = [NSURL fileURLWithPath:@"file URL"];

// Bucket name in the format: `BucketName-APPID`
put.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
put.object = @"exampleobject";

// Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` format
put.body =  url;
// Monitor the upload progress
[put setSendProcessBlock:^(int64_t bytesSent,
                           int64_t totalBytesSent,
                           int64_t totalBytesExpectedToSend) {
    // bytesSent                   Number of new bytes sent
    // totalBytesSent              Total number of bytes sent in the upload
    // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
}];

// Monitor the upload result
[put setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject returns information such as the Etag or custom headers in the response
    NSDictionary * result = (NSDictionary *)outputObject;
}];

[put setInitMultipleUploadFinishBlock:^(QCloudInitiateMultipartUploadResult * _Nullable multipleUploadInitResult, QCloudCOSXMLUploadObjectResumeData  _Nullable resumeData) {
    // This block will be called back after the Initiate Multipart Upload operation is complete so you can get resumeData and the uploadID
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];

// To cancel the upload, call `cancel`
[put abort:^(id outputObject, NSError *error) {

}];
```

>?
>- For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/TransferObject.m).
>- After an object is uploaded, you can use the same key to generate a link to download the file as instructed in [Generating a Pre-signed Link](https://cloud.tencent.com/document/product/436/46388). However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

**Swift**

[//]: # (.cssg-snippet-transfer-upload-file)
```swift
let put:QCloudCOSXMLUploadObjectRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>();

// Bucket name in the format: `BucketName-APPID`
put.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
put.object = "exampleobject";

// Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` format
put.body = NSURL.fileURL(withPath: "Local File Path") as AnyObject;

// Monitor the upload result
put.setFinish { (result, error) in
    // Get the upload result
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}

// Monitor the upload progress
put.sendProcessBlock = { (bytesSent, totalBytesSent,
    totalBytesExpectedToSend) in
    // bytesSent                   Number of new bytes sent
    // totalBytesSent              Total number of bytes sent in the upload
    // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
};
// Set the upload parameters
put.initMultipleUploadFinishBlock = {(multipleUploadInitResult, resumeData) in
    // This block will be called back after the Initiate Multipart Upload operation is complete so you can get resumeData
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(put);

// To cancel the upload, call `abort`
put.abort { (result, error) in
    
}
```

>?
>- For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/TransferObject.swift).
>- After an object is uploaded, you can use the same key to generate a link to download the file as instructed in [Generating a Pre-signed Link](https://cloud.tencent.com/document/product/436/46388). However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

#### Sample 2. Uploading binary data
**Objective-C**

[//]: # (.cssg-snippet-transfer-upload-bytes)
```objective-c
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];

// Bucket name in the format: `BucketName-APPID`
put.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
put.object = @"exampleobject";

// Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` format
put.body = [@"My Example Content" dataUsingEncoding:NSUTF8StringEncoding];

// Monitor the upload progress
[put setSendProcessBlock:^(int64_t bytesSent,
                           int64_t totalBytesSent,
                           int64_t totalBytesExpectedToSend) {
    
    // bytesSent                   Number of new bytes sent
    // totalBytesSent              Total number of bytes sent in the upload
    // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
}];

// Monitor the upload result
[put setFinishBlock:^(id outputObject, NSError *error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];
[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
```

>?
>- For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/TransferObject.m).
>- After an object is uploaded, you can use the same key to generate a link to download the file as instructed in [Generating a Pre-signed Link](https://cloud.tencent.com/document/product/436/46388). However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

**Swift**

[//]: # (.cssg-snippet-transfer-upload-bytes)
```swift
let put:QCloudCOSXMLUploadObjectRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>();

// Bucket name in the format: `BucketName-APPID`
put.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
put.object = "exampleobject";

// Content of the object to be uploaded
let dataBody:NSData = "wrwrwrwrwrw".data(using: .utf8)! as NSData;
put.body = dataBody;

// Monitor the upload result
put.setFinish { (result, error) in
    // Get the upload result
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}

// Monitor the upload progress
put.sendProcessBlock = { (bytesSent, totalBytesSent,
    totalBytesExpectedToSend) in
    
    // bytesSent                   Number of new bytes sent
    // totalBytesSent              Total number of bytes sent in the upload
    // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
};

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(put);
```

>?
>- For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/TransferObject.swift).
>- After an object is uploaded, you can use the same key to generate a link to download the file as instructed in [Generating a Pre-signed Link](https://cloud.tencent.com/document/product/436/46388). However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

### Copying an object

The advanced APIs encapsulate async requests for the simple copy and multipart copy APIs and support pausing, resuming, and canceling copy requests.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-transfer-copy-object)
```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Source bucket containing the file; the current account needs to have access permission for the bucket, or the bucket should have public-read permission enabled.
request.sourceBucket = @"sourcebucket-1250000000";

// Source file name
request.sourceObject = @"sourceObject";

// Source file `APPID`
request.sourceAPPID = @"1250000000";

// Source region
request.sourceRegion= @"COS_REGION";

[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    // outputObject returns information such as the Etag or custom headers in the response 
}];

// Note that for cross-region replication, the region used for `transferManager` must be the region of the destination bucket
[[QCloudCOSTransferMangerService defaultCOSTransferManager] CopyObject:request];

// Cancel copy
// To cancel the copy operation, call `cancel`
[request cancel];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/TransferObject.m).

**Swift**

[//]: # (.cssg-snippet-transfer-copy-object)
```swift
let copyRequest =  QCloudCOSXMLCopyObjectRequest.init();

// Bucket name in the format: `BucketName-APPID`
copyRequest.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
copyRequest.object = "exampleobject";

// Source bucket containing the file; the current account needs to have access permission for the bucket, or the bucket should have public-read permission enabled.
// Bucket name in the format: `BucketName-APPID`
copyRequest.sourceBucket = "sourcebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
copyRequest.sourceObject = "sourceObject";

// Source file `APPID`
copyRequest.sourceAPPID = "1250000000";

// Source region
copyRequest.sourceRegion = "COS_REGION";

copyRequest.setFinish { (copyResult, error) in
    if error != nil{
        print(error!);
    }else{
        print(copyResult!);
    }
    
}
// Note that for cross-region replication, the region used for `transferManager` must be the region of the destination bucket
QCloudCOSTransferMangerService.defaultCOSTransferManager().copyObject(copyRequest);

// Cancel copy
// To cancel the copy operation, call `cancel`
copyRequest.cancel();
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/TransferObject.swift).

## Simple Operations

### Uploading an object using simple upload

#### Feature description

This API is used to upload an object to a specified bucket. This operation requires the requester to have WRITE permission for the bucket. It can upload a file up to 5 GB in size. For larger files, please use [multipart upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89).

> !
> 1. The `Key` (filename) cannot end in `/`; otherwise, it will be recognized as a folder.
> 2. The total number of bucket ACL rules under a single root account (i.e., under the same `APPID`) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, you can choose not to configure an ACL for the object during upload, and the object will inherit the permissions of its bucket by default.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-object)
```objective-c
QCloudPutObjectRequest* put = [QCloudPutObjectRequest new];

// Bucket name in the format: `BucketName-APPID`
put.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
put.object = @"exampleobject";

put.body =  [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];

[put setFinishBlock:^(id outputObject, NSError *error) {
    
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutObject:put];
```

>?
>- For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/PutObject.m).
>- After an object is uploaded, you can use the same key to generate a link to download the file as instructed in [Generating a Pre-signed Link](https://cloud.tencent.com/document/product/436/46388). However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

**Swift**

[//]: # (.cssg-snippet-put-object)
```swift
let putObject = QCloudPutObjectRequest<AnyObject>.init();

// Bucket name in the format: `BucketName-APPID`
putObject.bucket = "examplebucket-1250000000";
let dataBody:NSData? = "wrwrwrwrwrw".data(using: .utf8) as NSData?;
putObject.body =  dataBody!;

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
putObject.object = "exampleobject";
putObject.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putObject(putObject);
```

>?
>- For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/PutObject.swift).
>- After an object is uploaded, you can use the same key to generate a link to download the file as instructed in [Generating a Pre-signed Link](https://cloud.tencent.com/document/product/436/46388). However, please note that if your file is set to private-read, the download link will only be valid for a certain period of time.

### Copying an object (modifying attributes)

This API is used to copy a file to a destination path.

#### Sample 1. Copying an object while retaining its attributes
**Objective-C**

[//]: # (.cssg-snippet-copy-object)
```objective-c
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as `Replaced`
request.metadataDirective = @"Copy";

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 ACL rules. If you do not need access control for the object, enter `default` for this parameter
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
request.accessControlList = @"default";

// Source object path
request.objectCopySource =
@"sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// Specify the `versionID` of the source file. This parameter is only relevant for buckets where versioning is enabled or suspended
request.versionID = @"objectVersion1";

[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    // `result` contains the request result
 
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/CopyObject.m).

**Swift**

[//]: # (.cssg-snippet-copy-object)
```swift
let putObjectCopy = QCloudPutObjectCopyRequest.init();

// Bucket name in the format: `BucketName-APPID`
putObjectCopy.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
putObjectCopy.object = "exampleobject";

// Source object path
putObjectCopy.objectCopySource = "sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as `Replaced`
putObjectCopy.metadataDirective = "Copy";

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 ACL rules. If you do not need access control for the object, enter `default` for this parameter
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
putObjectCopy.accessControlList = "default";

// Specify the `versionID` of the source file. This parameter is only relevant for buckets where versioning is enabled or suspended
putObjectCopy.versionID = "versionID";

putObjectCopy.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putObjectCopy(putObjectCopy);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/CopyObject.swift).

#### Sample 2. Copying an object while replacing its attributes
**Objective-C**

[//]: # (.cssg-snippet-copy-object-replaced)
```objective-c
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as `Replaced`
request.metadataDirective = @"Replaced";

// Modify the metadata
[request.customHeaders setValue:@"newValue" forKey:@"x-cos-meta-*"];

// Object storage class, such as `MAZ_STANDARD`, `MAZ_STANDARD_IA`,
// `STANDARD_IA`, and `ARCHIVE`. For the enumerated values, please see the Storage Class documentation. This header will be returned only if the storage class of the file is not `STANDARD`
// Modify the storage class
[request.customHeaders setValue:@"newValue" forKey:@"x-cos-storage-class"];

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 ACL rules. If you do not need access control for the object, enter `default` for this parameter
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
// Modify the ACL
request.accessControlList = @"private";

// Source object path
request.objectCopySource =
    @"sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// Specify the `versionID` of the source file. This parameter is only relevant for buckets where versioning is enabled or suspended
request.versionID = @"objectVersion1";

[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    // `result` contains the request result
    
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/CopyObject.m).

**Swift**

[//]: # (.cssg-snippet-copy-object-replaced)
```swift
let request : QCloudPutObjectCopyRequest  = QCloudPutObjectCopyRequest();

// Bucket name in the format: `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = "exampleobject";

// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as `Replaced`
request.metadataDirective = "Replaced";

// Modify the metadata
request.customHeaders.setValue("newValue", forKey: "x-cos-meta-*");

// Object storage class, such as `MAZ_STANDARD`, `MAZ_STANDARD_IA`,
// `STANDARD_IA`, and `ARCHIVE`. For the enumerated values, please see the Storage Class documentation. This header will be returned only if the storage class of the file is not `STANDARD`
// Modify the storage class
request.customHeaders.setValue("newValue", forKey: "x-cos-storage-class");

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 ACL rules. If you do not need access control for the object, enter `default` for this parameter
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
// Modify the ACL
request.accessControlList = "Source file ACL";
// Source object path
request.objectCopySource = "sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// Specify the `versionID` of the source file. This parameter is only relevant for buckets where versioning is enabled or suspended
request.versionID = "versionID";

request.setFinish { (result, error) in
   if error != nil{
       print(error!);
   }else{
       print(result!);
   }
       
}
QCloudCOSXMLService.defaultCOSXML().putObjectCopy(request);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/CopyObject.swift).

#### Sample 3. Modifying object metadata
**Objective-C**

[//]: # (.cssg-snippet-modify-object-metadata)
```objective-c
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as `Replaced`
request.metadataDirective = @"Replaced";

// Custom file header
[request.customHeaders setValue:@"newValue" forKey:@"x-cos-meta-*"];

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 ACL rules. If you do not need access control for the object, enter `default` for this parameter
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
request.accessControlList = @"default";
// Source object path
request.objectCopySource =
    @"examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    // `result` contains the request result
    
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/ModifyObjectProperty.m).

**Swift**

[//]: # (.cssg-snippet-modify-object-metadata)
```swift
let request : QCloudPutObjectCopyRequest = QCloudPutObjectCopyRequest();

// Bucket name in the format: `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = "exampleobject";

// Indicates whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path
// (i.e., when you want to modify the metadata), it must be specified as `Replaced`
request.metadataDirective = "Replaced";

// Custom file header
request.customHeaders.setValue("newValue", forKey: "x-cos-meta-*")

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 ACL rules. If you do not need access control for the object, enter `default` for this parameter
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
request.accessControlList = "default";

// Source object path
request.objectCopySource =
    "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

request.setFinish { (result, error) in
    // `result` contains the request result
}

QCloudCOSXMLService.defaultCOSXML().putObjectCopy(request);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/ModifyObjectProperty.swift).

#### Sample 4. Changing the object storage class
**Objective-C**

[//]: # (.cssg-snippet-modify-object-storage-class)
```objective-c
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Object storage class, such as `MAZ_STANDARD`, `MAZ_STANDARD_IA`,
// `STANDARD_IA`, and `ARCHIVE`. For the enumerated values, please see the Storage Class documentation. This header will be returned only if the storage class of the file is not `STANDARD`
[request.customHeaders setValue:@"ARCHIVE" forKey:@"x-cos-storage-class"];

// Source object path
request.objectCopySource =
    @"examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

// Specify the `versionID` of the source file. This parameter is only relevant for buckets where versioning is enabled or suspended
request.versionID = @"";

[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    // `result` contains the request result
   
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/ModifyObjectProperty.m).

**Swift**

[//]: # (.cssg-snippet-modify-object-storage-class)
```swift
let request : QCloudPutObjectCopyRequest = QCloudPutObjectCopyRequest();

// Bucket name in the format: `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = "exampleobject";

// Object storage class, such as `MAZ_STANDARD`, `MAZ_STANDARD_IA`,
// `STANDARD_IA`, and `ARCHIVE`. For the enumerated values, please see the Storage Class documentation. This header will be returned only if the storage class of the file is not `STANDARD`
request.customHeaders.setValue("newValue", forKey: "x-cos-storage-class");
// Source object path
request.objectCopySource =
    "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

request.setFinish { (result, error) in
    // `result` contains the request result
}

QCloudCOSXMLService.defaultCOSXML().putObjectCopy(request);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/ModifyObjectProperty.swift).

## Multipart Operations

The multipart upload process is outlined below.

#### Multipart upload/copy process

1. Initialize the multipart upload with `Initiate Multipart Upload` and get the `UploadId`.
2. Use the `UploadId` to upload parts with `Upload Part` or copy parts with `Upload Part Copy`.
3. Complete the multipart upload with `Complete Multipart Upload`.

#### How to resume a multipart upload/copy operation

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Use the `UploadId` to list the uploaded parts with `List Parts`.
2. Use the `UploadId` to upload the remaining parts with `Upload Part` or copy the remaining parts with `Upload Part Copy`.
3. Complete the multipart upload with `Complete Multipart Upload`.

#### Multipart upload/copy termination process

1. If you did not record the `UploadId` of the multipart upload, you can query the multipart upload job with `List Multipart Uploads` to get the `UploadId` of the corresponding file.
2. Abort the multipart upload and delete the uploaded parts with `Abort Multipart Upload`.

### Querying multipart upload operations

#### Feature description

This API is used to query the in-progress multipart uploads operations in a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-list-multi-upload)
```objective-c
QCloudListBucketMultipartUploadsRequest* uploads = [QCloudListBucketMultipartUploadsRequest new];

// Bucket name in the format: `BucketName-APPID`
uploads.bucket = @"examplebucket-1250000000";

// Set the maximum number of multiparts to be returned. Valid value: 1–1000
uploads.maxUploads = 100;

[uploads setFinishBlock:^(QCloudListMultipartUploadsResult* result,
                          NSError *error) {
    // Get the information on in-progress multipart uploads from `result`
    // Object in the ongoing multipart upload
    NSArray<QCloudListMultipartUploadContent*> *uploads = result.uploads;
}];

[[QCloudCOSXMLService defaultCOSXML] ListBucketMultipartUploads:uploads];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # (.cssg-snippet-list-multi-upload)
```swift
let listParts = QCloudListBucketMultipartUploadsRequest.init();

// Bucket name in the format: `BucketName-APPID`
listParts.bucket = "examplebucket-1250000000";

// Set the maximum number of multiparts to be returned. Valid value: 1–1000
listParts.maxUploads = 100;

listParts.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        // Get the information on in-progress multipart uploads from `result`
        print(result!);
        
        // Object in the ongoing multipart upload
        let uploads : Array<QCloudListMultipartUploadContent> = result!.uploads;
    }
}
QCloudCOSXMLService.defaultCOSXML().listBucketMultipartUploads(listParts);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Initializing a multipart upload operation

#### Feature description

This API is used to initialize a multipart upload operation and get its `uploadID`.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-init-multi-upload)
```objective-c
QCloudInitiateMultipartUploadRequest* initRequest = [QCloudInitiateMultipartUploadRequest new];

// Bucket name in the format: `BucketName-APPID`
initRequest.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
initRequest.object = @"exampleobject";

// This will be returned as object metadata
initRequest.cacheControl = @"cacheControl";

initRequest.contentDisposition = @"contentDisposition";

// Define the ACL attribute of the object. Valid values: private, public-read-write, public-read. Default value: private
initRequest.accessControlList = @"public";

// Grant read permission
initRequest.grantRead = @"grantRead";

// Grant write permission
initRequest.grantWrite = @"grantWrite";

// Grant read and write permission; grantFullControl = grantWrite + grantRead
initRequest.grantFullControl = @"grantFullControl";

[initRequest setFinishBlock:^(QCloudInitiateMultipartUploadResult* outputObject,
                              NSError *error) {
    // Get the `uploadId` of the multipart upload. This ID is required for subsequent uploads. Please save it for future use.
    self->uploadId = outputObject.uploadId;
    
}];

[[QCloudCOSXMLService defaultCOSXML] InitiateMultipartUpload:initRequest];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # (.cssg-snippet-init-multi-upload)
```swift
let initRequest = QCloudInitiateMultipartUploadRequest.init();

// Bucket name in the format: `BucketName-APPID`
initRequest.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
initRequest.object = "exampleobject";

initRequest.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        // Get the `uploadId` of the multipart upload. This ID is required for subsequent uploads. Please save it for future use.
        self.uploadId = result!.uploadId;
        print(result!.uploadId);
    }
}
QCloudCOSXMLService.defaultCOSXML().initiateMultipartUpload(initRequest);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Uploading parts

This API is used to upload parts.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-upload-part)
```objective-c
QCloudUploadPartRequest* request = [QCloudUploadPartRequest new];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Part number
request.partNumber = 1;

// The ID of the multipart upload. When you use the `Initiate Multipart Upload` API to initialize a multipart upload, you will get an `uploadId`
request.uploadId = uploadId;

// Uploaded data. Three types are supported, i.e., NSData*, NSURL (local URL), and QCloudFileOffsetBody*
request.body = [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];

[request setSendProcessBlock:^(int64_t bytesSent,
                               int64_t totalBytesSent,
                               int64_t totalBytesExpectedToSend) {
    // Upload progress
    // bytesSent                   Number of new bytes sent
    // totalBytesSent              Total number of bytes sent in the upload
    // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
}];
[request setFinishBlock:^(QCloudUploadPartResult* outputObject, NSError *error) {
    QCloudMultipartInfo *part = [QCloudMultipartInfo new];
    // Get the `etag` of the uploaded part
    part.eTag = outputObject.eTag;
    part.partNumber = @"1";
    // Save it for future use after the upload is complete
    self.parts = @[part];

}];

[[QCloudCOSXMLService defaultCOSXML]  UploadPart:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # (.cssg-snippet-upload-part)
```swift
let uploadPart = QCloudUploadPartRequest<AnyObject>.init();

// Bucket name in the format: `BucketName-APPID`
uploadPart.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
uploadPart.object = "exampleobject";
uploadPart.partNumber = 1;

// The ID of the multipart upload. When you use the `Initiate Multipart Upload` API to initialize a multipart upload, you will get an `uploadId`
// This ID not only uniquely identifies the data of the part, but also identifies its location in the entire file
if let uploadId = self.uploadId {
    uploadPart.uploadId = uploadId;
}

let dataBody:NSData? = "wrwrwrwrwrwwrwrwrwrwrwwwrwrw"
    .data(using: .utf8) as NSData?;
uploadPart.body = dataBody!;
uploadPart.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        let mutipartInfo = QCloudMultipartInfo.init();
        // Get the `etag` of the uploaded part
        mutipartInfo.eTag = result!.eTag;
        mutipartInfo.partNumber = "1";
        // Save it for future use after the upload is complete
        self.parts = [mutipartInfo];
    }
}
uploadPart.sendProcessBlock = {(bytesSent,totalBytesSent,totalBytesExpectedToSend) in
    
    // Upload progress
    // bytesSent                   Number of new bytes sent
    // totalBytesSent              Total number of bytes sent in the upload
    // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
    
}
QCloudCOSXMLService.defaultCOSXML().uploadPart(uploadPart);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Copying a part

#### Feature description

This API is used to copy an object as a part.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-upload-part-copy)
```objective-c
QCloudUploadPartCopyRequest* request = [[QCloudUploadPartCopyRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// URL path of the source file. A previous version can be specified by using the `versionid` subresource
request.source = @"sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// The Initiate Multipart Upload request returns an upload ID used to uniquely identify the upload.
request.uploadID = uploadId;

// Current part number
request.partNumber = 1;

[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    QCloudMultipartInfo *part = [QCloudMultipartInfo new];
    
    // Get the `etag` of the copied part
    part.eTag = result.eTag;
    part.partNumber = @"1";
    // Save it for future use after the upload is complete
    self.parts=@[part];
    
}];

[[QCloudCOSXMLService defaultCOSXML]UploadPartCopy:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/MultiPartsCopyObject.m).

**Swift**

[//]: # (.cssg-snippet-upload-part-copy)
```swift
let req = QCloudUploadPartCopyRequest.init();

// Bucket name in the format: `BucketName-APPID`
req.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
req.object = "exampleobject";

// URL path of the source file. A previous version can be specified by using the `versionid` subresource
req.source = "sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";
// The Initiate Multipart Upload request returns an upload ID used to uniquely identify the upload.
if let uploadId = self.uploadId {
    req.uploadID = uploadId;
}

// Current part number
req.partNumber = 1;
req.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        let mutipartInfo = QCloudMultipartInfo.init();
        // Get the `etag` of the copied part
        mutipartInfo.eTag = result!.eTag;
        mutipartInfo.partNumber = "1";
        // Save it for future use after the upload is complete
        self.parts = [mutipartInfo];
    }
}
QCloudCOSXMLService.defaultCOSXML().uploadPartCopy(req);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/MultiPartsCopyObject.swift).

### Querying uploaded parts

#### Feature description

This API is used to the query uploaded parts of a specified multipart upload operation.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-list-parts)
```objective-c
QCloudListMultipartRequest* request = [QCloudListMultipartRequest new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// The Initiate Multipart Upload request returns an upload ID used to uniquely identify the upload.
request.uploadId = uploadId;

[request setFinishBlock:^(QCloudListPartsResult * _Nonnull result,
                          NSError * _Nonnull error) {
    
    // Get the information on uploaded parts from `result`
    // Information on each part
    NSArray<QCloudMultipartUploadPart*> *parts = result.parts;
}];

[[QCloudCOSXMLService defaultCOSXML] ListMultipart:request];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # (.cssg-snippet-list-parts)
```swift
let req = QCloudListMultipartRequest.init();

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
req.object = "exampleobject";

// Bucket name in the format: `BucketName-APPID`
req.bucket = "examplebucket-1250000000";

// The Initiate Multipart Upload request returns an upload ID used to uniquely identify the upload.
if let uploadId = self.uploadId {
    req.uploadId = uploadId;
}
req.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        // Get the information on uploaded parts from `result`
        print(result!);
    }
}

QCloudCOSXMLService.defaultCOSXML().listMultipart(req);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Completing a multipart upload operation

#### Feature description

This API is used to complete the multipart upload of the entire file.

#### Sample code

**Objective-C**

[//]: # (.cssg-snippet-complete-multi-upload)
```objective-c
QCloudCompleteMultipartUploadRequest *completeRequst = [QCloudCompleteMultipartUploadRequest new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
completeRequst.object = @"exampleobject";

// Bucket name in the format: `BucketName-APPID`
completeRequst.bucket = @"examplebucket-1250000000";

// `uploadId` of the multipart upload to be queried. This ID can be obtained from `QCloudInitiateMultipartUploadResult`, i.e. the result of the multipart upload initialization request
completeRequst.uploadId = uploadId;

// Information on the uploaded parts
QCloudCompleteMultipartUploadInfo *partInfo = [QCloudCompleteMultipartUploadInfo new];
NSMutableArray * parts = [self.parts mutableCopy];

// Sort the uploaded parts
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
    // Get the upload result from `result`
}];

[[QCloudCOSXMLService defaultCOSXML] CompleteMultipartUpload:completeRequst];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # (.cssg-snippet-complete-multi-upload)
```swift
let  complete = QCloudCompleteMultipartUploadRequest.init();

// Bucket name in the format: `BucketName-APPID`
complete.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
complete.object = "exampleobject";

// `uploadId` of the multipart upload to be queried. This ID can be obtained from
// `QCloudInitiateMultipartUploadResult`, i.e. the result of the multipart upload initialization request
complete.uploadId = "exampleUploadId";
if let uploadId = self.uploadId {
    complete.uploadId = uploadId;
}

// Information on the uploaded parts
let completeInfo = QCloudCompleteMultipartUploadInfo.init();
if self.parts == nil {
    print("No parts to complete");
    return;
}
if self.parts != nil {
    completeInfo.parts = self.parts ?? [];
}

complete.parts = completeInfo;
complete.setFinish { (result, error) in
    if error != nil{
        print(error!)
    }else{
        // Get the upload result from `result`
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().completeMultipartUpload(complete);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Aborting a multipart upload operation

#### Feature description

This API is used to abort a multipart upload operation and delete the uploaded parts.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-abort-multi-upload)
```objective-c
QCloudAbortMultipfartUploadRequest *abortRequest = [QCloudAbortMultipfartUploadRequest new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
abortRequest.object = @"exampleobject";

// Bucket name in the format: `BucketName-APPID`
abortRequest.bucket = @"examplebucket-1250000000";

// `uploadId` of the multipart upload to be aborted.
// This ID can be obtained from `QCloudInitiateMultipartUploadResult`, i.e. the result of the multipart upload initialization request
abortRequest.uploadId = @"exampleUploadId";

[abortRequest setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject returns information such as the Etag or custom headers in the response 
    NSDictionary * result = (NSDictionary *)outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML]AbortMultipfartUpload:abortRequest];
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Objc/Examples/cases/AbortMultiPartsUpload.m).

**Swift**

[//]: # (.cssg-snippet-abort-multi-upload)
```swift
let abort = QCloudAbortMultipfartUploadRequest.init();

// Bucket name in the format: `BucketName-APPID`
abort.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
abort.object = "exampleobject";

// `uploadId` of the multipart upload to be queried. This ID can be obtained from
// `QCloudInitiateMultipartUploadResult`, i.e. the result of the multipart upload initialization request
abort.uploadId = self.uploadId!;

abort.finishBlock = {(result,error)in
    if error != nil{
        print(error!)
    }else{
        // `result` returns information such as the etag or custom headers in the response
        print(result!);
    }
}
QCloudCOSXMLService.defaultCOSXML().abortMultipfartUpload(abort);
```

>?For more samples, please visit [GitHub](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/COSAPIDemo/Swift/Examples/cases/AbortMultiPartsUpload.swift).

