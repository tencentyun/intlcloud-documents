## Overview

This document provides an overview of APIs related to simple object operations, multipart uploads, and other operations as well as their corresponding SDK sample code.

**Simple operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/7734) | Querying an object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting one object | Deletes a specified object in a bucket |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket in a single request |

**Multipart upload operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload job |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a file part |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for a specified object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object |

## Simple Operations

### Querying an object list

#### Feature description

This API is used to query some or all objects in a bucket.

#### Method prototype

```cpp
CosResult GetBucket(const GetBucketReq& req, GetBucketResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of GetBucketReq requires bucket_name to be passed in
qcloud_cos::GetBucketReq req(bucket_name);
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);

// The call is successful. You can call the resp member functions to get the return content
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

#### Parameter description

| Parameter | Description |
| ---- | ----------------------------------- |
| req  | GetBucketReq, the request for the GetBucket operation |
| resp | GetBucketResp, the return of the GetBucket operation |

GetBucketResp provides the following member functions for getting the specific content (in XML format) returned by Get Bucket. 

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
    std::string m_last_modified; // Time the object was last modified 
    std::string m_etag; // MD5 checksum of the file
    std::string m_size; // File size in bytes
    std::vector<std::string> m_owner_ids; // Bucket owner information
    std::string m_storage_class; // Storage class of the object. Enumerated values: STANDARD, STANDARD_IA
};
```

### Simply uploading an object

#### Feature description

This API is used to upload an object to a specified bucket.

#### Method prototype

```cpp
/// Upload via a stream
CosResult PutObject(const PutObjectByStreamReq& req, PutObjectByStreamResp* resp)

/// Upload a local file
CosResult PutObject(const PutObjectByFileReq& req, PutObjectByFileResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";

// Simple upload (stream)
{
    std::istringstream iss("put object");
    // The constructor of the request requires istream to be passed in
    qcloud_cos::PutObjectByStreamReq req(bucket_name, object_name, iss);
    // Call the Set method to set metadata, ACL, etc.
    req.SetXCosStorageClass("STANDARD_IA");
    // Disable MD5 check. To enable, use req.TurnOnComputeConentMd5(). This feature is enabled by default
    req.TurnOffComputeConentMd5();
    qcloud_cos::PutObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    if (result.IsSucc()) {
        // The call is successful. You can call the resp member functions to get the return content
        do sth
    } else {
        // The call failed. You can call the result member functions to get the error information
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
    // The constructor of the request requires the local file path to be passed in
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    // Call the Set method to set metadata, ACL, etc.
    req.SetXCosStorageClass("STANDARD_IA");
    // Disable MD5 check. To enable, use req.TurnOnComputeConentMd5(). This feature is enabled by default
    req.TurnOffComputeConentMd5();
    qcloud_cos::PutObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
        if (result.IsSucc()) {
        // The call is successful. You can call the resp member functions to get the return content
        do sth
    } else {
        // The call failed. You can call the result member functions to get the error information
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

#### Parameter description

| Parameter | Description |
| ---- | ------------------------------------------------------------ |
| req  | PutObjectByStreamReq/PutObjectByFileReq, the requests for the PutObject operation |
| resp | PutObjectByStreamResp/PutObjectByFileResp, the returns of the PutObject operation |

The Req parameter contains the following member functions:

```cpp
// Cache-Control: cache policy as defined in RFC 2616, will be stored as object metadata
void SetCacheControl(const std::string& str);

// Content-Disposition: filename as defined in RFC 2616, will be stored as object metadata
void SetContentDisposition(const std::string& str);

// Content-Encoding: encoding format as defined in RFC 2616, will be stored as object metadata
void SetContentEncoding(const std::string& str);

// Content-Type: content type (MIME) as defined in RFC 2616, will be stored as object metadata
void SetContentType(const std::string& str);

// Expect: if `Expect: 100-continue` is used, the request content will be sent only after confirmation from the server is received
void SetExpect(const std::string& str);

// Expires: file expiration time as defined in RFC 2616, will be stored as object metadata
void SetExpires(const std::string& str);

