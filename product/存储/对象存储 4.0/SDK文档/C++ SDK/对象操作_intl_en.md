## Overview

This document provides an overview of APIs related to simple object operations, multipart upload, and other operations and corresponding SDK sample code.

**Simple operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes the specified object in a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes objects in a bucket in batches |

**Multipart upload operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload task |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying Object List

#### Feature Description

This API is used to query some or all objects in a bucket.

#### Method Prototype

```cpp
CosResult GetBucket(const GetBucketReq& req, GetBucketResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of GetBucketReq requires bucket_name to be passed in
qcloud_cos::GetBucketReq req(bucket_name);
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    std::cout << "Name=" << resp.GetName() << std::endl;
    std::cout << "Prefix=" << resp.GetPrefix() << std::endl;
    std::cout << "Marker=" << resp.GetMarker() << std::endl;
    std::cout << "MaxKeys=" << resp.GetMaxKeys() << std::endl;
} else {
    std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
    std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
    std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
    std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
    std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
    std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
    std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ----------------------------------- |
| req  | GetBucketReq, which is the request for the GetBucket operation |
| resp | GetBucketResp, which is the return of the GetBucket operation |

GetBucketResp provides the following member functions for getting the specific content in XML format returned by Get Bucket. 

```cpp
std::vector<Content> GetContents();
std::string GetName();
std::string GetPrefix();
std::string GetMarker();
uint64_t GetMaxKeys();
bool IsTruncated();
std::vector<std::string> GetCommonPrefixes();
```

Content is defined as follows:

```
struct Content {
    std::string m_key; // Object key
    std::string m_last_modified; // Last modified time of the object
    std::string m_etag; // MD5 checksum of the file
    std::string m_size; // File size in bytes
    std::vector<std::string> m_owner_ids; // Bucket owner information
    std::string m_storage_class; // Storage class of the object. Enumerated values: STANDARD, STANDARD_IA
};
```

### Simply Uploading an Object

#### Feature Description

This API is used to upload an object to the specified bucket.

#### Method Prototype

```cpp
/// Upload via a stream
CosResult PutObject(const PutObjectByStreamReq& req, PutObjectByStreamResp* resp)

