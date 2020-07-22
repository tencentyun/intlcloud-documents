## Overview

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations, and other object operations, and how to use them.

- We assume that you have downloaded, installed and initialized the SDK as described in [Getting Started](https://intl.cloud.tencent.com/document/product/436/11280).
- We recommend using Command+F to search for the API you want, check the provided description of the API, and then copy the sample code to your project for execution.

> ?If you want to learn more about the function of the API or the meanings of its parameters, we recommend directly viewing the comments provided in the code. In Xcode, you can use a three-finger tap, Force Touch, or you can hover over a variable and press Control+Command+D to see its explanation.   

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Configuring pre-flight requests for cross-origin access | Sends a pre-flight request to confirm whether a real cross-origin access request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Object](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

**Multipart operations**

| API          | Operation                   | Description                                       |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in multiple parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an existing object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specific multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload operation | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload operation | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets the ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

## Advanced APIs (recommended)

This section outlines advanced APIs for uploading and copying. You only need to set the required parameters, and the APIs will automatically decide whether to perform simple upload/copy or multipart upload/copy based on the file size. Before using the APIs, make sure you have completed the initialization process as instructed in [Getting Started](https://intl.cloud.tencent.com/document/product/436/11280).

### Uploading an object

Refer to [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/11280#.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1) the in the Getting Started guide for more information.

#### Checkpoint restart for object uploads

>?Checkpoint restart is only supported for uploading files in the sandbox.

This SDK uses multipart upload to upload any object larger than 1 MB in size. That is, the object will be split into multiple parts, each of 1 MB in size, and then uploaded using up to 4 concurrent uploads. Each successfully uploaded part is then stored on the backend server, providing the basis for the Checkpoint restart function.  

During a multipart upload operation, resumeData is generated after you initialize or cancel an upload. This data is used to generate another upload request when you wish to resume the upload operation. The following example shows how to get ResumeData:


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
    //This block will be called back after the Initiate Multipart Upload operation is complete so you can get resumeData
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
    //You can get the result from “result”
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
//Abort the multipart upload operation and delete uploaded parts
[put abort:^(id outputObject, NSError *error) {
//
}];

//···When initialization is complete but upload is not complete
NSError* error;
//The following shows how resumeData is generated after you cancel an upload
QCloudCOSXMLUploadObjectResumeData resumeData = [put cancelByProductingResumeData:&error];
QCloudCOSXMLUploadObjectRequest* request = nil;
if (resumeData) {
    request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
}
//The request generated can be used to directly resume the previous unsuccessful multipart upload
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
//Set the upload parameters
uploadRequest.initMultipleUploadFinishBlock = {(multipleUploadInitResult,resumeData) in
    //This block will be called back after the Initiate Multipart Upload operation is complete so you can get resumeData and generate a new multipart upload request.
    let resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumeData as Data?);
}
uploadRequest.sendProcessBlock = {(bytesSent , totalBytesSent , totalBytesExpectedToSend) in
    
}
uploadRequest.setFinish { (result, error) in
    if error != nil{
        print(error!)
    }else{
        //Get the request result from “result”
        print(result!);
    }}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(uploadRequest);

//···When initialization is complete but upload is not complete
var error:NSError?;
    //The following shows how resumeData is generated after you cancel an upload
do {
    let resumedData = try uploadRequest.cancel(byProductingResumeData: &error);
        var resumeUploadRequest:QCloudCOSXMLUploadObjectRequest<AnyObject>?;
             resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>.init(request: resumedData as Data?);
             //The request generated can be used to directly resume the previous unsuccessful multipart upload
    if resumeUploadRequest != nil {
        QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(resumeUploadRequest!);
    }
             
} catch  {
    print("resumeData is blank");
    return;
}
```

Note: multipart uploads have an operational principle wherein parts must be uploaded in a particular sequence. That is, only once a part has been successfully uploaded will it be stored on the backend server and will the process begin to overlap. Please note that under the following circumstances, checkpoint restart cannot be used, but instead the entire upload process must restart from the beginning.

- An object less than 1 MB in size is uploaded not using multipart upload.
- The simple upload API rather than the QCloudCOSXMLUploadObjectRequest class is used to upload files.
- The Initiate Multipart upload operation was not completed (the callback used for this purpose has yet to be invoked) upon cancelation of the generation of resumeData.

### Downloading an object

Refer to [Downloading an Object](https://intl.cloud.tencent.com/document/product/436/11280#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1) in the Getting Started guide for more information.

### Copying an object

#### Notes

Initialize a QCloudCOSXMLCopyObjectRequest object, and then call CopyObject from the QCloudCOSTransferMangerService. Note that multipart copy is automatically used for large files, but users will not be aware of this process.  

> !For cross-region replication, the region used for transferManager must be the same as the region used for the bucket.

#### QCloudCOSXMLCopyObjectRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | --------------------- | ---- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;,<br>such as examplebucket-1250000000 | NSString * | Yes |
| sourceBucket | Bucket containing the copied source file | NSString * | Yes |
| sourceObject | Object name (key) of the copied source file | NSString * | Yes |
| sourceAPPID | APPID of the copied source file | NSString * | Yes |
| sourceRegion | Region of the copied source file | NSString * | Yes |
| metadataDirective  | Indicates whether to copy metadata. Enumerated values: `Copy`, `Replaced`. Default: `Copy`.<br><li>If you specify this parameter as `Copy`, the metadata of the source file is copied directly and the user-defined metadata in the headers is ignored. <br><li>If you specify this parameter as `Replaced`, the metadata of the source file is replaced with the user-defined metadata in the headers. If the destination path is the same as the source path, meaning you want to modify the metadata, you must specify this parameter as `Replaced`**. | NSString * | No |
| storageClass | Object storage class. Enumerated values:<br><li>STANDARD (QCloudCOSStorageStandard)<br><li>STANDARD_IA (QCloudCOSStorageStandardIA)<br>Default value: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-transfer-copy-object)
```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];

request.bucket = @ "examplebucket-1250000000"; //Destination bucket <BucketName-APPID>, which must have public-read enabled or the current account must have access permission
request.object = @"exampleobject";//Destination file name
//File source bucket <BucketName-APPID>, which must have public-read enabled or the current account must have access permission
request.sourceBucket = @"sourcebucket-1250000000";
request.sourceObject = @"sourceObject";//Source file name
request.sourceAPPID = @"1250000000";//Source file APPID
request.sourceRegion= @"COS_REGION";//Source region

[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    //You can get the etag or custom headers in the outputObject response
}];