// Headers that allow user-customization, will be returned as object metadata of up to 2 KB
void SetXCosMeta(const std::string& key, const std::string& value);

// x-cos-storage-class: sets the storage class of an object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE
// Default value: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Define the ACL attribute of the object. Valid values: private, public-read
// Default value: private
void SetXcosAcl(const std::string& str);

// Grant read permission in the format: x-cos-grant-read: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantRead(const std::string& str);

// Grant read-write permission in the format: x-cos-grant-full-control: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantFullControl(const std::string& str);

/// Set the algorithm used for server-side encryption. Currently, AES256 is supported
void SetXCosServerSideEncryption(const std::string& str);
```

The Resp parameter contains the following member functions:

```C++
/// Get the object’s version number. If versioning is not enabled for the bucket, an empty string will be returned
std::string GetVersionId();

/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption();
```

### Querying object metadata

#### Feature description

This API is used to query object metadata.

#### Method prototype

```cpp
CosResult HeadObject(const HeadObjectReq& req, HeadObjectResp* resp)
```



#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";
qcloud_cos::HeadObjectReq req(bucket_name, object_name);
qcloud_cos::HeadObjectResp resp;
qcloud_cos::CosResult result = cos.HeadObject(req, &resp);
if (result.IsSucc()) {
    // The download is successful. You can call the HeadObjectResp member functions
} else {
    // Failed to download. You can call the CosResult member functions to output the error information, such as requestID
}
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------------------------- |
| req  | HeadObjectReq, the request for the HeadObject operation |
| resp | HeadObjectResp, the return of the HeadObject operation |

In addition to member functions that read common headers, HeadObjectResp provides the following member functions:

```cpp
std::string GetXCosObjectType();

std::string GetXCosStorageClass();

// Get custom metadata. The parameter can be the "*" in x-cos-meta-*
std::string GetXCosMeta(const std::string& key);

// Return all custom metadata as a map. The map key does not contain the "x-cos-meta-" prefix
std::map<std::string, std::string> GetXCosMetas();

// Get the algorithm used for server-side encryption
std::string GetXCosServerSideEncryption(); 
```

### Downloading an object

#### Feature description

This API (Get Object) is used to download an object to the local file system.

#### Method prototype

```cpp
// Download the object to a local file
CosResult GetObject(const GetObjectByFileReq& req, GetObjectByFileResp* resp)

// Download the object to a stream
CosResult GetObject(const GetObjectByStreamReq& req, GetObjectByStreamResp* resp)

// Download the object to a local file (multi-threaded)
CosResult GetObject(const MultiGetObjectReq& req, MultiGetObjectResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";
std::string local_path = "/tmp/object_name";

// Download into a local file
{
    // The request needs to carry the appid, bucketname, object, and local path (including filename)
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // The download is successful. You can call the GetObjectByFileResp member functions
    } else {
        // You can call the CosResult member functions to output the error information, such as requestID
    }
}

// Download into a stream
{
    // The request needs to carry the appid, bucketname, object, and output stream
    std::ostringstream os;
    qcloud_cos::GetObjectByStreamReq req(bucket_name, object_name, os);
    qcloud_cos::GetObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // The download is successful. You can call the GetObjectByStreamResp member functions
    } else {
        // Failed to download. You can call the CosResult member functions to output the error information, such as requestID
    }
}

// Download a file to the local file system (multi-threaded)
{
    // request needs to carry the appid, bucketname, object, and local path (including filename)
    qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, local_path);
    qcloud_cos::MultiGetObjectResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // The download is successful. You can call the MultiGetObjectResp member functions
    } else {
        // Failed to download. You can call the CosResult member functions to output the error information, such as requestID
    }
}
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------------------------------------------------ |
| req  | GetObjectByFileReq/GetObjectByStreamReq/MultiGetObjectReq, the requests for the GetObject operation |
| resp | GetObjectByFileResp/GetObjectByStreamResp/MultiGetObjectResp, the returns of the GetObject operation |

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

In addition to member functions that read common headers, GetObjectResp provides the following member functions:

```cpp
// Get the time an object was last modified, a date in string format, such as "Wed, 28 Oct 2014 20:30:00 GMT"
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

### Setting object replication

This API is used to copy a file to the destination path.

#### Method prototype

```cpp
CosResult PutObjectCopy(const PutObjectCopyReq& req, PutObjectCopyResp* resp)
```

#### Sample request

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

#### Parameter description

| Parameter | Description |
| ---- | ------------------------------------------- |
| req  | PutObjectCopyReq, the request for the PutObjectCopy operation |
| resp | PutObjectCopyResp, the return of the PutObjectCopy operation |

PutObjectCopyReq contains the following member functions:

```
// Source file URL path. A previous version can be specified using the versionid sub-resource
void SetXCosCopySource(const std::string& str);

// Whether to copy metadata. Enumerated values: Copy, Replaced. Default value: Copy
// If the flag is Copy, the user-defined metadata in the header will be ignored and the object will be copied directly
// If the flag is Replaced, the metadata will be modified based on the header information
// If the destination path is the same as the source path (i.e., when you want to modify the metadata), the flag has to be Replaced
void SetXCosMetadataDirective(const std::string& str);

// If the object has been modified after the specified time, the operation is performed; otherwise, error code 412 is returned.
// This parameter can be used together with x-cos-copy-source-If-None-Match. If it is used together with other conditions, a conflict is returned.
void SetXCosCopySourceIfModifiedSince(const std::string& str);

// If the object has not been modified after the specified time, the operation is performed; otherwise, error code 412 is returned.
// This parameter can be used together with x-cos-copy-source-If-Match. If it is used together with other conditions, a conflict is returned.
void SetXCosCopySourceIfUnmodifiedSince(const std::string& str);

// If the Etag of the object is the same as the specified one, the operation is performed; otherwise, error code 412 is returned.
// This parameter can be used together with x-cos-copy-source-If-Unmodified-Since. If it is used together with other conditions, a conflict is returned.
void SetXCosCopySourceIfMatch(const std::string& str);

// If the Etag of the object is different from the specified one, the operation is performed; otherwise, error code 412 is returned.
// This parameter can be used together with x-cos-copy-source-If-Modified-Since. If it is used together with other conditions, a conflict is returned.
void SetXCosCopySourceIfNoneMatch(const std::string& str);

// x-cos-storage-class: sets the storage class of an object. Enumerated values: STANDARD, STANDARD_IA
// Default value: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Define the ACL attribute of the object. Valid values: private, public-read
// Default value: private
void SetXCosAcl(const std::string& str);

// Grant read permission in the format: id="[OwnerUin]"  
void SetXCosGrantRead(const std::string& str);

// Grant full permission in the format: id="[OwnerUin]"
void SetXCosGrantFullControl(const std::string& str);

// Headers that allow user-customization, will be returned as object metadata of up to 2 KB
void SetXCosMeta(const std::string& key, const std::string& value);

/// Set the algorithm used for server-side encryption. Currently, AES256 is supported
void SetXCosServerSideEncryption(const std::string& str);

```

PutObjectCopyResp contains the following member functions:

```
// Return the MD5 checksum of the file. The value of ETag can be used to check whether the object content has changed
std::string GetEtag();

// Return the time the file was last modified in GMT time
std::string GetLastModified();

// Return the version number
std::string GetVersionId();

/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption();