/// Upload a local file
CosResult PutObject(const PutObjectByFileReq& req, PutObjectByFileResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";

// Simple upload (stream)
{
    std::istringstream iss("put object");
    // The constructor of request requires istream to be passed in
    qcloud_cos::PutObjectByStreamReq req(bucket_name, object_name, iss);
    // Call the Set method to set metadata, ACL, etc.
    req.SetXCosStorageClass("STANDARD_IA");
    // Disable MD5 check. To enable it, use req.TurnOnComputeConentMd5(). This feature is enabled by default
    req.TurnOffComputeConentMd5();
    qcloud_cos::PutObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    if (result.IsSucc()) {
        // The call is successful. You can call the member function of resp to get the return content
        do sth
    } else {
        // The call failed. You can call the member function of result to get the error information
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
     }
}

// Simple upload (file)
{
    // The constructor of request requires the local file path to be passed in
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    // Call the Set method to set metadata, ACL, etc.
    req.SetXCosStorageClass("STANDARD_IA");
    // Disable MD5 check. To enable it, use req.TurnOnComputeConentMd5(). This feature is enabled by default
    req.TurnOffComputeConentMd5();
    qcloud_cos::PutObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
        if (result.IsSucc()) {
        // The call is successful. You can call the member function of resp to get the return content
        do sth
    } else {
        // The call failed. You can call the member function of result to get the error information
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
     }
}
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------------------------------ |
| req  | PutObjectByStreamReq/PutObjectByFileReq, which are the requests for the PutObject operation |
| resp | PutObjectByStreamResp/PutObjectByFileResp, which are the returns of the PutObject operation |

The Req parameter contains the following member functions:

```cpp
// Cache-Control: Cache policy as defined in RFC 2616, which will be stored as the object's metadata
void SetCacheControl(const std::string& str);

// Content-Disposition: File name as defined in RFC 2616, which will be stored as the object's metadata
void SetContentDisposition(const std::string& str);

// Content-Encoding: Encoding format as defined in RFC 2616, which will be stored as the object's metadata
void SetContentEncoding(const std::string& str);

// Content-Type: Content type (MIME) as defined in RFC 2616, which will be stored as the object's metadata
void SetContentType(const std::string& str);

// Expect: If Expect: 100-continue is used, the request content will be sent only after confirmation from the server is received
void SetExpect(const std::string& str);

// Expires: File expiration time as defined in RFC 2616, which will be stored as the object's metadata
void SetExpires(const std::string& str);

// Headers that can be customized, which will be returned as the object metadata of up to 2 KB
void SetXCosMeta(const std::string& key, const std::string& value);

// x-cos-storage-class: This sets the storage class of the object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE
// Default value: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Define the ACL attribute of the object. Value range: private, public-read
// Default value: private
void SetXcosAcl(const std::string& str);

// Grant the grantee read permission in the format of x-cos-grant-read: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantRead(const std::string& str);

// Grant the grantee read-write permission in the format of x-cos-grant-full-control: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantFullControl(const std::string& str);

/// Set the algorithm used for server-side encryption. Currently, AES256 is supported
void SetXCosServerSideEncryption(const std::string& str);
```

The Resp parameter contains the following member functions:

```C++
/// Get the version number of the object. If versioning is not enabled for the bucket, an empty string will be returned
std::string GetVersionId();

/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption();
```

### Querying Object Metadata

#### Feature Description

This API is used to query object metadata.

#### Method Prototype

```cpp
CosResult HeadObject(const HeadObjectReq& req, HeadObjectResp* resp)
```

#### Sample Request

```cpp
key := "test/hello.txt"
resp, err := client.Object.Head(context.Background(), key, nil)
```

#### Parameter Descriptions

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";
qcloud_cos::HeadObjectReq req(bucket_name, object_name);
qcloud_cos::HeadObjectResp resp;
qcloud_cos::CosResult result = cos.HeadObject(req, &resp);
if (result.IsSucc()) {
    // The download is successful. You can call the member function of HeadObjectResp
} else {
    // Failed to download. You can call the member function of CosResult to output the error information such as requestID
}
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------- |
| req  | HeadObjectReq, which is the request for the HeadObject operation |
| resp | HeadObjectResp, which is the return of the HeadObject operation |

In addition to the member functions that read the common headers, HeadObjectResp provides the following member functions:

```cpp
std::string GetXCosObjectType();

std::string GetXCosStorageClass();

// Get the custom metadata. The parameter can be the "*" in x-cos-meta-*
std::string GetXCosMeta(const std::string& key);

// Return all custom metadata as a map. The map key does not contain the "x-cos-meta-" prefix
std::map<std::string, std::string> GetXCosMetas();

// Get the algorithm used for server-side encryption
std::string GetXCosServerSideEncryption(); 
```

### Downloading an Object

#### Feature Description

This API (Get Object) is used to download an object to the local file system.

#### Method Prototype

```cpp
// Download the object into a local file
CosResult GetObject(const GetObjectByFileReq& req, GetObjectByFileResp* resp)

// Download the object into a stream
CosResult GetObject(const GetObjectByStreamReq& req, GetObjectByStreamResp* resp)

// Download the object into a local file (multi-threaded)
CosResult GetObject(const MultiGetObjectReq& req, MultiGetObjectResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";
std::string local_path = "/tmp/object_name";

// Download into a local file
{
    // request needs to carry the appid, bucketname, object, and local path (including filename)
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // The download is successful. You can call the member function of GetObjectByFileResp
    } else {
        // You can call the member function of CosResult to output the error information such as requestID
    }
}

// Download into a stream
{
    // request needs to carry the appid, bucketname, object, and output stream
    std::ostringstream os;
    qcloud_cos::GetObjectByStreamReq req(bucket_name, object_name, os);
    qcloud_cos::GetObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // The download is successful. You can call the member function of GetObjectByStreamResp
    } else {
        // Failed to download. You can call the member function of CosResult to output the error information such as requestID
    }
}

// Download a file to the local file system (multi-threaded)
{
    // request needs to carry the appid, bucketname, object, and local path (including filename)
    qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, local_path);
    qcloud_cos::MultiGetObjectResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // The download is successful. You can call the member function of MultiGetObjectResp
    } else {
        // Failed to download. You can call the member function of CosResult to output the error information such as requestID
    }
}
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------------------------------ |
| req  | GetObjectByFileReq/GetObjectByStreamReq/MultiGetObjectReq, which are the requests for the GetObject operation |
| resp | GetObjectByFileResp/GetObjectByStreamResp/MultiGetObjectResp, which are the returns of the GetObject operation |

The member functions are as follows:

```
// Set the Content-Type parameter in the response header
void SetResponseContentType(const std::string& str);

// Set the Content-Language parameter in the response header
void SetResponseContentLang(const std::string& str);

// Set the Content-Expires parameter in the response header
void SetResponseExpires(const std::string& str);

// Set the Cache-Control parameter in the response header
void SetResponseCacheControl(const std::string& str);

// Set the Content-Disposition parameter in the response header
void SetResponseContentDisposition(const std::string& str);

// Set the Content-Encoding parameter in the response header
void SetResponseContentEncoding(const std::string& str);

```

In addition to the member functions that read the common headers, GetObjectResp provides the following member functions:

```cpp
// Get the last modified time of the object, which is a date in string format, such as "Wed, 28 Oct 2014 20:30:00 GMT"
std::string GetLastModified();

// Get the object type, indicating whether the object can be appended to an upload operation. Enumerated values: normal, appendable
std::string GetXCosObjectType();

// Get the storage class of the object. Enumerated values: STANDARD, STANDARD_IA
std::string GetXCosStorageClass();

// Return all custom metadata as a map. The map key does not contain the "x-cos-meta-" prefix
std::map<std::string, std::string> GetXCosMetas();

// Get the custom metadata. The parameter can be the "*" in x-cos-meta-*
std::string GetXCosMeta(const std::string& key);

// Get the algorithm used for server-side encryption
std::string GetXCosServerSideEncryption(); 
```

### Setting Object Replication

This API is used to copy a file to the destination path.

#### Method Prototype

```cpp
CosResult PutObjectCopy(const PutObjectCopyReq& req, PutObjectCopyResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "sevenyou";

qcloud_cos::PutObjectCopyReq req(bucket_name, object_name);                                                                                                                       
req.SetXCosCopySource("sevenyousouthtest-12345656.cn-south.myqcloud.com/sevenyou_source_obj");
qcloud_cos::PutObjectCopyResp resp;
qcloud_cos::CosResult result = cos.PutObjectCopy(req, &resp);
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------------- |
| req  | PutObjectCopyReq, which is the request for the PutObjectCopy operation |
| resp | PutObjectCopyResp, which is the return of the PutObjectCopy operation |

PutObjectCopyReq contains the following member functions:

```
// Source file URL path. A previous version can be specified using the versionid sub-resource
void SetXCosCopySource(const std::string& str);

// Whether to copy metadata; enumerated values: Copy, Replaced; default value: Copy
// If the flag is Copy, the user-defined metadata in the header will be ignored and the object will be copied directly
// If the flag is Replaced, the metadata will be modified based on the header information
// If the destination path is the same as the source path (i.e., when you want to modify the metadata), the flag has to be Replaced
void SetXCosMetadataDirective(const std::string& str);

// If the object is modified after the specified time, the operation is performed; otherwise, 412 is returned.
// This parameter can be used together with x-cos-copy-source-If-None-Match. If it is used together with other conditions, a conflict is returned.
void SetXCosCopySourceIfModifiedSince(const std::string& str);

// If the object is not modified after the specified time, the operation is performed; otherwise, 412 is returned.
// This parameter can be used together with x-cos-copy-source-If-Match. If it is used together with other conditions, a conflict is returned.
void SetXCosCopySourceIfUnmodifiedSince(const std::string& str);

// If the Etag of the object is the same as the specified one, the operation is performed; otherwise, 412 is returned.
// This parameter can be used together with x-cos-copy-source-If-Unmodified-Since. If it is used together with other conditions, a conflict is returned.
void SetXCosCopySourceIfMatch(const std::string& str);

// If the Etag of the object is different from the specified one, the operation is performed; otherwise, 412 is returned.
// This parameter can be used together with x-cos-copy-source-If-Modified-Since. If it is used together with other conditions, a conflict is returned.
void SetXCosCopySourceIfNoneMatch(const std::string& str);

// x-cos-storage-class: This sets the storage class of the object. Enumerated values: STANDARD, STANDARD_IA
// Default value: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Define the ACL attribute of the object. Value range: private, public-read
// Default value: private
void SetXCosAcl(const std::string& str);

// Grant the grantee read permission in the format of id="[OwnerUin]"  
void SetXCosGrantRead(const std::string& str);

// Grant the grantee full permission in the format of id="[OwnerUin]"
void SetXCosGrantFullControl(const std::string& str);

// Headers that can be customized, which will be returned as the object metadata of up to 2 KB
void SetXCosMeta(const std::string& key, const std::string& value);

/// Set the algorithm used for server-side encryption. Currently, AES256 is supported
void SetXCosServerSideEncryption(const std::string& str);

```

PutObjectCopyResp contains the following member functions:

```
// Return the MD5 checksum of the file. The value of ETag can be used to check whether the object content has changed
std::string GetEtag();

// Return the last modified time of the file in GMT time
std::string GetLastModified();

// Return the version number
std::string GetVersionId();

/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption();

```

### Deleting a Single Object

#### Feature Description

This API is used to delete the specified object in a bucket.

#### Method Prototype

```cpp
CosResult DeleteObject(const DeleteObjectReq& req, DeleteObjectResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test_object";

qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
qcloud_cos::DeleteObjectResp resp;
qcloud_cos::CosResult result = cos.DeleteObject(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ---------------------------------------- |
| req  | DeleteObjectReq, which is the request for the DeleteObject operation |
| resp | DeletObjectResp, which is the return of the DeletObject operation |

### Deleting Multiple Objects

#### Feature Description

This API is used to delete objects in a bucket in batches.

#### Method Prototype

```cpp
CosResult DeleteObjects(const DeleteObjectsReq& req, DeleteObjectsResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

std::vector<std::string> objects;
std::vector<ObjectVersionPair> to_be_deleted;
objects.push_back("batch_delete_test_00");
objects.push_back("batch_delete_test_01");
objects.push_back("batch_delete_test_02");
objects.push_back("batch_delete_test_03");
for (size_t idx = 0; idx < objects.size(); ++idx) {
	ObjectVersionPair pair;
    pair.m_object_name = objects[idx];
	to_be_deleted.push_back(pair);
}
qcloud_cos::DeleteObjectsReq req(bucket_name, to_be_deleted);             qcloud_cos::DeleteObjectsResp resp;                                       qcloud_cos::CosResult result = cos.DeleteObjects(req, &resp);
// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 

```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------------- |
| req  | DeleteObjectsReq, which is the request for the DeleteObjects operation |
| resp | DeleteObjectsResp, which is the return of the DeleteObjects operation |

DeleteObjectsReq contains the following member functions:

```cpp
// Add an object and specify the version
void AddObjectVersion(const std::string& object, const std::string& version)
// Add an object with no versioning information
void AddObject(const std::string& object)
```

DeleteObjectsResp contains the following member functions:

```cpp
// Get the information of objects successfully deleted
std::vector<DeletedInfo> GetDeletedInfos() const

// Get the information of objects that failed to be deleted
std::vector<ErrorInfo> GetErrorinfos() const
```

The structures of the corresponding DeletedInfo and ErrorInfo are as follows:

```
struct DeletedInfo{
    std::string m_key; // Object key
}
struct ErrorInfo{
    std::string m_key; // Object key
    std::string m_code; // error code
    std::string m_message; // Error message
}
```

## Multipart Upload Operations

### Querying a Multipart Upload

#### Feature Description

This API (List Multipart Uploads) is used to query multipart uploads in progress in the specified bucket.

#### Method Prototype

```cpp
CosResult CosAPI::ListMultipartUpload(const ListMultipartUploadReq& request, ListMultipartUploadResp* response)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test_object";

qcloud_cos::ListMultipartUploadReq req(bucket_name, object_name);
qcloud_cos::ListMultipartUploadResp resp;
qcloud_cos::CosResult result = cos.ListMultipartUpload(req, &resp);

for (std::vector<qcloud_cos::Upload>::const_iterator itr = rst.begin(); itr != rst.end(); ++itr) {
	const qcloud_cos::Upload& upload = *itr;
	std::cout << "key = " << upload.m_key << ", uploadid= " << upload.m_uploadid << ", storagen class = " << upload.m_storage_class << ", m_initiated= " << upload.m_initiated << std::endl;
}   

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------------------------- |
| req  | ListMultipartUploadReq, which is the request for the ListMultipartUpload operation |
| resp | ListMultipartUploadResp, which is the return of the ListMultipartUpload operation |

ListMultipartUploadReq member functions:

```
// Specify that the returned object key must be prefixed with the "prefix". Note that when a prefix query is used, the returned key will still contain the prefix
void SetPrefix(const std::string& prefix);

// The delimiter is a symbol. The specified prefix in the object name before the first delimiter character is defined as a set of elements: common prefix. If there is no prefix, it starts at the beginning of the path
void SetDelimiter(const std::string& delimiter);

// Specify the encoding method of the return value; value range: url
void SetEncodingType(const std::string& encoding_type);

// Used together with upload-id-marker. If upload-id-marker is not specified, only the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list; otherwise, the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included, and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker.
void SetKeyMarker(const std::string& marker);

// Set the maximum number of parts returned between 1 and 1,000; default value: 1,000
void SetMaxUploads(const std::string& max_uploads);

// Used together with key-marker. If key-marker is not specified, upload-id-marker will be ignored; otherwise, the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list, and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker.
void SetUploadIdMarker(const std::string& upload_id_marker);
```

ListMultipartUploadResp member functions:

```
// Get the corresponding metadata of the object in the bucket
std::vector<Upload> GetUpload()；
// Bucket name
std::string GetName()；
// Encoding format
std::string GetEncodingType() const；
// By default, entries are listed in UTF-8 binary order, and the entry list starts at marker
std::string GetMarker() const；
// The entry list starts at this UploadId value
std::string GetUploadIdMarker() const；
// If the returned entries are truncated, then NextKeyMarker is the starting point of the next entry
std::string GetNextKeyMarker() const；
// If the returned entries are truncated, then UploadId is the starting point of the next entry
std::string GetNextUploadIdMarker() const；
// Set the maximum number of parts returned between 0 and 1,000
std::string GetMaxUploads () const；
// Whether response entries are truncated, which is a boolean value (true or false)
bool IsTruncated()；
// Returned file prefix
std::string GetPrefix() const；
// Get the delimiter 
std::string GetDelimiter() const；
// The identical paths between prefix and delimiter are grouped into one class and defined as a common prefix
std::vector<std::string> GetCommonPrefixes() const
```

### Uploading an Object in Parts

With multipart upload, you can do the following:

- Upload an object in parts, including initializing a multipart upload, uploading parts, and completing the upload of all parts.
- Delete uploaded parts.

### Initializing a Multipart Upload

#### Feature Description

This API (Initiate Multipart Upload) is used to initialize a multipart upload and get the corresponding uploadId.

#### Method Prototype

```cpp
CosResult InitMultiUpload(const InitMultiUploadReq& req, InitMultiUploadResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";

qcloud_cos::InitMultiUploadReq req(bucket_name, object_name);
qcloud_cos::InitMultiUploadResp resp;
qcloud_cos::CosResult result = cos.InitMultiUpload(req, &resp);

std::string upload_id = "";
if (result.IsSucc()) {
    upload_id = resp.GetUploadId();
}
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ----------------------------------------------- |
| req  | InitMultiUploadReq, which is the request for the InitMultiUpload operation |
| resp | InitMultiUploadResp, which is the return of the InitMultiUpload operation |

The member functions of InitMultiUploadReq are as follows:

```
// Cache-Control: Cache policy as defined in RFC 2616, which will be stored as the object's metadata
void SetCacheControl(const std::string& str);

// Content-Disposition: File name as defined in RFC 2616, which will be stored as the object's metadata
void SetContentDisposition(const std::string& str);

// Content-Encoding: Encoding format as defined in RFC 2616, which will be stored as the object's metadata
void SetContentEncoding(const std::string& str);

// Content-Type: Content type (MIME) as defined in RFC 2616, which will be stored as the object's metadata
void SetContentType(const std::string& str);

// Expires: File expiration time as defined in RFC 2616, which will be stored as the object's metadata
void SetExpires(const std::string& str);

// Headers that can be customized, which will be returned as the object metadata of up to 2 KB
void SetXCosMeta(const std::string& key, const std::string& value);

// x-cos-storage-class: This sets the storage class of the object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE
// Default value: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Define the ACL attribute of the object. Value range: private, public-read
// Default value: private
void SetXcosAcl(const std::string& str);

// Grant the grantee read permission in the format of x-cos-grant-read: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantRead(const std::string& str);

// Grant the grantee read-write permission in the format of x-cos-grant-full-control: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantFullControl(const std::string& str);

/// Set the algorithm used for server-side encryption. Currently, AES256 is supported
void SetXCosServerSideEncryption(const std::string& str);

```

After the request is successfully executed, the returned response will include the bucket, key, and uploadId, which represent the destination bucket of the multipart upload, the object name, and the number required by subsequent multipart uploads.

The member functions of InitMultiUploadResp are as follows:

```cpp
std::string GetBucket();
std::string GetKey();
std::string GetUploadId();

/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption();
```

### <span id = "MULIT_UPLOAD_PART">Uploading Parts</span>

This API (Upload Part) is used to upload parts.

#### Method Prototype

```cpp
CosResult UploadPartData(const UploadPartDataReq& request, UploadPartDataResp* response)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test_object";

// Upload the first part
{
    std::fstream is("demo_5M.part1");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name, upload_id, is);
    req.SetPartNumber(1);
    // Disable MD5 check. To enable it, use req.TurnOnComputeConentMd5(). This feature is enabled by default
    req.TurnOffComputeConentMd5();
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // After the upload is successful, record the part number and the returned ETag
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_numbers.push_back(1);
    }
    is.close();
}

// Upload the second part
{
    std::fstream is("demo_5M.part2");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name,
                                      upload_id, is);
    req.SetPartNumber(2);
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // After the upload is successful, record the part number and the returned ETag 
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_numbers.push_back(2);
    }
    is.close();
}
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | --------------------------------------------- |
| req  | UploadPartDataReq, which is the request for the UploadPartData operation |
| resp | UploadPartDataResp, which is the return of the UploadPartData operation |

