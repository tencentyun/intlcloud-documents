## Introduction

This document provides an overview of APIs and SDK code samples related to simple operations, multipart upload operations, and other operations on objects.

- We assume you have completed SDK download, installation, and initialization as described in [Getting Started](https://intl.cloud.tencent.com/document/product/436/8629).
We recommend you use Control+F to find the desired API, view our API description, copy the examples and run them in your project.

>If you need more features, or do not understand what the returned parameters mean, we recommend you view the comments in the code using three finger drag, Force-touch, or hovering over the variable and pressing Control+Command+D.   

**Simple Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket（List Object）](https://cloud.tencent.com/document/product/436/7734) | Querying object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
| [HEAD Object](https://cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [Options Object](https://cloud.tencent.com/document/product/436/8288) | CORS configuration for a pre-flight request | You can initiate a pre-flight request to determine whether a real request for COS can be sent |
| [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to a destination path |
| [DELETE Object](https://cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects in a single request |

**Multipart Upload Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Advanced APIs (Recommended)

This section encapsulates advanced APIs for uploading and copying. The user only needs to set the corresponding parameters. The APIs will decide internally whether to perform simple upload/copy or multipart upload/copy based on the file size. Before using the API, make sure you have completed initialization as instructed in [Getting Started](https://intl.cloud.tencent.com/document/product/436/8629).

### Uploading an object

Refer to [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/8629#.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1) in Getting Started.

### Resuming upload from breakpoint

> Resume upload from breakpoint only supports uploading files in the sandbox.

Multipart upload is used to upload a file larger than 1 MB. That is, split the file into multiple parts with each holding a size of 1 MB, and then upload these parts (4 at most) in parallel. Resuming upload from breakpoint is implemented on the basis that the uploaded parts are stored in the backend server.  

During multipart upload, resumeData for resuming upload is generated after you initialize multipart upload or cancel the upload. This is used to generate another upload request for resuming upload. The following example shows how to get ResumeData:


Objective-C code sample:

[//]: # (.cssg-snippet-objc-transfer-upload-object)
```objective-c
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
put.object = @"exampleobject";
put.bucket = @"examplebucket-1250000000";
put.body = [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];
// Set some upload parameters
put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult,
    QCloudCOSXMLUploadObjectResumeData resumeData) {
    // This block will be called back after the initial multipart upload is complete, so you can get resumeData,
    // and can generate a multipart upload request via resumeData
    QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest
        requestWithRequestData:resumeData];
};
[put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent,
    int64_t totalBytesExpectedToSend) {
    NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent,
        totalBytesExpectedToSend);
}];
[put setFinishBlock:^(QCloudUploadObjectResult *result, NSError* error) {
    // You can get the result from result
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
// Discard a multipart upload and delete uploaded parts
[put abort:^(id outputObject, NSError *error) {
//
}];

//···When initialization is completed and upload is not completed
NSError* error;
//The following shows how resumeData is generated after the user cancels the upload
QCloudCOSXMLUploadObjectResumeData resumeData = [put cancelByProductingResumeData:&error];
QCloudCOSXMLUploadObjectRequest* request = nil;
if (resumeData) {
    request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
}
//The generated request for resuming upload can be directly uploaded
[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-transfer-upload-object)
```swift
let uploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init();
let dataBody:NSData? = "wrwrwrwrwrw".data(using: .utf8) as NSData?;
uploadRequest.body = dataBody!;
uploadRequest.bucket = "examplebucket-1250000000";
uploadRequest.object = "exampleobject";
// Set upload parameters
uploadRequest.initMultipleUploadFinishBlock = {(multipleUploadInitResult,resumeData) in
    // This block will be called back after the initial multipart upload is completed, so you can get resumeData and generate a multipart upload request through resumeData
    let resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumeData as Data?);
}
uploadRequest.sendProcessBlock = {(bytesSent , totalBytesSent , totalBytesExpectedToSend) in
    
}
uploadRequest.setFinish { (result, error) in
    if error != nil{
        print(error!)
    }else{
        // Get the result of the request from result
        print(result!);
    }}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(uploadRequest);

//···When initialization is completed and upload is not completed
var error:NSError?;
    //The following shows how resumeData is generated after the user cancels the upload
do {
    let resumedData = try uploadRequest.cancel(byProductingResumeData: &error);
        var resumeUploadRequest:QCloudCOSXMLUploadObjectRequest<AnyObject>;
             resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumedData as Data?);
             //The generated request for resuming upload can be directly uploaded
    if resumeUploadRequest != nil {
        QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(resumeUploadRequest!);
    }
             
} catch  {
    print("resumeData is blank");
    return;
}
```

Note: The multipart upload uses the serial mode where parts must be uploaded in sequence. Under the following circumstances, resuming upload from breakpoint cannot be used.

-The uploaded object is less than 1MB, and no multipart upload is performed.
- The simple upload API rather than the QCloudCOSXMLUploadObjectRequest class is used to upload files.
- Multipart upload initialization is not completed (the callback for completed upload initialization is yet to be called) when you cancel the generation of resumeData.

### Downloading an object

Refer to [Downloading an Object](https://intl.cloud.tencent.com/document/product/436/8629#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1) in Getting Started.

- Replicating oibjects

#### Notes

Initialize a QCloudCOSXMLCopyObjectRequest object, and then call CopyObject of QCloudCOSTransferMangerService. Note that multipart copy is automatically used for large files, but users will not be aware of this process.  

> !For cross-origin replication, the region of transferManager must be the same as that of the bucket.

#### QCloudCOSXMLUploadObjectRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | --------------------- | ---- |
| bucket | Bucket name, format is &lt;BucketName-APPID&gt;,<br>such as examplebucket-1250000000 | NSString * | Yes |
| sourceBucket | Bucket of the copied source file | NSString * | Yes |
| sourceObject | Object name of the copied source file, key | NSString * | Yes |
| sourceAPPID | APPID of the copied source file | NSString * | Yes |
| sourceRegion | Region of the copied source file | NSString | Yes |
| MetadataDirective | Whether to copy the metadata. Enumerated values: `Copy`, `Replaced`. Default value: `Copy`. If its value is `Copy`, the user metadata in the corresponding header will be ignored and the copy will be performed; if its value is `Replaced`, the metadata will be replaced by the information in the corresponding header. **If the destination path is the same as the source path, which means you want to modify the metadata, you must specify this parameter as `Replaced`** | String | No |
| storageClass | Object storage class. Enumerated values:<br><li>STANDARD（QCloudCOSStorageStandard）<br><li>STANDARD_IA（QCloudCOSStorageStandardIA）<br>Default value: STANDARD（QCloudCOSStorageStandard） | QCloudCOSStorageClass | No |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-transfer-copy-object)
```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];

request.bucket = @ "examplebucket-1250000000"; // Destination <BucketName-APPID>, need to be public read or have permission in the current account
request.object = @"exampleobject";// Destination file name
File source bucket. Public read or access to the current account is required
request.sourceBucket = @"sourcebucket-1250000000";
request.sourceObject = @"sourceObject";// Source file name
request.sourceAPPID = @"1250000000";// Source file APPID
request.sourceRegion= @"COS_REGION";// Source region

[put setFinishBlock:^(QCloudUploadObjectResult* result, NSError* error) {
    // You can get etag or custom header information in response from outputObject
}];

> !For cross-origin replication, the region of transferManager must be the same as that of the bucket.
[[QCloudCOSTransferMangerService defaultCOSTransferManager] CopyObject:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-transfer-copy-object)
```swift
let copyRequest =  QCloudCOSXMLCopyObjectRequest.init();
copyRequest.bucket = "examplebucket-1250000000";// Destination<BucketName-APPID>, need to be public read or have permission in the current account
copyRequest.object = "exampleobject";// Destination file name
File source bucket. Public read or access to the current account is required
copyRequest.sourceBucket = "sourcebucket-1250000000";
copyRequest.sourceObject = "sourceObject";// Source file name
copyRequest.sourceAPPID = "1250000000";// Source file APPID
copyRequest.sourceRegion = "COS_REGION";// Source region
copyRequest.setFinish { (copyResult, error) in
    if error != nil{
        print(error!);
    }else{
        print(copyResult!);
    }
}
> !For cross-origin replication, the region of transferManager must be the same as that of the bucket.
QCloudCOSTransferMangerService.defaultCOSTransferManager().copyObject(copyRequest);
```

## Simple Operations

### Querying the object list

#### Feature

This API (GET Bucket (List Object)) is used to query some or all objects in a bucket.

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before bucket operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudGetBucketRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:

1. Instantiate QCloudGetBucketRequest and enter the required parameters.    
2. Call the GetBucket method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content from QCloudListBucketResult in finishBlock of callback.   

#### QCloudGetBucketRequest parameters

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| prefix | Prefix match, used to specify the prefix address of the returned file. | NSString * | No |
| delimiter | Delimiter is a sign. If Prefix exists, the same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix, and then all Common Prefixes are listed. If Prefix does not exist, the listing process starts from the beginning of the path. It can be considered as an ending symbol. For example, if you want a string to end with A, set delimiter to A. | NSString * | No |
| encodingType | Indicates the encoding method of the returned value. Available value: url | NSString * | No |
| marker | Entries are listed using UTF-8 binary order by default, starting from marker | NSString * | No |
| maxKeys | Maximum number of entries returned at a time. Default is 1000. | int | No |

#### Returned Result

QCloudListBucketResult parameters

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | -------------------------------- |
| name | Bucket name information | NSString * |
| prefix | Prefix match, used to specify the prefix address of the returned file. | NSString * | No |
| marker | Entries are listed using UTF-8 binary order by default, starting from marker | NSString * | No |
| - NextMarker | If the returned list is truncated, the `NextMarker` returned will be the starting point of the subsequent list | String |
| maxKeys | Maximum number of entries in returned results in a single response request | int |
| delimiter | Delimiter is a sign. If Prefix exists, the same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix, and then all Common Prefixes are listed. If Prefix does not exist, the listing process starts from the beginning of the path | NSString * |
| isTruncated | Whether the response request entry is truncated | BOOL |
| contents | Information for each object | NSArray<QCloudBucketContents*> * |
| - CommonPrefixes | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | ObjectArray |

QCloudBucketContents parameters

| Parameter Name | Description | Type |
| ------------ | --------------------------------------------------------- | ------------------------ |
| key | Object Key | NSString * |
| lastModified | Indicates when the object is last modified | NSString * |
| - - ETag | MD5 checksum of a part | String |
| size | File size, unit is byte | int |
| owner | Bucket owner information | QCloudBucketOwner * |
| storageClass | Object storage class. Enumerated values: STANDARD，STANDARD_IA，ARCHIVE | QCloudCOSStorageClass  * |

QCloudBucketOwner parameters

| Parameter Name | Description | Type |
| ----------- | ------------------- | ---------- |
| identifier  | Bucket APPID | NSString * |
| - - DisplayName | Object owner name | String |



QCloudCommonPrefixes parameters

| Parameter Name | Description | Type |
| -------- | ------------------ | ---------- |
| - - Prefix | A single common prefix | String |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-get-bucket)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
request.bucket = @"examplebucket-1250000000";
request.maxKeys = 1000;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    // result returns specific information
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-get-bucket)
```swift
let getBucketReq = QCloudGetBucketRequest.init();
getBucketReq.bucket = "examplebucket-1250000000";
getBucketReq.maxKeys = 1000;
getBucketReq.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print( result!.commonPrefixes);
    }}
QCloudCOSXMLService.defaultCOSXML().getBucket(getBucketReq);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### Uploading an object

#### Feature

Upload objects to the specified bucket (Put Object), simple upload is limited to small files (less than 20MB). Simple upload supports uploading files from memory.

> !The number of access policies is up to 1000. Do not set object ACL control when you upload an object if it is not required. The object inherits the bucket permissions by default.

#### QCloudPutObjectRequest parameters

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | --------------------- | ---- |
| Object | The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Overview](https://intl.cloud.tencent.com) | NSString * | Yes |
| bucket | Bucket name, format is &lt;BucketName-APPID&gt;, such as examplebucket-1250000000 | NSString * | Yes |
| body | If a file is stored in the disk, it is the path of the file to be uploaded, and you can enter a variable of NSURL * type. If a file is stored in memory, you can enter a variable of NSData * type that contains the file binary data. | BodyType | Yes |
| storageClass | Object storage class. Enumerated values: STANDARD（QCloudCOSStorageStandard），STANDARD_IA（QCloudCOSStorageStandardIA), ARCHIVE (QCloudCOSStorageARCHIVE). Default values: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |
| CacheControl | Cache policy as defined in RFC 2616, which will be stored in the object metadata | String | No |
| ContentDisposition | Filename as defined in RFC 2616, which will be stored in the object metadata | String | No |
| expect | When expect=@"100-Continue" is used, the request content will not be sent until the receipt of response from server. | NSString * | No |
| Expires | Expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| x-cos-acl | It defines the ACL attribute of the object. Value range: private, public-read, and default; default value: default (i.e., inheriting the bucket's permissions); <br>**Note:** Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, use "default" for this parameter or simply leave it blank, so that the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="[OwnerUin]"` | String | No |
| GrantWrite | Grants the grantee Write access in the format of `id="[OwnerUin]"` | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |

#### Samples    


Objective-C code sample:

[//]: # (.cssg-snippet-objc-put-object)
```objective-c
QCloudPutObjectRequest* put = [QCloudPutObjectRequest new];
put.object = @"exampleobject";
put.bucket = @"examplebucket-1250000000";
put.body =  [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];

[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get etag or custom header information in response from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] PutObject:put];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-put-object)
```swift
let putObject = QCloudPutObjectRequest<AnyObject>.init();
putObject.bucket = "examplebucket-1250000000";
let dataBody:NSData? = "wrwrwrwrwrw".data(using: .utf8) as NSData?;
putObject.body =  dataBody!;
putObject.object = "exampleobject";
putObject.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().putObject(putObject);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### Querying object metadata

#### Feature

This API (HEAD Object) is used to query object metadata.

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudHeadObjectRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudHeadObjectRequest and enter the required parameters.    
2. Call the HeadObject method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content from outputObject in finishBlock of callback.   

#### QCloudHeadObjectRequest parameters

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ---------- | ---- |
| Object | The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Overview](https://intl.cloud.tencent.com) | NSString * | Yes |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| ifModifiedSince | The file content is only returned if the file is modified after the specified time. Otherwise, 304 (not modified) is returned. | NSString * | Yes |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-head-object)
```objective-c
QCloudHeadObjectRequest* headerRequest = [QCloudHeadObjectRequest new];
headerRequest.object = @"exampleobject";
headerRequest.bucket = @"examplebucket-1250000000";

[headerRequest setFinishBlock:^(NSDictionary* result, NSError *error) {
    // result returns specific information
}];

[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```
Swift code sample:

[//]: # (.cssg-snippet-swift-head-object)
```swift
let headObject = QCloudHeadObjectRequest.init();
headObject.bucket = "examplebucket-1250000000";
headObject.object  = "exampleobject";
headObject.finishBlock =  {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().headObject(headObject);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### Downloading an object

#### Feature

This API is used to download an object locally.

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudOptionsObjectRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudHeadObjectRequest and enter the required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content from outputObject in finishBlock of callback.   

#### QCloudGetObjectACLRequest parameters

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| object | Object name | NSString * | Yes |
| range | The specified range of file download defined in RFC 2616 (in bytes) | NSString * | No |
| ifModifiedSince | The file content is only returned if the file is modified after the specified time. Otherwise, 304 (not modified) is returned. | NSString * | Yes |
| responseContentType | Sets the Content-Type parameter in the response header | NSString * | No |
| responseContentLanguage | Sets the Content-Language parameter in the response header | NSString * | No |
| responseContentExpires | Sets the Content-Expires parameter in the response header | NSString * | No |
| responseCacheControl | Sets the Cache-Control parameter in the response header | NSString * | No |
| responseContentDisposition | Sets the Content-Disposition parameter in the response header | NSString * | No |
| responseContentEncoding | Sets the Content-Encoding parameter in the response header | NSString * | No |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
// Set the URL for download. If it has been set, the file is downloaded to the specified path.
// If this parameter is not set, the file will be downloaded to memory and stored in the outputObject of finishBlock
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    // You can get etag or custom header information in response from outputObject
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload,
    int64_t totalBytesExpectedToDownload) {
    // Download Progress
}];

[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-get-object)
```swift
let getObject = QCloudGetObjectRequest.init();
getObject.bucket = "examplebucket-1250000000";
getObject.object = "exampleobject";
getObject.downloadingURL = URL.init(string: NSTemporaryDirectory())!.appendingPathComponent(getObject.object);
getObject.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }};
getObject.downProcessBlock = {(bytesDownload, totalBytesDownload,  totalBytesExpectedToDownload) in
    print("totalBytesDownload:\(totalBytesDownload) totalBytesExpectedToDownload:\(totalBytesExpectedToDownload)");
}
QCloudCOSXMLService.defaultCOSXML().getObject(getObject);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### Pre-requesting cross-origin configuration

#### Feature

Use pre-requests to confirm whether you can send cross-domain requests.

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudOptionsObjectRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudOptionsObjectRequest, enter the object name, the bucket name, the HTTP method of the simulate CORS request and the access sources allowed for the simulate CORS.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content from outputObject in finishBlock of callback.   

#### QCloudOptionsObjectRequest parameters

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | --------------------------- | ---- |
| Object | The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Overview](https://intl.cloud.tencent.com) | NSString * | Yes |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| accessControlRequestMethod | The HTTP method of the simulate CORS request | NSArray&lt;NSString`*`> * | Yes |
| origin | The access sources allowed for the simulate CORS. The wildcard "*" is supported. Format: protocol://domain name[:port], for example, `http://www.qq.com`. | NSString * | Yes |
| allowedHeader | It is used to notify the server about which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent. The wildcard "*" is supported. | NSArray&lt;NSString `*` > * | No |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-option-object)
```objective-c
QCloudOptionsObjectRequest* request = [[QCloudOptionsObjectRequest alloc] init];
request.bucket =@"examplebucket-1250000000";
request.origin = @"http://cloud.tencent.com";
request.accessControlRequestMethod = @"GET";
request.accessControlRequestHeaders = @"host";
request.object = @"exampleobject";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get etag or custom header information in response from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] OptionsObject:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-option-object)
```swift
let optionsObject = QCloudOptionsObjectRequest.init();
optionsObject.object = "exampleobject";
optionsObject.origin = "http://www.qcloud.com";
optionsObject.accessControlRequestMethod = "GET";
optionsObject.accessControlRequestHeaders = "origin";
optionsObject.bucket = "examplebucket-1250000000";
optionsObject.finishBlock = {(result,error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().optionsObject(optionsObject);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### Setting object replication

#### Feature

Copy the file to the destination path.

#### Request example


Objective-C code sample:

[//]: # (.cssg-snippet-objc-copy-object)
```Objective-C
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
request.object = @"exampleobject";
// The path where the source object is located
request.objectCopySource = @"sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject";
[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result, NSError * _Nonnull error) {
    // result returns specific information
}];
[[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-copy-object)
```swift
let putObjectCopy = QCloudPutObjectCopyRequest.init();
putObjectCopy.bucket = "examplebucket-1250000000";
putObjectCopy.object = "exampleobject";
putObjectCopy.objectCopySource = "sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject";
putObjectCopy.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().putObjectCopy(putObjectCopy);
```

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | --------------------- | ---- |
| bucket | Destination bucket name, format is &lt;BucketName-APPID&gt;,<br>such as examplebucket-1250000000 | NSString * | Yes |
| object | Object key of the destination file | NSString * | Yes |
| objectCopySource | The path of the copied source file | NSString * | Yes |
| MetadataDirective | Whether to copy the metadata. Enumerated values: `Copy`, `Replaced`. Default value: `Copy`. If its value is `Copy`, the user metadata in the corresponding header will be ignored and the copy will be performed; if its value is `Replaced`, the metadata will be replaced by the information in the corresponding header. **If the destination path is the same as the source path, which means you want to modify the metadata, you must specify this parameter as `Replaced`** | String | No |
| storageClass | Object storage class. Enumerated values:<br><li>STANDARD（QCloudCOSStorageStandard）<br><li>STANDARD_IA（QCloudCOSStorageStandardIA）<br>Default value: STANDARD（QCloudCOSStorageStandard） | QCloudCOSStorageClass | No |
| x-cos-acl | Defines the ACL attribute of the object. Value range: private, public-read, and default; default value: default (i.e., inheriting the bucket's permissions); <br>**Note:** Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, use "default" for this parameter or simply leave it blank, so that the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="[OwnerUin]"` | String | No |
| GrantWrite | Grants the grantee Write access in the format of `id="[OwnerUin]"` | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |
| versionID | Specifies the versionID of the source file. Only buckets that are opened or paused after opening will respond to this parameter. | NSString * | No |

#### Returned Result

Request result is returned through CopyObjectResult.

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ---------- |
| ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object content has changed | String |
| lastModified | Last modified time of the file, GMT format | NSString * |
| versionID | Version ID of the object (only when version control is enabled) | NSString * |

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### Deleting a single object

#### Feature

This API (Delete Object) is used to delete the specified object.

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudDeleteObjectRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudDeleteObjectRequest and enter the required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content from outputObject in finishBlock of callback.   

#### QCloudDeleteObjectRequest parameters

| Parameter Name | Type | Required | Description |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| Object | The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Overview](https://intl.cloud.tencent.com) | NSString * | Yes |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |

#### Samples


Objective-C code sample:


[//]: # (.cssg-snippet-objc-delete-object)
```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
deleteObjectRequest.bucket = @"examplebucket-1250000000";
deleteObjectRequest.object = @"exampleobject";

[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    // You can get etag or custom header information in response from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-delete-object)
```swift
let deleteObject = QCloudDeleteObjectRequest.init();
deleteObject.bucket = "examplebucket-1250000000";
deleteObject.object = "exampleobject";
deleteObject.finishBlock = {(result,error)in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().deleteObject(deleteObject);
```

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### Deleting multiple objects

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudDeleteMultipleObjectRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudDeleteMultipleObjectRequest, enter the required parameters, encapsulate the object you want to delete into a QCloudDeleteObjectInfo object, and place it in the objects array of deleteObjects.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content from outputObject in finishBlock of callback.   

#### QCloudDeleteMultipleObjectRequest parameters

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ------------------ | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| deleteObjects | Encapsulates information of multiple objects to be deleted in batches | QCloudDeleteInfo * | Yes |

#### QCloudDeleteInfo parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ----------------------------------------- | ---- |
| objects  | Array storing information about the object to be deleted | NSArray&lt;QCloudDeleteObjectInfo `*` > * | Yes |
Quiet | Boolean, this value determines whether to enable Quiet mode: <br> <li> true: Enable Quiet mode <br> <li> false: Enable Verbose mode <br>The default value is False | NSArray% encTxtlt; QCloudDeleteObjectInfo `*`> * | No |

#### QCloudDeleteObjectInfo parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| Object | The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Overview](https://intl.cloud.tencent.com) | NSString * | Yes |

#### Returned Result

QCloudDeleteResult parameters

| Parameter Name | Description | Type |
| -------------- | -------------------------------------------------- | --------------------------------- |
| deletedObjects | Array storing information about deleted objects | NSArray<QCloudDeleteResultRow*> * |
| lastModified | Last modified time of the file, GMT format | NSString * |
| versionID | Version ID of the object (only when version control is enabled) | NSString * |

QCloudDeleteResultRow parameters

| Parameter Name | Description | Type |
| -------- | --------------- | ---------- |
| key | Key of the deleted objects | NSString * |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-delete-multi-object)
```objective-c
QCloudDeleteMultipleObjectRequest* delteRequest = [QCloudDeleteMultipleObjectRequest new];
delteRequest.bucket = @"examplebucket-1250000000";

QCloudDeleteObjectInfo* deletedObject0 = [QCloudDeleteObjectInfo new];
deletedObject0.key = @"exampleobject";

QCloudDeleteInfo* deleteInfo = [QCloudDeleteInfo new];
deleteInfo.quiet = NO;
deleteInfo.objects = @[deletedObject0];
delteRequest.deleteObjects = deleteInfo;

[delteRequest setFinishBlock:^(QCloudDeleteResult* outputObject, NSError *error) {
    // You can get etag or custom header information in response from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-delete-multi-object)
```swift
let mutipleDel = QCloudDeleteMultipleObjectRequest.init();
mutipleDel.bucket = "examplebucket-1250000000";

let info1 = QCloudDeleteObjectInfo.init();
String key = "exampleobject";
let info2 = QCloudDeleteObjectInfo.init();


let deleteInfos = QCloudDeleteInfo.init();
deleteInfos.objects = [info1];
deleteInfos.quiet = false;
mutipleDel.deleteObjects = deleteInfos;

mutipleDel.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().deleteMultipleObject(mutipleDel);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

## Multipart Operations



- Multipart upload objects: Initializing multipart upload, uploading parts, and completing all multipart uploads
- Resuming the multipart upload: Querying the parts uploaded, uploading parts, and completing all multipart uploads
- Delete the part uploaded

### Querying multipart upload

#### Feature

This API is used to query in-progress multipart upload in the specified bucket.

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before bucket operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudListBucketMultipartUploadsRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudListBucketMultipartUploadsRequest and enter the required parameters, such as the prefix and the encoding method of the returned result.    
2. Call the ListBucketMultipartUploads method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content from outputObject in finishBlock of callback.   

#### QCloudListBucketMultipartUploadsRequest parameters

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| prefix | The returned Object key must be prefixed with Prefix. Note that the returned key will still contain Prefix when querying with prefix. | NSString * | No |
| delimiter | Delimiter is a sign. If Prefix exists, the same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix, and then all Common Prefixes are listed. If Prefix does not exist, the listing process starts from the beginning of the path. It can be considered as an ending symbol. For example, if you want a string to end with A, set delimiter to A. | NSString * | No |
| encodingType | Indicates the encoding method of the returned value. Available value: url | NSString * | No |
| keyMarker | Entries will be listed starting from this key value | NSString * | No |
| uploadIDMarker | Entries will be listed starting from this UploadId value | int | No |
| maxUploads | Sets the maximum number of multipart returned. Valid values: 1-1000 | int | No |

#### Returned Result

#### Parameters of returned result QCloudListMultipartUploadsResult

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ---------- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| prefix | The returned Object key must be prefixed with Prefix. Note that the returned key will still contain Prefix when querying with prefix. | NSString * |
| delimiter | Delimiter is a sign. If Prefix exists, the same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix, and then all Common Prefixes are listed. If Prefix does not exist, the listing process starts from the beginning of the path | NSString * |
| encodingType | Indicates the encoding method of the returned value. Available value: url | NSString * |
| keyMarker | Entries will be listed starting from this key value | NSString * |
| maxUploads | Sets the maximum number of multipart returned. Valid values: 1-1000 | int |
| uploads | Information of all multipart upload operations | NSArray* |
| isTruncated | Whether the file is truncated | NSString * |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-list-multi-upload)
```objecitve-c
QCloudListBucketMultipartUploadsRequest* uploads = [QCloudListBucketMultipartUploadsRequest new];
uploads.bucket = @"examplebucket-1250000000";
uploads.maxUploads = 100;

[uploads setFinishBlock:^(QCloudListMultipartUploadsResult* result, NSError *error) {
    // Can return block information from result
}];

[[QCloudCOSXMLService defaultCOSXML] ListBucketMultipartUploads:uploads];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-list-multi-upload)
```swift
let listParts = QCloudListBucketMultipartUploadsRequest.init();
listParts.bucket = "examplebucket-1250000000";
listParts.maxUploads = 100;
listParts.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().listBucketMultipartUploads(listParts);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem. Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.


### <span id = "INIT_MULIT_UPLOAD">Initializing multipart upload </span>

#### Feature

This API (Initiate Multipart Upload) is used to initialize multipart upload and obtain the corresponding uploadId.

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudInitiateMultipartUploadRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudInitiateMultipartUploadRequest and enter the required parameters.    
2. Call the InitiateMultipartUpload method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content in finishBlock callback.   

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | --------------------- | ---- |
| Object | The name of the file (object) to be uploaded, i.e. the key of the object. ObjectKey is the unique identifier of an object in a bucket. For example, in the object's access domain name "bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg", the key is "doc1/pic1.jpg". For more information, see [Object Overview](https://cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| cacheControl | Cache policy defined in RFC 2616 | NSString * | No |
| contentDisposition | File name defined in RFC 2616 | NSString * | No |
| expect | When `expect=@"100-continue"` is used, the request content will not be sent until the receipt of response from server. | NSString * | No |
| expires | Expiration time defined in RFC 2616 | NSString * | No |
| storageClass | Object storage class, enumerated values:<br><li>STANDARD(QCloudCOSStorageStandard)<br><li>STANDARD_IA(QCloudCOSStorageStandardIA)<br><li>ARCHIVE(QCloudCOSStorageARCHIVE)<br>Default values: STANDARD(QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |
| x-cos-acl | It defines the ACL attribute of the object. Value range: private, public-read, and default; default value: default (i.e., inheriting the bucket's permissions); <br>**Note:** Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, use "default" for this parameter or simply leave it blank, so that the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="[OwnerUin]"` | String | No |
| GrantWrite | Grants the grantee Write access in the format of `id="[OwnerUin]"` | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-init-multi-upload)
```objective-c
QCloudInitiateMultipartUploadRequest* initrequest = [QCloudInitiateMultipartUploadRequest new];
initrequest.bucket = @"examplebucket-1250000000";
initrequest.object = @"exampleobject";

[request setFinishBlock:^(QCloudUploadObjectResult* outputObject, NSError *error) {
    // Get the uploadId of the multipart upload. This ID is required for subsequent uploads. Please save it for future use.
    @"exampleUploadId" = outputObject.uploadId;
}];

[[QCloudCOSXMLService defaultCOSXML] InitiateMultipartUpload:initrequest];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-init-multi-upload)
```swift
let initRequest = QCloudInitiateMultipartUploadRequest.init();
initRequest.bucket = "examplebucket-1250000000";
initRequest.object = "exampleobject";
initRequest.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        // Get the uploadId of the multipart upload. This ID is required for subsequent uploads. Please save it for future use.
        self.uploadId = result!.uploadId;
        print(result!.uploadId);
    }}
QCloudCOSXMLService.defaultCOSXML().initiateMultipartUpload(initRequest);
```

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### Uploading Parts

#### Feature

### Multipart upload

#### QCloudUploadPartRequest parameters

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of this multipart upload. <br>When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file | String | Yes |
| partNumber  | A number which identifies this multipart upload                                       | String | Yes  |
| contentSHA1 | Sha1 value of this multipart upload | NSString * | Yes |
| body | Uploaded data: support `NSData *`, `NSURL` (local URL) and` QCloudFileOffsetBody * `three types | BodyType | Yes |

#### Returned Result

QCloudUploadPartResult parameters

| Parameter Name | Description | Type |
| -------- | ----------- | ---------- |
| eTag | File etag | NSString * |

#### Method Prototype

The specific steps for multipart upload request in COS iOS SDK are as follows:

1. Instantiate QCloudHeadObjectRequest and enter the required parameters.
2. Call the HeadObject method in the QCloudCOSXMLService object to initiate a request.
3. Obtain specific content from QCloudListBucketResult in finishBlock of callback.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-upload-part)
```objective-c
QCloudUploadPartRequest* request = [QCloudUploadPartRequest new];
request.bucket = @"examplebucket-1250000000";
request.object = @"exampleobject";
request.partNumber = 1;
// Identify the ID of this multipart upload; when you use Initiate Multipart Upload API to initialize the multipart upload, you will get an uploadId
// This ID not only uniquely identifies this data part, but also its relative position of in the entire file
request.uploadId = @"exampleUploadId";
// Uploaded data: supports NSData *, NSURL (local URL) and QCloudFileOffsetBody * three types
request.body = [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];

[request setSendProcessBlock:^(int64_t bytesSent,
                               int64_t totalBytesSent,
                               int64_t totalBytesExpectedToSend) {
    // Upload progress information
}];
[request setFinishBlock:^(QCloudUploadObjectResult* outputObject, NSError *error) {
    QCloudMultipartInfo *part = [QCloudMultipartInfo new];
    // Get the etag of the uploaded parts
    part.eTag = outputObject.eTag;
    part.partNumber = @"1";
    // Saved for use when upload is complete
    self.parts = @[part];
}];

[[QCloudCOSXMLService defaultCOSXML]  UploadPart:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-upload-part)
```swift

let uploadPart = QCloudUploadPartRequest<AnyObject>.init();
uploadPart.bucket = "examplebucket-1250000000";
uploadPart.object = "exampleobject";
uploadPart.partNumber = 1;
// Identify the ID of this multipart upload; when you use Initiate Multipart Upload API to initialize the multipart upload, you will get an uploadId
// This ID not only uniquely identifies this data part, but also its relative position of in the entire file
uploadPart.uploadId = "exampleUploadId";
if self.uploadId != nil {
     uploadPart.uploadId = self.uploadId!;
}

let dataBody:NSData? = "wrwrwrwrwrwwrwrwrwrwrwwrwrwrwrwrwwrwrwrwrwrwwrwrwrwrwrwwrwrwrwrwrwwrwrwrwrwrwwrwrwrwrwrwwrwrwrwrwrwwrwrwrwrwrwwrwrwrwrwrwwrwrwrwrwrwwrwrwrwrwrw".data(using: .utf8) as NSData?;
uploadPart.body = dataBody!;
uploadPart.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        let mutipartInfo = QCloudMultipartInfo.init();
        // Get the etag of the uploaded parts
        mutipartInfo.eTag = result!.eTag;
        mutipartInfo.partNumber = "1";
        // Saved for use when upload is complete
        self.parts = [mutipartInfo];
    }}
uploadPart.sendProcessBlock = {(bytesSent,totalBytesSent,totalBytesExpectedToSend) in
    // Upload progress information
    print("totalBytesSent:\(totalBytesSent) totalBytesExpectedToSend:\(totalBytesExpectedToSend)");
    
}
QCloudCOSXMLService.defaultCOSXML().uploadPart(uploadPart);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### Copying Parts

#### Feature

This API is used for multipart copy.

#### QCloudUploadPartRequest parameters

| Parameter Name | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of this multipart upload. <br>When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file | String | Yes |
| partNumber  | A number which identifies this multipart upload                                       | String | Yes  |
| CopySource | URL path to the source file. A historical version can be specified using the `versionId` subresource | String | Yes |
| body | Uploaded data: support `NSData *`, `NSURL` (local URL) and` QCloudFileOffsetBody * `three types | BodyType | Yes |

#### Returned Result

QCloudUploadPartResult parameters

| Parameter Name | Description | Type |
| -------- | ----------- | ---------- |
| eTag | File etag | NSString * |

#### Method Prototype

The specific steps for multipart upload request in COS iOS SDK are as follows:

1. Instantiate QCloudUploadPartCopyRequest and enter the required parameters.
2. Call the InitiateMultipartUpload method in the QCloudCOSXMLService object to initiate a request.
3. Obtain specific content from QCloudListBucketResult in finishBlock of callback.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-upload-part-copy)
```objective-c
QCloudUploadPartCopyRequest* request = [[QCloudUploadPartCopyRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
request.object = @"exampleobject";
// The path of source file URL. You can specify the history version with the versionid sub-resource
request.source = @"sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject";
// In the response of the initial multipart upload, a unique descriptor (upload ID) will be returned
request.uploadID = @"exampleUploadId";
request.partNumber = 1; // Mark the number of the current part

[put setFinishBlock:^(QCloudUploadObjectResult* result, NSError* error) {
    QCloudMultipartInfo *part = [QCloudMultipartInfo new];
    // Get the etag of the copied parts
    part.eTag = result.eTag;
    part.partNumber = @"1";
    // Saved for use when the upload is complete
    self.parts=@[part];
}];

[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-upload-part-copy)
```swift
let req = QCloudUploadPartCopyRequest.init();
req.bucket = "examplebucket-1250000000";
req.object = "exampleobject";
// The path of source file URL. You can specify the history version with the versionid sub-resource
req.source = "sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject";
// In the response of the initial multipart upload, a unique descriptor (upload ID) will be returned
req.uploadID = "exampleUploadId";
if self.uploadId != nil {
    req.uploadID = self.uploadId!;
}

// Mark the serial number of the current part
req.partNumber = 1;
req.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        let mutipartInfo = QCloudMultipartInfo.init();
        // Get the etag of the copied parts
        mutipartInfo.eTag = result!.eTag;
        mutipartInfo.partNumber = "1";
        self.parts = [mutipartInfo];
    }}
QCloudCOSXMLService.defaultCOSXML().uploadPartCopy(req);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### <span id = "LIST_MULIT_UPLOAD">Query uploaded parts</span>

#### Feature

This API (List Parts) is used to query the parts uploaded to the specified uploadId.

#### QCloudListMultipartRequest parameters

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | UploadId of the multipart upload to be quired | NSString * | Yes |
| MaxParts | Maximum number of entries returned at a time. Default value: 1,000 | String | No |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting from the marker | String | No |
| EncodingType | Specifies the encoding type of the returned value | String | No |

#### Returned Result

 QCloudListPartsResult parameters

| Parameter Name | Description | Type |
| ---------------- | ------------------------------------------------------------ | -------------------------- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| - Encoding-type | Specifies the encoding type of the returned value | String |
| key | Object Name | NSString * |
| uploadId | UploadId of the multipart upload queried this time | NSString * |
| storageClass | Storage class of an object | QCloudCOSStorageClass | Yes |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting from the marker | String |
| - NextPartNumberMarker | If the returned list is truncated, the `NextMarker` returned will be the starting point of the subsequent list | String |
| maxParts | Maximum number of entries returned at a time | QCloudCOSStorageClass |
| isTruncated | Whether the returned entry is truncated | BOOL |
| initiator | Identifies information about the initiator of this upload | NSString * |
| owner | Identifies information about owners of these parts | QCloudCOSStorageClass |
| parts | Represents information about each part | QCloudMultipartUploadPart* |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-list-parts)
```objective-c
QCloudListMultipartRequest* request = [QCloudListMultipartRequest new];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";
// In the response of the initial multipart upload, a unique descriptor (upload ID) will be returned
request.uploadId = @"exampleUploadId";

[request setFinishBlock:^(QCloudListPartsResult * _Nonnull result, NSError * _Nonnull error) {
    // Get information about uploaded parts from result
}];

[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-list-parts)
```swift
let req = QCloudListMultipartRequest.init();
req.object = "exampleobject";
req.bucket = "examplebucket-1250000000";
// In the response of the initial multipart upload, a unique descriptor (upload ID) will be returned
req.uploadId = "exampleUploadId";
if self.uploadId != nil {
    req.uploadId = self.uploadId!;
}
req.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        // Get information about uploaded multipart parts from result
        print(result!);
    }}

QCloudCOSXMLService.defaultCOSXML().listMultipart(req);
```

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### <span id = "COMPLETE_MULIT_UPLOAD"> Complete multipart upload </ span>

#### Feature

This API (Complete Multipart Upload) is used to complete the entire multipart upload.

#### QCloudCompleteMultipartUploadRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ----------------------------------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of this multipart upload. <br>When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file | String | Yes |
| parts | Completes information about multipart upload | QCloudCompleteMultipartUploadInfo * | Yes |

#### Returned Result

 QCloudUploadObjectResult parameters

| Parameter Name | Description | Type |
| --------- | ------------------------------------------------------------ | ---------- |
| location | Create an object's extranet access domain name | NSString * |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| key | Object Name | NSString * |
| eTag | MD5 algorithm checksum of the merged file | NSString * |
| versionID | Version ID of the object (only when version control is enabled) | NSString * |

#### Method Prototype

The specific steps for completing the entire multipart upload request in COS iOS SDK are as follows:

1. Instantiate QCloudInitiateMultipartUploadRequest and enter the required parameters.
2. Call the InitiateMultipartUpload method in the QCloudCOSXMLService object to initiate a request.
3. Obtain specific content from QCloudListBucketResult in finishBlock of callback.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-complete-multi-upload)
```objective-c
QCloudCompleteMultipartUploadRequest *completeRequst = [QCloudCompleteMultipartUploadRequest new];
completeRequst.object = @"exampleobject";
completeRequst.bucket = @"examplebucket-1250000000";
// The uploadId of the multipart upload to be queried this time can be obtained from the request result of the initial block upload QCloudInitiateMultipartUploadResult
completeRequst.uploadId = @"exampleUploadId";
// Information about uploaded parts
QCloudCompleteMultipartUploadInfo *partInfo = [QCloudCompleteMultipartUploadInfo new];
partInfo.parts = self.parts;
completeRequst.parts = partInfo;

[completeRequst setFinishBlock:^(QCloudUploadObjectResult * _Nonnull result, NSError * _Nonnull error) {
    // Get the upload result from result
}];

[[QCloudCOSXMLService defaultCOSXML] CompleteMultipartUpload:completeRequst];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-complete-multi-upload)
```swift
let  complete = QCloudCompleteMultipartUploadRequest.init();
complete.bucket = "examplebucket-1250000000";
complete.object = "exampleobject";
// The uploadId of the multipart upload to be queried this time can be obtained from the request result of the initial block upload QCloudInitiateMultipartUploadResult
complete.uploadId = "exampleUploadId";
if self.uploadId != nil {
    complete.uploadId = self.uploadId!;
}


// Information about uploaded parts
let completeInfo = QCloudCompleteMultipartUploadInfo.init();
if self.parts == nil {
    print ("parts that have not completed yet");
    return;
}

completeInfo.parts = self.parts!;
complete.parts = completeInfo;
complete.setFinish { (result, error) in
    if error != nil{
        print(error!)
    }else{
        // Get the upload result from result
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().completeMultipartUpload(complete);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### <span id = "ABORT_MULIT_UPLOAD"> Terminate a multipart upload </ span>

#### Feature

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### QCloudAbortMultipfartUploadRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of this multipart upload. <br>When the Initiate Multipart Upload API is used to initialize a multipart upload, an uploadId will be obtained, which not only uniquely identifies the data but also identifies the data position in the entire file | String | Yes |

#### Method Prototype

The specific steps for discarding a multipart upload in COS iOS SDK, and deleting the uploaded block request are as follows:

1. Instantiate QCloudInitiateMultipartUploadRequest and enter the required parameters.
2. Call the InitiateMultipartUpload method in the QCloudCOSXMLService object to initiate a request.
3. Obtain specific content from outputObject in finishBlock of callback.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-abort-multi-upload)
```objective-c
QCloudAbortMultipfartUploadRequest *abortRequest = [QCloudAbortMultipfartUploadRequest new];
abortRequest.object = @"exampleobject";
abortRequest.bucket = @"examplebucket-1250000000";
// The uploadId of the multipart upload to be queried this time can be obtained from the request result of the initial block upload QCloudInitiateMultipartUploadResult
abortRequest.uploadId = @"exampleUploadId";

[request setFinishBlock:^(id outputObject, NSError* error) {
    // You can get etag or custom header information in response from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML]AbortMultipfartUpload:abortRequest];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-abort-multi-upload)
```swift
let abort = QCloudAbortMultipfartUploadRequest.init();
abort.bucket = "examplebucket-1250000000";
abort.object = "exampleobject";
// The uploadId of the multipart upload to be queried this time can be obtained from the request result of the initial block upload QCloudInitiateMultipartUploadResult
abort.uploadId = "exampleUploadId";
if self.uploadId != nil {
    abort.uploadId = self.uploadId!;
}

abort.finishBlock = {(result,error)in
    if error != nil{
        print(error!)
    }else{
        // You can get etag or custom header information in response from outputObject
        print(result!);
    }    
}
QCloudCOSXMLService.defaultCOSXML().abortMultipfartUpload(abort);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

## Other Operations

### Restoring an archived object

#### Feature

This API (POST Object restore) is used to restore an archived object.

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudOptionsObjectRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudPostObjectRestoreRequest and enter the object name and bucket name to be set.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content in finishBlock callback.   

#### QCloudPostObjectRestoreRequest parameters

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| Object | The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Overview](https://intl.cloud.tencent.com) | NSString * | Yes |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| restoreRequest | Restore data configuration Information | QCloudRestoreRequest * | Yes |

QCloudRestoreRequest parameters

| Parameter Name | Description | Type | Required |
| ---------------- | ---------------------- | ------------------ | ---- |
| days | Set expiration time for temporary copies | int64_t | Yes |
| CASJobParameters | Restored process type configuration information | CASJobParameters * | Yes |

CASJobParameters parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------------- | ---- |
| tier | Restore mode, three types are supported: <br> <li> Standard (standard mode, restore task is completed in 3-5 hours) <br> <li> Expedited (speed mode, restore task can be completed in 15 minutes) <br> <li> Bulk (batch mode, restore task is completed in 5-12 hours) | QCloudCASTier | Yes |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-restore-object)
```objective-c
QCloudPostObjectRestoreRequest *req = [QCloudPostObjectRestoreRequest new];
req.bucket = @"examplebucket-1250000000";
req.object = @"exampleobject";
req.restoreRequest.days  = 10;
req.restoreRequest.CASJobParameters.tier =QCloudCASTierStandard;

[req setFinishBlock:^(id outputObject, NSError *error) {
    // You can get etag or custom header information in response from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] PostObjectRestore:req];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-restore-object)
```swift
let restore = QCloudPostObjectRestoreRequest.init();
restore.bucket = "examplebucket-1250000000";
restore.object = "exampleobject";
restore.restoreRequest.days = 10;
restore.restoreRequest.casJobParameters.tier = .standard;
restore.finishBlock = {(result,error)in
    if error != nil{
        print(error!)
    }else{
        // You can get etag or custom header information in response from outputObject
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().postObjectRestore(restore);
```

#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### Setting object ACL

#### Feature

This API is used to set the object access control list (ACL).

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before object operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudPutObjectACLRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudPutObjectACLRequest, and enter the bucket name and additionally required parameters, such as authorization information.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain whether the configuration is completed from finishBlock in callback. If error is null, configuration is successful.   

#### QCloudPutObjectACLRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| object | Object name | NSString * | Yes |
| x-cos-acl | It defines the ACL attribute of the object. Value range: private, public-read, and default; default value: default (i.e., inheriting the bucket's permissions); <br>**Note:** Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, use "default" for this parameter or simply leave it blank, so that the object will inherit the permissions of the bucket | String | No |
| GrantRead | Grants the grantee the read permission in the format of id="[OwnerUin]" | String | No |
| GrantWrite | Grants the grantee the write permission in the format of id="[OwnerUin]" | String | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="[OwnerUin]"` | String | No |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-put-object-acl)
```objective-c
QCloudPutObjectACLRequest* request = [QCloudPutObjectACLRequest new];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",@"1250000000"];
request.grantFullControl = grantString;
[request setFinishBlock:^(id outputObject, NSError *error) {
    // You can get etag or custom header information in response from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] PutObjectACL:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-put-object-acl)
```swift
let putObjectACl = QCloudPutObjectACLRequest.init();
putObjectACl.bucket = "examplebucket-1250000000";
putObjectACl.object = "exampleobject";
let grantString = "id=\"1250000000\"";
putObjectACl.grantFullControl = grantString;
putObjectACl.finishBlock = {(result,error)in
    if error != nil{
        print(error!)
    }else{
        // You can get etag or custom header information in response from outputObject
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().putObjectACL(putObjectACl);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

### Querying object ACL

#### Feature

This API is used to query the object's access control list (ACL).

#### Method Prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudGetObjectACLRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudGetObjectACLRequest, and enter the bucket name and the name of the object to be queried.    
2. Call the GetObjectACL method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the specific ACL information encapsulated in the QCloudACLPolicy object obtained from finishBlock in callback.   

#### QCloudGetObjectACLRequest parameters

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| Object | The object key is the unique identifier of the object in the bucket.<br>For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key is doc/picture.jpg, see [Object Overview](https://intl.cloud.tencent.com) | NSString * | Yes |
| versionID | Specifies the Version ID in version control | NSString * | Yes |

#### Returned Result

#### Parameters of returned result QCloudACLPolicy

| Parameter Name | Description | Type |
| ----------------- | ---------------------- | ------------------------- |
| owner | Bucket owner information | QCloudACLOwner * |
| accessControlList | Information of the authorized user and permissions | QCloudAccessControlList * |

QCloudACLOwner parameters

| Parameter Name | Description | Type |
| ----------- | ------------------- | ---------- |
| - - DisplayName | Bucket owner name | String |
| identifier  | Bucket owner ID | NSString * |

QCloudAccessControlList parameters

| Parameter Name | Description | Type |
| --------- | ---------------------- | -------------------------- |
| ACLGrants | An array storing grantee information | NSArray<QCloudACLGrant*> * |

QCloudACLGrant parameters

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------------------- |
| - - Grantee | Describes the information on the grantee. The type can be RootAccount or Subaccount <br><li>If the type is RootAccount, the ID specifies a root account <br><li>If the type is Subaccount, the ID specifies a sub-account | Object |
| permission | Specifies the permission information granted to the grantee, enumerated values: READ, FULL_CONTROL | QCloudCOSPermission |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-get-object-acl)
```objective-c
QCloudGetObjectACLRequest *request = [QCloudGetObjectACLRequest new];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";
__block QCloudACLPolicy* policy;
[request setFinishBlock:^(QCloudACLPolicy * _Nonnull result, NSError * _Nonnull error) {
    policy = result;
}];

[[QCloudCOSXMLService defaultCOSXML] GetObjectACL:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-get-object-acl)
```swift
let getObjectACL = QCloudGetObjectACLRequest.init();
getObjectACL.bucket = "examplebucket-1250000000";
getObjectACL.object = "exampleobject";
getObjectACL.setFinish { (result, error) in
    if error != nil{
        print(error!)
    }else{
        // You can get the ACL of the object from the accessControlList of result
        print(result!.accessControlList);
    }}
QCloudCOSXMLService.defaultCOSXML().getObjectACL(getObjectACL);
```
#### Error Codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.
-For SDK custom error codes, they are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, you can refer to the [SDK Error Code](https://intl.cloud.tencent.com/document/product/436/30610) for solutions.

## Adding custom headers

You can add custom headers as needed. Classes allowing addition of custom headers are provided with the attribute customHeaders:

```objective-c
@property (strong, nonatomic) NSMutableDictionary* customHeaders;
```

Key-value pairs in this attribute will be added to the HTTP headers of creation requests accordingly.

## Server Encryption

You can encrypt the uploaded objects in the following ways.

### Using server-side encryption with COS-hosted encryption keys (SSE-COS) to protect data

COS can automatically encrypt data as it is written to the IDC and automatically decrypt it when you access it. COS master key is used to apply AES-256 encryption to data.

You can achieve this by calling -(void)setCOSServerSideEncyption in the iOS SDK.

Objective-C code sample:
```objective-c
[request setCOSServerSideEncyption];
```

Swift code sample:
```swift
request.setCOSServerSideEncyption();
```

### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

You can achieve this by calling -(void)setCOSServerSideEncyptionWithCustomerKey:(NSString *)customerKey in the iOS SDK.

>
>-The service operated on by this encryption requires HTTPS requests.
2. customerKey: The key provided by the user, which shall be a 32-byte string consisting of numbers, letters and strings. Chinese characters are not supported.
3. If the uploaded source file calls this method, it should also be called when downloading, querying, uploading and copying the source object using QCloudCOSXMLDownloadObjectRequest, QCloudHeadObjectRequest, QCloudCOSXMLUploadObjectRequest and QCloudCOSXMLUploadObjectRequest.

Objective-C code sample:
```objective-c
NSString *customKey = @"123456qwertyuioplkjhgfdsazxcvbnm";
[put setCOSServerSideEncyptionWithCustomerKey:customKey];
```

Swift code sample

```swift
let customKey = "123456qwertyuioplkjhgfdsazxcvbnm";
putObject.setCOSServerSideEncyptionWithCustomerKey(customKey);
```