```

### Deleting a single object

#### Feature description

This API is used to delete a specified object in a bucket.

#### Method prototype

```cpp
CosResult DeleteObject(const DeleteObjectReq& req, DeleteObjectResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test_object";

qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
qcloud_cos::DeleteObjectResp resp;
qcloud_cos::CosResult result = cos.DeleteObject(req, &resp);

// The call is successful. You can call the resp member functions to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Parameter description

| Parameter | Description |
| ---- | ---------------------------------------- |
| req  | DeleteObjectReq, the request for the DeleteObject operation |
| resp | DeletObjectResp, the return of the DeletObject operation |

### Deleting multiple objects

#### Feature description

This API is used to delete multiple objects from a bucket in a single request.

#### Method prototype

```cpp
CosResult DeleteObjects(const DeleteObjectsReq& req, DeleteObjectsResp* resp)
```

#### Sample request

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
// The call is successful. You can call the resp member functions to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 

```

#### Parameter description

| Parameter | Description |
| ---- | ------------------------------------------- |
| req  | DeleteObjectsReq, the request for the DeleteObjects operation |
| resp | DeleteObjectsResp, the return of the DeleteObjects operation |

DeleteObjectsReq contains the following member functions:

```cpp
// Add an object and specify the version
void AddObjectVersion(const std::string& object, const std::string& version)
// Add an object with no versioning information
void AddObject(const std::string& object)
```

DeleteObjectsResp contains the following member functions:

```cpp
// Get the information of successfully deleted objects
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

### Querying a multipart upload

#### Feature description

This API (List Multipart Uploads) is used to query multipart uploads in progress in a specified bucket.

#### Method prototype

```cpp
CosResult CosAPI::ListMultipartUpload(const ListMultipartUploadReq& request, ListMultipartUploadResp* response)
```

#### Sample request

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

// The call is successful. You can call the resp member functions to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------------------------------------------- |
| req  | ListMultipartUploadReq, the request for the ListMultipartUpload operation |
| resp | ListMultipartUploadResp, the return of the ListMultipartUpload operation |

ListMultipartUploadReq member functions:

```
// Specify that the returned object keys must have a specified prefix. Note that when a prefix query is used, the returned key will still contain the prefix
void SetPrefix(const std::string& prefix);

// The delimiter is a symbol. Objects that contain the same string between the specified prefix and the first occurrence of the delimiter are grouped together as a set of elements: common prefix. If there is no prefix, the delimiter starts at the beginning of the path
void SetDelimiter(const std::string& delimiter);

// Specify the encoding method of the return value. Valid value: url
void SetEncodingType(const std::string& encoding_type);

// Used together with upload-id-marker. If upload-id-marker is not specified, only the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list; otherwise, the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included, and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker.
void SetKeyMarker(const std::string& marker);

// Set the maximum number of parts returned between 1 and 1,000. Default value: 1,000
void SetMaxUploads(const std::string& max_uploads);

// Used together with key-marker. If key-marker is not specified, upload-id-marker will be ignored; otherwise, the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list, and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker.
void SetUploadIdMarker(const std::string& upload_id_marker);
```

ListMultipartUploadResp member functions:

```
// Get the corresponding metadata of an object in a bucket
std::vector<Upload> GetUpload()；
// Bucket name
std::string GetName()；
// Encoding format
std::string GetEncodingType() const；
// By default, entries are listed in UTF-8 binary order starting from the marker
std::string GetMarker() const；
// The entry list starts from this UploadId value
std::string GetUploadIdMarker() const；
// If the returned entries are truncated, then NextKeyMarker is the starting point of the next entry
std::string GetNextKeyMarker() const；
// If the returned entries are truncated, then UploadId is the starting point of the next entry
std::string GetNextUploadIdMarker() const；
// Set the maximum number of multiparts returned, valid values are between 0 and 1,000
std::string GetMaxUploads () const；
// Whether response request entries are truncated, is a boolean value (true or false)
bool IsTruncated()；
// Returned file prefix
std::string GetPrefix() const；
// Get the delimiter 
std::string GetDelimiter() const；
// Identical paths between a specified prefix and the delimiter are grouped into one class and defined as common prefix
std::vector<std::string> GetCommonPrefixes() const
```

### Uploading an object in parts

With multipart upload, you can do the following:

- Upload an object in parts, including initializing a multipart upload, uploading parts, and completing the upload of all parts.
- Delete uploaded parts.

### Initializing a multipart upload

#### Feature description

This API (Initiate Multipart Upload) is used to initialize a multipart upload and get the corresponding `uploadId`.

#### Method prototype

```cpp
CosResult InitMultiUpload(const InitMultiUploadReq& req, InitMultiUploadResp* resp)
```

#### Sample request

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

#### Parameter description

| Parameter | Description |
| ---- | ----------------------------------------------- |
| req  | InitMultiUploadReq, the request for the InitMultiUpload operation |
| resp | InitMultiUploadResp, the return of the InitMultiUpload operation |

The InitMultiUploadReq member functions are as follows:

```
// Cache-Control: cache policy as defined in RFC 2616, will be stored as object metadata
void SetCacheControl(const std::string& str);

// Content-Disposition: filename as defined in RFC 2616, will be stored as object metadata
void SetContentDisposition(const std::string& str);

// Content-Encoding: encoding format as defined in RFC 2616, will be stored as object metadata
void SetContentEncoding(const std::string& str);

// Content-Type: content type (MIME) as defined in RFC 2616, will be stored as object metadata
void SetContentType(const std::string& str);

// Expires: file expiration time as defined in RFC 2616, will be stored as object metadata
void SetExpires(const std::string& str);

// Headers that allow user-customization, will be returned as object metadata of up to 2 KB
void SetXCosMeta(const std::string& key, const std::string& value);

// x-cos-storage-class: sets the storage class of an object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE
// Default value: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Define the ACL attribute of the object. Valid values: private, public-read
// Default value: private
void SetXcosAcl(const std::string& str);

// Grant read permission in the format: x-cos-grant-read: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantRead(const std::string& str);

// Grant read-write permission in the format: x-cos-grant-full-control: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXcosGrantFullControl(const std::string& str);

/// Set the algorithm used for server-side encryption. Currently, AES256 is supported
void SetXCosServerSideEncryption(const std::string& str);

```

After the request is successfully executed, the returned response will include the bucket, key, and uploadId, which represent respectively the destination bucket of the multipart upload, the object name, and the ID number required by subsequent multipart uploads.

The InitMultiUploadResp member functions are as follows:

```cpp
std::string GetBucket();
std::string GetKey();
std::string GetUploadId();

/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption();
```

### <span id = "MULIT_UPLOAD_PART">Uploading parts</span>

This API (Upload Part) is used to upload parts.

#### Method prototype

```cpp
CosResult UploadPartData(const UploadPartDataReq& request, UploadPartDataResp* response)
```

#### Sample request

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
    // Disable MD5 check. To enable, use req.TurnOnComputeConentMd5(). This feature is enabled by default
    req.TurnOffComputeConentMd5();
    qcloud_cos::UploadPartDataResp resp;
    qcloud_cos::CosResult result = cos.UploadPartData(req, &resp);

    // After the upload is successful, you should record the part number and the returned ETag
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

    // After the upload is successful, you should record the part number and the returned ETag 
    if (result.IsSucc()) {
        etags.push_back(resp.GetEtag());
        part_numbers.push_back(2);
    }
    is.close();
}
```

#### Parameter description

| Parameter | Description |
| ---- | --------------------------------------------- |
| req  | UploadPartDataReq, the request for the UploadPartData operation |
| resp | UploadPartDataResp, the return of the UploadPartData operation |

When you construct UploadPartDataReq, you need to specify the request APPID, bucket, object, the UploadId obtained after successful initialization, and the uploaded data stream (which you should close after the call is completed).

```
UploadPartDataReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id,
                    std::istream& in_stream);