//For cross-region replication, the region used for transferManager must be the same as the region used for the bucket
[[QCloudCOSTransferMangerService defaultCOSTransferManager] CopyObject:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-transfer-copy-object)
```swift
let copyRequest =  QCloudCOSXMLCopyObjectRequest.init();
copyRequest.bucket = "examplebucket-1250000000";//Destination bucket <BucketName-APPID>, which must have public-read enabled or the current account must have access permission
copyRequest.object = "exampleobject";//Destination file name
//File source bucket <BucketName-APPID>, which must have public-read enabled or the current account must have access permission
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
//For cross-region replication, the region used for transferManager must be the same as the region used for the bucket
QCloudCOSTransferMangerService.defaultCOSTransferManager().copyObject(copyRequest);
```

## Simple Operations

### Querying an object list

#### Feature description

This API is used to query some or all objects in a bucket.

#### Method prototype

This operation requires importing the header file `QCloudCOSXML/QCloudCOSXML.h`. Before importing the file, you need to complete the [Initialization] (https://intl.cloud.tencent.com/document/product/436/11280#step1) process. First, generate a `QCloudPutBucketCORSRequest` instance, specify additional parameters as required, send the request, and then get the response. The detailed steps are outlined below:

1. Instantiate the QCloudGetBucketRequest and enter the required parameters.    
2. Call the GetBucket method from the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from QCloudListBucketResult in the callback block finishBlock.   

#### QCloudGetBucketRequest parameters

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| prefix | Prefix to be matched during the list operation; this parameter is used to specify the URL prefix of the files to be returned |  NSString * | No   |
| delimiter | The delimiter is a symbol that can be used to limit the results of a list operation.<br><li>If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed.<br><li>If no prefix is specified, the listing will start from the beginning of the path. It can be roughly regarded as an end marker. For example, to get paths that end with A, simply set this parameter to A. |  NSString * | No   |
| encodingType | Indicates the encoding method of the returned value. Valid value: url | NSString * | No |
| marker | By default, entries are listed in UTF-8 binary order starting from this marker | NSString * | No |
| maxKeys | Maximum number of entries returned at a time. Default: 1000 (Max.) | int | No |

#### Response description 

QCloudListBucketResult parameters

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | -------------------------------- |
| name | Bucket name | NSString * |
| prefix | Prefix to be matched during the list operation; this parameter is used to specify the URL prefix of the files to be returned | NSString *  |
| marker | by default, entries are listed in UTF-8 binary order starting from this marker | NSString * | No |
| nextMarker        | Marks the starting point of the next entry if the returned entry is truncated  | NSString *   |
| maxKeys | Maximum number of entries returned in a single response | int |
| delimiter | The delimiter is a symbol that can be used to limit the results of a list operation.<br><li>If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed.<br><li>If no prefix is specified, the listing will start from the beginning of the path. | NSString * |
| isTruncated | Indicates whether an entry in the response is truncated | BOOL |
| contents | Information about each object | NSArray<QCloudBucketContents*> * |
| commonPrefixes  | Groups together the identical paths between the values specified for `Prefix` and `delimiter` and defines them as a common prefix | NSArray<QCloudCommonPrefixes*> * |

QCloudBucketContents parameters

| Parameter Name | Description | Type |
| ------------ | --------------------------------------------------------- | ------------------------ |
| key | Object Key | NSString * |
| lastModified | Indicates when the object was last modified | NSString * |
| eTag | MD5 checksum of the file | NSString * |
| size | File size in bytes | int |
| owner | Bucket owner | QCloudBucketOwner * |
| storageClass | Object storage class. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE | QCloudCOSStorageClass  * |

QCloudBucketOwner parameters

| Parameter Name | Description | Type |
| ----------- | ------------------- | ---------- |
| identifier  | Bucket APPID | NSString * |
| displayName  | Name of the object owner | NSString * |



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
    //“result” contains the request result
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

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Uploading an object

#### Feature description

This API is used to upload an object (smaller than 20 MB) to a bucket. It supports uploading files stored in memory.

> !The number of ACL policies cannot exceed 1,000. Therefore, refrain from configuring an ACL policy for a particular object unless absolutely necessary as objects will inherit bucket permissions by default.

#### QCloudPutObjectRequest parameters

| Parameter Name           | Description                                                         | Type                  | Required |
| ------------------ | ------------------------------------------------------------ | --------------------- | ---- |
| Object | An object key is the unique identifier of an object in a bucket. For example, if an object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, such as `examplebucket-1250000000` | NSString * | Yes |
| body | If the file to be uploaded is stored on a disk, use the `NSURL * type variable` to indicate the file path.<br><li>If the file is stored in memory, use the `NSData * type variable` containing the file’s binary data. | BodyType | Yes    |
| storageClass | Object storage class. Enumerated values: STANDARD (QCloudCOSStorageStandard), STANDARD_IA (QCloudCOSStorageStandardIA), ARCHIVE (QCloudCOSStorageARCHIVE). Default value: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |
| cacheControl | Cache policy as defined in RFC 2616, which will be stored in the object metadata | NSString * | No |
| contentDisposition | Filename as defined in RFC 2616, which will be stored in the object metadata | NSString * | No |
| expect | When expect=@"100-Continue" is used, the request content will be sent only after confirmation from the server is received. | NSString * | No |
| expires | Expiration time as defined in RFC 2616, which will be stored in the object metadata | NSString * | No |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read, and default; Default value: default (i.e., the object inherits bucket permissions).<br>Note: currently, you can set up to 1,000 bucket ACL rules. If you do not need to configure an ACL rule for a particular object, set this parameter to `default`, or simply leave it blank and bucket permissions will be inherited by default. | NSString * | No |
| grantRead | Grants read permission in the format: id="OwnerUin" | NSString * | No |
| grantWrite | Grants write permission in the format: `id="OwnerUin"` | NSString * | No |
| grantFullControl | Grants full permission in the format: id="OwnerUin" | NSString * | No |

#### Samples    


Objective-C code sample:

[//]: # (.cssg-snippet-objc-put-object)
```objective-C
QCloudPutObjectRequest* put = [QCloudPutObjectRequest new];
put.object = @"exampleobject";
put.bucket = @"examplebucket-1250000000";
put.body =  [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];

[put setFinishBlock:^(id outputObject, NSError *error) {
    //You can get the etag or custom headers in the outputObject response
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

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying object metadata

#### Feature description

This API is used to query the metadata of an object.

#### Method prototype

This operation requires importing the header file `QCloudCOSXML/QCloudCOSXML.h`. Before importing the file, you need to complete the [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1) process. First, generate a QCloudHeadObjectRequest instance, specify additional parameters as required, send the request, and then get the response. The detailed steps are outlined below:    

1. Instantiate the QCloudHeadObjectRequest and specify the required parameters.    
2. Call the HeadObject method from the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudHeadObjectRequest parameters

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ---------- | ---- |
| Object | An object key is the unique identifier of an object in a bucket. For example, if an object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/text.txt`, the object key would be `doc/text.txt`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| ifModifiedSince | The file content is only returned if the file is modified after the specified time. Otherwise, HTTP status code 304 (not modified) is returned. | NSString * | Yes |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-head-object)
```objective-c
QCloudHeadObjectRequest* headerRequest = [QCloudHeadObjectRequest new];
headerRequest.object = @"exampleobject";
headerRequest.bucket = @"examplebucket-1250000000";

[headerRequest setFinishBlock:^(NSDictionary* result, NSError *error) {
    //“result” contains the request result
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

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Downloading an object

#### Feature description

This API is used to download an object to the local file system.

#### Method prototype

This operation requires importing the header file `QCloudCOSXML/QCloudCOSXML.h`. Before importing the file, you need to complete the [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1) process. First, generate an instance, specify additional parameters as required, send the request, and then get the response. The detailed steps are outlined below:    

1. Instantiate the object QCloudGetObjectRequest and specify the required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudGetObjectRequest parameters

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| range | The specified byte range for file downloads as defined in RFC 2616 | NSString * | No |
| ifModifiedSince | The file content is only returned if the file is modified after the specified time. Otherwise, HTTP status code 412 (not modified) is returned. | NSString * | No |
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
//Set the download URL. Once set, the file will be downloaded to the specified path.
//If this parameter is not set, the file will be downloaded to memory and stored in the outputObject of finishBlock.
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";

[request setFinishBlock:^(id outputObject, NSError *error) {
    //You can get the etag or custom headers in the outputObject response
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

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Configuring pre-flight requests for cross-origin access

#### Feature description

This API is used to initiate a pre-flight request to check whether you can send a cross-origin access request.

#### Method prototype

This operation requires importing the header file `QCloudCOSXML/QCloudCOSXML.h`. Before importing the file, you need to complete the [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1) process. First, generate a QCloudOptionsObjectRequest instance, specify additional parameters as required, send the request, and then get the response. The detailed steps are outlined below:    

1. Instantiate the QCloudOptionsObjectRequest, specify the object name, bucket name, and both the HTTP method and allowed access sources to simulate the CORS request.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudOptionsObjectRequest parameters

| Parameter Name |  Description | Type |Required |
| -------------------------- | ------------------------------------------------------------ | --------------------------- | ---- |
| object | An object key is the unique identifier of an object in a bucket. For example, if an object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| accessControlRequestMethod | The HTTP method used to simulate the CORS request | NSArray&lt;NSString`*`> * | Yes |
| origin | The allowed access sources used to simulate the CORS requests. The wildcard `*` is supported.<br>Format: `protocol://domain name[:port]`,<br>for example, `http://www.qq.com`. | NSString * | Yes |
| allowedHeader | Tells the server what custom HTTP request headers can be used for subsequent requests when the `OPTIONS` request is sent. The wildcard `*` is supported | NSArray&lt;NSString `*` > * | No |

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
    //You can get the etag or custom headers in the outputObject response
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

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Copying an object

#### Feature description

This API is used to copy a file to the destination path.

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
    //“result” contains the response result
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
| bucket | Destination bucket name in the format: &lt;BucketName-APPID&gt;,<br>such as examplebucket-1250000000 | NSString * | Yes |
| object | Object key of the destination file | NSString * | Yes |
| objectCopySource | The path of the copied source file | NSString * | Yes |
| metadataDirective  | Indicates whether to copy metadata. Enumerated values: `Copy`, `Replaced`. Default: `Copy`.<br><li>If you specify this parameter as `Copy`, the metadata of the source file is copied directly and the user-defined metadata in the headers is ignored. <br><li>If you specify this parameter as `Replaced`, the metadata of the source file is replaced with the user-defined metadata in the headers. If the destination path is the same as the source path, meaning you want to modify the metadata, you must specify this parameter as `Replaced`**. | NSString * | No |
| storageClass | Object storage class. Enumerated values:<br><li>STANDARD (QCloudCOSStorageStandard)<br><li>STANDARD_IA (QCloudCOSStorageStandardIA)<br>Default value: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read, and default; Default value: default (i.e., the object inherits bucket permissions).<br>Note: currently, you can set up to 1,000 bucket ACL rules. If you do not need to configure an ACL rule for a particular object, set this parameter to `default`, or simply leave it blank and bucket permissions will be inherited by default. | NSString * | No |
| grantRead | Grants read permission in the format: id="OwnerUin" | NSString * | No |
| grantWrite | Grants write permission in the format: id="OwnerUin" | NSString * | No |
| grantFullControl | Grants full permission in the format: id="OwnerUin" | NSString * | No |
| versionID | Specifies the versionID of the source file. Only buckets that have versioning enabled or suspended will provide a response for this parameter. | NSString * | No |

#### Response description

The response is returned using QCloudCopyObjectResult.

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ---------- |
| ETag | Returns the MD5 checksum of the file; this value is used to check whether the object content has changed | NSString * |
| lastModified | Indicates when the file was last modified in GMT format  | NSString * |
| versionID | Version ID of the object; only used for a versioning-enabled bucket | NSString * |

#### Error codes

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting a single object

#### Feature description

This API is used to delete a specified object from a bucket.

#### Method prototype

This operation requires importing the header file `QCloudCOSXML/QCloudCOSXML.h`. Before importing the file, you need to complete the [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1) process. First, generate a QCloudDeleteObjectRequest instance, specify additional parameters as required, send the request, and then get the response. The detailed steps are outlined below:    

1. Instantiate the QCloudDeleteObjectRequest and specify the required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudDeleteObjectRequest parameters

| Parameter Name | Type | Required |Description |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| object | An object key is the unique identifier of an object in a bucket. For example, if an object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key would be `doc/pic.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket). | NSString * | Yes |

#### Samples


Objective-C code sample:


[//]: # (.cssg-snippet-objc-delete-object)
```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
deleteObjectRequest.bucket = @"examplebucket-1250000000";
deleteObjectRequest.object = @"exampleobject";

[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    //You can get the etag or custom headers in the outputObject response
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

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting multiple objects

#### Method prototype

This operation requires importing the header file `QCloudCOSXML/QCloudCOSXML.h`. Before importing the file, you need to complete the [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1) process. First, generate a QCloudDeleteMultipleObjectRequest instance, specify additional parameters as required, send the request, and then get the response. The detailed steps are outlined below:    

1. Instantiate the QCloudDeleteMultipleObjectRequest, enter the required parameters, encapsulate the object you want to delete into a QCloudDeleteObjectInfo object, and place it in the deleteObjects object array.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudDeleteMultipleObjectRequest parameters

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ------------------ | ---- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| deleteObjects | Encapsulates the multiple objects to be deleted | QCloudDeleteInfo * | Yes |

QCloudDeleteInfo parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ----------------------------------------- | ---- |
| objects  | An array of objects to be deleted | NSArray&lt;QCloudDeleteObjectInfo `*` > * | Yes |
| Quiet | A boolean value that specifies whether Quiet mode is enabled: <br><li>true: enable Quiet mode<br><li>false: enable Verbose mode<br>Default: false | NSArray% encTxtlt; QCloudDeleteObjectInfo `*`> * | No |

CloudDeleteObjectInfo parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| key | An object key is the unique identifier of an object in a bucket. For example, if an object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |

#### Response description

QCloudDeleteResult parameters

| Parameter Name | Description | Type |
| -------------- | -------------------------------------------------- | --------------------------------- |
| deletedObjects | An array of deleted objects | NSArray<QCloudDeleteResultRow*> * |
| lastModified | Indicates when the file was last modified in GMT format | NSString * |
| versionID | Version ID of the object; only used for a versioning-enabled bucket | NSString * |

QCloudDeleteResultRow parameters

| Parameter Name | Description | Type |
| -------- | --------------- | ---------- |
| key | The key of a deleted object | NSString * |

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
    //You can get the etag or custom headers in the outputObject response
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

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by the device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Multipart Operations



- Uploading objects with multipart upload: initializing a multipart upload, uploading parts, and completing a multipart upload.
- Resuming a multipart upload: querying uploaded parts, uploading remaining parts, and completing a multipart upload.
- Deleting uploaded parts.

### Querying multipart uploads

#### Feature description

This API is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

This operation requires importing the header file `QCloudCOSXML/QCloudCOSXML.h`. Before importing the file, you need to complete the [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1) process. First, generate a QCloudListBucketMultipartUploadsRequest instance, specify additional parameters as required, send the request, and then get the response. The detailed steps are outlined below:    

1. Instantiate the QCloudListBucketMultipartUploadsRequest and enter the required parameters, such as the prefix and the encoding method of the returned result.    
2. Call the ListBucketMultipartUploads method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response content from outputObject in the callback block finishBlock.   

#### QCloudListBucketMultipartUploadsRequest parameters

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| prefix | Specifies that the returned object key must be prefixed with this value. Note that when using a prefix to query object keys, the returned key will still contain the specified prefix. | NSString * | No |
| delimiter | The delimiter is a symbol that can be used to limit the results of a list operation.<br><li>If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed.<br><li>If no prefix is specified, the listing will start from the beginning of the path. It can be roughly regarded as an end marker. For example, to get paths that end with A, simply set this parameter to A. |  NSString * | No   |
| encodingType | Indicates the encoding method of the returned value. Valid value: url | NSString * | No |
| keyMarker | Entries will be listed starting from this key | NSString * | No |
| uploadIDMarker | Entries will be listed starting from this UploadId | int | No |
| maxUploads | Sets the maximum number of returned multipart uploads. Valid value: 1-1000 | int | No |

#### Response description

QCloudListMultipartUploadsResult parameters

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ---------- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * |
| prefix | Specifies that the returned object key must be prefixed with this value. Note that when using a prefix to query object keys, the returned key will still contain the specified prefix. | NSString * |
| delimiter | The delimiter is a symbol that can be used to limit the results of a list operation.<br><li>If a particular prefix is specified, identical paths between the prefix and the delimiter will be grouped together and defined as a common prefix, and then all common prefixes will be listed.<br><li>If no prefix is specified, the listing will start from the beginning of the path. |  NSString * |
| encodingType | Indicates the encoding method of the returned value. Valid value: url | NSString * |
| keyMarker | Entries will be listed starting from this key | NSString * |
| maxUploads | Sets the maximum number of returned multipart uploads. Valid value: 1-1000 | int |
| uploads | Information on all uploaded parts | NSArray* |
| isTruncated | Indicates whether the file is truncated | NSString * |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-list-multi-upload)
```objecitve-c
QCloudListBucketMultipartUploadsRequest* uploads = [QCloudListBucketMultipartUploadsRequest new];
uploads.bucket = @"examplebucket-1250000000";
uploads.maxUploads = 100;

[uploads setFinishBlock:^(QCloudListMultipartUploadsResult* result, NSError *error) {
    //Get the information on multipart uploads from “result”
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

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues. Error codes (outlined in the returned error field) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).


### <span id = "INIT_MULIT_UPLOAD">Initializing a multipart upload </span>

#### Feature description

This API is used to initialize a multipart upload operation and obtain its uploadId.

#### Method prototype

This operation requires importing the header file `QCloudCOSXML/QCloudCOSXML.h`. Before importing the file, you need to complete the [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1) process. First, generate a QCloudInitiateMultipartUploadRequest instance, specify additional parameters as required, send the request, and then get the response. The detailed steps are outlined below:    

1. Instantiate the QCloudInitiateMultipartUploadRequest and enter the required parameters.    
2. Call the InitiateMultipartUpload method in the QCloudCOSXMLService object to initiate a request.    
3. Get the response content from the callback block finishBlock.   

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | --------------------- | ---- |
| Object | The file name, or object key, is the unique identifier of an uploaded file (object) in a bucket. For example, if an object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| cacheControl | Cache policy defined in RFC 2616 | NSString * | No |
| contentDisposition | File name defined in RFC 2616 | NSString * | No |
| expect | If `expect=@"100-continue"` is used, the request content will be sent only after confirmation from the server is received |  NSString * | No |
| expires | Expiration time defined in RFC 2616 | NSString * | No |
| storageClass | Object storage class, enumerated values:<br><li>STANDARD(QCloudCOSStorageStandard)<br><li>STANDARD_IA(QCloudCOSStorageStandardIA)<br><li>ARCHIVE(QCloudCOSStorageARCHIVE)<br>Default: STANDARD(QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read, and default; Default value: default (i.e., the object inherits bucket permissions).<br>Note: currently, you can set up to 1,000 bucket ACL rules. If you do not need to configure an ACL rule for a particular object, set this parameter to `default`, or simply leave it blank and bucket permissions will be inherited by default. | NSString * | No |
| grantRead | Grants read permission in the format: id="OwnerUin" | NSString * | No |
| grantWrite | Grants write permission in the format: `id="OwnerUin"` | NSString * | No |
| grantFullControl | Grants full permission in the format: id="OwnerUin" | NSString * | No |

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

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Uploading parts

#### Feature description

This API is used to upload a file in multiple parts.

#### QCloudUploadPartRequest parameters

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of the multipart upload.<br>When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID helps uniquely identify parts in the multipart upload, and their relative position in the entire file | NSString * | Yes |
| partNumber  | A number used to identify a part | int | Yes  |
| contentSHA1 | SHA1 value of the part | NSString * | Yes |
| body | Uploaded data: supports `NSData *`, `NSURL` (local URL) and `QCloudFileOffsetBody*` | BodyType | Yes |

#### Response description

QCloudUploadPartResult parameters

| Parameter Name | Description | Type |
| -------- | ----------- | ---------- |
| eTag | File etag | NSString * |

#### Method prototype

The specific steps for requesting a multipart upload in the COS iOS SDK are outlined below:

1. Instantiate the QCloudUploadPartRequest and specify the required parameters.
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
//Marks the ID of the multipart upload. When you use the Initiate Multipart Upload API to initialize a multipart upload, you will get an uploadId.
//This ID not only helps uniquely identify the parts in the multipart upload, but also their relative position in the entire file.
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
    //Save it for future use after the upload is complete
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
//Marks the ID of the multipart upload. When you use the Initiate Multipart Upload API to initialize a multipart upload, you will get an uploadId.
//This ID not only helps uniquely identify the parts in the multipart upload, but also their relative position in the entire file.
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
        //Save it for future use after the upload is complete
        self.parts = [mutipartInfo];
    }}
uploadPart.sendProcessBlock = {(bytesSent,totalBytesSent,totalBytesExpectedToSend) in
    //Upload progress information
    print("totalBytesSent:\(totalBytesSent) totalBytesExpectedToSend:\(totalBytesExpectedToSend)");
    
}
QCloudCOSXMLService.defaultCOSXML().uploadPart(uploadPart);
```
#### Error codes

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Copying a part

#### Feature description

This API (Upload Part - Copy) is used to copy an existing object to be part of a new object.

#### QCloudUploadPartRequest parameters

| Parameter Name | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of the multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID helps uniquely identify parts in the multipart upload, and their relative position in the entire file | NSString *  | Yes |
| partNumber  | A number used to identify a part                                     | int | Yes  |
| source | URL path of the source file. A past object version can be specified using the `versionId` sub-resource | NSString * | Yes |
| body | Uploaded data: supports `NSData *`, `NSURL` (local URL) and `QCloudFileOffsetBody*` | BodyType | Yes |

#### Response description

QCloudUploadPartResult parameters

| Parameter Name | Description | Type |
| -------- | ----------- | ---------- |
| eTag | File etag | NSString * |

#### Method prototype

The specific steps for requesting a multipart upload in the COS iOS SDK are outlined below:

1. Instantiate the QCloudUploadPartCopyRequest and enter the required parameters.
2. Call the UploadPartCopy method in the QCloudCOSXMLService object to initiate a request.
3. Obtain the response content from QCloudCopyObjectResult in the callback block finishBlock.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-upload-part-copy)
```objective-c
QCloudUploadPartCopyRequest* request = [[QCloudUploadPartCopyRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
request.object = @"exampleobject";
//The URL path of the source file. You can specify a past object version using the versionId sub-resource.
request.source = @"sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject";
//The Initiate Multipart Upload request returns an upload ID used to uniquely identify the upload.
request.uploadID = @"exampleUploadId";
request.partNumber = 1; //Mark the part number of the current part.

[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    QCloudMultipartInfo *part = [QCloudMultipartInfo new];
    //Get the etag of the copied part
    part.eTag = result.eTag;
    part.partNumber = @"1";
    //Save it for future use after the upload is complete
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
//The URL path of the source file. You can specify a past object version using the versionId sub-resource.
req.source = "sourcebucket-1250000000.cos.COS_REGION.myqcloud.com/sourceObject";
//The Initiate Multipart Upload request returns an upload ID used to uniquely identify the upload.
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

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### <span id = "LIST_MULIT_UPLOAD">Querying uploaded parts</span>

#### Feature description

This API is used to query the uploaded parts associated with a specified uploadId.

#### QCloudListMultipartRequest parameters

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | uploadId of the multiple upload for which the parts are to be queried | NSString * | Yes |
| maxPartsCount | Maximum number of entries returned at a time. Default value: 1,000 | NSString * | No |
| partNumberMarker | Marks the starting point of the list of parts; by default, entries are listed in UTF-8 binary order starting from this marker | NSString * | No   |
| encodingType | Specifies the encoding type of the returned value | int        | No   |

#### Response description

 QCloudListPartsResult parameters

| Parameter Name | Description | Type |
| ---------------- | ------------------------------------------------------------ | -------------------------- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * |
| encodingType | Specifies the encoding type of the returned value | NSString * |
| key | Object Name | NSString * |
| uploadId | UploadId of the multipart upload for which the parts are to be queried | NSString * |
| storageClass | Indicates the storage class of the object parts | QCloudCOSStorageClass |
| partNumberMarker | Marks the starting point of the list of parts; by default, entries are listed in UTF-8 binary order starting from this marker | int |
| nextNumberMarker | Marks the starting point of the next entry if the returned entry is truncated | NSString * |
| maxParts | Maximum number of entries returned at a time | QCloudCOSStorageClass |
| isTruncated | Indicates whether the returned entry is truncated | BOOL |
| initiator | Identifies the initiator of the upload | NSString * |
| owner | Identifies the owner of parts | QCloudCOSStorageClass |
| parts | Provides information on each part | QCloudMultipartUploadPart* |

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-list-parts)
```objective-c
QCloudListMultipartRequest* request = [QCloudListMultipartRequest new];
request.object = @"exampleobject";
request.bucket = @"examplebucket-1250000000";
//The Initiate Multipart Upload request returns an upload ID used to uniquely identify the upload.
request.uploadId = @"exampleUploadId";