When you construct UploadPartDataReq, you need to specify the request APPID, bucket, object, the UploadId obtained after successful initialization, and the uploaded data stream (which should be closed by the caller after the call is completed).

```
UploadPartDataReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id,
                    std::istream& in_stream);

```

In addition, you should set the part number for the request, which will also be used when you complete the multipart upload.

```
void SetPartNumber(uint64_t part_number);

```

The member functions of UploadPartDataResp are as follows:

```
/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption();

```

### Copying Parts

This API is used to copy an object as a part.

#### Method Prototype

```cpp
CosResult UploadPartCopyData(const UploadPartCopyDataReq& request,UploadPartCopyDataResp* response)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test_object";

std::string upload_id;
std::vector<uint64_t> numbers;
std::vector<std::string> etags;
std::string etag1 = "", etag2 = "";
InitMultiUpload(cos, bucket_name, object_name, &upload_id);

// First part
qcloud_cos::UploadPartCopyDataReq req(bucket_name, object_name, upload_id, 1);
req.SetXCosCopySource("sevenyousouth-1251668577.cos.ap-guangzhou.myqcloud.com/seven_10G.tmp");
req.SetXCosCopySourceRange("bytes=0-1048576000");                         qcloud_cos::UploadPartCopyDataResp resp;                                 qcloud_cos::CosResult result = cos.UploadPartCopyData(req, &resp);
if(result.IsSucc()) {
    etag1 = resp.GetEtag();
}
numbers.push_back(1);
etags.push_back(etag1);

// Second part
qcloud_cos::UploadPartCopyDataReq req2(bucket_name, object_name, upload_id, 2);                                                       req2.SetXCosCopySource("sevenyoutest-7319456.cos.cn-north.myqcloud.com/sevenyou_2G_part");
req2.SetXCosCopySourceRange("bytes=1048576000-2097152000");
qcloud_cos::UploadPartCopyDataResp resp2;
qcloud_cos::CosResult result = cos.UploadPartCopyData(req2, &resp2);
if(result.IsSucc()) {
    etag2 = resp2.GetEtag();
}
numbers.push_back(2)；
etags.push_back(etag2);

CompleteMultiUpload(cos, bucket_name, object_name, upload_id, etags, numbers);
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ----------------------------------------------------- |
| req  | UploadPartCopyDataReq, which is the request for the UploadPartCopyData operation |
| resp | UploadPartCopyDataResp, which is the return of the UploadPartCopyData operation |

```cpp
/// Set the ID of this multipart copy
void SetUploadId(const std::string& upload_id)
/// Set the number of this multipart copy
void SetPartNumber(uint64_t part_number)
/// Set the source file URL path for this multipart copy. A previous version can be specified using the versionid sub-resource
void SetXCosCopySource(const std::string& src)
/// Set the byte range of the source file in the format of bytes=first-last
void SetXCosCopySourceRange(const std::string& range)
 /// If the object is modified after the specified time, the operation is performed; otherwise, 412 is returned