```

In addition, you should set the part number for the request, which will also be used when you complete the multipart upload.

```
void SetPartNumber(uint64_t part_number);

```

The UploadPartDataResp member functions are as follows:

```
/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption();

```

### Copying parts

This API is used to copy an object as a part.

#### Method prototype

```cpp
CosResult UploadPartCopyData(const UploadPartCopyDataReq& request,UploadPartCopyDataResp* response)
```

#### Sample request

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

#### Parameter description

| Parameter | Description |
| ---- | ----------------------------------------------------- |
| req  | UploadPartCopyDataReq, the request for the UploadPartCopyData operation |
| resp | UploadPartCopyDataResp, the return of the UploadPartCopyData operation |

```cpp
/// Set the ID of the multipart copy
void SetUploadId(const std::string& upload_id)
/// Set the number of the multipart copy
void SetPartNumber(uint64_t part_number)
/// Set the source file URL path for the multipart copy. A previous version can be specified using the versionid sub-resource
void SetXCosCopySource(const std::string& src)
/// Set the byte range of the source file in the format: bytes=first-last
void SetXCosCopySourceRange(const std::string& range)
 /// If the object has been modified after the specified time, the operation is performed; otherwise, error code 412 is returned
void SetXCosCopySourceIfModifiedSince(const std::string& date)
/// If the object has not been modified after the specified time, the operation is performed; otherwise, error code 412 is returned
void SetXCosCopySourceIfUnmodifiedSince(const std::string& date)
/// If the Etag of the object is the same as the specified one, the operation is performed; otherwise, error code 412 is returned 
void SetXCosCopySourceIfMatch(const std::string& etag)
/// If the Etag of the object is different from the specified one, the operation is performed; otherwise, error code 412 is returned
void SetXCosCopySourceIfNoneMatch(const std::string& etag)
```

```
/// Get the MD5 checksum of the returned file
std::string GetEtag() const
/// Return the time the file was last modified time in GMT time
std::string GetLastModified() const
/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption() const
```

### Querying uploaded parts

#### Feature description

This API is used to query uploaded parts in a specified multipart upload operation.

#### Method prototype

```cpp
CosResult ListParts(const ListPartsReq& req, ListPartsResp* resp)
```

#### Sample request

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

// The call is successful. You can call the resp member functions to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Parameter description

| Parameter | Description |
| ---- | ----------------------------------- |
| req  | ListPartsReq, the request for the ListParts operation |
| resp | ListPartsResp, the return of the ListParts operation |

ListPartsReq contains the following member functions:

```
// Constructor, bucket name, object name, multipart upload ID
ListPartsReq(const std::string& bucket_name,                                                                                                                                      
             const std::string& object_name,
             const std::string& upload_id); 