[request setFinishBlock:^(QCloudListPartsResult * _Nonnull result, NSError * _Nonnull error) {
    //Get the information on uploaded parts from “result”
}];

[[QCloudCOSXMLService defaultCOSXML] ListMultipart:request];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-list-parts)
```swift
let req = QCloudListMultipartRequest.init();
req.object = "exampleobject";
req.bucket = "examplebucket-1250000000";
//The Initiate Multipart Upload request returns an upload ID used to uniquely identify the upload.
req.uploadId = "exampleUploadId";
if self.uploadId != nil {
    req.uploadId = self.uploadId!;
}
req.setFinish { (result, error) in
    if error != nil{
        print(error!);
    }else{
        //Get the information on uploaded parts from “result”
        print(result!);
    }}

QCloudCOSXMLService.defaultCOSXML().listMultipart(req);
```

#### Error codes

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### <span id = "COMPLETE_MULIT_UPLOAD"> Completing a multipart upload operation </span>

#### Feature description

This API is used to complete a multipart upload operation.

#### QCloudCompleteMultipartUploadRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ----------------------------------- | ---- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of the multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID helps uniquely identify parts in the multipart upload, and their relative position in the entire file | NSString * | Yes |
| parts | Information about completing the multipart upload | QCloudCompleteMultipartUploadInfo * | Yes |