void SetXCosCopySourceIfModifiedSince(const std::string& date)
/// If the object is not modified after the specified time, the operation is performed; otherwise, 412 is returned
void SetXCosCopySourceIfUnmodifiedSince(const std::string& date)
/// If the Etag of the object is the same as the specified one, the operation is performed; otherwise, 412 is returned 
void SetXCosCopySourceIfMatch(const std::string& etag)
/// If the Etag of the object is different from the specified one, the operation is performed; otherwise, 412 is returned
void SetXCosCopySourceIfNoneMatch(const std::string& etag)
```

```
/// Get the MD5 checksum of the returned file
std::string GetEtag() const
/// Return the last modified time of the file in GMT time
std::string GetLastModified() const
/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption() const
```

### Querying Uploaded Parts

#### Feature Description

This API is used to query uploaded parts in the specified multipart upload operation.

#### Method Prototype

```cpp
CosResult ListParts(const ListPartsReq& req, ListPartsResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test_object";

// uploadId is obtained after InitMultiUpload is called
qcloud_cos::ListPartsReq req(bucket_name, object_name, upload_id);
req.SetMaxParts(1);                                                                                                                                                               
req.SetPartNumberMarker("1");
qcloud_cos::ListPartsResp resp;
qcloud_cos::CosResult result = cos.ListParts(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ----------------------------------- |
| req  | ListPartsReq, which is the request for the ListParts operation |
| resp | ListPartsResp, which is the return of the ListParts operation |

ListPartsReq contains the following member functions:

```
// Constructor, bucket name, object name, multipart upload ID
ListPartsReq(const std::string& bucket_name,                                                                                                                                      
             const std::string& object_name,
             const std::string& upload_id); 

// \brief Specify the encoding method of the return value
void SetEncodingType(const std::string& encoding_type);

// \brief Maximum number of entries returned at a time; 1,000 will be used by default if this is not set
void SetMaxParts(uint64_t max_parts);

// \brief By default, entries are listed in UTF-8 binary order, and the entry list starts at marker
void SetPartNumberMarker(const std::string& part_number_marker);

```

ListPartsResp contains the following member functions:

```
// Destination bucket for the multipart upload
std::string GetBucket();

// Specify the encoding method of the return value
std::string GetEncodingType();

// Object name
std::string GetKey();

// ID of this multipart upload
std::string GetUploadId();

// Identify the initiator of this upload
Initiator GetInitiator();

// Identify the owner of the parts
Owner GetOwner();

// By default, entries are listed in UTF-8 binary order, and the entry list starts at marker
uint64_t GetPartNumberMarker();

// Return the information of each part
std::vector<Part> GetParts();

// If the returned entries are truncated, then NextMarker is the starting point of the next entry
uint64_t GetNextPartNumberMarker();

// Indicate the part storage class; enumerated values: Standard, Standard_IA, Archive
std::string GetStorageClass();

// Maximum number of entries returned at a time
uint64_t GetMaxParts();

// Whether returned entries are truncated, which is a boolean value (TRUE or FALSE)
bool IsTruncated();

```

Part, Owner, and Initiator are defined as follows:

```cpp
struct Initiator {
    std::string m_id; // Unique ID of the creator
    std::string m_display_name; // Creator's username
};

struct Owner {
    std::string m_id; // Unique ID of the user
    std::string m_display_name; // Username
};

struct Part {
    uint64_t m_part_num; // Part number
    uint64_t m_size; // Part size in bytes
    std::string m_etag; // MD5 checksum of the object part
    std::string m_last_modified; // Last modified time of the part
};

```

### Completing a Multipart Upload

#### Feature Description

The API is used to complete the multipart upload of the entire file.

#### Method Prototype

```cpp
CosResult CompleteMultiUpload(const CompleteMultiUploadReq& request, CompleteMultiUploadResp* response)
```

#### Sample Request

```cpp
qcloud_cos::CompleteMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::CompleteMultiUploadResp resp;
req.SetEtags(etags);
req.SetPartNumbers(part_numbers);

qcloud_cos::CosResult result = cos.CompleteMultiUpload(req, &resp);
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------------------------- |
| req  | CompleteMultiUploadReq, which is the request for the CompleteMultiUpload operation |
| resp | CompleteMultiUploadResp, which is the return of the CompleteMultiUpload operation |

When you construct CompleteMultiUploadReq, you need to specify the request APPID, bucket, object, and the UploadId obtained after successful initialization.

```
CompleteMultiUploadReq(const std::string& bucket_name,
                       const std::string& object_name, const std::string& upload_id)

```

In addition, you need to set the part numbers and Etags of all uploaded parts for the request.

```
// When calling the following method, you should make sure that the order of part numbers is the same as that of ETags.
void SetPartNumbers(const std::vector<uint64_t>& part_numbers);
void SetEtags(const std::vector<std::string>& etags) ;

// Add a pair of part_number and ETag
void AddPartEtagPair(uint64_t part_number, const std::string& etag);

/// Set the algorithm used for server-side encryption. Currently, AES256 is supported
void SetXCosServerSideEncryption(const std::string& str);
```

The return contents of CompleteMultiUploadResp include Location, Bucket, Key, and ETag, which respectively represent the public network access domain name of the created object, destination bucket for the multipart upload, name of the object, and MD5 checksum of the merged file. The following member functions can be called to access the contents of the response.

```
std::string GetLocation();
std::string GetKey();
std::string GetBucket();
std::string GetEtag();

/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption();

```

### Aborting a Multipart Upload

#### Feature Description

This API is used to abort a multipart upload operation and delete the uploaded parts.

#### Method Prototype

```cpp
CosResult AbortMultiUpload(const AbortMultiUploadReq& request, AbortMultiUploadResp* response)
```

#### Sample Request

```cpp
qcloud_cos::AbortMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::AbortMultiUploadResp resp;
qcloud_cos::CosResult result = cos.AbortMultiUpload(req, &resp);
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------------------- |
| req  | AbortMultiUploadReq, which is the request for the AbortMultiUpload operation |
| resp | AbortMultiUploadResp, which is the return of the AbortMultiUpload operation |

When you construct AbortMultiUploadReq, you need to specify the bucket, object, and Upload_id.

```cpp
AbortMultiUploadReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id);
```

There is no special method. You can call the member function of BaseResp to get the common header content.

## Other Operations

### Restoring an Archived Object 

#### Feature Description

This API is used to retrieve an archived object for access.

#### Method Prototype

```cpp
CosResult PostObjectRestore(const PostObjectRestoreReq& req, PostObjectRestoreResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "sevenyou";

{   
    qcloud_cos::PostObjectRestoreReq req(bucket_name, object_name);
    req.SetExiryDays(30);
    req.SetTier("Standard");
    qcloud_cos::PostObjectRestoreResp resp;
    qcloud_cos::CosResult result = cos.PostObjectRestore(req, &resp);
    // The call is successful. You can call the member function of resp to get the return content
    if (result.IsSucc()) {
        // ...
    } else {
        // You can call the member function of CosResult to output the error information such as requestID
    } 
}   
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ---------------------------------------------------- |
| req  | PostObjectRestoreReq, which is the request for the PostObjectRestore operation |
| resp | PostObjectRestoreResp, which is the return of the PostObjectRestore operation |

PostObjectRestoreReq contains the following member functions:

```
// Set expiration time of the temporary copy
void SetExiryDays(uint64_t days);

// Enumerated values: Expedited, Standard, Bulk; default value: Standard
void SetTier(const std::string& tier);
```

### Setting Object ACL

#### Feature Description

This API is used to set the ACL for an object.

#### Method Prototype

```cpp
CosResult PutObjectACL(const PutObjectACLReq& req, PutObjectACLResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "sevenyou";

// 1. Set the ACL configuration (through the body. You can set the ACL in either body or header mode, but you can choose only one of them; otherwise, there will be conflicts)
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);
    qcloud_cos::Owner owner = {"qcs::cam::uin/xxxxx:uin/xxx", "qcs::cam::uin/xxxxxx:uin/xxxxx" };
    qcloud_cos::Grant grant;
    req.SetOwner(owner);
    grant.m_grantee.m_type = "Group";
    grant.m_grantee.m_uri = "http://cam.qcloud.com/groups/global/AllUsers";
    grant.m_perm = "READ";
    req.AddAccessControlList(grant);

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    // The call is successful. You can call the member function of resp to get the return content
    if (result.IsSucc()) {
        // ...
    } else {
        // Set the ACL. You can call the member function of CosResult to output the error information such as requestID
    } 
}   

// 2. Set the ACL configuration (through the header. You can set the ACL in either body or header mode, but you can choose only one of them; otherwise, there will be conflicts)
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);                                                                                                                    
    req.SetXCosAcl("public-read-write");

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    // The call is successful. You can call the member function of resp to get the return content
    if (result.IsSucc()) {
        // ...
    } else {
        // You can call the member function of CosResult to output the error information such as requestID
    } 
}   
```



#### Parameter Descriptions

| Parameter | Description |
| ---- | ----------------------------------------- |
| req  | PutObjectACLReq, which is the request for the PutObjectACL operation |
| resp | PutObjectACLResp, which is the return of the PutObjectACL operation |

PutObjectACLReq contains the following member functions:

```
// Define the ACL attribute of the object. Value range: private, public-read
// Default value: private
void SetXCosAcl(const std::string& str);