// \brief Specify the encoding method of the return value
void SetEncodingType(const std::string& encoding_type);

// \brief Maximum number of entries returned at a time; 1,000 will be used as the default value if not set
void SetMaxParts(uint64_t max_parts);

// \brief By default, entries are listed in UTF-8 binary order starting from the marker
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

// ID of the multipart upload
std::string GetUploadId();

// Identify the upload initiator 
Initiator GetInitiator();

// Identify the owner of specified parts
Owner GetOwner();

// By default, entries are listed in UTF-8 binary order starting from the marker
uint64_t GetPartNumberMarker();

// Return the information for each part
std::vector<Part> GetParts();

// If the returned entries are truncated, then NextMarker is the starting point of the next entry
uint64_t GetNextPartNumberMarker();

// Indicate the part storage class. Enumerated values: Standard, Standard_IA, Archive
std::string GetStorageClass();

// Maximum number of entries returned at a time
uint64_t GetMaxParts();

// Whether returned entries are truncated, is a boolean value (TRUE or FALSE)
bool IsTruncated();

```

Part, Owner, and Initiator are defined as follows:

```cpp
struct Initiator {
    std::string m_id; // Creator’s unique ID 
    std::string m_display_name; // Creator's username
};

struct Owner {
    std::string m_id; // User’s unique ID
    std::string m_display_name; // Username
};

struct Part {
    uint64_t m_part_num; // Part number
    uint64_t m_size; // Part size in bytes
    std::string m_etag; // MD5 checksum of the object part
    std::string m_last_modified; // Time the part was last modified 
};

```

### Completing a multipart upload

#### Feature description

The API is used to complete the multipart upload of the entire file.

#### Method prototype

```cpp
CosResult CompleteMultiUpload(const CompleteMultiUploadReq& request, CompleteMultiUploadResp* response)
```

#### Sample request

```cpp
qcloud_cos::CompleteMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::CompleteMultiUploadResp resp;
req.SetEtags(etags);
req.SetPartNumbers(part_numbers);

qcloud_cos::CosResult result = cos.CompleteMultiUpload(req, &resp);
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------------------------------------------- |
| req  | CompleteMultiUploadReq, the request for the CompleteMultiUpload operation |
| resp | CompleteMultiUploadResp, the return of the CompleteMultiUpload operation |

When you construct CompleteMultiUploadReq, you need to specify the request APPID, bucket, object, and the UploadId obtained after successful initialization.

```
CompleteMultiUploadReq(const std::string& bucket_name,
                       const std::string& object_name, const std::string& upload_id)

```

In addition, you need to set the part numbers and Etags of all uploaded parts for the request.