#### Response description

 QCloudUploadObjectResult parameters

| Parameter Name | Description | Type |
| --------- | ------------------------------------------------------------ | ---------- |
| location | The public endpoint for the existing object | NSString * |
| bucket | Name of the destination bucket for the multipart upload in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * |
| key | Object Name | NSString * |
| eTag | MD5 checksum of the merged file | NSString * |
| versionID | Version ID of the object; only used for a versioning-enabled bucket | NSString * |

#### Method prototype

The specific steps for initiating a Complete Multipart Upload request in the COS iOS SDK are outlined below:

1. Instantiate the QCloudCompleteMultipartUploadRequest and specify the required parameters.
2. Call the CompleteMultipartUpload method in the QCloudCOSXMLService object to initiate a request.
3. Obtain the response content from QCloudUploadObjectResult in the callback block finishBlock.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-complete-multi-upload)
```objective-c
QCloudCompleteMultipartUploadRequest *completeRequst = [QCloudCompleteMultipartUploadRequest new];
completeRequst.object = @"exampleobject";
completeRequst.bucket = @"examplebucket-1250000000";
//The uploadId of the multipart upload for which the parts are to be queried can be obtained from the request result QCloudInitiateMultipartUploadResult
completeRequst.uploadId = @"exampleUploadId";
//Information on the uploaded parts
QCloudCompleteMultipartUploadInfo *partInfo = [QCloudCompleteMultipartUploadInfo new];
partInfo.parts = self.parts;
completeRequst.parts = partInfo;

[completeRequst setFinishBlock:^(QCloudUploadObjectResult * _Nonnull result, NSError * _Nonnull error) {
    //Get the upload result from “result”
}];

[[QCloudCOSXMLService defaultCOSXML] CompleteMultipartUpload:completeRequst];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-complete-multi-upload)
```swift
let  complete = QCloudCompleteMultipartUploadRequest.init();
complete.bucket = "examplebucket-1250000000";
complete.object = "exampleobject";
//The uploadId of the multipart upload for which the parts are to be queried can be obtained from the request result QCloudInitiateMultipartUploadResult
complete.uploadId = "exampleUploadId";
if self.uploadId != nil {
    complete.uploadId = self.uploadId!;
}


