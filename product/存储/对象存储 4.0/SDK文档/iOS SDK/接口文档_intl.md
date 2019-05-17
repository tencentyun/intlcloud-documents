The API documentation contains a detailed API list and usage examples, which are written for those who completed initialization. It is recommended to use Command+F to find the API, check its description, and apply in your project.    

> ?If you need more features, or do not understand what the returned parameters mean, you are advised to view the comments in the code using three finger drag, Force-touch, or hovering over the variable and pressing Control+Command+D.

## Best Practices of Common Operations

This section describes the best practices of some common operations, which are available after you complete the initialization according to Getting Started.

### Upload a file

See the [Upload a file](https://cloud.tencent.com/document/product/436/11280#step---2-.E4.B8.8A.E4.BC.A0.E6.96.87.E4.BB.B6) section in Getting Started.

### Resume upload from breakpoint

Multipart upload is used to upload a file larger than 1 MB. That is, split the file into multiple parts with each holding a size of 1 MB, and then upload these parts (4 at most) in parallel. Resuming upload from breakpoint is implemented on the basis that the uploaded parts are stored in the backend server.    

During multipart upload, resumeData for resuming upload is generated after you initialize multipart upload or cancel the upload. This is used to generate another upload request for resuming upload. The following example shows how to get ResumeData:

```objective-C
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
//···Set some parameters for upload
put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult, QCloudCOSXMLUploadObjectResumeData resumeData) {
	//Call back the block after you initialize multipart upload, in which you can obtain resumeData for generating a multipart upload request
	QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
};

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];

//···When initialization is completed and upload is not completed
NSError* error;
//The following shows how resumeData is generated after the user cancels the upload
resumeData = [put cancelByProductingResumeData:&error];
if (resumeData) {
QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
 }
 //The generated request for resuming upload can be directly uploaded
 [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];

```

Note: The multipart upload uses the serial mode where parts must be uploaded in sequence. Under the following circumstances, resuming upload from breakpoint cannot be used.

- The file to be uploaded is smaller than 1 MB and multipart upload is not used.
- A simple upload API rather than the QCloudCOSXMLUploadObjectRequest class is used to upload files.
- Multipart upload initialization is not completed (the callback for completed upload initialization is yet to be called) when you cancel the generation of resumeData.

### Download a file

See the [Download a file](https://cloud.tencent.com/document/product/436/11280#3.-.E4.B8.8B.E8.BD.BD.E6.96.87.E4.BB.B6) section in Getting Started.

### Copy a file

#### Notes

Initialize a QCloudCOSXMLCopyObjectRequest object, and then call CopyObject of QCloudCOSTransferMangerService. Note that multipart copy is automatically used for large files, but users will not be aware of this process.  

> !For cross-origin replication, the region of transferManager must be the same as that of the bucket.

#### Example

```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];
request.bucket = @"Destination bucket";
request.object = @"Destination file name";
request.sourceBucket = @"File source bucket. Public read or access to the current account is required";
request.sourceObject = @"Source file name";
request.sourceAPPID = @"Source APPID";
request.sourceRegion= @"Source region";
[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    //Complete callback
    if (nil == error) {
      //Successful
    }
}];
//For cross-origin replication, the region of transferManager must be the same as that of the bucket.
[[QCloudCOSTransferMangerService defaultCOSTransferManager] CopyObject:request];
```

## Service Operations

### List all buckets - Get Service

This API (Get Service) is used to obtain all Bucket lists of the requester.

#### Parameters of returned result QCloudListAllMyBucketsResult

| Parameter Name | Description | Type |
| -------- | ------------------ | ------------- |
| owner | Bucket owner information | QCloudOwner * |
| buckets | All bucket information | NSArray<QCloudBucket*> * |

#### Example

```objective-c
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result, NSError* error) {
//Process after callback is completed
}];
[[QCloudCOSXMLService defaultCOSXML] GetService:request];
```

### Generate and use pre-signed URLs

You can generate a pre-signed URL from the SDK or server, and then upload, download or perform other operations as needed.

#### Description

1. Create a QCloudGetPresignedURLRequest instance.
2. Enter required information such as Bucket, Object, and HTTPMethod.
3. If additional HTTP headers or parameters are required for use, call the method in QCloudGetPresignedURLRequest to add them when generating pre-signed URLs.
4. Call getPresignedURL in QCloudCOSXMLService to send requests, and obtain pre-signed URLs in results.

#### QCloudGetPresignedURLRequest parameters

| Parameter Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | --------- | ---- |
| bucket      | Bucket using a pre-signed request | NSString* | Yes |
| object | Object using a pre-signed request. ObjectKey is the unique identifier of an object in a bucket. For example, in the object's access domain name "bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg", the key is "doc1/pic1.jpg". For more information, see [Object Description](https://cloud.tencent.com/document/product/436/13324). | NSString* | Yes |
| HTTPMethod  | HTTP method of the request using a pre-signed URL. Valid values (case-sensitive): @"GET", @"PUT", @"POST" and @"DELETE". | NSString* | Yes |
| contentType | This parameter is available when the request using a pre-signed URL has this header. | NSString* | No |
| contentMD5 | This parameter is available when the request using a pre-signed URL has this header. | NSString* | No |

**Note:** To set the header or URL parameter of the request using a pre-signed URL, do the following:    

```objective-c
/**
 Add the header of the request using a pre-signed request

 @param value HTTP header value
 @param requestHeader HTTP header key
 */
- (void)setValue:(NSString * _Nullable)value forRequestHeader:(NSString * _Nullable)requestHeader;

/**
 Add the URL parameter of the request using a pre-signed request

 @param value Parameter value
 @param requestParameter Parameter key
 */
- (void)setValue:(NSString * _Nullable)value forRequestParameter:(NSString *_Nullable)requestParameter;
```

#### Example on how to obtain a pre-signed URL

```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];
getPresignedURLRequest.bucket = self.bucket;
getPresignedURLRequest.HTTPMethod = @"GET";
getPresignedURLRequest.object = @"testUploadWithPresignedURL";
[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result, NSError * _Nonnull error) {
if (nil == error) {
 NSString* presignedURL = result.presienedURL;
}
}
[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];

```

#### Example on how to use a pre-signed URL

The following example shows how to download with a pre-signed URL.

```objective-C
NSMutableURLRequest* request = [[NSMutableURLRequest alloc] initWithURL:[NSURL URLWithString:@"Pre-signed URL"]];
request.HTTPMethod = @"GET";
request.HTTPBody = [@"File content" dataUsingEncoding:NSUTF8StringEncoding];
[[[NSURLSession sharedSession] downloadTaskWithRequest:request completionHandler:^(NSURL * _Nullable location, NSURLResponse * _Nullable response, NSError * _Nullable error) {
    NSInteger statusCode = [(NSHTTPURLResponse*)response statusCode];
}] resume];
```

## Bucket Operations

### Create a bucket

#### Method prototype

Before using COS, you need to create a bucket under the specific account for use and management of objects, and define the region of the bucket. The creator of the bucket is the owner of the bucket by default. The bucket access permission is Private Read/Write by default if not otherwise specified upon creation. Specific steps are as follows:    

1. Instantiate QCloudPutBucketRequest and enter the required parameters.
2. Call the PutBucket method in the QCloudCOSXMLService object to initiate a request.
3. Obtain specific content from outputObject in finishBlock of callback. 

#### QCloudPutBucketRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket            | The name of the bucket to be created, which can be viewed in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket). Note that the bucket name can only consist of numbers and lowercase letters with a length limited to 40 characters; otherwise, the creation will fail. | NSString * | Yes |
| accessControlList | Defines the ACL attribute of a bucket. Valid values: private, public-read-write, public-read; Default: private | NSString * | No |
| grantRead | Grants read permission to the authorized user. Format: id=" ",id=" ". For authorization to a subaccount, id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"; for authorization to the root account, id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>", where OwnerUin refers to the ID of the root account and SubUin refers to the ID of the subaccount. | NSString * | No |
| grantWrite | Grants write permission to the authorized user. The format is the same as above. | NSString * | No |
| grantFullControl | Grants read and write permissions to the authorized user. The format is the same as above. | NSString * | No |

#### Example

```objective-c
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];
request.bucket = @"bucketname-appid"; //additional actions after finishing
[request setFinishBlock:^(id outputObject, NSError* error) {

}];
[[QCloudCOSXMLService defaultCOSXML] PutBucket:request];
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.

### List contents in a bucket

#### Method prototype

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

#### Example

```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
request.bucket = @“testBucket-123456789”;
request.maxKeys = 1000;
[request setFinishBlock:^(QCloudListBucketResult * result, NSError*   error) {
//additional actions after finishing
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.

### Obtain bucket ACL (Access Control List)

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before bucket operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudGetBucketACLRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudGetBucketACLRequest and enter the bucket whose ACL is to be obtained.    
2. Call the GetBucketACL method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content from QCloudACLPolicy in finishBlock of callback.    

#### QCloudGetBucketACLRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |

#### Parameters of returned result QCloudACLPolicy

| Parameter Name | Description | Type |
| -------- | ---------------------------------- | ---------------- |
| owner | Bucket owner information | QCloudACLOwner * |
| accessControlList     | Information of the authorized user and permissions | QCloudAccessControlList *  |

#### Example

```objective-c
QCloudGetBucketACLRequest* getBucketACl   = [QCloudGetBucketACLRequest new];
getBucketACl.bucket = @"testbucket-123456789";
[getBucketACl setFinishBlock:^(QCloudACLPolicy * _Nonnull result, NSError * _Nonnull error) {
   //QCloudACLPolicy contains Bucket ACL information.
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketACL:getBucketACl];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.

### Set bucket ACL (Access Control List)

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before bucket operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudPutBucketACLRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudPutBucketACLRequest, enter the bucket to be set, and then enter corresponding parameters according to the permission type of the bucket.    
2. Call the PutBucketACL method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the setting result (successful or failed) from finishBlock of callback, and perform some additional operations if the setting is successful.   

#### QCloudPutBucketACLRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt; , such as testBucket-1253653367 | NSString * | Yes |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read-write, public-read; Default: private | NSString * | No |
| grantRead | Grants read permission to the authorized user. Format: id=" ",id=" ".<br>For authorization to a subaccount, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;",<br>for authorization to the root account, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;", <br>where OwnerUin refers to the ID of the root account and SubUin refers to the ID of the subaccount. | NSString * | No |
| grantWrite | Grants write permission to the authorized user. The format is the same as above. | NSString * | No |
| grantFullControl | Grants read and write permissions to the authorized user. The format is the same as above. | NSString * | No |

#### Example

```objective-c
QCloudPutBucketACLRequest* putACL = [QCloudPutBucketACLRequest new];
NSString* appID = @“Your APPID”;
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@", appID, appID];
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];
putACL.grantFullControl = grantString;
putACL.bucket = @“testBucket-123456789”;
[putACL setFinishBlock:^(id outputObject, NSError *error) {
//error occucs if error != nil
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketACL:putACL];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.

### Obtain bucket CORS configuration

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before bucket operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudGetBucketCORSRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudGetBucketCORSRequest and enter the bucket whose CORS is to be obtained.    
2. Call the GetBucketCORS method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the result from finishBlock of callback. The result is encapsulated in the QCloudCORSConfiguration object whose "rules" attribute is an array containing a set of QCloudCORSRule. The specific CORS configurations are encapsulated in the QCloudCORSRule object.   

#### QCloudGetBucketACLRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |

#### Parameters of returned result QCloudCORSConfiguration

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------ | ----------------------------------- |
| rules | The array containing CORS. It is a QCloudCORSRule instance. | NSArray&lt;CloudCORSRule`*`&gt; `*` |

#### QCloudCORSRule parameters

| Parameter Name | Description | Type |
| ------------- | ------------------------------------------------------------ | ------------------------------ |
| identifier | ID of the configuration rule | NSString * |
| allowedMethod | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | NSArray&lt;NSString`*`&gt;`*` |
| allowedOrigin | Allowed access source. The wildcard "*" is supported. Format: protocol://domain name[:port], for example, `http://www.qq.com` | NSString * |
| allowedHeader | It is used to notify the server about which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent. The wildcard "*" is supported. | NSArray&lt;NSString`*`&gt; `*` |
| maxAgeSeconds | Configures the valid period of the results obtained by OPTIONS request | int |
| exposeHeader | Configures the custom header information that can be received by the browser from the server | NSString * |

#### Example

```objective-c
QCloudGetBucketCORSRequest* corsReqeust = [QCloudGetBucketCORSRequest new];
corsReqeust.bucket = @"testBucket-123456789";
[corsReqeust setFinishBlock:^(QCloudCORSConfiguration * _Nonnull result, NSError * _Nonnull error) {
   //CORS is encapsulated in result.
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketCORS:corsReqeust];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Configure bucket CORS

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before bucket operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudPutBucketCORSRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudPutBucketCORSRequest, configure the bucket, and put the required CORS into QCloudCORSRule. If there are multiple CORS configurations, you can place multiple QCloudCORSRule in an NSArray, put the array into QCloudCORSConfiguration's rules attribute, and then into the request.    
2. Call the PutBucketCORS method in the QCloudCOSXMLService object to initiate the request.    
3. Obtain the setting result (error is empty or not) from finishBlock of callback, and perform additional operations if the setting is successful.   

#### QCloudPutBucketCORSRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------------------------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| corsConfiguration | Specific parameter that encapsulates CORS | QCloudCORSConfiguration * | Yes |

#### QCloudCORSConfiguration parameters

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------ | -------------------------------- |
| rules | The array containing CORS. It is a QCloudCORSRule instance. | NSArray&lt;QCloudCORSRule`*` > * |

#### QCloudCORSRule parameters

| Parameter Name | Description | Type |
| ------------- | ------------------------------------------------------------ | ---------------------------- |
| identifier | ID of the configuration rule | NSString * |
| allowedMethod | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | NSArray &lt;NSString`*`> * |
| allowedOrigin | Allowed access source. The wildcard "*" is supported. Format: protocol://domain name[:port], for example, `http://www.qq.com` | NSString * |
| allowedHeader | It is used to notify the server about which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent. The wildcard "*" is supported. | NSArray &lt;NSString `*` > * |
| maxAgeSeconds | Configures the valid period of the results obtained by OPTIONS request | int |
| exposeHeader | Configures the custom header information that can be received by the browser from the server | NSString * |

#### Example

```objective-c
QCloudPutBucketCORSRequest* putCORS = [QCloudPutBucketCORSRequest new];
QCloudCORSConfiguration* cors = [QCloudCORSConfiguration new];

QCloudCORSRule* rule = [QCloudCORSRule new];
rule.identifier = @"sdk";
rule.allowedHeader = @[@"origin",@"host",@"accept",@"content-type",@"authorization"];
rule.exposeHeader = @"ETag";
rule.allowedMethod = @[@"GET",@"PUT",@"POST", @"DELETE", @"HEAD"];
rule.maxAgeSeconds = 3600;
rule.allowedOrigin = @"*";
cors.rules = @[rule];
putCORS.corsConfiguration = cors;
putCORS.bucket = @"testBucket-123456789";
[putCORS setFinishBlock:^(id outputObject, NSError *error) {
    if (!error) {
      //success
  }
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketCORS:putCORS];
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Get bucket location

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before bucket operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudGetBucketLocationRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudGetBucketLocationRequest and enter the Bucket name.    
2. Call the GetBucketLocation method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content in finishBlock of callback.   

#### QCloudGetBucketLocationRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |

#### Parameters of returned result QCloudBucketLocationConstraint

| Parameter Name | Description | Type |
| ------------------ | -------------------- | --------- |
| locationConstraint | The region where the bucket resides | NSString* |

#### Example

```objective-c
QCloudGetBucketLocationRequest* locationReq = [QCloudGetBucketLocationRequest new];
locationReq.bucket = @"testBucket-123456789";
 __block QCloudBucketLocationConstraint* location;
[locationReq setFinishBlock:^(QCloudBucketLocationConstraint * _Nonnull result, NSError * _Nonnull error) {
       location = result;
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketLocation:locationReq];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Delete bucket CORS configuration

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before bucket operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudDeleteBucketCORSRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudDeleteBucketCORSRequest and enter the required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content in finishBlock of callback.   

#### QCloudDeleteBucketCORSRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |

#### Example

```objective-c
QCloudDeleteBucketCORSRequest* deleteCORS = [QCloudDeleteBucketCORSRequest new];
deleteCORS.bucket = @"testBucket-123456789";
[deleteCORS setFinishBlock:^(id outputObject, NSError *error) {
   //success if error == nil
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketCORS:deleteCORS];
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Query multipart upload in a bucket (List Bucket Multipart Uploads)

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before bucket operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudListBucketMultipartUploadsRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudListBucketMultipartUploadsRequest and enter the required parameters, such as the prefix and the encoding method of the returned result.    
2. Call the ListBucketMultipartUploads method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content in finishBlock of callback.   

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

#### Parameters of returned result QCloudListMultipartUploadsResult

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ---------- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * |
| prefix | The returned Object key must be prefixed with Prefix. Note that the returned key will still contain Prefix when querying with prefix. | NSString * |
| delimiter | Delimiter is a sign. If Prefix exists, the same paths between Prefix and delimiter are grouped as the same type and defined as Common Prefix, and then all Common Prefixes are listed. If Prefix does not exist, the listing process starts from the beginning of the path | NSString * |
| encodingType | Indicates the encoding method of the returned value. Available value: url | NSString * |
| keyMarker | Entries will be listed starting from this key value | NSString * |
| maxUploads | Sets the maximum number of multipart returned. Valid values: 1-1000 | int |
| uploads | Information of all multipart upload operations | NSArray* |

#### Example

```objecitve-c
QCloudListBucketMultipartUploadsRequest* uploads = [QCloudListBucketMultipartUploadsRequest new];
uploads.bucket = @"testBucket-123456789";
uploads.maxUploads = 100;
__block NSError* resulError;
__block QCloudListMultipartUploadsResult* multiPartUploadsResult;
[uploads setFinishBlock:^(QCloudListMultipartUploadsResult* result, NSError *error) {
    multiPartUploadsResult = result;
    localError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] ListBucketMultipartUploads:uploads];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem. Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Query whether a bucket exists (Head Bucket)

Head Bucket request is used to determine whether a bucket exists and whether you can access the bucket. Head and Read have the same permission. 200 is returned if the bucket exists; 403 is returned if you cannot access the bucket; and 404 is returned if the bucket does not exist.    

#### QCloudHeadBucketRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |

#### Example

```objective-c
 QCloudHeadBucketRequest* request = [QCloudHeadBucketRequest new];
 request.bucket = @"testBucket-123456789";
 [request setFinishBlock:^(id outputObject, NSError* error) {
     //Set the completion callback. If no error, the bucket can be accessed normally. Otherwise, you can get the specific failure reason by viewing the error code and message.
 }];
 [[QCloudCOSXMLService defaultCOSXML] HeadBucket:request];
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.

### Put Bucket Lifecycle

COS allows you to manage the lifecycle of an object in a bucket by configuring lifecycle. The lifecycle configuration contains one or more rule sets that will be applied to a group of object rules (each rule defines an operation for COS).
These operations are divided into the following two types:

- Transition: Specify the time when an object is transited to another storage class. For example, you can choose to transit an object to STANDARD_IA (applicable to infrequent access) storage class after 30 days of its creation.
- Expiration: Specify the expiration time of an Object. COS will automatically delete the objects that have expired.

Put Bucket Lifecycle is used to create a new lifecycle configuration for a Bucket. If the Bucket has been configured with a lifecycle, you can use this API to create a new configuration which will overwrite the existing one.

#### Parameters

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ----------------------------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| lifeCycle | Lifecycle configuration | QCloudLifecycleConfiguration* | Yes |

#### QCloudLifecycleConfiguration parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------ | ------------------------------- | ---- |
| rules | An array describing a collection of rules | NSArray<QCloudLifecycleRule*> *| Yes |

#### QCloudLifecycleRule parameters

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------- | --------------------------------------------- | ---- |
| identifier | Uniquely identifies a rule. Its length cannot exceed 255 characters. | NSString* | Yes |
| filter | Describes the collection of Objects affected by rules | QCloudLifecycleRuleFilter* |
| status | Indicates whether the rule is enabled. Enumerated values: Enabled, Disabled. | QCloudLifecycleStatue | Yes |
| abortIncompleteMultipartUpload | Sets the maximum length of time allowed for a continuous multipart upload | QCloudLifecycleAbortIncompleteMultipartUpload | No |
| transition | Rule transition attribute, which indicates when an object is transited to Standard_IA etc. | QCloudLifecycleTransition* | No |
| expiration | Rule expiration attribute | QCloudLifecycleExpiration* | No |
| noncurrentVersionExpiration | Indicates when objects of non-current version expire | QCloudLifecycleExpiration* | No |
| noncurrentVersionTransition | Indicates when objects of non-current version are transited to STANDARD_IA etc. | QCloudNoncurrentVersionExpiration* | No |

#### Example

```objective-c
QCloudPutBucketLifecycleRequest* request = [QCloudPutBucketLifecycleRequest new];
request.bucket = @"Enter bucket name";
__block QCloudLifecycleConfiguration* configuration = [[QCloudLifecycleConfiguration alloc] init];
QCloudLifecycleRule* rule = [[QCloudLifecycleRule alloc] init];
rule.identifier = @"identifier";
rule.status = QCloudLifecycleStatueEnabled;
QCloudLifecycleRuleFilter* filter = [[QCloudLifecycleRuleFilter alloc] init];
filter.prefix = @"0";
rule.filter = filter;

QCloudLifecycleTransition* transition = [[QCloudLifecycleTransition alloc] init];
transition.days = 100;
transition.storageClass = QCloudCOSStorageStandarIA;
rule.transition = transition;
request.lifeCycle = configuration;
request.lifeCycle.rules = @[rule];
[request setFinishBlock:^(id outputObject, NSError* error) {
   //Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketLifecycle:request];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Get Bucket Lifecycle

#### Parameters of returned result QCloudLifecycleConfiguration

Same with QCloudLifecycleConfiguration in the API Put Bucket Lifecycle.

#### Example

```objective-c
QCloudGetBucketLifecycleRequest* request = [QCloudGetBucketLifecycleRequest new];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(QCloudLifecycleConfiguration* result,NSError* error) {
    //Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketLifecycle:request];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Delete Bucket Lifecycle

#### Parameters of returned result QCloudLifecycleConfiguration

Same with QCloudLifecycleConfiguration in the API Put Bucket Lifecycle.

#### Example

```objective-c
QCloudDeleteBucketLifeCycleRequest* request = [[QCloudDeleteBucketLifeCycleRequest alloc ] init];
request.bucket = @"testBucket-123456789";
 [request setFinishBlock:^(QCloudLifecycleConfiguration* result, NSError* error) {
 //Set the completion callback
}];
 [[QCloudCOSXMLService defaultCOSXML] DeleteBucketLifeCycle:request];
```

### <span id="pbv">Put Bucket Versioning</span>   

This API (Put Bucket Versioning) is used to enable or suspend the bucket version control feature. Note: this is an irreversible API, and cannot be disabled after being enabled.

#### QCloudPutBucketVersioningRequest parameters

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ------------------------------------ | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| configuration | Version control details | QCloudBucketVersioningConfiguration* | Yes |

#### QCloudBucketVersioningConfiguration parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------- | ------------------------------- | ---- |
| status | Indicates whether version control is enabled. Enumerated values: Suspended\Enabled. | QCloudCOSBucketVersioningStatus | Yes |

#### Example

```objective-c
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];
request.bucket = @"testBucket-123456789";
QCloudBucketVersioningConfiguration* configuration = [[QCloudBucketVersioningConfiguration alloc] init];
request.configuration = configuration;
configuration.status = QCloudCOSBucketVersioningStatusEnabled;
[request setFinishBlock:^(id outputObject, NSError* error) {
   //Set the completion callback
 }];
 [[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.

### Get Bucket Versioning  

#### Parameters of returned result QCloudBucketVersioningConfiguration

| Parameter Name | Description | Type |
| -------- | ------------------------------------------- | ------------------------------- |
| status | Indicates whether version control is enabled. Enumerated values: Suspended\Enabled. | QCloudCOSBucketVersioningStatus |

#### Example

```objective-c
QCloudGetBucketVersioningRequest* request = [[QCloudGetBucketVersioningRequest alloc] init];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result, NSError* error) {
   //Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

### Put Bucket Replication  

Put Bucket Replication request is used to add replication configuration to the bucket for which the version control is enabled. If the bucket already has a replication configuration, the request will replace the existing configuration.    

#### QCloudPutBucketReplicationRequest parameters

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------------------------------------ | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| configuration | Describes all the cross-origin configuration | QCloudBucketReplicationConfiguration* | Yes |



> !To use this API, version management must be enabled for the bucket. For more information on version management, see [Put Bucket Versioning](#pbv).



#### Parameters of returned result

#### Example

```objective-c
QCloudPutBucketReplicationRequest* request = [[QCloudPutBucketReplicationRequest alloc] init];
request.bucket = @"source-bucket";
QCloudBucketReplicationConfiguation* configuration = [[QCloudBucketReplicationConfiguation alloc] init];
configuration.role = [NSString identifierStringWithID:@"uin" :@"uin"];
QCloudBucketReplicationRule* rule = [[QCloudBucketReplicationRule alloc] init];
rule.identifier = @"identifier";
rule.status = QCloudQCloudCOSXMLStatusEnabled;

QCloudBucketReplicationDestination* destination = [[QCloudBucketReplicationDestination alloc] init];
//qcs:id/0:cos:[region]:appid/[AppId]:[bucketname]
NSString* destinationBucket = @"destinationBucket";
NSString* region = @"destinationRegion"
destination.bucket = [NSString stringWithFormat:@"qcs:id/0:cos:%@:appid/%@:%@",@"region",@"appid",@"destinationBucket"];
rule.destination = destination;
configuration.rule = @[rule];
request.configuation = configuration;
[request setFinishBlock:^(id outputObject, NSError* error) {
     //Set the completion callback
}];
 [[QCloudCOSXMLService defaultCOSXML] PutBucketRelication:request];
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.

### Get Bucket Replication

This API (Get Bucket Replication) is used to read the cross-origin replication configuration information in a bucket.

#### Parameters of returned result QCloudBucketReplicationConfiguration

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | --------------------------------------- |
| role | Initiator ID, in the format of qcs::cam::uin/<OwnerUin>:uin/<SubUin> | NSString* |
| rule | Specific configuration information. Up to 1000 rules are supported. All rules must be directed to one destination bucket. | NSArray<QCloudBucketReplicationRule*> *|

#### QCloudBucketReplicationRule parameters

| Parameter Name | Description | Type |
| ----------- | -------------------------------------------------------- | ----------------------------------- |
| status | Indicates whether the Rule takes effect | QCloudQCloudCOSXMLStatus |
| identifier |  Indicates the name of a specific Rule | NSString* |
| prefix | Prefix match policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned. | NSString* |
| destination | Destination bucket information | QCloudBucketReplicationDestination* |

#### Example

```objective-c
QCloudGetBucketReplicationRequest* request = [[QCloudGetBucketReplicationRequest alloc] init];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(QCloudBucketReplicationConfiguation* result, NSError* error) {
    //Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketReplication:request];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Delete Bucket Replication  

This API (Delete Bucket Replication) is used to delete the cross-origin replication configuration in a bucket.

#### Parameters

#### Parameters of returned result

#### Example

```objective-c
QCloudDeleteBucketReplicationRequest* request = [[QCloudDeleteBucketReplicationRequest alloc] init];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(id outputObject, NSError* error) {
   //Set the completion callback
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketReplication:request];
```

## File-Related Operations

In COS, each file is an Object. Operating on a file is actually operating on an Object.

### Simple upload (Put Object)

Simple upload only applies to files less than 20 MB, and supports uploading files from memory.

> !The number of access policies is up to 1000. Do not set object ACL control when you upload an object if it is not required. The object inherits the bucket permissions by default.

#### QCloudPutObjectRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------------------- | ------------------------------------------------------------ | --------------------- | ---- |
| Object | ObjectKey is the unique identifier of an object in a bucket. For example, in the object's access domain name "bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg", the ObjectKey is "doc1/pic1.jpg". For more information, see [Object Description](https://cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| body | If a file is stored in the disk, it is the path of the file to be uploaded, and you can enter a variable of NSURL * type. If a file is stored in memory, you can enter a variable of NSData * type that contains the file binary data. | BodyType | Yes |
| storageClass | Storage class of an object | QCloudCOSStorageClass | Yes |
| cacheControl | Cache policy defined in RFC 2616 | NSString * | No |
| contentDisposition | File name defined in RFC 2616 | NSString * | No |
| expect | When expect=@"100-Continue" is used, the request content will not be sent until the receipt of response from server. | NSString * | No |
| expires | Expiration time defined in RFC 2616 | NSString * | No |
| initMultipleUploadFinishBlock | If the request generates a multipart upload request, after the initialization of multipart upload, a callback is performed via the block. The bucket, key, and uploadID after the completion of multipart upload, and ResumeData for resuming subsequent failed upload can be obtained from this callback block. | block | No |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read-write, public-read; Default: private | NSString * | No |
| grantRead | Grants read permission to the authorized user. Format: id=" ",id=" ". For authorization to a subaccount, id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>"; for authorization to the root account, id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>", where OwnerUin refers to the ID of the root account and SubUin refers to the ID of the subaccount. | NSString * | No |
| grantWrite | Grants write permission to the authorized user. The format is the same as above. | NSString * | No |
| grantFullControl | Grants read and write permissions to the authorized user. The format is the same as above. | NSString * | No |

#### Example    

```objective-C
QCloudPutObjectRequest* put = [QCloudPutObjectRequest new];
put.object = @"object-name";
put.bucket = @"bucket-12345678";
put.body =  [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];
[put setFinishBlock:^(id outputObject, NSError *error) {
   //Complete callback
  if (nil == error) {
   //Successful
   }
   }];
[[QCloudCOSXMLService defaultCOSXML] PutObject:put];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Query object ACL (Access Control List)

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudGetObjectACLRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudGetObjectACLRequest, and enter the bucket name and the name of the object to be queried.    
2. Call the GetObjectACL method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain the specific ACL information encapsulated in the QCloudACLPolicy object obtained from finishBlock in callback.   

#### QCloudGetObjectACLRequest parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| object | ObjectKey is the unique identifier of an object in a bucket. For example, in the object's access domain name "bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg", the key is "doc1/pic1.jpg". For more information, see [Object Description](https://cloud.tencent.com/document/product/436/13324). | NSString * | Yes |

#### Example

```objective-c
request.bucket = self.aclBucket;
request.object = @"Object name";
request.bucket = @"testBucket-123456789"
__block QCloudACLPolicy* policy;
[request setFinishBlock:^(QCloudACLPolicy * _Nonnull result, NSError * _Nonnull error) {
     policy = result;
}];
[[QCloudCOSXMLService defaultCOSXML] GetObjectACL:request];
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.

### Set object ACL (Access Control List)

The number of access policies is up to 1000. Do not set object ACL control if it is not required. The object inherits the bucket permissions by default.

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before object operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudPutObjectACLRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudPutObjectACLRequest, and enter the bucket name and additionally required parameters, such as authorization information.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain whether the configuration is completed from finishBlock in callback. If error is null, configuration is successful.   

#### QCloudPutObjectACLRequest parameters

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| object | Object name | NSString * | Yes |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read-write, public-read; Default: private | NSString * | No |
| grantRead | Grants read permission to the authorized user. Format: id=" ",id=" ".<br>For authorization to a subaccount, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;", <br>for authorization to the root account, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;", <br>where OwnerUin refers to the ID of the root account and SubUin refers to the ID of the subaccount | NSString * | No |
| grantWrite | Grants write permission to the authorized user. The format is the same as above. | NSString * | No |
| grantFullControl | Grants read and write permissions to the authorized user. The format is the same as above. | NSString * | No |

#### Example

```objective-c
QCloudPutObjectACLRequest* request = [QCloudPutObjectACLRequest new];
request.object = @"Name of the object whose ACL needs to be set";
request.bucket = @"testBucket-123456789";
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@",self.appID, self.appID];
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];
request.grantFullControl = grantString;
__block NSError* localError;
[request setFinishBlock:^(id outputObject, NSError *error) {
     localError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] PutObjectACL:request];
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Download a file

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating an instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Complete instantiation, and enter required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content in finishBlock of callback.   

#### Parameters

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| object | Object name | NSString * | Yes |
| range | The specified range of file download defined in RFC 2616 (in bytes) | NSString * | No |
| ifModifiedSince | The file content is only returned if the file is modified after the specified time. Otherwise, 412 (not modified) is returned. | NSString * | No |
| responseContentType | Sets the Content-Type parameter in the response header | NSString * | No |
| responseContentLanguage | Sets the Content-Language parameter in the response header | NSString * | No |
| responseContentExpires | Sets the Content-Expires parameter in the response header | NSString * | No |
| responseCacheControl | Sets the Cache-Control parameter in the response header | NSString * | No |
| responseContentDisposition | Sets the Content-Disposition parameter in the response header | NSString * | No |
| responseContentEncoding | Sets the Content-Encoding parameter in the response header | NSString * | No |

#### Example

```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
//Set the URL for download. If it has been set, the file is downloaded to the specified path. Otherwise, the file is downloaded to outputObject of finishBlock in memory.
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @“Your Object-Key”;
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(id outputObject, NSError *error) {
    //additional actions after finishing
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload, int64_t totalBytesExpectedToDownload) {
   //Progress of download
}];
[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Pre-request for CORS configuration of objects

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudOptionsObjectRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudOptionsObjectRequest, enter the object name, the bucket name, the HTTP method of the simulate CORS request and the access sources allowed for the simulate CORS.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content in finishBlock of callback.   

#### QCloudOptionsObjectRequest parameters

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | --------------------------- | ---- |
| object | ObjectKey is the unique identifier of an object in a bucket. For example, in the object's access domain name "bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg", the key is "doc1/pic1.jpg". For more information, see [Object Description](https://cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| accessControlRequestMethod | The HTTP method of the simulate CORS request | NSArray&lt;NSString`*`> * | Yes |
| origin | The access sources allowed for the simulate CORS. The wildcard "*" is supported. Format: protocol://domain name[:port], for example, `http://www.qq.com`. | NSString * | Yes |
| allowedHeader | It is used to notify the server about which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent. The wildcard "*" is supported. | NSArray&lt;NSString `*` > * | No |

#### Example

```objective-c
QCloudOptionsObjectRequest* request = [[QCloudOptionsObjectRequest alloc] init];
request.bucket =@"Bucket name";
request.origin = @"*";
request.accessControlRequestMethod = @"get";
request.accessControlRequestHeaders = @"host";
request.object = @"Object name";
__block id resultError;
[request setFinishBlock:^(id outputObject, NSError* error) {
     resultError = error;
 }];

[[QCloudCOSXMLService defaultCOSXML] OptionsObject:request];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Delete a single object

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudDeleteObjectRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudDeleteObjectRequest and enter the required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content in finishBlock of callback.   

#### QCloudDeleteObjectRequest parameters

| Parameter Name | Type | Required | Description |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| object | ObjectKey is the unique identifier of an object in a bucket. For example, in the object's access domain name "bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg", the key is "doc1/pic1.jpg". For more information, see [Object Description](https://cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |

#### Example

```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
deleteObjectRequest.bucket = @"testBucket-123456789";
deleteObjectRequest.object = @"Object name";
__block NSError* resultError;
[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    resultError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Delete multiple objects

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudDeleteMultipleObjectRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudDeleteMultipleObjectRequest and enter the required parameters.    
2. Call the method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content in finishBlock of callback.   

#### QCloudDeleteMultipleObjectRequest parameters

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ------------------ | ---- |
| object | ObjectKey is the unique identifier of an object in a bucket. For example, in the object's access domain name "bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg", the key is "doc1/pic1.jpg". For more information, see [Object Description](https://cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| deleteObjects | Encapsulates information of multiple objects to be deleted in batches | QCloudDeleteInfo * | Yes |

#### QCloudDeleteInfo parameters

| Parameter Name | Description | Type | Required |
| -------- | -------------------------- | ----------------------------------------- | ---- |
| objects | An array containing information on the objects to be deleted | NSArray&lt;QCloudDeleteObjectInfo `*` > * | Yes |

#### QCloudDeleteObjectInfo parameters

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| key | ObjectKey is the unique identifier of an object in a bucket. For example, in the object's access domain name "bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg", the key is "doc1/pic1.jpg". For more information, see [Object Description](https://cloud.tencent.com/document/product/436/13324). | NSString * | Yes |

#### Example

```objective-c
QCloudDeleteMultipleObjectRequest* delteRequest = [QCloudDeleteMultipleObjectRequest new];
delteRequest.bucket = @"testBucket-123456789";

QCloudDeleteObjectInfo* deletedObject0 = [QCloudDeleteObjectInfo new];
deletedObject0.key = @"Name of the first object";

QCloudDeleteObjectInfo* deleteObject1 = [QCloudDeleteObjectInfo new];
deleteObject1.key = @"Name of the second object";

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

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.



### Initialize multipart upload

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudInitiateMultipartUploadRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudInitiateMultipartUploadRequest and enter the required parameters.    
2. Call the InitiateMultipartUpload method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content in finishBlock of callback.   

#### Parameters

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | --------------------- | ---- |
| Object | The name of the file (object) to be uploaded, i.e. the key of the object. ObjectKey is the unique identifier of an object in a bucket. For example, in the object's access domain name "bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg", the key is "doc1/pic1.jpg". For more information, see [Object Description](https://cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| cacheControl | Cache policy defined in RFC 2616 | NSString * | No |
| contentDisposition | File name defined in RFC 2616 | NSString * | No |
| expect | When `expect=@"100-continue"` is used, the request content will not be sent until the receipt of response from server. | NSString * | No |
| expires | Expiration time defined in RFC 2616 | NSString * | No |
| storageClass | Storage class of an object | QCloudCOSStorageClass | No |
| accessControlList | Defines the ACL attribute of an object. Valid values: private, public-read-write, public-read; Default: private | NSString * | No |
| grantRead | Grants read permission to the authorized user. Format: id=" ",id=" ".<br>For authorization to a subaccount, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;", <br>for authorization to the root account, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;", <br>where OwnerUin refers to the ID of the root account and SubUin refers to the ID of the subaccount | NSString * | No |
| grantWrite | Grants write permission to the authorized user. The format is the same as above. | NSString * | No |
| grantFullControl | Grants read and write permissions to the authorized user. The format is the same as above. | NSString * | No |

#### Example

```objective-c
QCloudInitiateMultipartUploadRequest* initrequest = [QCloudInitiateMultipartUploadRequest new];
initrequest.bucket = @"testBucket-123456789";
initrequest.object = @"Object name";
__block QCloudInitiateMultipartUploadResult* initResult;
[initrequest setFinishBlock:^(QCloudInitiateMultipartUploadResult* outputObject, NSError *error) {
    initResult = outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] InitiateMultipartUpload:initrequest];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.

### Obtain object meta information

#### Method prototype

The header file QCloudCOSXML/QCloudCOSXML.h needs to be imported before file operations. Before that, you need to complete the initialization described in Getting Started by creating a QCloudHeadObjectRequest instance and enter some additional restrictions as needed to get the approved content. Specific steps are as follows:    

1. Instantiate QCloudHeadObjectRequest and enter the required parameters.    
2. Call the HeadObject method in the QCloudCOSXMLService object to initiate a request.    
3. Obtain specific content in finishBlock of callback.   

#### QCloudHeadObjectRequest parameters

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ---------- | ---- |
| Object | ObjectKey is the unique identifier of an object in a bucket. For example, in the object's access domain name "bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg", the key is "doc1/pic1.jpg". For more information, see [Object Description](https://cloud.tencent.com/document/product/436/13324). | NSString * | Yes |
| bucket | Bucket name, which can be found in the [COS V5 Console](https://console.cloud.tencent.com/cos5/bucket), with a format of &lt;bucketName&gt;-&lt;APPID&gt;, such as testBucket-1253653367. | NSString * | Yes |
| ifModifiedSince | The file content is only returned if the file is modified after the specified time. Otherwise, 304 (not modified) is returned. | NSString * | Yes |

#### Example

```objective-c
QCloudHeadObjectRequest* headerRequest = [QCloudHeadObjectRequest new];
headerRequest.object = @“Object name”;
headerRequest.bucket = @"testBucket-123456789";

   __block id resultError;
[headerRequest setFinishBlock:^(NSDictionary* result, NSError *error) {
      resultError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] HeadObject:headerRequest];

```

#### Error codes

When the SDK request fails, the error returned is not empty and includes the error code, error description, and other necessary debugging information to help developers quickly solve the problem.

Error codes (encapsulated in the returned error) include those returned by the device due to network problems and those returned by COS.

- Error codes generated by the device due to network problems are negative four digits, for example -1001. These error codes are defined by Apple. For more information, see the definitions in the header file NSURLError.h or [Apple's official documentation](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes).
- Error codes returned by COS are based on HTTP status codes, such as 404 and 503. For solutions to these error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) in COS official documentation.

## Adding Custom Headers

You can add custom headers as needed. Classes allowing addition of custom headers are provided with the attribute customHeaders:

```objective-c
@property (strong, nonatomic) NSMutableDictionary* customHeaders;
```

Key-value pairs in this attribute will be added to the HTTP headers of creation requests accordingly.

## Server Encryption

You can encrypt the uploaded objects in the following ways.

### Use server-side encryption with COS-hosted encryption keys (SSE-COS) to protect data

COS can automatically encrypt data as it is written to the IDC and automatically decrypt it when you access it. COS master key is used to apply AES-256 encryption to data.

You can achieve this by calling -(void)setCOSServerSideEncyption in the iOS SDK.

```objective-c
[request setCOSServerSideEncyption];
```

### Use server-side encryption with customer-provided encryption keys (SSE-C) to protect data

You can achieve this by calling -(void)setCOSServerSideEncyptionWithCustomerKey:(NSString *)customerKey in the iOS SDK.
  Note:

1. To use server side encryption, HTTPS connection is required. See the [Enable HTTPS Service](#https) section.
2. customerKey: The key provided by the user, which shall be a 32-byte string consisting of numbers, letters and strings. Chinese characters are not supported.
3. If the uploaded source file calls this method, it should also be called when downloading, querying, uploading and copying the source object using QCloudCOSXMLDownloadObjectRequest, QCloudHeadObjectRequest, QCloudCOSXMLUploadObjectRequest and QCloudCOSXMLUploadObjectRequest.

```objective-c
NSString *customKey = @"123456qwertyuioplkjhgfdsazxcvbnm";
[put setCOSServerSideEncyptionWithCustomerKey:customKey];
```

## <span id="https">Enable HTTPS Service</span>

The iOS SDK supports HTTPS requests. You only need to, when initializing the configuration object QCloudServiceConfiguration, set useHTTPS for its endpoint to YES.

```objective-c
QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
configuration.appID = kAppID;
configuration.signatureProvider = self;
QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
endpoint.regionName = kRegion;
endpoint.useHTTPS = YES;
configuration.endpoint = endpoint;
[QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
[QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
}
```