```
// When calling the following method, you should make sure that the order of the part numbers is the same as that of the ETags.
void SetPartNumbers(const std::vector<uint64_t>& part_numbers);
void SetEtags(const std::vector<std::string>& etags) ;

// Add a pair consisting of a part_number and an ETag
void AddPartEtagPair(uint64_t part_number, const std::string& etag);

/// Set the algorithm used for server-side encryption. Currently, AES256 is supported
void SetXCosServerSideEncryption(const std::string& str);
```

The return contents of CompleteMultiUploadResp include Location, Bucket, Key, and ETag, which represent respectively the public network access domain name of the created object, the destination bucket for the multipart upload, the name of the object, and the MD5 checksum of the merged file. The following member functions can be called to access the contents of the response.

```
std::string GetLocation();
std::string GetKey();
std::string GetBucket();
std::string GetEtag();

/// Algorithm used for server-side encryption
std::string GetXCosServerSideEncryption();

```

### Aborting a multipart upload

#### Feature description

This API is used to abort a multipart upload operation and delete the uploaded parts.

#### Method prototype

```cpp
CosResult AbortMultiUpload(const AbortMultiUploadReq& request, AbortMultiUploadResp* response)
```

#### Sample request

```cpp
qcloud_cos::AbortMultiUploadReq req(bucket_name, object_name, upload_id);
qcloud_cos::AbortMultiUploadResp resp;
qcloud_cos::CosResult result = cos.AbortMultiUpload(req, &resp);
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------------------------------------- |
| req  | AbortMultiUploadReq, the request for the AbortMultiUpload operation |
| resp | AbortMultiUploadResp, the return of the AbortMultiUpload operation |

When you construct AbortMultiUploadReq, you need to specify the bucket, object, and Upload_id.

```cpp
AbortMultiUploadReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id);
```

// The download is successful. You can call the MultiGetObjectResp member functions

## Other Operations

### Restoring an archived object 

#### Feature description

This API is used to retrieve an archived object for access.

#### Method prototype

```cpp
CosResult PostObjectRestore(const PostObjectRestoreReq& req, PostObjectRestoreResp* resp)
```

#### Sample request

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
    // The call is successful. You can call the resp member functions to get the return content
    if (result.IsSucc()) {
        // ...
    } else {
        // You can call the CosResult member functions to output the error information, such as requestID
    } 
}   
```

#### Parameter description

| Parameter | Description |
| ---- | ---------------------------------------------------- |
| req  | PostObjectRestoreReq, the request for the PostObjectRestore operation |
| resp | PostObjectRestoreResp, the return of the PostObjectRestore operation |

PostObjectRestoreReq contains the following member functions:

```
// Set expiration time of the temporary copy
void SetExiryDays(uint64_t days);

// Enumerated values: Expedited, Standard, Bulk. Default value: Standard
void SetTier(const std::string& tier);
```

### Setting object ACL

#### Feature description

This API is used to set the ACL for an object.

#### Method prototype

```cpp
CosResult PutObjectACL(const PutObjectACLReq& req, PutObjectACLResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "sevenyou";

// 1. Set the ACL configuration (through the body. You can set the ACL through either the body or header, but you may only use one of these two methods; otherwise, a conflict will occur)
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
    // The call is successful. You can call the resp member functions to get the return content
    if (result.IsSucc()) {
        // ...
    } else {
        // Set the ACL. You can call the CosResult member functions to output the error information, such as requestID
    } 
}   

// 2. Set the ACL configuration (through the header. You can set the ACL through either the body or header, but you may only use one of these two methods; otherwise, a conflict will occur)
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);                                                                                                                    
    req.SetXCosAcl("public-read-write");

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    // The call is successful. You can call the resp member functions to get the return content
    if (result.IsSucc()) {
        // ...
    } else {
        // You can call the CosResult member functions to output the error information, such as requestID
    } 
}   
```



#### Parameter description

| Parameter | Description |
| ---- | ----------------------------------------- |
| req  | PutObjectACLReq, the request for the PutObjectACL operation |
| resp | PutObjectACLResp, the return of the PutObjectACL operation |