//Information on the uploaded parts
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
        //Get the upload result from “result”
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().completeMultipartUpload(complete);
```
#### Error codes

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### <span id = "ABORT_MULIT_UPLOAD"> Aborting a multipart upload operation </span>

#### Feature description

This API is used to abort a multipart upload operation and delete the uploaded parts.

#### QCloudAbortMultipfartUploadRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format: BucketName-APPID, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| uploadId | ID of the multipart upload to abort. When the `Initiate Multipart Upload` API is used to initialize a multipart upload operation, an `uploadId` will be returned. This ID helps uniquely identify parts in the multipart upload, and their relative position in the entire file | NSString * | Yes |

#### Method prototype

The specific steps for initiating an Abort Multipart Upload request in the COS iOS SDK are outlined below:

1. Instantiate the QCloudAbortMultipfartUploadRequest and specify the required parameters.
2. Call the AbortMultipfartUpload method in the QCloudCOSXMLService object to initiate a request.
3. Obtain the response content from outputObject in the callback block finishBlock.

#### Samples


Objective-C code sample:

[//]: # (.cssg-snippet-objc-abort-multi-upload)
```objective-c
QCloudAbortMultipfartUploadRequest *abortRequest = [QCloudAbortMultipfartUploadRequest new];
abortRequest.object = @"exampleobject";
abortRequest.bucket = @"examplebucket-1250000000";
//The uploadId of the multipart upload for which the parts are to be queried can be obtained from the request result QCloudInitiateMultipartUploadResult
abortRequest.uploadId = @"exampleUploadId";

