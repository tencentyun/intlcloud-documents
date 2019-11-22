## Overview

This document provides an overview of APIs related to simple object operations, multipart upload, and other operations, corresponding SDK sample code, and usage examples.

- It is assumed that you have downloaded, installed, and initialized the SDK as instructed in [Getting Started](https://intl.cloud.tencent.com/document/product/436/11280).
- You are recommended to use Command+F to search for the API you want to query, check the provided descriptions of the API, and then copy the sample code to your project for execution.

>  If you want to learn more about the function of the API or the meanings of its parameters, you are recommended to directly view the comments in the code. In Xcode, you can use three-finger tap or Force Touch or hover over a variable and press Control+Command+D to see its interpretation.   

**Simple operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | Getting object list | Gets the list of objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object | Uploads an object (file/object) to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Getting object metadata | Gets the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Getting an object | Downloads an object (file/object) to the local file system |
| [Options Object](https://intl.cloud.tencent.com/document/product/436/8288) | Pre-requesting cross-origin configuration | Uses a pre-request to confirm whether a real cross-origin request can be sent |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes the specified object (file/object) in a bucket |
| [DELETE Multiple Object](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes objects (files/objects) in a bucket in batches |

**Multipart upload operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object (file/object) in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Getting object ACL | Gets the ACL of an object (file/object) |

## Advanced API (Recommended)

This section describes the advanced API that encapsulate the upload and copy operations. You only need to set the corresponding parameters, and the API will decide whether to perform simple upload/copy or multipart upload/copy according to the file size. Please confirm that the initialization as described in [Getting Started](https://intl.cloud.tencent.com/document/product/436/11280) has been completed before you use this API.

### Uploading an Object

You can see the [Uploading an Object](https://intl.cloud.tencent.com/document/product/436/11280#upload-a-file) section in Getting Started.

### Upload Resumption

If an object is larger than 1 MB, the SDK will upload it in a multipart manner, i.e., dividing it into multiple 1 MB parts and uploading them in parallel (up to 4 concurrent connections). The backend server will save each part upon upload completion, which serves as the basis for upload resumption.    

In the process of a multipart upload, a resumeData is generated when the multipart upload is completely initialized or canceled, which can be used to generate a new upload request for continued upload and the progress will be resumed. Below is an example of how to get the resumeData:

```objective-C
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
// Set some parameters of the upload
put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult, QCloudCOSXMLUploadObjectResumeData resumeData) {
	// After the initialization of the multipart upload is completed, this block will be called back, where you can get the resumeData which can be used to generate a new multipart upload request
	QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
};

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];

//••• After initialization is completed before upload is completed
NSError* error;
// This is an example of resumetData generated after cancellation is called
resumeData = [put cancelByProductingResumeData:&error];
if (resumeData) {
QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
 }
 // The request generated for resumption can start an upload directly
 [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];

```

Note that according to the mechanism of multipart upload, a part will be recorded and counted into the upload progress only after it is completely uploaded. In the following situations, an upload cannot be resumed; instead, it can only be restarted:

- The object to be uploaded is smaller than 1 MB, so multipart upload is not used.
- The simple upload API instead of the QCloudCOSXMLUploadObjectRequest class is used for upload.
- The initialization of the multipart upload has not been completed when the resumeData is generated upon cancellation, i.e., the callback of multipart upload initialization completion has not been called yet.

### Downloading an Object

You can see the [Downloading an Object](https://intl.cloud.tencent.com/document/product/436/11280#download-a-file) section in Getting Started.

### Copying an Object

#### Notes

Initialize a QCloudCOSXMLCopyObjectRequest object and then call the CopyObject method of QCloudCOSTransferMangerService. Note that larger files will be copied in a multipart manner, which is imperceptible to the user.  

> For cross-region replication, the region of the transferManager used must be the region of the destination bucket.

#### QCloudCOSXMLCopyObjectRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | --------------------- | ---- |
| bucket | Bucket name,  Its format is &lt;BucketName-APPID&gt;, such as examplebucket-1250000000 | NSString * | Yes |
| sourceBucket | Bucket of the file to be copied | NSString * | Yes |
| SourceObject | Object name (key) of the file to be copied | NSString * | Yes |
| sourceAPPID | APPID of the file to be copied | NSString * | Yes |
| sourceRegion | Region of the file to be copied | NSString * | Yes |
| metadataDirective | Whether to copy the metadata. Enumerated values: Copy, Replaced. Default value: Copy. If the flag is Copy, the user metadata in the header is ignored and the copy is performed directly; if the flag is Replaced, the metadata is modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), the flag has to be Replaced | NSString * | No |
| storageClass | Storage class of an object. Enumerated values: STANDARD (QCloudCOSStorageStandard), STANDARD_IA (QCloudCOSStorageStandardIA). Default value: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |

#### Examples

```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];
request.bucket = @"examplebucket-1250000000";// Destination <BucketName-APPID>, which should be public read or accessible by the current account
request.object = @"text.txt";// Destination file name
request.sourceBucket = @"examplebucket-1250000000";// File source <BucketName-APPID>, which should be public read or accessible by the current account
request.sourceObject = @"text.txt";// Source file name
request.sourceAPPID = @"appid";// Source file appid
request.sourceRegion= @"ap-beijing";// Source region
[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    // Complete the callback
   // You can get information such as etag or custom header in the response from outputObject (more header information can be viewed by printing the outputObject)
    if (nil == error) {
      // Success
    }
}];
// For cross-region replication, the region of the transferManager used must be the region of the destination bucket
[[QCloudCOSTransferMangerService defaultCOSTransferManager] CopyObject:request];
```

## Simple Operations

### Getting Object List

#### Feature Description

This API (Object List) is used to get all objects in a bucket.

#### Method Prototype

Before performing a bucket operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudGetBucketRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:

1. Instantiate QCloudGetBucketRequest and enter the required parameters.    
2. Call the GetBucket method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the QCloudListBucketResult in the finishBlock of the callback.   

#### QCloudGetBucketRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| prefix | Prefix match, used to specify the prefix address of the file returned | NSString * | No |
| delimiter | The delimiter is a symbol. If there is a prefix, the identical paths between prefix and delimiter are grouped into one class and defined as a common prefix, and then all common prefixes are listed. If there is no prefix, it starts at the beginning of the path and can be seen as the ending symbol. For example, if you want the results ending in A, then set delimiter to A. | NSString * | No |
| encodingType | Specifies the encoding method of the return value. Value range: url | NSString * | No |
| marker | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | NSString * | No |
| maxKeys | Maximum number of entries returned at a time; 1,000 by default; up to 1,000 | int | No |

#### Return Result Descriptions

QCloudListBucketResult parameter descriptions

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | -------------------------------- |
| name | Bucket name information | NSString * |
| prefix | Prefix match, used to specify the prefix address of the file returned in the response | NSString * |
| marker | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | NSString * |
| nextMarker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | NSString * |
| maxKeys | Maximum number of results returned in one response | int |
| delimiter | The delimiter is a symbol. If there is a prefix, the identical paths between prefix and delimiter are grouped into one class and defined as a common prefix, and then all common prefixes are listed. If there is no prefix, it starts at the beginning of the path | NSString * |
| isTruncated    | Whether response entries are truncated                                       | BOOL                             |
| contents | Information of each object | NSArray<QCloudBucketContents*> * |
| commonPrefixes | The identical paths between prefix and delimiter are grouped into one class and defined as a common prefix | NSArray<QCloudCommonPrefixes*> * |

QCloudBucketContents parameter descriptions

| Parameter Name | Description | Type |
| ------------ | --------------------------------------------------------- | ------------------------ |
| key | Object key | NSString * |
| lastModified | Describes when the object was last modified | NSString * |
| eTag | MD5 checksum of the file | NSString * |
| size | File size in bytes | int |
| owner | Bucket owner information | QCloudBucketOwner * |
| storageClass | Storage class of an object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE | QCloudCOSStorageClass  * |

QCloudBucketOwner parameter descriptions

| Parameter Name | Description | Type |
| ----------- | ------------------- | ---------- |
| identifier | Bucket APPID | NSString * |
| displayName | Object owner name | NSString * |



QCloudCommonPrefixes parameter descriptions

| Parameter Name | Description | Type |
| -------- | ------------------ | ---------- |
| prefix | A single common prefix | NSString * |

#### Examples

```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
request.bucket = @"examplebucket-1250000000";
request.maxKeys = 1000;
[request setFinishBlock:^(QCloudListBucketResult * result, NSError*   error) {
//additional actions after finishing
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Uploading an Object

#### Feature Description

This API (Put Object) is used to upload an object to the specified bucket. Simple upload can be used for small files (below 20 MB) only, but it supports uploading files from the memory.

>  Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, do not set it during the upload, so that the object will inherit the permissions of the bucket.

#### QCloudPutObjectRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | --------------------- | ---- |
| Object | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg, the object key is doc/picture.jpg. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | NSString * | Yes |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| body | If the file to be uploaded is stored on the disk, this parameter is the path to the file, and you should enter a `variable in NSURL * type`. If the file is stored in the memory, you can enter a `variable in NSData * type containing the file's binary data | BodyType | Yes |
| storageClass | Storage class of an object. Enumerated values: STANDARD (QCloudCOSStorageStandard), STANDARD_IA (QCloudCOSStorageStandardIA), ARCHIVE (QCloudCOSStorageARCHIVE). Default value: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |
| cacheControl | Cache policy as defined in RFC 2616, which will be stored as the object's metadata | NSString * | No |
| contentDisposition | File name as defined in RFC 2616, which will be stored as the object's metadata | NSString * | No |
| expect | If expect=@"100-Continue" is used, the request content will be sent only after confirmation from the server is received | NSString * | No|
| expires | File date and time as defined in RFC 2616, which will be stored as the object's metadata | NSString * | No |
| accessControlList | Defines the ACL attribute of the object, such as private, public-read, and default; default value: default (i.e., inheriting the bucket's permissions). Note: Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, use "default" for this parameter or simply leave it blank, so that the object will inherit the permissions of the bucket | NSString * | No |
| grantRead         | Grants the grantee read permission in the format of id="OwnerUin"                    | NSString * | No |
| grantWrite        | Grants the grantee write permission in the format of id="OwnerUin"                    | NSString * | No   |
| grantFullControl  | Grants the grantee read/write permission in the format of id="OwnerUin"                    | NSString * | No   |

#### Examples    

```objective-C
QCloudPutObjectRequest* put = [QCloudPutObjectRequest new];
put.object = @"text.txt";
put.bucket = @"examplebucket-1250000000";
put.body =  [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];
[put setFinishBlock:^(id outputObject, NSError *error) {
   // Complete the callback
  // You can get information such as etag or custom header in the response from outputObject (more header information can be viewed by printing the outputObject)
  if (nil == error) {
   // Success
   }
   }];
[[QCloudCOSXMLService defaultCOSXML] PutObject:put];

```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Getting Object Metadata

#### Feature Description

This API (Head Object) is used to query whether the specified object exists in a bucket.

#### Method Prototype

Before performing a file operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudHeadObjectRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudHeadObjectRequest and enter the required parameters.    
2. Call the HeadObject method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the outputObject in the finishBlock of the callback.   

#### QCloudHeadObjectRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ---------- | ---- |
| Object | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/text.txt, the object key is doc/text.txt. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | NSString * | Yes |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| ifModifiedSince | The file content is returned only if the file's last modified time is after the specified time; otherwise, 304 (not modified) is returned | NSString * | Yes |

#### Examples

```objective-c
QCloudHeadObjectRequest* headerRequest = [QCloudHeadObjectRequest new];
headerRequest.object = @"text.txt";
headerRequest.bucket = @"examplebucket-1250000000";

__block id resultError;
[headerRequest setFinishBlock:^(NSDictionary* result, NSError *error) {
      resultError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] HeadObject:headerRequest];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Getting an Object

#### Method Prototype

Before performing a file operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate an instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate the QCloudGetObjectRequest object and enter the required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the outputObject in the finishBlock of the callback.   

#### QCloudGetObjectRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| object | Object name | NSString * | Yes |
| range | Specified file download range in bytes as defined in RFC 2616 | NSString * | No |
| ifModifiedSince | The file content is returned only if the file's last modified time is after the specified time; otherwise, 412 (not modified) is returned | NSString * | No |
| responseContentType | Sets the Content-Type parameter in the response header | NSString * | No |
| responseContentLanguage | Sets the Content-Language parameter in the response header | NSString * | No |
| responseContentExpires | Sets the Content-Expires parameter in the response header | NSString * | No |
| responseCacheControl | Sets the Cache-Control parameter in the response header | NSString * | No |
| responseContentDisposition | Sets the Content-Disposition parameter in the response header | NSString * | No |
| responseContentEncoding | Sets the Content-Encoding parameter in the response header | NSString * | No |

#### Examples

```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
// Set the download path URL; if this is set, the file will be downloaded to the specified path; otherwise, the file will be downloaded to the memory and stored in the 	outputObject of the finishBlock.
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @“text.txt”;
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(id outputObject, NSError *error) {
    //additional actions after finishing
   // You can get information such as etag or custom header in the response from outputObject (more header information can be viewed by printing the outputObject)
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload, int64_t totalBytesExpectedToDownload) {
   // Download progress
}];
[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Pre-requesting Cross-origin Configuration

#### Feature Description

This API (Options Object) is used to pre-request the cross-origin configuration.

#### Method Prototype

Before performing a file operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudOptionsObjectRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudOptionsObjectRequest and enter the object name, bucket name, HTTP method of the simulated cross-origin access request, and the origin allowed for the simulated cross-origin access.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the outputObject in the finishBlock of the callback.   

#### QCloudOptionsObjectRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | --------------------------- | ---- |
| object | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg, the object key is doc/picture.jpg. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | NSString * | Yes |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| accessControlRequestMethod | HTTP method of the simulated cross-origin access request | NSArray&lt;NSString`*`> * | Yes |
| origin | Origin allowed for the simulated cross-origin access in the format of protocol://domain name[:port number], such as `http://www.qq.com`. Wildcard * is supported | NSString * | Yes |
| allowedHeader | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard * is supported | NSArray&lt;NSString `*` > * | No |

#### Examples

```objective-c
QCloudOptionsObjectRequest* request = [[QCloudOptionsObjectRequest alloc] init];
request.bucket =@"examplebucket-1250000000";
request.origin = @"*";
request.accessControlRequestMethod = @"get";
request.accessControlRequestHeaders = @"host";
request.object = @"picture.jpg";
__block id resultError;
[request setFinishBlock:^(id outputObject, NSError* error) {
     resultError = error;
	// You can get information such as etag or custom header in the response from outputObject (more header information can be viewed by printing the outputObject)
 }];

[[QCloudCOSXMLService defaultCOSXML] OptionsObject:request];

```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Setting Object Replication

This API (Put Object - Copy) is used to copy an object to another object.

#### Sample Request

```Objective-C
  QCloudPutObjectCopyRequest* request = [[QCloudPutObjectCopyRequest alloc] init];
  request.bucket = @"examplebucket-1250000000";
  request.object = @" ";
  [request setFinishBlock:^(QCloudCopyObjectResult * _Nonnull result, NSError * _Nonnull error) {

  }];
  request.objectCopySource = objectCopySource;// Path to the source object
  [[QCloudCOSXMLService defaultCOSXML]  PutObjectCopy:request];
```

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | --------------------- | ---- |
| bucket | Bucket name,  Its format is &lt;BucketName-APPID&gt;, such as examplebucket-1250000000 | NSString * | Yes |
| object | Object name (key) of the destination file | NSString * | Yes |
| objectCopySource  | Path to the copied source file | NSString * | Yes |
| metadataDirective | Whether to copy the metadata. Enumerated values: Copy, Replaced. Default value: Copy. If the flag is Copy, the user metadata in the header is ignored and the copy is performed directly; if the flag is Replaced, the metadata is modified based on the header information. If the destination path is the same as the source path (i.e., when you want to modify the metadata), the flag has to be Replaced | NSString * | No |
| storageClass | Storage class of an object. Enumerated values: STANDARD (QCloudCOSStorageStandard), STANDARD_IA (QCloudCOSStorageStandardIA). Default value: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |
| accessControlList | Defines the ACL attribute of the object, such as private, public-read, and default; default value: default (i.e., inheriting the bucket's permissions). Note: Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, use "default" for this parameter or simply leave it blank, so that the object will inherit the permissions of the bucket | NSString * | No |
| grantRead         | Grants the grantee read permission in the format of id="OwnerUin"                    | NSString * | No |
| grantWrite        | Grants the grantee write permission in the format of id="OwnerUin"                    | NSString * | No   |
| grantFullControl | Defines the ACL attribute of the object. Value range: private, public-read; default value: private | NSString * | No |
| versionID | Specifies the versionID of the source file. This parameter is responded to only for buckets where versioning is enabled or suspended | NSString * | No|

#### Return Result Descriptions

The result of the request is returned through QCloudCopyObjectResult.

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ---------- |
| eTag | Returns the MD5 checksum of the file. The value of ETag can be used to check whether the object content has changed | NSString * |
| lastModified | Last modified time of the file in GMT time | NSString * |
| versionID | Version ID of the object (available only if versioning is enabled) | NSString * |

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting a Single Object

#### Feature Description

This API (Delete Object) is used to delete a single object.

#### Method Prototype

Before performing a file operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudDeleteObjectRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudDeleteObjectRequest and enter the required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the outputObject in the finishBlock of the callback.   

#### QCloudDeleteObjectRequest Parameter Descriptions

| Parameter Name | Type | Required | Description |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| object | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | NSString * | Yes |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |

#### Examples

```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
deleteObjectRequest.bucket = @"examplebucket-1250000000";
deleteObjectRequest.object = @"text.txt";
__block NSError* resultError;
[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    resultError = error;
   // You can get information such as etag or custom header in the response from outputObject (more header information can be viewed by printing the outputObject)
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];

```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Deleting Multiple Objects

#### Method Prototype

Before performing a file operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudDeleteMultipleObjectRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudDeleteMultipleObjectRequest, enter the required parameters, encapsulate the objects you want to delete into a QCloudDeleteObjectInfo object, and put it into the objects array of deleteObjects.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the outputObject in the finishBlock of the callback.   

#### QCloudDeleteMultipleObjectRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ------------------ | ---- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| deleteObjects | Encapsulates information of multiple objects to be deleted in batches | QCloudDeleteInfo * | Yes |

QCloudDeleteInfo parameter descriptions

| Parameter Name | Description | Type | Required |
| -------- | -------------------------- | ----------------------------------------- | ---- |
| objects | The array that stores the information of multiple objects to be deleted | NSArray&lt;QCloudDeleteObjectInfo `*` > * | Yes |

| Quiet | A boolean value which determines whether to enable Quiet mode.
If the value is true, Quiet mode is enabled; if it is false, Verbose mode is enabled. The default value is false | NSArray&lt;QCloudDeleteObjectInfo `*` > * | No   |

CloudDeleteObjectInfo parameter descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg, the object key is doc/picture.jpg. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | NSString * | Yes |

#### Return Result Descriptions

QCloudDeleteResult parameter descriptions

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------ | --------------------------------- |
| deletedObjects | The array that stores the information of multiple deleted objects | NSArray<QCloudDeleteResultRow*> * |
| lastModified | Last modified time of the file in GMT time | NSString * |
| versionID | Version ID of the object (available only if versioning is enabled) | NSString * |

QCloudDeleteResultRow parameter descriptions

| Parameter Name | Description | Type |
| -------- | --------------- | ---------- |
| key | Key of the deleted object | NSString * |

#### Examples

```objective-c
QCloudDeleteMultipleObjectRequest* delteRequest = [QCloudDeleteMultipleObjectRequest new];
delteRequest.bucket = @"examplebucket-1250000000";

QCloudDeleteObjectInfo* deletedObject0 = [QCloudDeleteObjectInfo new];
deletedObject0.key = @"text,txt";

QCloudDeleteObjectInfo* deleteObject1 = [QCloudDeleteObjectInfo new];
deleteObject1.key = @"picture.jpg";

QCloudDeleteInfo* deleteInfo = [QCloudDeleteInfo new];
deleteInfo.quiet = NO;
deleteInfo.objects = @[ deletedObject0,deleteObject2];
delteRequest.deleteObjects = deleteInfo;
__block NSError* resultError;
[delteRequest setFinishBlock:^(QCloudDeleteResult* outputObject, NSError *error) {
      localError = error;
      deleteResult = outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];

```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Multipart Upload Operations

### Querying a Multipart Upload

#### Feature Description

This API is used to query a multipart upload in progress in the specified bucket.

#### Method Prototype

Before performing a bucket operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudListBucketMultipartUploadsRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudListBucketMultipartUploadsRequest and enter the required parameters such as the prefix of the return result and encoding method.    
2. Call the ListBucketMultipartUploads method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the outputObject in the finishBlock of the callback.   

#### QCloudListBucketMultipartUploadsRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| prefix | Specifies that the returned object key must be prefixed with the "prefix". Note that when a prefix query is used, the returned key will still contain the prefix | NSString * | No |
| delimiter | The delimiter is a symbol. If there is a prefix, the identical paths between prefix and delimiter are grouped into one class and defined as a common prefix, and then all common prefixes are listed. If there is no prefix, it starts at the beginning of the path and can be seen as the ending symbol. For example, if you want the results ending in A, then set delimiter to A. | NSString * | No |
| encodingType | Specifies the encoding method of the return value. Value range: url | NSString * | No |
| keyMarker      | The entry list starts at this key value                                      | NSString * | No   |
| uploadIDMarker | The entry list starts at this UploadId value                                 | int        | No   |
| maxUploads | Sets the maximum number of parts returned between 1 and 1,000 | int | No |

#### Return Result Descriptions

QCloudListMultipartUploadsResult parameter descriptions

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ---------- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * |
| prefix | Specifies that the returned object key must be prefixed with the "prefix". Note that when a prefix query is used, the returned key will still contain the prefix | NSString * |
| delimiter | The delimiter is a symbol. If there is a prefix, the identical paths between prefix and delimiter are grouped into one class and defined as a common prefix, and then all common prefixes are listed. If there is no prefix, it starts at the beginning of the path | NSString * |
| encodingType | Specifies the encoding method of the return value. Value range: url | NSString * |
| keyMarker      | The entry list starts at this key value                                      | NSString * |
| maxUploads | Sets the maximum number of parts returned between 1 and 1,000 | int |
| uploads | Information of all uploaded parts | NSArray* |
| isTruncated | Whether the file is truncated | NSString * |

#### Examples

```objecitve-c
QCloudListBucketMultipartUploadsRequest* uploads = [QCloudListBucketMultipartUploadsRequest new];
uploads.bucket = @"examplebucket-1250000000";
uploads.maxUploads = 100;
__block NSError* resulError;
__block QCloudListMultipartUploadsResult* multiPartUploadsResult;
[uploads setFinishBlock:^(QCloudListMultipartUploadsResult* result, NSError *error) {
    multiPartUploadsResult = result;
    localError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] ListBucketMultipartUploads:uploads];

```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly. There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Uploading an Object in Parts

With multipart upload, you can do the following:

- Upload an object in parts, including initializing a multipart upload, uploading parts, and completing the upload of all parts.
- Resume a multipart upload, including querying uploaded parts, uploading parts, and completing the upload of all parts.
- Delete uploaded parts.

### <span id = "INIT_MULIT_UPLOAD">Initializing a Multipart Upload</span>

#### Feature Description

This API (Initiate Multipart Upload) is used to initialize a multipart upload and get the corresponding uploadId.

#### Method Prototype

Before performing a file operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudInitiateMultipartUploadRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudInitiateMultipartUploadRequest and enter the required parameters.    
2. Call the InitiateMultipartUpload method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the outputObject in the finishBlock of the callback.   

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | --------------------- | ---- |
| Object | Name (and also key) of the uploaded file (object). An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg, the object key is doc/picture.jpg. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | NSString * | Yes |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| cacheControl | Cache policy as defined in RFC 2616 | NSString * | No |
| contentDisposition | File name as defined in RFC 2616 | NSString * | No |
| expect | If `expect=@"100-continue"` is used, the request content will be sent only after confirmation from the server is received | NSString * | No|
| expires | File date and time as defined in RFC 2616 | NSString * | No |
| storageClass | Storage class of an object. Enumerated values: STANDARD (QCloudCOSStorageStandard), STANDARD_IA (QCloudCOSStorageStandardIA), ARCHIVE (QCloudCOSStorageARCHIVE). Default value: STANDARD (QCloudCOSStorageStandard) | QCloudCOSStorageClass | No |
| accessControlList | Defines the ACL attribute of the object. Value range: private, public-read; default value: private | NSString * | No |
| grantRead         | Grants the grantee read permission in the format of id="[OwnerUin]"                    | NSString * | No |
| grantWrite        | Grants the grantee write permission in the same format as described above                    | NSString * | No   |
| grantFullControl  | Grants the grantee read/write permission in the same format as described above                    | NSString * | No   |

#### Examples

```objective-c
QCloudInitiateMultipartUploadRequest* initrequest = [QCloudInitiateMultipartUploadRequest new];
initrequest.bucket = @"examplebucket-1250000000";
initrequest.object = @"text.txt";
__block QCloudInitiateMultipartUploadResult* initResult;
[initrequest setFinishBlock:^(QCloudInitiateMultipartUploadResult* outputObject, NSError *error) {
    initResult = outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] InitiateMultipartUpload:initrequest];

```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Uploading Parts

#### Feature Description

This API is used to upload a file in parts.

#### QCloudUploadPartRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| object      | Object name                                                   | NSString * | Yes   |
| UploadId | ID of this multipart upload; when the Initiate Multipart Upload API is used to initialize a multipart upload, an uploadId will be obtained, which not only uniquely identifies the data but also identifies the data position in the entire file | NSString * | Yes |
| partNumber  | Identifies a part number                                       | int        | Yes  |
| contentSHA1 | SHA1 value of this multipart upload                                       | NSString * | Yes   |
| body | Uploaded data. Three types are supported, i.e., `NSData*`, NSURL (local URL), and QCloudFileOffsetBody* | BodyType | Yes |

#### Return Result Descriptions

QCloudUploadPartResult parameter descriptions

| Parameter Name | Description | Type |
| -------- | ----------- | ---------- |
| eTag     | File etag | NSString * |

#### Method Prototype

The steps to initiate a multipart upload request in the COS SDK for iOS are as follows:

1. Instantiate QCloudUploadPartRequest and enter the required parameters.
2. Call the UploadPart method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the QCloudUploadPartResult in the finishBlock of the callback.

#### Examples

```objective-c
QCloudUploadPartRequest* request = [QCloudUploadPartRequest new];
request.bucket = @"examplebucket-1250000000";
request.object = @"text.txt";
request.partNumber = @"partNumber"
request.uploadId = @"uploadId"; // ID of this multipart upload; when the Initiate Multipart Upload API is used to initialize a multipart upload, an uploadId will be obtained, which not only uniquely identifies the data but also identifies the data position in the entire file
request.body = body;// Uploaded data. Three types are supported, i.e., NSData*, NSURL (local URL), and QCloudFileOffsetBody*  
[request setSendProcessBlock:^(int64_t bytesSent,
                                    int64_t totalBytesSent,
                                    int64_t totalBytesExpectedToSend) {
}];
[request setFinishBlock:^(QCloudUploadPartResult* outputObject, NSError *error) {
// You can get information such as etag or custom header in the response from outputObject (more header information can be viewed by printing the outputObject)
}];
[[QCloudCOSXMLService defaultCOSXML]  UploadPart:request];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Copying Parts

#### Feature Description

This API is used to copy a file in parts.

#### QCloudUploadPartRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| object      | Object name                                                   | NSString * | Yes   |
| UploadId | ID of this multipart upload; when the Initiate Multipart Upload API is used to initialize a multipart upload, an uploadId will be obtained, which not only uniquely identifies the data but also identifies the data position in the entire file | NSString * | Yes |
| partNumber  | Identifies a part number                                       | int        | Yes  |
| source | Source file URL path. A previous version can be specified using the versionid sub-resource | NSString * | Yes |
| body | Uploaded data. Three types are supported, i.e., `NSData*`, NSURL (local URL), and QCloudFileOffsetBody* | BodyType | Yes |

#### Return Result Descriptions

QCloudUploadPartResult parameter descriptions

| Parameter Name | Description | Type |
| -------- | ----------- | ---------- |
| eTag     | File etag | NSString * |

#### Method Prototype

The steps to initiate a multipart upload request in the COS SDK for iOS are as follows:

1. Instantiate QCloudUploadPartCopyRequest and enter the required parameters.
2. Call the UploadPartCopy method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the QCloudCopyObjectResult in the finishBlock of the callback.

#### Examples

```objective-c
QCloudUploadPartCopyRequest* request = [[QCloudUploadPartCopyRequest alloc] init];
request.bucket = @"examplebucket-1250000000";
request.object = @"text.txt";
request.source = @"objectCopySource"; // Source file URL path. A previous version can be specified using the versionid sub-resource
request.uploadID = @"uploadID"; // In the response of multipart upload initialization, a unique descriptor (upload ID) is returned
request.partNumber = 1; // Current part number
[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
}];
[[QCloudCOSXMLService defaultCOSXML]UploadPartCopy:request];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### <span id = "LIST_MULIT_UPLOAD">Querying Uploaded Parts</span>

#### Feature Description

This API (List Parts) is used to query the uploaded parts for the specified uploadId.

#### QCloudListMultipartRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| object      | Object name                                                   | NSString * | Yes   |
| uploadId         | uploadId of the multipart upload to be queried                               | NSString * | Yes   |
| maxPartsCount    | Maximum number of entries returned at a time; 1,000 by default                             | NSString * | No  |
| partNumberMarker | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | NSString * | No |
| encodingType | Specifies the encoding method of the return value | int | No |

#### Return Result Descriptions

 QCloudListPartsResult parameter

| Parameter Name | Description | Type |
| ---------------- | ------------------------------------------------------------ | -------------------------- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * |
| encodingType | Specifies the encoding method of the return value | NSString * |
| key | Object name | NSString * |
| uploadId         | uploadId of the multipart upload to be queried                                | NSString *                 |
| storageClass     | Identifies the storage class of the parts                                   | QCloudCOSStorageClass      |
| partNumberMarker | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | int |
| nextNumberMarker | If the returned entries are truncated, then NextMarker is the starting point of the next entry | NSString * |
| maxParts         | Maximum number of entries returned at a time                                         | QCloudCOSStorageClass      |
| isTruncated    | Whether returned entries are truncated                                       | BOOL                             |
| initiator        | Identifies the initiator of this upload                                 | NSString *                 |
| owner            | Identifies the owner of the parts                                 | QCloudCOSStorageClass      |
| parts            | Identifies the information of each part                                       | QCloudMultipartUploadPart* |

#### Examples

```objective-c
  QCloudListMultipartRequest* request = [QCloudListMultipartRequest new];
  request.object = @"text.txt"
  request.bucket = @"examplebucket-1250000000";
  request.uploadId = @"uploadId";// uploadId of the multipart upload to be queried, which can be obtained from the result QCloudInitiateMultipartUploadResult of the multipart upload initialization request
  [request setFinishBlock:^(QCloudListPartsResult * _Nonnull result,
                              NSError * _Nonnull error) {
  }];

  [[QCloudCOSXMLService defaultCOSXML] ListMultipart:request];

```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### <span id = "COMPLETE_MULIT_UPLOAD">Completing a Multipart Upload</span>

#### Feature Description

The API (Complete Multipart Upload) is used to complete the entire multipart upload.

#### QCloudCompleteMultipartUploadRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ----------------------------------- | ---- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| object      | Object name                                                   | NSString * | Yes   |
| UploadId | ID of this multipart upload; when the Initiate Multipart Upload API is used to initialize a multipart upload, an uploadId will be obtained, which not only uniquely identifies the data but also identifies the data position in the entire file | NSString * | Yes |
| parts    | Information of completed parts                                           | QCloudCompleteMultipartUploadInfo * | Yes   |

#### Return Result Descriptions

 QCloudUploadObjectResult parameter descriptions

| Parameter Name | Description | Type |
| --------- | ------------------------------------------------------------ | ---------- |
| location | Public network access domain name for the created object | NSString * |
| bucket   | Name of the destination bucket for the multipart upload in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * |
| key | Object name | NSString * |
| eTag | MD5 checksum of the merged file | NSString * |
| versionID | Version ID of the object (available only if versioning is enabled) | NSString * |

#### Method Prototype

The steps to complete a multipart upload request in the COS SDK for iOS are as follows:

1. Instantiate QCloudCompleteMultipartUploadRequest and enter the required parameters.
2. Call the CompleteMultipartUpload method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the QCloudUploadObjectResult in the finishBlock of the callback.

#### Examples

```objective-c
QCloudCompleteMultipartUploadRequest *completeRequst = [QCloudCompleteMultipartUploadRequest new];
completeRequst.bucket = @"examplebucket-1250000000";
completeRequst.object = @"text.txt";
completeRequst.uploadId = @"uploadId"; // uploadId of this multipart upload
[completeRequst setFinishBlock:^(QCloudUploadObjectResult * _Nonnull result, NSError * _Nonnull error) {

}];
[[QCloudCOSXMLService defaultCOSXML] CompleteMultipartUpload:completeRequst];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### <span id = "ABORT_MULIT_UPLOAD">Aborting a Multipart Upload</span>

#### Feature Description

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### QCloudAbortMultipfartUploadRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000, which can be viewed in the COS V5 Console | NSString * | Yes   |
| object      | Object name                                                   | NSString * | Yes   |
| UploadId | ID of the multipart upload to be aborted; when the Initiate Multipart Upload API is used to initialize a multipart upload, an uploadId will be obtained, which not only uniquely identifies the data but also identifies the data position in the entire file | NSString * | Yes |

#### Method Prototype

The steps to abort a multipart upload and delete the uploaded parts in the COS SDK for iOS are as follows:

1. Instantiate QCloudAbortMultipfartUploadRequest and enter the required parameters.
2. Call the AbortMultipfartUpload method in the QCloudCOSXMLService object to initiate a request.
3. Get the specific content from the outputObject in the finishBlock of the callback.

#### Examples

```objective-c
QCloudAbortMultipfartUploadRequest *abortRequest = [QCloudAbortMultipfartUploadRequest new];
abortRequest.bucket = @"examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
abortRequest.object = @"text.txt";
abortRequest.uploadId = @"uploadId";
[abortRequest setFinishBlock:^(id outputObject, NSError *error) {
//additional actions after finishing
// You can get information such as etag or custom header in the response from outputObject (more header information can be viewed by printing the outputObject)
}];
[[QCloudCOSXMLService defaultCOSXML]AbortMultipfartUpload:abortRequest];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Other Operations

### Restoring an Archived Object

#### Feature Description

This API (POST Object restore) is used to restore an archived object.

#### Method Prototype

Before performing a file operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudPostObjectRestoreRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudPostObjectRestoreRequest and enter the object name and bucket name.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific content from the outputObject in the finishBlock of the callback.   

#### QCloudPostObjectRestoreRequest Request Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ---------------------- | ---- |
| object | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg, the object key is doc/picture.jpg. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | NSString * | Yes |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| restoreRequest | Configuration information of the data to be restored                                         | QCloudRestoreRequest * | Yes   |

QCloudRestoreRequest parameter descriptions

| Parameter Name | Description | Type | Required |
| ---------------- | ---------------------- | ------------------ | ---- |
| days | Sets expiration time of the temporary copy | int64_t | Yes |
| CASJobParameters | Configuration information of the restoration type | CASJobParameters * | Yes |

CASJobParameters parameter descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------------- | ---- |
| tier | Restoration mode. Three modes are supported: Standard (standard mode where a restoration task can be completed in 3-5 hours), Expedited (expedited mode where a restoration task can be completed in 15 minutes), and Bulk (bulk mode where a restoration task can be completed in 5 - 12 hours) | QCloudCASTier | Yes |

#### Examples

```objective-c
QCloudPostObjectRestoreRequest *req = [QCloudPostObjectRestoreRequest new];
req.bucket = @"examplebucket-1250000000";
req.object = @"text.txt";
req.restoreRequest.days  = 10;
req.restoreRequest.CASJobParameters.tier =QCloudCASTierStandard;
[req setFinishBlock:^(id outputObject, NSError *error) {
// You can get information such as etag or custom header in the response from outputObject (more header information can be viewed by printing the outputObject)
}];
[[QCloudCOSXMLService defaultCOSXML] PostObjectRestore:req];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Setting Object ACL

#### Feature Description

This API is used to set the access control list (ACL) for an object.

#### Method Prototype

Before performing an object operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudPutObjectACLRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudPutObjectACLRequest and enter the bucket name and some additional required parameters such as the specific authorization information.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Check whether the setting succeeded in the finishBlock of the callback. If error is empty, the setting succeeded.   

#### QCloudPutObjectACLRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| object      | Object name                                                   | NSString * | Yes   |

| accessControlList | Defines the ACL attribute of the object. Value range: private, public-read, and default; default value: default (i.e., inheriting the bucket's permissions).
 Note: Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, use "default" for this parameter or simply leave it blank, so that the object will inherit the permissions of the bucket | NSString * | No |
| grantRead         | Grants the grantee read permission in the format of id="OwnerUin"                    | NSString * | No |
| grantWrite        | Grants the grantee write permission in the format of id="OwnerUin"                    | NSString * | No   |
| grantFullControl  | Grants the grantee read/write permission in the format of id="OwnerUin"                    | NSString * | No   |

#### Examples

```objective-c
QCloudPutObjectACLRequest* request = [QCloudPutObjectACLRequest new];
request.object = @"text.txt";
request.bucket = @"examplebucket-1250000000";
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];
request.grantFullControl = grantString;
__block NSError* localError;
[request setFinishBlock:^(id outputObject, NSError *error) {
     localError = error;
	// You can get information such as etag or custom header in the response from outputObject (more header information can be viewed by printing the outputObject)
}];
[[QCloudCOSXMLService defaultCOSXML] PutObjectACL:request];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

### Getting Object ACL

#### Feature Description

This API is used to get the access control list (ACL) of an object.

#### Method Prototype

Before performing a file operation, you need to import the header QCloudCOSXML/QCloudCOSXML.h after completing the [initialization](https://intl.cloud.tencent.com/document/product/436/11280#step1). First, generate a QCloudGetObjectACLRequest instance, enter some additional required restrictions, have them passed, and get the content. The steps are as follows:    

1. Instantiate QCloudGetObjectACLRequest and enter the bucket name and the name of the object to be queried.    
2. Call the GetObjectACL method in the QCloudCOSXMLService object to initiate a request.    
3. Get the specific information of the encapsulated ACL from the QCloudACLPolicy object in the finishBlock of the callback.   

#### QCloudGetObjectACLRequest Parameter Descriptions

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | Bucket name in the format of &lt;BucketName-APPID&gt;, such as examplebucket-1250000000, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket) | NSString * | Yes   |
| object | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg, the object key is doc/pic.jpg. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | NSString * | Yes |
| versionID | Specifies the version ID in versioning                                    | NSString * | Yes   |

#### Return Result Descriptions

QCloudACLPolicy parameter descriptions

| Parameter Name | Description | Type |
| ----------------- | ---------------------- | ------------------------- |
| owner             | Owner information           | QCloudACLOwner *          |
| accessControlList | Information of the grantee and permission | QCloudAccessControlList * |

QCloudACLOwner parameter descriptions

| Parameter Name | Description | Type |
| ----------- | ------------------- | ---------- |
| displayName | Bucket owner name | NSString * |
| identifier  | Bucket owner ID | NSString * |

QCloudAccessControlList parameter descriptions

| Parameter Name | Description | Type |
| --------- | ---------------------- | -------------------------- |
| ACLGrants | Array used to store the grantee information | NSArray<QCloudACLGrant*> * |

QCloudACLGrant parameter descriptions

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------------------- |
| grantee | Describes the information of the grantee. The type can be RootAccount or Subaccount. If the type is RootAccount, the ID specifies a root account; if the type is Subaccount, the ID specifies a sub-account | QCloudACLGrantee * |
| permission | Specifies the permission granted to the grantee. Enumerated values: READ, FULL_CONTROL | QCloudCOSPermission |

#### Examples

```objective-c
QCloudGetObjectACLRequest *request = [QCloudGetObjectACLRequest new];
request.object = @"text.txt";
request.bucket = @"examplebucket-1250000000"
__block QCloudACLPolicy* policy;
[request setFinishBlock:^(QCloudACLPolicy * _Nonnull result, NSError * _Nonnull error) {
     policy = result;
}];
[[QCloudCOSXMLService defaultCOSXML] GetObjectACL:request];
```

#### Notes on Returned Error Codes

When an SDK request fails, the returned error will not be empty and will include error code, error message, and other information required for troubleshooting to help developers fix the problem quickly.

There are mainly two types of returned error codes (encapsulated in the returned error): error codes returned by the device for network reasons and error codes returned by COS.

- All the error codes returned by the device for network reasons are 4-digit negative numbers such as -1001, which are defined by Apple. For more information, see the definitions in the NSURLError.h header of the Foundation framework or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes such as 404 and 503. For solutions to this type of error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).
- All the error codes customized by the SDK are 5-digit positive numbers such as 10000 and 20000. For solutions to this type of error codes, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).

## Adding a Custom Header

You can add custom headers to a request. All classes that support adding custom headers have the customHeaders attribute:

```objective-c
@property (strong, nonatomic) NSMutableDictionary* customHeaders;
```

All key-value pairs within this attribute will be added to the HTTP header that builds the request in the corresponding form.

## Server-side Encryption

If you need to encrypt the uploaded object, the following encryption methods can be used.

### Server-side Encryption (SSE-COS) Using COS-managed Encryption Keys

COS will automatically encrypt the data as it is written to the IDC and automatically decrypt it when you retrieve it. Currently, AES-256 encryption with the COS master key is supported.

The SDK for iOS does so by calling the -(void)setCOSServerSideEncyption method.

```objective-c
[request setCOSServerSideEncyption];
```

### Server-side Encryption (SSE-C) Using Customer-supplied Encryption Keys

The SDK for iOS does so by calling the -(void)setCOSServerSideEncyptionWithCustomerKey:(NSString \*)customerKey method.


>- The service that the encryption runs should use an HTTPS request.
>- customerKey: Customer-supplied key. Pass in a 32-byte string which can contain number, letters, and special characters.
>- If the uploaded source object calls this method, it should also be called when QCloudCOSXMLDownloadObjectRequest (download), QCloudHeadObjectRequest (query), QCloudCOSXMLUploadObjectRequest (upload), and QCloudCOSXMLUploadObjectRequest (copy) are used to manipulate the source object.

```objective-c
NSString *customKey = @"123456qwertyuioplkjhgfdsazxcvbnm";
[put setCOSServerSideEncyptionWithCustomerKey:customKey];
```
