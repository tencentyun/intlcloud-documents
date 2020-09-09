## Overview

This document provides an overview of APIs and SDK sample codes related to uploading and replicating objects.


**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | Uploading an object using HTML form | Uploads an object using HTML form |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object (modifying object attributes) | Copies a file to a destination path |

**Multipart operations**

| API          | Operation                   | Description                                       |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a part in multipart upload |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts |  Queries the uploaded parts of a specific multipart upload |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts |

## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, please see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Advanced APIs (recommended)

### Uploading an object

The advanced upload API encapsulates both PUT Object (simple upload) and multipart upload APIs, and can automatically select the upload method based on file size. It also supports checkpoint restart for resuming a suspended multipart upload.

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
    //      bytesSent                   Number of new bytes
    // totalBytesSent              Total number of bytes sent in the upload
    // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
}];

// Monitor the upload result
[put setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject returns information such as the Etag or custom headers in the response
    NSDictionary * result = (NSDictionary *)outputObject;
}];

[put setInitMultipleUploadFinishBlock:^(QCloudInitiateMultipartUploadResult *
                                        multipleUploadInitResult,
                                        QCloudCOSXMLUploadObjectResumeData resumeData) {
    // This block will be called back after the Initiate Multipart Upload operation is complete so you can get resumeData and the uploadId
    NSString* uploadId = multipleUploadInitResult.uploadId;
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferUploadObject.m).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

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
    if let result = result {
        // Etag of the file
        let eTag = result.eTag
    } else {
        print(error!);
    }
}

// Monitor the upload progress
put.sendProcessBlock = { (bytesSent, totalBytesSent,
    totalBytesExpectedToSend) in
    //      bytesSent                   Number of new bytes sent
    // totalBytesSent              Total number of bytes sent in the upload
    // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
};
// Set the upload parameters
put.initMultipleUploadFinishBlock = {(multipleUploadInitResult, resumeData) in
    // This block will be called back after the Initiate Multipart Upload operation is complete so you can get resumeData and the uploadId
    if let multipleUploadInitResult = multipleUploadInitResult {
        let uploadId = multipleUploadInitResult.uploadId
    }
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(put);
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferUploadObject.swift).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

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
    //      bytesSent                   Number of new bytes
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
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferUploadObject.m).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

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
    if let result = result {
        // Etag of the file
        let eTag = result.eTag
    } else {
        print(error!);
    }
}

// Monitor the upload progress
put.sendProcessBlock = { (bytesSent, totalBytesSent,
    totalBytesExpectedToSend) in
    
    //      bytesSent                   Number of new bytes sent
    // totalBytesSent              Total number of bytes sent in the upload
    // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
};

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(put);
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferUploadObject.swift).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

#### Sample 5. Suspending, resuming and canceling an upload
**Objective-C**

To suspend an upload, use the code below:

[//]: # (.cssg-snippet-transfer-upload-pause)
```objective-c
NSError *error;
NSData *resmeData = [put cancelByProductingResumeData:&error];
```

To resume a suspended download, run the code below:

[//]: # (.cssg-snippet-transfer-upload-resume)
```objective-c
QCloudCOSXMLUploadObjectRequest *resumeRequest = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resmeData];
[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:resumeRequest];
```

To cancel an upload, run this code:

[//]: # (.cssg-snippet-transfer-upload-cancel)
```objective-c
// Abort the upload
[put abort:^(id outputObject, NSError *error) {
    
}];
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferUploadObject.m).

**Swift**

To suspend an upload, use the code below:

[//]: # (.cssg-snippet-transfer-upload-pause)
```swift
var error : NSError?;
var uploadResumeData:Data = put.cancel(byProductingResumeData:&error) as Data;
```

To resume a suspended download, run the code below:

[//]: # (.cssg-snippet-transfer-upload-resume)
```swift
var resumeRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: uploadResumeData);
QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(resumeRequest);
```

To cancel an upload, run this code:

[//]: # (.cssg-snippet-transfer-upload-cancel)
```swift
// Abort the upload
put.abort { (outputObject, error) in
    
}
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferUploadObject.swift).

#### 
**Objective-C**

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```objective-c
for (int i = 0; i<20; i++) {
    QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
    
    // Bucket name in the format: `BucketName-APPID`
    put.bucket = @"examplebucket-1250000000";
    
    // Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
    put.object = [NSString stringWithFormat:@"exampleobject-%d",i];
    
    // Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` format
    put.body = [@"My Example Content" dataUsingEncoding:NSUTF8StringEncoding];
    
    // Monitor the upload progress
    [put setSendProcessBlock:^(int64_t bytesSent,
                               int64_t totalBytesSent,
                               int64_t totalBytesExpectedToSend) {
        //      bytesSent                   Number of new bytes
        // totalBytesSent              Total number of bytes sent in the upload
        // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
    }];
    
    // Monitor the upload result
    [put setFinishBlock:^(id outputObject, NSError *error) {
        // `outputObject` contains all the HTTP response headers
        NSDictionary* info = (NSDictionary *) outputObject;
    }];
    [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
}
```

**Swift**

[//]: # (.cssg-snippet-transfer-batch-upload-objects)
```swift
for i in 1...10 {
    let put:QCloudCOSXMLUploadObjectRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>();
    
    // Bucket name in the format: `BucketName-APPID`
    put.bucket = "examplebucket-1250000000";
    
    // Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
    put.object = "exampleobject-".appendingFormat("%d", i);
    
    // Content of the object to be uploaded
    let dataBody:NSData = "wrwrwrwrwrw".data(using: .utf8)! as NSData;
    put.body = dataBody;
    
    // Monitor the upload result
    put.setFinish { (result, error) in
        // Get the upload result
        if let result = result {
            // Etag of the file
            let eTag = result.eTag
        } else {
            print(error!);
        }
    }

    // Monitor the upload progress
    put.sendProcessBlock = { (bytesSent, totalBytesSent,
        totalBytesExpectedToSend) in
        
        //      bytesSent                   Number of new bytes sent
        // totalBytesSent              Total number of bytes sent in the upload
        // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
    };
    
    QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(put);
}
```

### Copying an object

The advanced replication API encapsulates PUT Object - Copy, and the APIs for multipart replication to allow asynchronous requests for suspending, resuming and canceling a replication request.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-transfer-copy-object)
```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Bucket of the source file, which should be public-read, or your account should have access to
request.sourceBucket = @"sourcebucket-1250000000";

// Source file name
request.sourceObject = @"sourceObject";

// Source file APPID
request.sourceAPPID = @"1250000000";

// Source file’s region
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

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferCopyObject.m).

**Swift**

[//]: # (.cssg-snippet-transfer-copy-object)
```swift
let copyRequest =  QCloudCOSXMLCopyObjectRequest.init();

// Bucket name in the format: `BucketName-APPID`
copyRequest.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
copyRequest.object = "exampleobject";

// Bucket of the source file, which should be public-read, or your account should have access to
// Bucket name in the format: `BucketName-APPID`
copyRequest.sourceBucket = "sourcebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
copyRequest.sourceObject = "sourceObject";

// Source file APPID
copyRequest.sourceAPPID = "1250000000";

// Source file’s region
copyRequest.sourceRegion = "COS_REGION";

copyRequest.setFinish { (copyResult, error) in
    if let copyResult = copyResult {
        // Etag of the file
        let eTag = copyResult.eTag
    } else {
        print(error!);
    }
    
}
// Note that for cross-region replication, the region used for `transferManager` must be the region of the destination bucket
QCloudCOSTransferMangerService.defaultCOSTransferManager().copyObject(copyRequest);

// Cancel copy
// To cancel the copy operation, call `cancel`
copyRequest.cancel();
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferCopyObject.swift).

## Simple Operations

### Uploading an object using simple upload

#### API description 

This API is used to upload an object to a specified bucket. This operation requires the requester to have WRITE permission for the bucket and can upload a file of up to 5 GB in size. To upload larger objects, please use [Multipart Upload](#.E5.88.86.E5.9D.97.E6.93.8D.E4.BD.9C) or [the advanced upload API](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89).

> !
> 1. The Key (file name) cannot end with `/`; otherwise, it will be identified as a folder.
> 2. Each root account (APPID) can have up to 1,000 bucket ACLs and an unlimited number of object ACLs. If you do not need ACL control over an object, please leave it to the default option of inheriting bucket permissions.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-put-object)
```objective-c
QCloudPutObjectRequest* put = [QCloudPutObjectRequest new];

// Bucket name in the format: `BucketName-APPID`
put.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
put.object = @"exampleobject";

// Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` format
put.body =  [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];

[put setFinishBlock:^(id outputObject, NSError *error) {
    // `outputObject` contains all the HTTP response headers
    NSDictionary* info = (NSDictionary *) outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML] PutObject:put];
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PutObject.m).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