[abortRequest setFinishBlock:^(id outputObject, NSError *error) {
    //You can get the etag or custom headers in the outputObject response
}];

[[QCloudCOSXMLService defaultCOSXML]AbortMultipfartUpload:abortRequest];
```

Swift code sample:

[//]: # (.cssg-snippet-swift-abort-multi-upload)
```swift
let abort = QCloudAbortMultipfartUploadRequest.init();
abort.bucket = "examplebucket-1250000000";
abort.object = "exampleobject";
//The uploadId of the multipart upload for which the parts are to be queried can be obtained from the request result QCloudInitiateMultipartUploadResult
abort.uploadId = "exampleUploadId";
if self.uploadId != nil {
    abort.uploadId = self.uploadId!;
}

abort.finishBlock = {(result,error)in
    if error != nil{
        print(error!)
    }else{
        //You can get the etag or custom headers in the outputObject response
        print(result!);
    }    
}
QCloudCOSXMLService.defaultCOSXML().abortMultipfartUpload(abort);
```
#### Error codes

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Other Operations

### Restoring an archived object

#### Feature description

This API is used to restore an archived object for access.

#### Method prototype

This operation requires importing the header file `QCloudCOSXML/QCloudCOSXML.h`. Before importing the file, you need to complete the [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1) process. First, generate a QCloudPostObjectRestoreRequest instance, specify additional parameters as required, send the request, and then get the response. The detailed steps are outlined below:    

1. Instantiate the QCloudPostObjectRestoreRequest and enter the relevant object name and bucket name.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Get the response content from the callback block finishBlock.   

#### QCloudPostObjectRestoreRequest parameters

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| object | An object key is the unique identifier of an object in a bucket. For example, if an object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`, the object key would be `doc/picture.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| restoreRequest | Data restoration configuration | QCloudRestoreRequest * | Yes |

QCloudRestoreRequest parameters

| Parameter Name | Description | Type | Required |
| ---------------- | ---------------------- | ------------------ | ---- |
| days | Specifies the number of days before a temporary copy expires | int64_t | Yes |
| CASJobParameters | Restoration type configuration | CASJobParameters * | Yes |

CASJobParameters parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------------- | ---- |
| tier | Specifies one of the three restoration types: <br><li>Standard, which completes a restoration job in 3-5 hours<br><li>Expedited, which completes a restoration job in 1-5 minutes<br><li>Bulk, which completes multiple restoration jobs in 5-12 hours | QCloudCASTier | Yes |

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
    //You can get the etag or custom headers in the outputObject response
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
        //You can get the etag or custom headers in the outputObject response
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().postObjectRestore(restore);
```

