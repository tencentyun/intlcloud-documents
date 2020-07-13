## Overview

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations, and other object operations, and how to use them.

- We assume that you have downloaded, installed and initialized the SDK as described in [Getting Started](https://intl.cloud.tencent.com/document/product/436/11280).
- We recommend using Command+F to search for the API you want, check the provided description of the API, and then copy the sample code to your project for execution.

> ?If you want to learn more about the function of the API or the meanings of its parameters, we recommend directly viewing the comments in the code. In Xcode, you can use a three-finger tap, Force Touch, or you can hover over a variable and press Control+Command+D to see its interpretation.   

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring pre-flight requests for cross-origin access | Sends a pre-flight request to confirm whether a real cross-origin access request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Object](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects in a single request |

**Multipart operations**

| API          | Operation                   | Description                                       |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in multiple parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an existing object to a part of a new object |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts in the specific multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACLs | Queries ACLs of an object |

## Advanced APIs (recommended)

This section encapsulates advanced APIs for uploading and copying. You only need to set required parameters, and the APIs will automatically decide whether to perform simple upload/copy or multipart upload/copy based on the file size. Before using the API, make sure you have completed initialization as instructed in [Getting Started](https://intl.cloud.tencent.com/document/product/436/11280).

### Uploading an object

Refer to [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/11280#.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1) in Getting Started.

#### Checkpoint restart for object uploads

>?Checkpoint restart is only supported for uploading files in the sandbox.

This SDK uploads any object larger than 1 MB using multipart upload. That is, split the object into multiple parts, each 1 MB in size, and upload them using concurrent (up to 4) multiple uploads. Checkpoint restart is implemented on the basis that each uploaded part is stored in the backend server.  

During a multipart upload, resumeData for resuming the upload is generated after you initialized or canceled the upload. This is used to generate another upload request for resuming the upload. The following example shows how to get ResumeData:


Objective-C code sample:

[//]: # (.cssg-snippet-objc-transfer-upload-object)
```objective-C
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
put.object = @"exampleobject";
put.bucket = @"examplebucket-1250000000";
put.body = [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];
//Set upload parameters
put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult,
    QCloudCOSXMLUploadObjectResumeData resumeData) {
    //This block will be called back after the Initiate Multipart Upload operation is completed, so you can get resumeData,
    //and can generate a multipart upload request through resumeData
    QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest
        requestWithRequestData:resumeData];
};
[put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent,
    int64_t totalBytesExpectedToSend) {
    NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent,
        totalBytesExpectedToSend);
}];
[put setFinishBlock:^(QCloudUploadObjectResult *result, NSError* error) {
    //You can get the result from `result`
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
//Abort a multipart upload and delete uploaded parts
[put abort:^(id outputObject, NSError *error) {
//
}];

//···When initialization is complete and upload is not complete
NSError* error;
//The following shows how resumeData is generated after the user cancels the upload
QCloudCOSXMLUploadObjectResumeData resumeData = [put cancelByProductingResumeData:&error];
QCloudCOSXMLUploadObjectRequest* request = nil;
if (resumeData) {
    request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
}
//The request generated can be used to resume the previous unsuccessful multipart upload directly
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
//Set upload parameters
uploadRequest.initMultipleUploadFinishBlock = {(multipleUploadInitResult,resumeData) in
    //This block will be called back after the Initiate Multipart Upload operation is completed, so you can get resumeData, and generate a new multipart upload request through resumeData
    let resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumeData as Data?);
}
uploadRequest.sendProcessBlock = {(bytesSent , totalBytesSent , totalBytesExpectedToSend) in
    
}
uploadRequest.setFinish { (result, error) in
    if error != nil{
        print(error!)
    }else{
        //Get the request result from result
        print(result!);
    }}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(uploadRequest);

//···When initialization is complete and upload is not complete
var error:NSError?;
    //The following shows how resumeData is generated after the user cancels the upload
do {
    let resumedData = try uploadRequest.cancel(byProductingResumeData: &error);
        var resumeUploadRequest:QCloudCOSXMLUploadObjectRequest<AnyObject>?;
             resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumedData as Data?);
             //The request generated can be used to resume the previous unsuccessful multipart upload directly
    if resumeUploadRequest != nil {
        QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(resumeUploadRequest!);
    }
             
} catch  {
    print("resumeData is blank");
    return;
}
```

Note: the multipart upload uses the serial mode where parts must be uploaded in sequence. Under the following circumstances, checkpoint restart cannot be used.

- An object less than 1 MB is uploaded not using multipart upload.
- The simple upload API rather than the QCloudCOSXMLUploadObjectRequest class is used to upload files.
- The Initiate Multipart upload operation is not completed (the callback used for this purpose is yet to be invoked) when you cancel the generation of resumeData.

### Downloading an object

Refer to [Downloading an Object](https://intl.cloud.tencent.com/document/product/436/11280#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1) in Getting Started.

### Copying an object

#### Notes

Initialize a QCloudCOSXMLCopyObjectRequest object, and then call CopyObject of QCloudCOSTransferMangerService. Note that multipart copy is automatically used for large files, but users will not be aware of this process.  

> !For cross-origin replication, the region of transferManager must be the same as that of the bucket.

#### QCloudCOSXMLCopyObjectRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | --------------------- | ---- |
| bucket | Bucket name in the format of &lt;BucketName-APPID&gt;,<br>such as examplebucket-1250000000 | NSString * | Yes |
| sourceBucket | Bucket of the copied source file | NSString * | Yes |
| sourceObject | Object name (key) of the copied source file | NSString * | Yes |
| sourceAPPID | APPID of the copied source file | NSString * | Yes |
| sourceRegion | Region of the copied source file | NSString * | Yes |
| metadataDirective  | Indicates whether to copy metadata. Enumerated values: `Copy`, `Replaced`. Default: `Copy`.<br><li>If you specify this parameter as `Copy`, metadata are copied from the source file with user-defined metadata in the headers ignored. <br><li>If you specify this parameter as `Replaced`, the source file metadata are replaced by user-defined metadata in the headers. If the destination path is the same as the source path, which means you want to modify the metadata, you must specify this parameter as `Replaced`**. | NSString * | No |
| storageClass | Object storage class. Enumerated values:<br><li>STANDARD (QCloudCOSStorageStandard)<br><li>STANDARD_IA (QCloudCOSStorageStandardIA)<br>Default value: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-transfer-copy-object)
```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];

request.bucket = @ "examplebucket-1250000000"; //Destination bucket <BucketName-APPID>, which needs to be public read or the current account must have access to
request.object = @"exampleobject";//Destination file name
//File source bucket <BucketName-APPID>, which needs to be public read or the current account must have access to
request.sourceBucket = @"sourcebucket-1250000000";
request.sourceObject = @"sourceObject";//Source file name
request.sourceAPPID = @"1250000000";//Source file APPID
request.sourceRegion= @"COS_REGION";//Source region

[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    //You can get the etag or custom headers in the response from outputObject
}];

//For cross-origin replication, the region of transferManager must be the same as that of the bucket
[[QCloudCOSTransferMangerService defaultCOSTransferManager] CopyObject:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-transfer-copy-object)
```swift
let copyRequest =  QCloudCOSXMLCopyObjectRequest.init();
copyRequest.bucket = "examplebucket-1250000000";//Destination bucket <BucketName-APPID>, which needs to be public read or the current account must have access to
copyRequest.object = "exampleobject";//Destination file name
//File source bucket <BucketName-APPID>, which needs to be public read or the current account must have access to
copyRequest.sourceBucket = "sourcebucket-1250000000";
copyRequest.sourceObject = "sourceObject";//Source file name
copyRequest.sourceAPPID = "1250000000";//Source file APPID
copyRequest.sourceRegion = "COS_REGION";//Source region
copyRequest.setFinish { (copyResult, error) in
    if error != nil{
        print(error!);
    }else{
        print(copyResult!);
    }
}
//For cross-origin replication, the region of transferManager must be the same as that of the bucket
QCloudCOSTransferMangerService.defaultCOSTransferManager().copyObject(copyRequest);
```

## Simple Operations

### Querying object list

#### Feature description

This API (GET Bucket (List Object)) is used to query some or all objects in a bucket.

#### Method prototype

This operation requires importing the header file QCloudCOSXML/QCloudCOSXML.h. Before the import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudPutBucketCORSRequest instance, specify additional parameters as required, send the request, and get the response. Detailed steps are as follows:

1. Instantiate QCloudGetBucketRequest and enter the required parameters.    
2. Call the GetBucket method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from QCloudListBucketResult in the callback block finishBlock.   

#### QCloudGetBucketRequest parameters

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format of &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| prefix | Prefix to be matched, which is used to specify the URL prefix of the files to be returned |  NSString * | No   |
| delimiter | The delimiter is a symbol.<br><li>If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed.<br><li>If no prefix is specified, the listing will start from the beginning of the path. It can be roughly regarded as an end mark. For example, to get paths that end with A, simply set this parameter to A. |  NSString * | No   |
| encodingType | Indicates the encoding method of the returned value. Valid value: url | NSString * | No |
| marker | By default, entries are listed in UTF-8 binary order starting from this marker | NSString * | No |
| maxKeys | Maximum number of entries returned at a time. Default: 1000 (Max.) | int | No |

#### Response

QCloudListBucketResult parameters

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | -------------------------------- |
| name | Bucket name | NSString * |
| prefix | Prefix to be matched, which is used to specify the URL prefix of the files to be returned | NSString *  |
| marker | by default, entries are listed in UTF-8 binary order starting from this marker | NSString * | No |
| nextMarker        | Marks the starting point of the next entry if the returned entry is truncated  | NSString *   |
| maxKeys | Maximum number of entries returned in a single response | int |
| delimiter | The delimiter is a symbol.<br><li>If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed.<br><li>If no prefix is specified, the listing will start from the beginning of the path. | NSString * |
| isTruncated | Indicates whether an entry in the response is truncated | BOOL |
| contents | Information about each object | NSArray<QCloudBucketContents*> * |
| commonPrefixes  | The identical paths between `Prefix` and `delimiter` are grouped together and defined as a common prefix | NSArray<QCloudCommonPrefixes*> * |

QCloudBucketContents parameters

| Parameter Name | Description | Type |
| ------------ | --------------------------------------------------------- | ------------------------ |
| key | Object Key | NSString * |
| lastModified | Indicates when an object is last modified | NSString * |
| eTag                                 | MD5 checksum of a file                                         | NSString *      |
| size | File size in byte | int |
| owner | Bucket owner | QCloudBucketOwner * |
| storageClass | Object storage class. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE | QCloudCOSStorageClass  * |

QCloudBucketOwner parameters

| Parameter Name | Description | Type |
| ----------- | ------------------- | ---------- |
| identifier  | Bucket APPID | NSString * |
| displayName  | Object owner name | NSString * |



QCloudCommonPrefixes parameters

| Parameter Name | Description | Type |
| -------- | ------------------ | ---------- |
| prefix | A single common prefix | NSString * |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-get-bucket)
```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
request.bucket = @"examplebucket-1250000000";
request.maxKeys = 1000;

[request setFinishBlock:^(QCloudListBucketResult * result, NSError* error) {
    //result contains the request result
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
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Uploading an object

#### Feature description

This API (Put Object) is used to upload an object (smaller than 20 MB) to a bucket. It supports uploading files from memory.

> !The number of bucket ACL rules is up to 1,000. If you do not need object ACL control, leave it to the default option: inherit bucket permissions.

#### QCloudPutObjectRequest parameters

| Parameter Name           | Description                                                         | Type                  | Required |
| ------------------ | ------------------------------------------------------------ | --------------------- | ---- |
| Object | Object key is the unique identifier of an object in a bucket. For example, if the object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format of &lt;BucketName-APPID&gt;, such as `examplebucket-1250000000` | NSString * | Yes |
| body                          | If the file to upload is stored in a disk, use the NSURL * type variable to indicate the file path.<br><li>If the file is stored in memory, use the NSData * type variable to indicate containing the file’s binary data. | BodyType | Yes    |
| storageClass | Object storage class. Enumerated values: STANDARD (QCloudCOSStorageStandard), STANDARD_IA (QCloudCOSStorageStandardIA), ARCHIVE (QCloudCOSStorageARCHIVE). Default value: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |
| cacheControl | Cache policy as defined in RFC 2616, which will be stored in the object metadata | NSString * | No |
| contentDisposition | Filename as defined in RFC 2616, which will be stored in the object metadata | NSString * | No |
| expect | When expect=@"100-Continue" is used, the request content will be sent only after confirmation from the server is received. | NSString * | No |
| expires | Expiration time as defined in RFC 2616, which will be stored in the object metadata | NSString * | No |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read, and default; default: default (i.e., inheriting the bucket's permissions).<br>Note: currently, you can set up to 1,000 bucket ACL rules. If you do not need object ACL control, set this parameter manually to `default`, or simply leave it to default. | NSString * | No |
| grantRead | Grants read access in the format: id="OwnerUin" | NSString * | No |
| grantWrite | Grants write access in the format: `id="OwnerUin"` | NSString * | No |
| grantFullControl | Grants full access in the format: id="OwnerUin" | NSString * | No |

#### Samples    


Objective-C code sample:

[//]: # (.cssg-snippet-objc-put-object)
```objective-C
QCloudPutObjectRequest* put = [QCloudPutObjectRequest new];
put.object = @"exampleobject";
put.bucket = @"examplebucket-1250000000";
put.body =  [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];

[put setFinishBlock:^(id outputObject, NSError *error) {
    //You can get the etag or custom headers in the response from outputObject
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
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying object metadata

#### Feature description

This API (HEAD Object) is used to query object metadata.

#### Method prototype

This operation requires importing the header file QCloudCOSXML/QCloudCOSXML.h. Before the import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudHeadObjectRequest instance, specify additional parameters as required, send the request, and then get the response. Detailed steps are as follows:    

1. Instantiate QCloudHeadObjectRequest and specify required parameters.    
2. Call the HeadObject method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudHeadObjectRequest parameters

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ---------- | ---- |
| Object | Object key is the unique identifier of an object in a bucket. For example, if the object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/text.txt`, the object key would be `doc/text.txt`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format&lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| ifModifiedSince | The file content is only returned if the file is modified after the specified time. Otherwise, 304 (not modified) is returned. | NSString * | Yes |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-head-object)
```objective-c
QCloudHeadObjectRequest* headerRequest = [QCloudHeadObjectRequest new];
headerRequest.object = @"exampleobject";
headerRequest.bucket = @"examplebucket-1250000000";

[headerRequest setFinishBlock:^(NSDictionary* result, NSError *error) {
    //result contains the request result
}];

[[QCloudCOSXMLService defaultCOSXML] HeadObject:headerRequest];
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
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Downloading an object

#### Feature description

This API (GET Object) is used to download an object to the local file system.

#### Method prototype

This operation requires importing the header file QCloudCOSXML/QCloudCOSXML.h. Before the import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate an instance, specify additional parameters as required, send the request, and then get the response. Detailed steps are as follows:    

1. Instantiate the object QCloudGetObjectRequest and specify required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudGetObjectRequest parameters

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| range | The specified byte range for file downloads as defined in RFC 2616 | NSString * | No |
| ifModifiedSince | The file content is only returned if the file is modified after the specified time. Otherwise, 412 (not modified) is returned. | NSString * | No |
| responseContentType | Sets the value of the `Content-Type` header in the response  | NSString * | No |
| responseContentLanguage | Sets the value of the `Content-Language` header in the response | NSString * | No |
| responseContentExpires | Sets the value of the `Content-Expires` header in the response | NSString * | No |
| responseCacheControl | Sets the value of the `Cache-Control` header in the response | NSString * | No |
| responseContentDisposition | Sets the value of the `Content-Disposition` header in the response  | NSString * | No |
| responseContentEncoding | Sets the value of the `Content-Encoding` header in the response  | NSString * | No |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-get-object)
```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
//Set the download URL. Once set, the file is downloaded to the specified path.
//If this parameter is not set, the file will be downloaded to memory and stored in the outputObject of finishBlock.
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    //You can get the etag or custom headers in the response from outputObject
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload,
    int64_t totalBytesExpectedToDownload) {
    //Download progress
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
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Configuring pre-flight requests for cross-origin access

#### Feature description

This API (Options Object) is used to initiate preflight requests to check whether you can send cross-origin access requests.

#### Method prototype

This operation requires importing the header file QCloudCOSXML/QCloudCOSXML.h. Before the import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudOptionsObjectRequest instance, specify additional parameters as required, send the request, and then get the response. Detailed steps are as follows:    

1. Instantiate QCloudOptionsObjectRequest, specify the object name, bucket name, and both the HTTP method and access sources allowed for simulating CORS requests.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudOptionsObjectRequest parameters

| Parameter Name |  Description | Type |Required |
| -------------------------- | ------------------------------------------------------------ | --------------------------- | ---- |
| object | Object key is the unique identifier of an object in a bucket. For example, if the object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| accessControlRequestMethod | The HTTP method for simulating CORS requests | NSArray&lt;NSString`*`> * | Yes |
| origin | The access sources allowed for simulating CORS requests. The wildcard `*` is supported.<br>Format: `protocol://domain name[:port]`,<br>for example, `http://www.qq.com`. | NSString * | Yes |
| allowedHeader | Tells the server what custom HTTP request headers can be used for subsequent requests when the `OPTIONS` request is sent. Wildcard `*` is supported | NSArray&lt;NSString `*` > * | No |

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
    //You can get the etag or custom headers in the response from outputObject
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
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Copying an object

#### Feature description

This API (PUT Object - Copy) is used to copy a file to the destination path.

#### Sample request


Objective-C code sample:

[//]: # (.cssg-snippet-objc-copy-object)
```Objective-C
QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
request.object = @"exampleobject";
//The path where the source object is located
request.objectCopySource = @"sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject";
[request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result, NSError * _Nonnull error) {
    //result contains the response result
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
| bucket | Destination bucket name in the format &lt;BucketName-APPID&gt;,<br>such as examplebucket-1250000000 | NSString * | Yes |
| object | Object key of the destination file | NSString * | Yes |
| objectCopySource | The path of the copied source file | NSString * | Yes |
| metadataDirective  | Indicates whether to copy metadata. Enumerated values: `Copy`, `Replaced`. Default: `Copy`.<br><li>If you specify this parameter as `Copy`, metadata are copied from the source file with user-defined metadata in the headers ignored. <br><li>If you specify this parameter as `Replaced`, the source file metadata are replaced by user-defined metadata in the headers. If the destination path is the same as the source path, which means you want to modify the metadata, you must specify this parameter as `Replaced`**. | NSString * | No |
| storageClass | Object storage class. Enumerated values:<br><li>STANDARD (QCloudCOSStorageStandard)<br><li>STANDARD_IA (QCloudCOSStorageStandardIA)<br>Default value: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read, and default; default: default (i.e., inheriting the bucket's permissions).<br>Note: currently, you can set up to 1,000 bucket ACL rules. If you do not need object ACL control, set this parameter manually to `default`, or simply leave it to default. | NSString * | No |
| grantRead | Grants read access in the format: id="OwnerUin" | NSString * | No |
| grantWrite | Grants write access in the format: id="OwnerUin" | NSString * | No |
| grantFullControl | Grants full access in the format: id="OwnerUin" | NSString * | No |
| versionID | Specifies the versionID of the source file. Only buckets that have versioning enabled or suspended respond to this parameter. | NSString * | No |

#### Response

The response is returned using QCloudCopyObjectResult.

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ---------- |
| ETag | Returns MD5 checksum of the file to check whether the object content has changed | NSString * |
| lastModified | Last modified time in GMT of the file  | NSString * |
| versionID | Version ID of the object; only used for a versioning-enabled bucket | NSString * |

#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting a single object

#### Feature description

This API (DELETE Object) is used to delete a specified object.

#### Method prototype

This operation requires importing the header file QCloudCOSXML/QCloudCOSXML.h. Before the import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudDeleteObjectRequest instance, specify additional parameters as required, send the request, and then get the response. Detailed steps are as follows:    

1. Instantiate QCloudDeleteObjectRequest and specify required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudDeleteObjectRequest parameters

| Parameter Name | Type | Required |Description |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| object | Object key is the unique identifier of an object in a bucket. For example, if the object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key would be `doc/pic.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket). | NSString * | Yes |

#### Samples


Objective-C code sample:


[//]: # (.cssg-snippet-objc-delete-object)
```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
deleteObjectRequest.bucket = @"examplebucket-1250000000";
deleteObjectRequest.object = @"exampleobject";

[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    //You can get the etag or custom headers in the response from outputObject
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

#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting multiple objects

#### Method prototype

This operation requires importing the header file QCloudCOSXML/QCloudCOSXML.h. Before the import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudDeleteMultipleObjectRequest instance, specify additional parameters as required, send the request, and then get the response. Detailed steps are as follows:    

1. Instantiate QCloudDeleteMultipleObjectRequest, enter the required parameters, encapsulate the object you want to delete into a QCloudDeleteObjectInfo object, and place it in the objects array of deleteObjects.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudDeleteMultipleObjectRequest parameters

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ------------------ | ---- |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| deleteObjects | Encapsulates multiple objects to be deleted | QCloudDeleteInfo * | Yes |

QCloudDeleteInfo parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ----------------------------------------- | ---- |
| objects  | An array of objects to be deleted | NSArray&lt;QCloudDeleteObjectInfo `*` > * | Yes |
| Quiet | Boolean; specifies the state of Quiet mode: <br><li>true: enable Quiet mode<br><li>false: enable Verbose mode<br>Default: false | NSArray% encTxtlt; QCloudDeleteObjectInfo `*`> * | No |

CloudDeleteObjectInfo parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| key | Object key is the unique identifier of an object in a bucket. For example, if the object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |

#### Response

QCloudDeleteResult parameters

| Parameter Name | Description | Type |
| -------------- | -------------------------------------------------- | --------------------------------- |
| deletedObjects | An array of deleted objects | NSArray<QCloudDeleteResultRow*> * |
| lastModified | Last modified time in GMT of the file | NSString * |
| versionID | Version ID of the object; only used for a versioning-enabled bucket | NSString * |

QCloudDeleteResultRow parameters

| Parameter Name | Description | Type |
| -------- | --------------- | ---------- |
| key | Key of a deleted object | NSString * |

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
    //You can get the etag or custom headers in the response from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-delete-multi-object)
```swift
let mutipleDel = QCloudDeleteMultipleObjectRequest.init();
mutipleDel.bucket = "examplebucket-1250000000";

let info1 = QCloudDeleteObjectInfo.init();
info1.key = "exampleobject";
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
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Multipart Operations



- Uploading objects with multipart upload: initializing a multipart upload, uploading parts, and completing a multipart upload.
- Resuming a multipart upload: querying uploaded parts, uploading remaining parts, and completing a multipart upload.
- Deleting uploaded parts.

### Querying multipart uploads

#### Feature description

This API (List Multipart Uploads) is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

This operation requires importing the header file QCloudCOSXML/QCloudCOSXML.h. Before the import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudListBucketMultipartUploadsRequest instance, specify additional parameters as required, send the request, and then get the response. Detailed steps are as follows:    

1. Instantiate QCloudListBucketMultipartUploadsRequest and enter the required parameters, such as the prefix and the encoding method of the returned result.    
2. Call the ListBucketMultipartUploads method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudListBucketMultipartUploadsRequest parameters

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| prefix | The returned Object key must be prefixed with this value. Note that the returned key will still contain Prefix when querying with prefix. | NSString * | No |
| delimiter | The delimiter is a symbol.<br><li>If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed.<br><li>If no prefix is specified, the listing will start from the beginning of the path. It can be roughly regarded as an end mark. For example, to get paths that end with A, simply set this parameter to A. |  NSString * | No   |
| encodingType | Indicates the encoding method of the returned value. Valid value: url | NSString * | No |
| keyMarker | Entries will be listed starting from this key value | NSString * | No |
| uploadIDMarker | Entries will be listed starting from this UploadId value | int | No |
| maxUploads | Sets the maximum number of multipart uploads returned. Value range: 1-1000 | int | No |

#### Response

QCloudListMultipartUploadsResult parameters

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ---------- |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * |
| prefix | The returned Object key must be prefixed with this value. Note that the returned key will still contain Prefix when querying with prefix. | NSString * |
| delimiter | The delimiter is a symbol.<br><li>If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed.<br><li>If no prefix is specified, the listing will start from the beginning of the path. It can be roughly regarded as an end mark. For example, to get paths that end with A, simply set this parameter to A. |  NSString * |
| encodingType | Indicates the encoding method of the returned value. Valid value: url | NSString * |
| keyMarker | Entries will be listed starting from this key value | NSString * |
| maxUploads | Sets the maximum number of multipart uploads returned. Value range: 1-1000 | int |
| uploads | Information about all uploaded parts | NSArray* |
| isTruncated | Indicates whether the file is truncated | NSString * |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-list-multi-upload)
```objecitve-c
QCloudListBucketMultipartUploadsRequest* uploads = [QCloudListBucketMultipartUploadsRequest new];
uploads.bucket = @"examplebucket-1250000000";
uploads.maxUploads = 100;

[uploads setFinishBlock:^(QCloudListMultipartUploadsResult* result, NSError *error) {
    //Get the information about multipart uploads from result
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
#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem. Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).


### <span id = "INIT_MULIT_UPLOAD">Initializing multipart upload </span>

#### Feature description

This API (Initiate Multipart Upload) is used to initialize a multipart upload and obtain an uploadId.

#### Method prototype

This operation requires importing the header file QCloudCOSXML/QCloudCOSXML.h. Before the import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudInitiateMultipartUploadRequest instance, specify additional parameters as required, send the request, and then get the response. Detailed steps are as follows:    

1. Instantiate QCloudInitiateMultipartUploadRequest and enter the required parameters.    
2. Call the InitiateMultipartUpload method in the QCloudCOSXMLService object to initiate a request.    
3. Get the response content from the callback block finishBlock.   

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | --------------------- | ---- |
| Object | File name or object key that uniquely identifies an uploaded file (object) in a bucket. For example, if the object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| cacheControl | Cache policy defined in RFC 2616 | NSString * | No |
| contentDisposition | File name defined in RFC 2616 | NSString * | No |
| expect | If `expect=@"100-continue"` is used, the request content will be sent only after confirmation from the server is received |  NSString * | No |
| expires | Expiration time defined in RFC 2616 | NSString * | No |
| storageClass | Object storage class, enumerated values:<br><li>STANDARD(QCloudCOSStorageStandard)<br><li>STANDARD_IA(QCloudCOSStorageStandardIA)<br><li>ARCHIVE(QCloudCOSStorageARCHIVE)<br>Default: STANDARD(QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read, and default; default: default (i.e., inheriting the bucket's permissions).<br>Note: currently, you can set up to 1,000 bucket ACL rules. If you do not need object ACL control, set this parameter manually to `default`, or simply leave it to default. | NSString * | No |
| grantRead | Grants read access in the format: id="OwnerUin" | NSString * | No |
| grantWrite | Grants write access in the format: `id="OwnerUin"` | NSString * | No |
| grantFullControl | Grants full access in the format: id="OwnerUin" | NSString * | No |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-init-multi-upload)
```objective-c
QCloudInitiateMultipartUploadRequest* initrequest = [QCloudInitiateMultipartUploadRequest new];
initrequest.bucket = @"examplebucket-1250000000";
initrequest.object = @"exampleobject";

[initrequest setFinishBlock:^(QCloudInitiateMultipartUploadResult* outputObject, NSError *error) {
    //Get the uploadId of the multipart upload. This ID is required for subsequent uploads. Please save it for future use.
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
        //Get the uploadId of the multipart upload. This ID is required for subsequent uploads. Please save it for future use.
        self.uploadId = result!.uploadId;
        print(result!.uploadId);
    }}
QCloudCOSXMLService.defaultCOSXML().initiateMultipartUpload(initRequest);
```

#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Uploading parts

#### Feature description

This API (Upload Part) is used to upload a file in multiple parts.

#### QCloudUploadPartRequest parameters

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of the multipart upload.<br>When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID helps uniquely identify parts in the multipart upload, and their relative position in the entire file | NSString * | Yes |
| partNumber  | A number which identifies the part                                       | int | Yes  |
| contentSHA1 | SHA1 value of the part | NSString * | Yes |
| body | Uploaded data: supports `NSData *`, `NSURL` (local URL) and `QCloudFileOffsetBody*` | BodyType | Yes |

#### Response

QCloudUploadPartResult parameters

| Parameter Name | Description | Type |
| -------- | ----------- | ---------- |
| eTag | File etag | NSString * |

#### Method prototype

The specific steps for requesting a multipart upload in COS iOS SDK are as follows:

1. Instantiate QCloudUploadPartRequest and specify required parameters.
2. Call the UploadPart method in the QCloudCOSXMLService object to initiate a request.
3. Obtain the response content from QCloudUploadPartResult in the callback block finishBlock.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-upload-part)
```objective-c
QCloudUploadPartRequest* request = [QCloudUploadPartRequest new];
request.bucket = @"examplebucket-1250000000";
request.object = @"exampleobject";
request.partNumber = 1;
//Mark ID of the multipart upload. When you use the Initiate Multipart Upload API to initialize a multipart upload, you will get an uploadId.
//This ID not only helps uniquely identify parts in the multipart upload, but also their relative position in the entire file.
request.uploadId = @"exampleUploadId";
//Uploaded data: supports NSData *, NSURL (local URL) and QCloudFileOffsetBody * three types
request.body = [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];

[request setSendProcessBlock:^(int64_t bytesSent,
                               int64_t totalBytesSent,
                               int64_t totalBytesExpectedToSend) {
    //Upload progress information
}];
[request setFinishBlock:^(QCloudUploadPartResult* outputObject, NSError *error) {
    QCloudMultipartInfo *part = [QCloudMultipartInfo new];
    //Get the etag of the uploaded part
    part.eTag = outputObject.eTag;
    part.partNumber = @"1";
    //Save it for use when the upload is complete
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
//Mark ID of the multipart upload. When you use the Initiate Multipart Upload API to initialize a multipart upload, you will get an uploadId.
//This ID not only helps uniquely identify parts in the multipart upload, but also their relative position in the entire file.
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
        //Get the etag of the uploaded part
        mutipartInfo.eTag = result!.eTag;
        mutipartInfo.partNumber = "1";
        //Save it for use when the upload is complete
        self.parts = [mutipartInfo];
    }}
uploadPart.sendProcessBlock = {(bytesSent,totalBytesSent,totalBytesExpectedToSend) in
    //Upload progress information
    print("totalBytesSent:\(totalBytesSent) totalBytesExpectedToSend:\(totalBytesExpectedToSend)");
    
}
QCloudCOSXMLService.defaultCOSXML().uploadPart(uploadPart);
```
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Copying a part

#### Feature description

This API (Upload Part - Copy) is used to copy an existing object to be part of a new object.

#### QCloudUploadPartRequest parameters

| Parameter Name | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of the multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID helps uniquely identify parts in the multipart upload, and their relative position in the entire file | NSString *  | Yes |
| partNumber  | A number which identifies a part                                     | int | Yes  |
| source | URL path to the source file. A historical version can be specified using the `versionId` subresource | NSString * | Yes |
| body | Uploaded data: supports `NSData *`, `NSURL` (local URL) and `QCloudFileOffsetBody*` | BodyType | Yes |

#### Response

QCloudUploadPartResult parameters

| Parameter Name | Description | Type |
| -------- | ----------- | ---------- |
| eTag | File etag | NSString * |

#### Method prototype

The specific steps for requesting a multipart upload in COS iOS SDK are as follows:

1. Instantiate QCloudUploadPartCopyRequest and enter the required parameters.
2. Call the UploadPartCopy method in the QCloudCOSXMLService object to initiate a request.
3. Obtain the response content from QCloudCopyObjectResult in the callback block finishBlock.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-upload-part-copy)
```objective-c
QCloudUploadPartCopyRequest* request = [[QCloudUploadPartCopyRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
request.object = @"exampleobject";
//The URL path to the source file. You can specify a historical version using the versionid sub-resource.
request.source = @"sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject";
//The response to the initial multipart upload request returns a unique descriptor (upload ID).
request.uploadID = @"exampleUploadId";
request.partNumber = 1; //Mark the number of the current part.

[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    QCloudMultipartInfo *part = [QCloudMultipartInfo new];
    //Get the etag of the copied part.
    part.eTag = result.eTag;
    part.partNumber = @"1";
    //Save it for use when the upload is complete
    self.parts=@[part];
}];

[[QCloudCOSXMLService defaultCOSXML]UploadPartCopy:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-upload-part-copy)
```swift
let req = QCloudUploadPartCopyRequest.init();
req.bucket = "examplebucket-1250000000";
req.object = "exampleobject";
//The URL path to the source file. You can specify a historical version using the versionid sub-resource.
req.source = "sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject";
//The Initiate Multipart Upload request returns a unique descriptor (upload ID).
req.uploadID = "exampleUploadId";
if self.uploadId != nil {
    req.uploadID = self.uploadId!;
}

//Mark the serial number of the current part.
req.partNumber = 1;
req.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        let mutipartInfo = QCloudMultipartInfo.init();
        //Get the etag of the copied part
        mutipartInfo.eTag = result!.eTag;
        mutipartInfo.partNumber = "1";
        self.parts = [mutipartInfo];
    }}
QCloudCOSXMLService.defaultCOSXML().uploadPartCopy(req);
```
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### <span id = "LIST_MULIT_UPLOAD">Querying uploaded parts</span>

#### Feature description

This API (List Parts) is used to query parts uploaded with the specified uploadId.

#### QCloudListMultipartRequest parameters

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | uploadId of the multiple upload for parts to be queried | NSString * | Yes |
| maxPartsCount | Maximum number of entries returned at a time. Default value: 1,000 | NSString * | No |
| partNumberMarker | Marks the starting point of the list of parts; by default, entries are listed in UTF-8 binary order starting from this marker | NSString * | No   |
| encodingType | Specifies the encoding type of the returned value | int        | No   |

#### Response

 QCloudListPartsResult parameters

| Parameter Name | Description | Type |
| ---------------- | ------------------------------------------------------------ | -------------------------- |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * |
| encodingType | Specifies the encoding type of the returned value | NSString * |
| key | Object Name | NSString * |
| uploadId | UploadId of the multipart upload for parts to be queried | NSString * |
| storageClass | Storage class of object parts | QCloudCOSStorageClass |
| partNumberMarker | Marks the starting point of the list of parts; by default, entries are listed in UTF-8 binary order starting from this marker | int |
| nextNumberMarker | Marks the starting point of the next entry if the returned entry is truncated | NSString * |
| maxParts | Maximum number of entries returned at a time | QCloudCOSStorageClass |
| isTruncated | Indicates whether the returned entry is truncated | BOOL |
| initiator | Identifies the initiator of the upload | NSString * |
| owner | Identifies the owner of parts | QCloudCOSStorageClass |
| parts | Represents information about each part | QCloudMultipartUploadPart* |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-list-parts)
```objective-c
QCloudListMultipartRequest* request = [QCloudListMultipartRequest new];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";
//The Initiate Multipart Upload request returns a unique descriptor (upload ID).
request.uploadId = @"exampleUploadId";

[request setFinishBlock:^(QCloudListPartsResult * _Nonnull result, NSError * _Nonnull error) {
    //Get information about uploaded parts from result
}];

[[QCloudCOSXMLService defaultCOSXML] ListMultipart:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-list-parts)
```swift
let req = QCloudListMultipartRequest.init();
req.object = "exampleobject";
req.bucket = "examplebucket-1250000000";
//The Initiate Multipart Upload request returns a unique descriptor (upload ID).
req.uploadId = "exampleUploadId";
if self.uploadId != nil {
    req.uploadId = self.uploadId!;
}
req.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        //Get information about uploaded multipart parts from result
        print(result!);
    }}

QCloudCOSXMLService.defaultCOSXML().listMultipart(req);
```

#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### <span id = "COMPLETE_MULIT_UPLOAD"> Completing a multipart upload </span>

#### Feature description

This API (Complete Multipart Upload) is used to complete a multipart upload.

#### QCloudCompleteMultipartUploadRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ----------------------------------- | ---- |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of the multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID helps uniquely identify parts in the multipart upload, and their position in the entire file | NSString * | Yes |
| parts | Information about completing the multipart upload | QCloudCompleteMultipartUploadInfo * | Yes |

#### Response

 QCloudUploadObjectResult parameters

| Parameter Name | Description | Type |
| --------- | ------------------------------------------------------------ | ---------- |
| location | The public endpoint for the existing object | NSString * |
| bucket | Destination bucket name for the multipart upload in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * |
| key | Object Name | NSString * |
| eTag | MD5 checksum of the merged file | NSString * |
| versionID | Version ID of the object; only used for a versioning-enabled bucket | NSString * |

#### Method prototype

The specific steps for initiating a Complete Multipart Upload request in COS iOS SDK are as follows:

1. Instantiate QCloudCompleteMultipartUploadRequest and specify required parameters.
2. Call the CompleteMultipartUpload method in the QCloudCOSXMLService object to initiate a request.
3. Obtain the response content from QCloudUploadObjectResult in the callback block finishBlock.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-complete-multi-upload)
```objective-c
QCloudCompleteMultipartUploadRequest *completeRequst = [QCloudCompleteMultipartUploadRequest new];
completeRequst.object = @"exampleobject";
completeRequst.bucket = @"examplebucket-1250000000";
//The uploadId of the multipart upload for parts to be queried can be obtained from the request result QCloudInitiateMultipartUploadResult
completeRequst.uploadId = @"exampleUploadId";
//Information about uploaded parts
QCloudCompleteMultipartUploadInfo *partInfo = [QCloudCompleteMultipartUploadInfo new];
partInfo.parts = self.parts;
completeRequst.parts = partInfo;

[completeRequst setFinishBlock:^(QCloudUploadObjectResult * _Nonnull result, NSError * _Nonnull error) {
    //Get the upload result from result
}];

[[QCloudCOSXMLService defaultCOSXML] CompleteMultipartUpload:completeRequst];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-complete-multi-upload)
```swift
let  complete = QCloudCompleteMultipartUploadRequest.init();
complete.bucket = "examplebucket-1250000000";
complete.object = "exampleobject";
//The uploadId of the multipart upload for parts to be queried can be obtained from the request result QCloudInitiateMultipartUploadResult
complete.uploadId = "exampleUploadId";
if self.uploadId != nil {
    complete.uploadId = self.uploadId!;
}


//Information about uploaded parts
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
        //Get the upload result from result
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().completeMultipartUpload(complete);
```
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### <span id = "ABORT_MULIT_UPLOAD"> Aborting a multipart upload </span>

#### Feature description

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### QCloudAbortMultipfartUploadRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format BucketName-APPID, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of the multipart upload to abort. When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID helps uniquely identify parts in the multipart upload, and their relative position in the entire file | NSString * | Yes |

#### Method prototype

The specific steps for initiating an Abort Multipart Upload request in COS iOS SDK are as follows:

1. Instantiate QCloudAbortMultipfartUploadRequest and specify required parameters.
2. Call the AbortMultipfartUpload method in the QCloudCOSXMLService object to initiate a request.
3. Obtain the response content from outputObject in the callback block finishBlock.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-abort-multi-upload)
```objective-c
QCloudAbortMultipfartUploadRequest *abortRequest = [QCloudAbortMultipfartUploadRequest new];
abortRequest.object = @"exampleobject";
abortRequest.bucket = @"examplebucket-1250000000";
//The uploadId of the multipart upload for parts to be queried can be obtained from the request result QCloudInitiateMultipartUploadResult
abortRequest.uploadId = @"exampleUploadId";

[abortRequest setFinishBlock:^(id outputObject, NSError *error) {
    //You can get the etag or custom headers in the response from outputObject
}];

[[QCloudCOSXMLService defaultCOSXML]AbortMultipfartUpload:abortRequest];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-abort-multi-upload)
```swift
let abort = QCloudAbortMultipfartUploadRequest.init();
abort.bucket = "examplebucket-1250000000";
abort.object = "exampleobject";
//The uploadId of the multipart upload for parts to be queried can be obtained from the request result QCloudInitiateMultipartUploadResult
abort.uploadId = "exampleUploadId";
if self.uploadId != nil {
    abort.uploadId = self.uploadId!;
}

abort.finishBlock = {(result,error)in
    if error != nil{
        print(error!)
    }else{
        //You can get the etag or custom headers in the response from outputObject
        print(result!);
    }    
}
QCloudCOSXMLService.defaultCOSXML().abortMultipfartUpload(abort);
```
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Other Operations

### Restoring an archived object

#### Feature description

This API (POST Object restore) is used to restore an archived object.

#### Method prototype

This operation requires importing the header file QCloudCOSXML/QCloudCOSXML.h. Before the import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudPostObjectRestoreRequest instance, specify additional parameters as required, send the request, and get a response. Detailed steps are as follows:    

1. Instantiate QCloudPostObjectRestoreRequest and enter the object name and bucket name to be set.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Get the response content from the callback block finishBlock.   

#### QCloudPostObjectRestoreRequest parameters

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| object | Object key is the unique identifier of an object in a bucket. For example, if the object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| restoreRequest | Data restoration configuration | QCloudRestoreRequest * | Yes |

QCloudRestoreRequest parameters

| Parameter Name | Description | Type | Required |
| ---------------- | ---------------------- | ------------------ | ---- |
| days | Set the number of days before a temporary copy expires | int64_t | Yes |
| CASJobParameters | Restoration type configuration | CASJobParameters * | Yes |

CASJobParameters parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------------- | ---- |
| tier | Specifies one of the restoration types: <br><li>Standard, which completes a restore task in 3-5 hours<br><li>Expedited, which completes a restore task in 1-5 minutes)<br><li>Bulk, which completes multiple restore tasks in 5-12 hours | QCloudCASTier | Yes |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-restore-object)
```objective-c
QCloudPostObjectRestoreRequest *req = [QCloudPostObjectRestoreRequest new];
req.bucket = @"examplebucket-1250000000";
req.object = @"exampleobject";
req.restoreRequest.days  = 10;
req.restoreRequest.CASJobParameters.tier =QCloudCASTierStandard;

[request setFinishBlock:^(id outputObject, NSError* error) {
    //You can get the etag or custom headers in the response from outputObject
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
        //You can get the etag or custom headers in the response from outputObject
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().postObjectRestore(restore);
```

#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Setting object ACL

#### Feature description

This API (PUT Object acl) is used to set an access control list (ACL) for an object.

#### Method prototype

This operation requires importing the header file QCloudCOSXML/QCloudCOSXML.h. Before the import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudPutObjectACLRequest instance, specify additional parameters as required, send the request, and then get the response. Detailed steps are as follows:    

1. Instantiate QCloudPutObjectACLRequest, and enter the bucket name and additionally required parameters, such as authorization information.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response from the callback block finishBlock where an empty `error` indicates a successful request.   

#### QCloudPutObjectACLRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read, and default; default: default (i.e., inheriting the bucket's permissions).<br>Note: currently, you can set up to 1,000 bucket ACL rules. If you do not need object ACL control, set this parameter manually to `default`, or simply leave it to default. | NSString * | No |
| grantRead | Grants read access in the format: id="OwnerUin" | NSString * | No |
| grantWrite | Grants write access in the format: id="OwnerUin" | NSString * | No |
| grantFullControl | Grants full access in the format: id="OwnerUin" | NSString * | No |

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
    //You can get the etag or custom headers in the response from outputObject
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
        //You can get the etag or custom headers in the response from outputObject
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().putObjectACL(putObjectACl);
```
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying object ACLs

#### Feature description

This API (GET Object acl) is used to query ACLs of an object.

#### Method prototype

This operation requires importing the header file QCloudCOSXML/QCloudCOSXML.h. Before the import, you need to complete [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudGetObjectACLRequest instance, specify additional parameters as required, send the request, and then get the response. Detailed steps are as follows:    

1. Instantiate QCloudGetObjectACLRequest, and enter the bucket name and the name of the object to be queried.    
2. Call the GetObjectACL method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the ACLs encapsulated in the QCloudACLPolicy object in the callback block finishBlock.   

#### QCloudGetObjectACLRequest parameters

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`. The bucket name can be found in the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object key is the unique identifier of an object in a bucket. For example, if the object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key would be `doc/pic.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| versionID | Specifies Version ID of an object if versioning is enabled | NSString * | Yes |

#### Response

QCloudACLPolicy parameters

| Parameter Name | Description | Type |
| ----------------- | ---------------------- | ------------------------- |
| owner | Bucket owner | QCloudACLOwner * |
| accessControlList | Information about the authorized user and permissions | QCloudAccessControlList * |

QCloudACLOwner parameters

| Parameter Name | Description | Type |
| ----------- | ------------------- | ---------- |
| displayName | Bucket owner name | NSString * |
| identifier  | Bucket owner ID | NSString * |

QCloudAccessControlList parameters

| Parameter Name | Description | Type |
| --------- | ---------------------- | -------------------------- |
| ACLGrants | Contains an array of grantees | NSArray<QCloudACLGrant*> * |

QCloudACLGrant parameters

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------------------- |
| grantee | Describes the information on the grantee. The type can be RootAccount or Subaccount<br><li>If the type is RootAccount, the ID specifies a root account<br><li>If the type is Subaccount, the ID specifies a sub-account | QCloudACLGrantee * |
| permission | Specifies the permissions granted to the grantee. Enumerated values: READ, FULL_CONTROL | QCloudCOSPermission |

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
        //You can get the object ACL from the accessControlList of result
        print(result!.accessControlList);
    }}
QCloudCOSXMLService.defaultCOSXML().getObjectACL(getObjectACL);
```
#### Error codes

When the SDK request fails, the `error` returned is not empty, and instead includes an error code, error description, and other necessary debugging information to help developers quickly fix the problem.

Error codes (encapsulated in the returned `error`) include those returned by your device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h using Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- Custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For such error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Using Custom Headers

You can use custom headers as needed. Classes allowing custom headers are all provided with the attribute customHeaders:

```objective-c
@property (strong, nonatomic) NSMutableDictionary* customHeaders;
```

All key-value pairs in this attribute will be added accordingly to the HTTP headers that build a request.

## Server-Side Encryption

You can encrypt uploaded objects in the following ways.

#### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

COS can automatically encrypt your data as you write it to the IDC and automatically decrypt it when you access it. Currently, COS allows AES-256 encryption using COS master key pair.

You can achieve this by calling -(void)setCOSServerSideEncyption in the iOS SDK.

Objective-C code sample:
```objective-c
[request setCOSServerSideEncyption];
```

Swift code sample:
```swift
request.setCOSServerSideEncyption();
```

#### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

You can achieve this by calling -(void)setCOSServerSideEncyptionWithCustomerKey:(NSString \*)customerKey in the iOS SDK.

> !
>- This encryption feature requires using HTTPS requests.
>- customerKey: the key provided by the user, which should be a 32-byte string consisting of numbers, letters and strings. Chinese characters are not supported.
>- If this method was called for uploading the source file, it should also be called when downloading, querying, uploading and copying the source object using QCloudCOSXMLDownloadObjectRequest, QCloudHeadObjectRequest, QCloudCOSXMLUploadObjectRequest and QCloudCOSXMLUploadObjectRequest respectively.

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