PutObjectACLReq contains the following member functions:

```
// Define the ACL attribute of the object. Valid values: private, public-read
// Default value: private
void SetXCosAcl(const std::string& str);

// Grant read permission in the format: id="[OwnerUin]" 
void SetXCosGrantRead(const std::string& str);

// Grant full permission in the format: id="[OwnerUin]"
void SetXCosGrantFullControl(const std::string& str);

// Object owner ID
void SetOwner(const Owner& owner);

// Set grantee and permission information
void SetAccessControlList(const std::vector<Grant>& grants);

// Add the permission information for a single object
void AddAccessControlList(const Grant& grant);
        

```

>APIs such as `SetXCosAcl/SetXCosGrantRead/SetXCosGrantWrite/SetXCosGrantFullControl` cannot be used together with `SetAccessControlList/AddAccessControlList` at the same time. Because the former type is implemented by setting the HTTP header, while the latter is used for adding content in XML format to the body, you can only choose one type. The former type is preferred within the SDK.

ACLRule is defined as follows:

```
struct Grantee {
    // The type can be RootAccount or SubAccount
    // If the type is RootAccount, you can enter an account ID in the uin field or enter "anyone" (representing all types of users) in place of uin/<OwnerUin> and uin/<SubUin>
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

### Querying an object ACL

#### Feature description

This API is used to query the ACL of an object.

#### Method prototype

```cpp
CosResult GetObjectACL(const GetObjectACLReq& req, GetObjectACLResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";

// The constructor of GetObjectACLReq requires Object_name to be passed in
qcloud_cos::GetObjectACLReq req(bucket_name, object_name);
qcloud_cos::GetObjectACLResp resp;
qcloud_cos::CosResult result = cos.GetObjectACL(req, &resp);

// The call is successful. You can call the resp member functions to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Parameter description

| Parameter | Description |
| ---- | ----------------------------------------- |
| req  | GetObjectACLReq, the request for the GetObjectACL operation |
| resp | GetObjectACLResp, the return of the GetObjectACL operation |

GetObjectACLResp contains the following member functions:

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();
```

## Advanced API (Recommended)

### Composite upload

#### Feature description

This API is used to upload a file concurrently by encapsulating various APIs of a multipart upload.

#### Method prototype

```cpp
CosResult MultiUploadObject(const MultiUploadObjectReq& request, MultiUploadObjectResp* response)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";
std::string local_file = "./test"

qcloud_cos::MultiUploadObjectReq req(bucket_name, object_name, local_file);
// To keep the chunks alive inside the completion API, we recommend setting a longer timeout period.
req.SetRecvTimeoutInms(1000 * 60);
qcloud_cos::MultiUploadObjectResp resp;
qcloud_cos::CosResult result = cos.MultiUploadObject(req, &resp);

// The call is successful. You can call the resp member functions to get the return content
if (result.IsSucc()) {
    // ...
} else {
	// You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Parameter description

| Parameter | Description |
| ---- | --------------------------------------------------- |
| req  | MultiUploadObjectReq, the request for the MultiUploadObject operation |
| resp | MultiUploadObjectResp, the return of the MultiUploadObject operation |

MultiUploadObjectReq contains the following member functions:

```cpp
// Set the part size. If it is less than 1 MB, it will be calculated as 1 MB. If it is greater than 5 GB, it will be calculated as 5 GB
void SetPartSize(uint64_t bytes)
// Headers that allow user-customization, will be returned as object metadata of up to 2 KB 
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

### Composite download

#### Feature description

This API is used to download a file using concurrent ranges.

#### Method prototype

```cpp
CosResult GetObject(const MultiGetObjectReq& request, 
MultiGetObjectResp* response)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";
std::string file_path = "./test";

qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, file_path);   qcloud_cos::MultiGetObjectResp resp;                                     qcloud_cos::CosResult result = cos.GetObject(req, &resp); 

// The call is successful. You can call the resp member functions to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Parameter description

| Parameter | Description |
| ---- | ---------------------------------------- |
| req  | MultiGetObjectReq, the request for the GetObject operation |
| resp | MultiGetObjectResp, the return of the GetObject operation |

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