#### Error codes

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Setting an object ACL

#### Feature description

This API is used to set an access control list (ACL) for an object.

#### Method prototype

This operation requires importing the header file `QCloudCOSXML/QCloudCOSXML.h`. Before importing the file, you need to complete the [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1) process. First, generate a QCloudPutObjectACLRequest instance, specify additional parameters as required, send the request, and then get the response. The detailed steps are outlined below:    

1. Instantiate the QCloudPutObjectACLRequest and enter the bucket name, authorization information, and any other required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the response from the callback block finishBlock. An empty `error` field indicates a successful request.   

#### QCloudPutObjectACLRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`.<br>The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | Object name | NSString * | Yes |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read, and default; Default value: default (i.e., the object inherits bucket permissions).<br>Note: currently, you can set up to 1,000 bucket ACL rules. If you do not need to configure an ACL rule for a particular object, set this parameter to `default`, or simply leave it blank and bucket permissions will be inherited by default. | NSString * | No |
| grantRead | Grants read permission in the format: id="OwnerUin" | NSString * | No |
| grantWrite | Grants write permission in the format: id="OwnerUin" | NSString * | No |
| grantFullControl | Grants full permission in the format: id="OwnerUin" | NSString * | No |

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
    //You can get the etag or custom headers in the outputObject response
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
        //You can get the etag or custom headers in the outputObject response
        print(result!);
    }}