**Swift**

[//]: # (.cssg-snippet-put-object)
```swift
let putObject = QCloudPutObjectRequest<AnyObject>.init();

// Bucket name in the format: `BucketName-APPID`
putObject.bucket = "examplebucket-1250000000";
// Content of the object to be uploaded. You can pass in variables in `NSData*` or `NSURL*` format
let dataBody:NSData? = "wrwrwrwrwrw".data(using: .utf8) as NSData?;
putObject.body =  dataBody!;

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
putObject.object = "exampleobject";
putObject.finishBlock = {(result,error) in
    if let result = result {
        // “result” contains response headers
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().putObject(putObject);
```

>?
>- For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PutObject.swift).
>- You can generate a download URL for the uploaded file using the same key. For detailed directions, see [Generating a Pre-Signed Link](https://intl.cloud.tencent.com/document/product/436/37680). Please note that for private-read files, the download URL is only valid for a limited period of time.

### Copying an object (modifying object attributes)

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

// Indicate whether to copy metadata. Enumerated values: Copy (default), Replaced
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as `Replaced`
request.metadataDirective = @"Copy";

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 bucket ACLs. If you do not need ACL control over an object, specify `default` for this parameter,
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
request.accessControlList = @"default";

//The path to the source object
request.objectCopySource =
@"sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// Specify the `versionID` of the source file. This parameter is only relevant for buckets where versioning is enabled or suspended
request.versionID = @"objectVersion1";

[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    //“result” contains the request result
 
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/CopyObject.m).

**Swift**

[//]: # (.cssg-snippet-copy-object)
```swift
let putObjectCopy = QCloudPutObjectCopyRequest.init();

// Bucket name in the format: `BucketName-APPID`
putObjectCopy.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
putObjectCopy.object = "exampleobject";

//The path to the source object
putObjectCopy.objectCopySource = "sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// Indicate whether to copy metadata. Enumerated values: Copy (default), Replaced
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as `Replaced`
putObjectCopy.metadataDirective = "Copy";

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 bucket ACLs. If you do not need ACL control over an object, specify `default` for this parameter,
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
putObjectCopy.accessControlList = "default";

// Specify the `versionID` of the source file. This parameter is only relevant for buckets where versioning is enabled or suspended
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

[//]: # (.cssg-snippet-copy-object-replaced)
```objective-c
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Indicate whether to copy metadata. Enumerated values: Copy (default), Replaced
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as `Replaced`
request.metadataDirective = @"Replaced";

// Modify the metadata
[request.customHeaders setValue:@"newValue" forKey:@"x-cos-meta-*"];

// Object storage class. For enumerate values, such as
// `STANDARD_IA`, and `ARCHIVE`, please see the Storage Class documentation. This header will be returned only if the storage class of the object is not `STANDARD`
// Modify the storage class
[request.customHeaders setValue:@"newValue" forKey:@"x-cos-storage-class"];

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 bucket ACLs. If you do not need ACL control over an object, specify `default` for this parameter,
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
// Modify the ACL
request.accessControlList = @"private";

//The path to the source object
request.objectCopySource =
    @"sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// Specify the `versionID` of the source file. This parameter is only relevant for buckets where versioning is enabled or suspended
request.versionID = @"objectVersion1";

[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    //“result” contains the request result
    
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/CopyObject.m).

**Swift**

[//]: # (.cssg-snippet-copy-object-replaced)
```swift
let request : QCloudPutObjectCopyRequest  = QCloudPutObjectCopyRequest();

// Bucket name in the format: `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = "exampleobject";

// Indicate whether to copy metadata. Enumerated values: Copy (default), Replaced
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as `Replaced`
request.metadataDirective = "Replaced";

// Modify the metadata
request.customHeaders.setValue("newValue", forKey: "x-cos-meta-*");

// Object storage class. For enumerate values, such as
// `STANDARD_IA`, and `ARCHIVE`, please see the Storage Class documentation. This header will be returned only if the storage class of the object is not `STANDARD`
// Modify the storage class
request.customHeaders.setValue("newValue", forKey: "x-cos-storage-class");

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 bucket ACLs. If you do not need ACL control over an object, specify `default` for this parameter,
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
// Modify the ACL
request.accessControlList = "Source file ACL";
//The path to the source object
request.objectCopySource = "sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// Specify the `versionID` of the source file. This parameter is only relevant for buckets where versioning is enabled or suspended
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

[//]: # (.cssg-snippet-modify-object-metadata)
```objective-c
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Indicate whether to copy metadata. Enumerated values: Copy (default), Replaced
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), it must be specified as `Replaced`
request.metadataDirective = @"Replaced";

// Custom headers
[request.customHeaders setValue:@"newValue" forKey:@"x-cos-meta-*"];

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 bucket ACLs. If you do not need ACL control over an object, specify `default` for this parameter,
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
request.accessControlList = @"default";
//The path to the source object
request.objectCopySource =
    @"examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    //“result” contains the request result
    
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ModifyObjectProperty.m).

**Swift**

[//]: # (.cssg-snippet-modify-object-metadata)
```swift
let request : QCloudPutObjectCopyRequest = QCloudPutObjectCopyRequest();

// Bucket name in the format: `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = "exampleobject";

// Indicate whether to copy metadata. Enumerated values: Copy (default), Replaced
// If this field is specified as `Copy`, the user-defined metadata in the header will be ignored and the object will be copied directly
// If it is specified as `Replaced`, the metadata will be modified based on the header information. If the destination path is the same as the source path
// (i.e., when you want to modify the metadata), it must be specified as `Replaced`
request.metadataDirective = "Replaced";

// Custom headers
request.customHeaders.setValue("newValue", forKey: "x-cos-meta-*")

// Define the ACL attribute of the object. Valid values: private, public-read, default.
// Default value: default (i.e., the object will inherit the bucket's permissions).
// Note: currently, you can configure up to 1,000 bucket ACLs. If you do not need ACL control over an object, specify `default` for this parameter,
// or simply leave it blank, and the object will inherit the permissions of the bucket by default.
request.accessControlList = "default";

//The path to the source object
request.objectCopySource =
    "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

request.setFinish { (result, error) in
    if let result = result {
        // Generate Etag for the destination object
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

[//]: # (.cssg-snippet-modify-object-storage-class)
```objective-c
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];

// Bucket name in the format: `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Object storage class. For enumerate values, such as
// `STANDARD_IA`, and `ARCHIVE`, please see the Storage Class documentation. This header will be returned only if the storage class of the object is not `STANDARD`
[request.customHeaders setValue:@"ARCHIVE" forKey:@"x-cos-storage-class"];

//The path to the source object
request.objectCopySource =
    @"examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

// Specify the `versionID` of the source file. This parameter is only relevant for buckets where versioning is enabled or suspended
request.versionID = @"";

[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result,
                          NSError * _Nonnull error) {
    //“result” contains the request result
   
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ModifyObjectProperty.m).

**Swift**

[//]: # (.cssg-snippet-modify-object-storage-class)
```swift
let request : QCloudPutObjectCopyRequest = QCloudPutObjectCopyRequest();

// Bucket name in the format: `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = "exampleobject";

// Object storage class. For enumerate values, such as
// `STANDARD_IA`, and `ARCHIVE`, please see the Storage Class documentation. This header will be returned only if the storage class of the object is not `STANDARD`
request.customHeaders.setValue("newValue", forKey: "x-cos-storage-class");
//The path to the source object
request.objectCopySource =
    "examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject";

request.setFinish { (result, error) in
    if let result = result {
        // Generate Etag for the destination object
        let eTag = result.eTag
    } else {
        print(error!);
    }
}

QCloudCOSXMLService.defaultCOSXML().putObjectCopy(request);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/ModifyObjectProperty.swift).

## Multipart Operations

The multipart operation process is outlined below.

#### How to perform a multipart upload/replication

1. Initialize the multipart upload with `Initiate Multipart Upload` and get the `UploadId`.
2. Use the `UploadId` to upload parts with `Upload Part` or copy parts with `Upload Part Copy`
3. Complete the multipart upload with `Complete Multipart Upload`.

#### How to resume a multipart upload/replication

1. If you did not record the `UploadId` of a multipart upload, you can query the multipart upload with `List Multipart Uploads` to get it.
2. Use the `UploadId` to list the uploaded parts with `List Parts`.
3. Use the `UploadId` to upload the remaining parts with `Upload Part` or copy the remaining parts with `Upload Part Copy`.
4. Complete the multipart upload with `Complete Multipart Upload`.

#### How to abort a multipart upload/replication

1. If you did not record the `UploadId` of a multipart upload, you can query the multipart upload with `List Multipart Uploads` to get it.
2. Abort the multipart upload and delete the uploaded parts with `Abort Multipart Upload`.

### Querying multipart uploads

#### API description 

This API is used to query in-progress multipart uploads in a specified bucket.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-list-multi-upload)
```objective-c
QCloudListBucketMultipartUploadsRequest* uploads = [QCloudListBucketMultipartUploadsRequest new];

// Bucket name in the format: `BucketName-APPID`
uploads.bucket = @"examplebucket-1250000000";

// Set the maximum number of multipart uploads to return. Value range: 1-1000
uploads.maxUploads = 100;

[uploads setFinishBlock:^(QCloudListMultipartUploadsResult* result,
                          NSError *error) {
    // “result” returns the information on in-progress multipart uploads
    // Object for which the in-progress multipart upload is performed
    NSArray<QCloudListMultipartUploadContent*> *uploads = result.uploads;
}];

[[QCloudCOSXMLService defaultCOSXML] ListBucketMultipartUploads:uploads];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # (.cssg-snippet-list-multi-upload)
```swift
let listParts = QCloudListBucketMultipartUploadsRequest.init();

// Bucket name in the format: `BucketName-APPID`
listParts.bucket = "examplebucket-1250000000";

// Set the maximum number of multiparts to be returned. Valid value: 1–1000
listParts.maxUploads = 100;

listParts.setFinish { (result, error) in
    if let result = result {
        // List all incomplete multipart uploads
        let uploads = result.uploads;
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().listBucketMultipartUploads(listParts);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Initializing a multipart upload

#### API description 

This API is used to initialize a multipart upload, and gets its uploadId.

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

// Define the ACL attribute of the object. Valid values: private (default), public-read-write, public-read
initRequest.accessControlList = @"public";

// Grant read permission
initRequest.grantRead = @"grantRead";

// Grant write permission
initRequest.grantWrite = @"grantWrite";

// Grant read and write permission; grantFullControl = grantWrite + grantRead
initRequest.grantFullControl = @"grantFullControl";

[initRequest setFinishBlock:^(QCloudInitiateMultipartUploadResult* outputObject,
                              NSError *error) {
    // Get `uploadId` of the multipart upload for use in subsequent part uploads
    self->uploadId = outputObject.uploadId;
    
}];

[[QCloudCOSXMLService defaultCOSXML] InitiateMultipartUpload:initRequest];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # (.cssg-snippet-init-multi-upload)
```swift
let initRequest = QCloudInitiateMultipartUploadRequest.init();

// Bucket name in the format: `BucketName-APPID`
initRequest.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
initRequest.object = "exampleobject";

initRequest.setFinish { (result, error) in
    if let result = result {
        // Get `uploadId` of the multipart upload for use in subsequent part uploads
        self.uploadId = result.uploadId;
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().initiateMultipartUpload(initRequest);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Upload a part

This API is used to upload parts in a multipart upload.

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

// uploadId that identifies the multipart upload. It was returned by calling the “Initiate Multipart Upload” API
request.uploadId = uploadId;

// Data to upload must follow one of the three formats: NSData*, NSURL (local URL) and QCloudFileOffsetBody*
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
    // Get Etag of the uploaded part
    part.eTag = outputObject.eTag;
    part.partNumber = @"1";
    // Save it for use in completing the upload
    self.parts = @[part];

}];

[[QCloudCOSXMLService defaultCOSXML]  UploadPart:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # (.cssg-snippet-upload-part)
```swift
let uploadPart = QCloudUploadPartRequest<AnyObject>.init();

// Bucket name in the format: `BucketName-APPID`
uploadPart.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
uploadPart.object = "exampleobject";
uploadPart.partNumber = 1;

// ID of the multipart upload
if let uploadId = self.uploadId {
    uploadPart.uploadId = uploadId;
}

// Example file
let dataBody:NSData? = "wrwrwrwrwrwwrwrwrwrwrwwwrwrw"
    .data(using: .utf8) as NSData?;

uploadPart.body = dataBody!;
uploadPart.setFinish { (result, error) in
    if let result = result {
        let mutipartInfo = QCloudMultipartInfo.init();
        // Get Etag of the part
        mutipartInfo.eTag = result.eTag;
        mutipartInfo.partNumber = "1";
        // Save it for use in completing the upload
        self.parts = [mutipartInfo];
    } else {
        print(error!);
    }
}
uploadPart.sendProcessBlock = {(bytesSent,totalBytesSent,
                                totalBytesExpectedToSend) in
    // Upload progress
    // bytesSent                   Number of new bytes sent
    // totalBytesSent              Total number of bytes sent in the upload
    // totalBytesExpectedToSend    Target number of bytes expected to be sent in the upload
    
}
QCloudCOSXMLService.defaultCOSXML().uploadPart(uploadPart);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Copying a part

#### API description 

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

// URL of the source file. An object version can be specified by using the `versionid` subresource
request.source = @"sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";

// uploadId that the Initiate Multipart Upload request returned to uniquely identify the upload
request.uploadID = uploadId;

// Number that identifies the part
request.partNumber = 1;

[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    QCloudMultipartInfo *part = [QCloudMultipartInfo new];
    
    // Get Etag of the copied part
    part.eTag = result.eTag;
    part.partNumber = @"1";
    // Save it for use in completing the upload
    self.parts=@[part];
    
}];

[[QCloudCOSXMLService defaultCOSXML]UploadPartCopy:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MultiPartsCopyObject.m).

**Swift**

[//]: # (.cssg-snippet-upload-part-copy)
```swift
let req = QCloudUploadPartCopyRequest.init();

// Bucket name in the format: `BucketName-APPID`
req.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
req.object = "exampleobject";

// URL of the source file. An object version can be specified by using the `versionid` subresource
req.source = "sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject";
// uploadId that the Initiate Multipart Upload request returned to uniquely identify the upload
if let uploadId = self.uploadId {
    req.uploadID = uploadId;
}

// Number that identifies the part
req.partNumber = 1;
req.setFinish { (result, error) in
    if let result = result {
        let mutipartInfo = QCloudMultipartInfo.init();
        // Get Etag of the copied part
        mutipartInfo.eTag = result.eTag;
        mutipartInfo.partNumber = "1";
        // Save it for use in completing the upload
        self.parts = [mutipartInfo];
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().uploadPartCopy(req);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/MultiPartsCopyObject.swift).

### Querying uploaded parts

#### API description 

This API is used to query the uploaded parts of a specific multipart upload.

#### Sample code
**Objective-C**

[//]: # (.cssg-snippet-list-parts)
```objective-c
QCloudListMultipartRequest* request = [QCloudListMultipartRequest new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
request.object = @"exampleobject";

// Bucket name in the format: BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// uploadId that the Initiate Multipart Upload request returned to uniquely identify the upload
request.uploadId = uploadId;

[request setFinishBlock:^(QCloudListPartsResult * _Nonnull result,
                          NSError * _Nonnull error) {
    
    // “result” returns information on uploaded parts
    // Information on each part
    NSArray<QCloudMultipartUploadPart*> *parts = result.parts;
}];

[[QCloudCOSXMLService defaultCOSXML] ListMultipart:request];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**

[//]: # (.cssg-snippet-list-parts)
```swift
let req = QCloudListMultipartRequest.init();

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
req.object = "exampleobject";

// Bucket name in the format: `BucketName-APPID`
req.bucket = "examplebucket-1250000000";

// uploadId that the Initiate Multipart Upload request returned to uniquely identify the upload
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

### Completing a multipart upload

#### API description 

This API is used to complete the multipart upload of an entire file.

#### Sample code
**Objective-C**
[//]: # (.cssg-snippet-complete-multi-upload)
```objective-c
QCloudCompleteMultipartUploadRequest *completeRequst = [QCloudCompleteMultipartUploadRequest new];

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
completeRequst.object = @"exampleobject";

// Bucket name in the format: `BucketName-APPID`
completeRequst.bucket = @"examplebucket-1250000000";

// `uploadId` of the multipart upload, which can be obtained from `QCloudInitiateMultipartUploadResult`, the result of the Initiate Multipart Upload request
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
    // “result” returns the upload result
}];

[[QCloudCOSXMLService defaultCOSXML] CompleteMultipartUpload:completeRequst];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/MultiPartsUploadObject.m).

**Swift**
[//]: # (.cssg-snippet-complete-multi-upload)
```swift
let  complete = QCloudCompleteMultipartUploadRequest.init();

// Bucket name in the format: `BucketName-APPID`
complete.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
complete.object = "exampleobject";

// `uploadId` of the multipart upload, which can be obtained from
// `QCloudInitiateMultipartUploadResult`, the result of the Initiate Multipart Upload request
complete.uploadId = "exampleUploadId";
if let uploadId = self.uploadId {
    complete.uploadId = uploadId;
}

// Information on the uploaded parts
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
    if let result = result {
        // Etag of the file
        let eTag = result.eTag
        // Unsigned file URL
        let location = result.location
    } else {
        print(error!);
    }
}
QCloudCOSXMLService.defaultCOSXML().completeMultipartUpload(complete);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/MultiPartsUploadObject.swift).

### Aborting a multipart upload

#### API description 

This API is used to abort a multipart upload and delete the uploaded parts.

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
// This ID can be obtained from `QCloudInitiateMultipartUploadResult`, i.e. the result of the Initiate Multipart Upload request
abortRequest.uploadId = @"exampleUploadId";

[abortRequest setFinishBlock:^(id outputObject, NSError *error) {
    // outputObject returns information such as the Etag or custom headers in the response 
    NSDictionary * result = (NSDictionary *)outputObject;
}];

[[QCloudCOSXMLService defaultCOSXML]AbortMultipfartUpload:abortRequest];
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/AbortMultiPartsUpload.m).

**Swift**

[//]: # (.cssg-snippet-abort-multi-upload)
```swift
let abort = QCloudAbortMultipfartUploadRequest.init();

// Bucket name in the format: `BucketName-APPID`
abort.bucket = "examplebucket-1250000000";

// Object key, i.e. the full path of a COS object. If the object is in a directory, the path should be "dir1/object1"
abort.object = "exampleobject";

// `uploadId` of the multipart upload to be queried. This ID can be obtained from
// `QCloudInitiateMultipartUploadResult`, i.e. the result of the Initiate Multipart Upload request
abort.uploadId = self.uploadId!;

abort.finishBlock = {(result,error)in
    if let result = result {
        // “result” obtains headers returned by the browser
    } else {
        print(error!)
    }
}
QCloudCOSXMLService.defaultCOSXML().abortMultipfartUpload(abort);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/AbortMultiPartsUpload.swift).