// Grant the grantee read permission in the format of id="[OwnerUin]" 
void SetXCosGrantRead(const std::string& str);

// Grant the grantee full permission in the format of id="[OwnerUin]"
void SetXCosGrantFullControl(const std::string& str);

// Object owner ID
void SetOwner(const Owner& owner);

// Set the information of grantee and permission
void SetAccessControlList(const std::vector<Grant>& grants);

// Add the permission information of a single object
void AddAccessControlList(const Grant& grant);
        

```

> APIs such as SetXCosAcl, SetXCosGrantRead, SetXCosGrantWrite, and SetXCosGrantFullControl cannot be used together with SetAccessControlList or AddAccessControlList at the same time, because the former type is actually implemented by setting the HTTP header, while the latter type is to add content in XML format to the body. You can choose only one type of them. The former type is preferred within the SDK.

ACLRule is defined as follows:

```
struct Grantee {
    // The type can be RootAccount or SubAccount
    // If the type is RootAccount, you can enter an account ID in the uin field in the ID or enter anyone (representing all types of users) in place of uin/<OwnerUin> and uin/<SubUin>
    // If the type is RootAccount, uin represents the root account, while Subaccount represents the sub-account
    std::string m_type; 
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; // Optional
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; // Resource information of the grantee
    std::string m_perm; // Specify the permission granted to the grantee. Enumerated values: READ, FULL_CONTROL
};