QCloudCOSXMLService.defaultCOSXML().putObjectACL(putObjectACl);
```
#### Error codes

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Querying an object ACL

#### Feature description

This API is used to query the ACL of an object.

#### Method prototype

This operation requires importing the header file `QCloudCOSXML/QCloudCOSXML.h`. Before importing the file, you need to complete the [Initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1) process. First, generate a QCloudGetObjectACLRequest instance, specify additional parameters as required, send the request, and then get the response. The detailed steps are outlined below:    

1. Instantiate the QCloudGetObjectACLRequest and enter the bucket name and the name of the object to be queried.    
2. Call the GetObjectACL method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the ACLs encapsulated in the QCloudACLPolicy object in the callback block finishBlock.   

#### QCloudGetObjectACLRequest parameters

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name in the format: &lt;BucketName-APPID&gt;, for example: `examplebucket-1250000000`. The bucket name can also be found on the [COS Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes |
| object | An object key is the unique identifier of an object in a bucket. For example, if an object's endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key would be `doc/pic.jpg`. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| versionID | Specifies Version ID of an object if versioning is enabled | NSString * | Yes |

#### Response description

QCloudACLPolicy parameters

| Parameter Name | Description | Type |
| ----------------- | ---------------------- | ------------------------- |
| owner | Bucket owner | QCloudACLOwner * |
| accessControlList | Information on the authorized user and granted permissions | QCloudAccessControlList * |

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
| grantee | Describes information on the grantee. The grantee type can be either a RootAccount or Subaccount<br><li>If it is a RootAccount, the ID specifies a root account<br><li>If it is a Subaccount, the ID specifies a sub-account | QCloudACLGrantee * |
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
        //You can get the object ACL from the accessControlList field in the result
        print(result!.accessControlList);
    }}
QCloudCOSXMLService.defaultCOSXML().getObjectACL(getObjectACL);
```
#### Error codes

When the SDK request fails, the `error` field returned is not empty, but instead includes an error code, error description, and other necessary debugging information to help developers quickly fix any issues.

Error codes (outlined in the returned `error` field) include those returned by your device due to network problems as well as those returned by COS.

- Error codes generated by your device due to network problems are all 4-digit negative numbers, such as -1001. These error codes are defined by Apple. For more information, see the definitions present in the header file NSURLError.h in Foundation framework or see [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- The custom error codes for the SDK are all 5-digit positive numbers, such as 10000, 20000, etc. For more information on these error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Using Custom Headers

You can use custom headers as needed. Classes allowing custom headers are all marked with the customHeaders attribute:

```objective-c
@property (strong, nonatomic) NSMutableDictionary* customHeaders;
```

All key-value pairs in this attribute will be added accordingly to the HTTP headers used to construct the request.

## Server-Side Encryption

You can encrypt uploaded objects in the following ways.

#### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

COS can automatically encrypt your data when entered in IDC and will automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.

You can enable SSE-COS encryption by calling -(void)setCOSServerSideEncyption in the iOS SDK.

Objective-C code sample:
```objective-c
[request setCOSServerSideEncyption];
```

Swift code sample:
```swift
request.setCOSServerSideEncyption();
```

#### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

You can enable SSE-C encryption by calling -(void)setCOSServerSideEncyptionWithCustomerKey:(NSString \*)customerKey in the iOS SDK.

> !
>- This type of encryption requires using HTTPS requests.
>- customerKey: the key provided by the user; this key should be a 32-byte string consisting of numbers, letters, and symbols. Chinese characters are not supported.
>- If you used this method when uploading the source file, then it should also be used when downloading, querying, uploading, and copying the source object using QCloudCOSXMLDownloadObjectRequest, QCloudHeadObjectRequest, QCloudCOSXMLUploadObjectRequest and QCloudCOSXMLUploadObjectRequest respectively.

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