```

### Querying Object ACL

#### Feature Description

This API is used to query the ACL of an object.

#### Method Prototype

```cpp
CosResult GetObjectACL(const DGetObjectACLReq& req, GetObjectACLResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";

// The constructor of GetObjectACLReq requires Object_name to be passed in
qcloud_cos::GetObjectACLReq req(bucket_name, object_name);
qcloud_cos::GetObjectACLResp resp;
qcloud_cos::CosResult result = cos.GetObjectACL(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ----------------------------------------- |
| req  | GetObjectACLReq, which is the request for the GetObjectACL operation |
| resp | GetObjectACLResp, which is the return of the GetObjectACL operation |

GetObjectACLResp contains the following member functions:

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();
```

## Advanced API (Recommended)

### Composite Upload

#### Feature Description

This API is used to upload a file concurrently by encapsulating various APIs of multipart upload.

#### Method Prototype

```cpp
CosResult MultiUploadObject(const MultiUploadObjectReq& request, MultiUploadObjectResp* response)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";
std::string local_file = "./test"

qcloud_cos::MultiUploadObjectReq req(bucket_name, object_name, local_file);
// To keep the parts alive inside the completion API, it is recommended to set a longer timeout.
req.SetRecvTimeoutInms(1000 * 60);
qcloud_cos::MultiUploadObjectResp resp;
qcloud_cos::CosResult result = cos.MultiUploadObject(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
	// You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | --------------------------------------------------- |
| req  | MultiUploadObjectReq, which is the request for the MultiUploadObject operation |
| resp | MultiUploadObjectResp, which is the return of the MultiUploadObject operation |

MultiUploadObjectReq contains the following member functions:

```cpp
// Set the part size. If it is less than 1 MB, it will be calculated as 1 MB. If it is greater than 5 GB, it will be calculated as 5 GB
void SetPartSize(uint64_t bytes)
// Headers that can be customized, which will be returned as the object metadata of up to 2 KB 
void SetXCosMeta(const std::string& key, const std::string& value)
// Set the algorithm used for server-side encryption. Currently, AES256 is supported
void SetXCosServerSideEncryption(const std::string& str)
// Set the internal thread pool size
void SetThreadPoolSize(int size)
```

MultiUploadObjectResp contains the following member functions:

```
std::string GetRespTag()
/// Algorithm used for server-side encryption 
std::string GetXCosServerSideEncryption() const
```

### Composite Download

#### Feature Description

This API is used to download a file using concurrent ranges.

#### Method Prototype

```cpp
CosResult GetObject(const MultiGetObjectReq& request, 
MultiGetObjectResp* response)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";
std::string file_path = "./test";

qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, file_path);   qcloud_cos::MultiGetObjectResp resp;                                     qcloud_cos::CosResult result = cos.GetObject(req, &resp); 

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ---------------------------------------- |
| req  | MultiGetObjectReq, which is the request for the GetObject operation |
| resp | MultiGetObjectResp, which is the return of the GetObject operation |

MultiGetObjectReq contains the following member functions:

```cpp
// Set part size
void SetSliceSize(uint64_t bytes)
// Set thread pool size
void SetThreadPoolSize(int size)
```

MultiGetObjectResp contains the following member functions:

```cpp
/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption() const
```
