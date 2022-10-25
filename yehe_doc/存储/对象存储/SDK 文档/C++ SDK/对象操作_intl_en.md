## Overview

This document provides an overview of APIs and SDK code samples related to simple operations, multipart operations, and other object operations.

### Simple operations

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket. |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object in whole | Uploads an object in whole to a bucket. |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object to the local file system. |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to a destination path. |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes a specified object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket. |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |

### Multipart operations

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in parts. |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | Copying a part | Copies an object as a part. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |

## Simple Operations

### Querying objects

#### Description

This API is used to query some or all the objects in a bucket.

#### Method prototype

```cpp
CosResult GetBucket(const GetBucketReq& req, GetBucketResp* resp)
```

#### Sample request 1: Listing objects in a directory

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.

qcloud_cos::GetBucketReq req(bucket_name);
req.SetPrefix("image/"); // List objects in the `image/` directory
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);

// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
   std::vector<Content> contents = get_bucket_resp.GetContents();
   // Traverse the listed objects
   for (auto &content: contents) {
     // do something
   }
} else {
    std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
    std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
    std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
    std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
    std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
    std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
} 
```

#### Sample request 2: Listing all objects in a bucket

```cpp
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    // 1. Specify the path to the configuration file and initialize CosConfig
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    // 2. Construct a request to query the object list
    std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
    qcloud_cos::GetBucketReq req(bucket_name);
    qcloud_cos::CosResult result;   
	bool is_truncated = false;

    // 3. Traverse all objects
    do {
    	qcloud_cos::GetBucketResp resp;
        result = cos.GetBucket(req, &resp);
        if (result.IsSucc()) {
            std::vector<Content> contents = get_bucket_resp.GetContents();
            for (auto &content: contents) {
            	// do something
            }
            req.SetMarker(resp.GetNextMarker()); // Set the start key for the next listing
            is_truncated = resp.IsTruncated();
        }
    } while (result.IsSucc() && is_truncated);
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | --------------------| --------------| ------|
| req  | Request of the `GetBucket` operation | GetBucketReq | Yes |
| resp | Response of the `GetBucket` operation | GetBucketResp | Yes |

`GetBucketReq` provides the following member functions: 

```cpp
/// \@brief Set a prefix, specifying the addresses of the returned files
void SetPrefix(const std::string& prefix);
/// \brief Set a delimiter, specifying that paths that start with the specified prefix and end with the first occurrence of the delimiter will be returned
void SetDelimiter(const std::string& delimiter);
/// \brief Encoding type of returned values. Valid value: `url`
void SetEncodingType(const std::string& encoding_type);
/// \brief By default, entries are listed in UTF-8 binary order. The list starts after the marker.
void SetMarker(const std::string& marker);
/// \brief Maximum number of entries returned at a time. Default: 1000
void SetMaxKeys(uint64_t max_keys);
```

`GetBucketResp` provides the following member functions: 

```cpp
/// \brief Get the metadata of an object in a bucket.
std::vector<Content> GetContents() const;
/// \brief Bucket name
std::string GetName() const;
/// \brief Get the delimiter.
std::string GetDelimiter() const;
/// \brief Encoding format
std::string GetEncodingType() const;
/// \brief Prefix of the returned file
std::string GetPrefix() const;
/// \brief By default, entries are listed in UTF-8 binary order. The list starts after the marker.
std::string GetMarker() const;
/// \brief Maximum number of entries returned in a single response
uint64_t GetMaxKeys() const;
// \brief Whether the returned list is truncated. The parameter is a boolean (true or false).
bool IsTruncated() const;
// \brief If the returned list is truncated, "NextMarker" represents the object after which the next returned list begins.
std::string GetNextMarker() const;
```

`Content` is defined as follows:

```
struct Content {
    std::string m_key; // Key of the object
    std::string m_last_modified; // Time when the object was last modified
    std::string m_etag; // MD5 checksum of the file
    std::string m_size; // File size, in bytes
    std::vector<std::string> m_owner_ids; // Information about the bucket owner
    std::string m_storage_class; // Storage class of the object. Enumerated values: STANDARD, STANDARD_IA
};
```

### Uploading an object in whole

#### Description

This API is used to upload an object to a specified bucket.

#### Method prototype

```cpp
/// Upload using a stream.
CosResult PutObject(const PutObjectByStreamReq& req, PutObjectByStreamResp* resp)

/// Upload a local file.
CosResult PutObject(const PutObjectByFileReq& req, PutObjectByFileResp* resp)
```

#### Sample request 1: Stream upload

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "object_name";
std::istringstream iss("put object");
// istream is required in the request constructor.
qcloud_cos::PutObjectByStreamReq req(bucket_name, object_name, iss);
// Call the Set method to set metadata, ACL, etc.
req.SetXCosStorageClass("STANDARD_IA");
// Disable MD5 checksum. To enable it, use "req.TurnOnComputeConentMd5()". MD5 checksum is enabled by default.
req.TurnOffComputeConentMd5();
qcloud_cos::PutObjectByStreamResp resp;
qcloud_cos::CosResult result = cos.PutObject(req, &resp);

if (result.IsSucc()) {
    // The call is successful. You can call the resp member functions to get the return content.
} else {
    // The call failed. You can call the result member functions to get the error information.
    std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
    std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
    std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
    std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
    std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
    std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
}
```

#### Sample request 2: Uploading a file

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "object_name";
// The local file path is required in the request constructor.
qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
// Call the Set method to set metadata, ACL, etc.
req.SetXCosStorageClass("STANDARD_IA");
// Disable MD5 checksum. To enable it, use "req.TurnOnComputeConentMd5()". MD5 checksum is enabled by default.
req.TurnOffComputeConentMd5();
qcloud_cos::PutObjectByFileResp resp;
qcloud_cos::CosResult result = cos.PutObject(req, &resp);
if (result.IsSucc()) {
    // The call is successful. You can call the resp member functions to get the return content.
} else {
    // The call failed. You can call the result member functions to get the error information.
    std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
    std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
    std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
    std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
    std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
    std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
}
```

#### Sample 3: limiting the upload speed

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "object_name";
// The local file path is required in the request constructor.
qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
// The speed range is 819200 to 838860800 (in bit/s), that is, 100 KB/s to 100 MB/s.
req.SetTrafficLimitByHeader(1048576);
qcloud_cos::PutObjectByFileResp resp;
qcloud_cos::CosResult result = cos.PutObject(req, &resp);
if (result.IsSucc()) {
    // The call is successful. You can call the resp member functions to get the return content.
} else {
    // The call failed. You can call the result member functions to get the error information.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | --------------------| -----------------------------------------| ------|
| req  | Request of the `PutObject` operation | PutObjectByStreamReq/PutObjectByFileReq | Yes |
| resp | Response of the `PutObject` operation | PutObjectByStreamResp/PutObjectByFileResp | Yes |


The `req` parameter contains the following member functions:

```cpp
// Cache-Control: cache policy defined in RFC 2616, which is saved as object metadata
void SetCacheControl(const std::string& str);

// Content-Disposition: filename defined in RFC 2616, which is stored as object metadata
void SetContentDisposition(const std::string& str);

// Content-Encoding: encoding format defined in RFC 2616, which is stored as object metadata
void SetContentEncoding(const std::string& str);

// Content-Type: content type (MIME) defined in RFC 2616, which is stored as object metadata
void SetContentType(const std::string& str);

// Expect: If `Expect: 100-continue` is used, the requested content will be sent only after confirmation from the server is received.
void SetExpect(const std::string& str);

// Expires: expiration time defined in RFC 2616, which is stored as object metadata
void SetExpires(const std::string& str);

// Customizable headers, which will be returned as object metadata of up to 2 KB
void SetXCosMeta(const std::string& key, const std::string& value);

// x-cos-storage-class: the storage class of an object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE
// Default: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Define the ACL attribute of the object. Valid values: private, public-read
// Default: private
void SetXcosAcl(const std::string& str);

// Grant read permission in the format of x-cos-grant-read: id=" ",id=" ".
// To authorize a sub-account, use id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>".
// To authorize the root account, use id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>".
void SetXcosGrantRead(const std::string& str);

// Grant read-write permission in the format of x-cos-grant-full-control: id=" ",id=" ".
// To authorize a sub-account, use id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>".
// To authorize the root account, use id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>".
void SetXcosGrantFullControl(const std::string& str);

/// Set the algorithm for server-side encryption. Currently, AES-256 is supported.
void SetXCosServerSideEncryption(const std::string& str);
```

The `resp` parameter contains the following member functions:

```C++
/// Get the object’s version number. If versioning is not enabled for the bucket, an empty string will be returned.
std::string GetVersionId();

/// Get the algorithm for server-side encryption.
std::string GetXCosServerSideEncryption();
```

### Querying object metadata

#### Description

This API is used to query the metadata of an object.

#### Method prototype

```cpp
CosResult HeadObject(const HeadObjectReq& req, HeadObjectResp* resp)
```


#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "object_name";
qcloud_cos::HeadObjectReq req(bucket_name, object_name);
qcloud_cos::HeadObjectResp resp;
qcloud_cos::CosResult result = cos.HeadObject(req, &resp);
if (result.IsSucc()) {
    // The query is successful. You can call the HeadObjectResp member functions.
} else {
    // The query failed. You can call the CosResult member functions to get the error information, such as requestID.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ---------------------| --------------| ------|
| req  | Request of the `HeadObject` operation | HeadObjectReq | Yes |
| resp | Response of the `HeadObject` operation | HeadObjectResp | Yes |


In addition to member functions that read common headers, `HeadObjectResp` provides the following member functions:

```cpp
std::string GetXCosObjectType();

std::string GetXCosStorageClass();

// Get the custom metadata. The parameter can be the asterisk (*) in "x-cos-meta-*".
std::string GetXCosMeta(const std::string& key);

// Return all custom meta in the form of a map. The key of a map does not contain the "x-cos-meta-" prefix.
std::map<std::string, std::string> GetXCosMetas();

// Get the server-side encryption algorithm
std::string GetXCosServerSideEncryption(); 
```

### Downloading an object

#### Description

This API is used to download an object to the local file system.

#### Method prototype

```cpp
// Download the object to a local file
CosResult GetObject(const GetObjectByFileReq& req, GetObjectByFileResp* resp)

// Download the object to a stream
CosResult GetObject(const GetObjectByStreamReq& req, GetObjectByStreamResp* resp)

// Download the object to a local file (multi-threaded)
CosResult GetObject(const MultiGetObjectReq& req, MultiGetObjectResp* resp)
```

#### Sample request 1: Downloading an object to a local file

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "object_name";
std::string local_path = "/tmp/object_name";

// appid, bucketname, object, and a local path (including filename) are required for the request.
qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
qcloud_cos::GetObjectByFileResp resp;
qcloud_cos::CosResult result = cos.GetObject(req, &resp);
if (result.IsSucc()) {
    // The download is successful. You can call the GetObjectByFileResp member functions.
} else {
    // You can call the CosResult member functions to get the error information, such as requestID.
}
```

#### Sample request 2: Downloading an object to a stream

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "object_name";
std::string local_path = "/tmp/object_name";
// appid, bucketname, object, and output stream are required for the request.
std::ostringstream os;
qcloud_cos::GetObjectByStreamReq req(bucket_name, object_name, os);
qcloud_cos::GetObjectByStreamResp resp;
qcloud_cos::CosResult result = cos.GetObject(req, &resp);
if (result.IsSucc()) {
    // The download is successful. You can call the GetObjectByStreamResp member functions.
} else {
    // The download failed. You can call the CosResult member functions to get the error information, such as requestID.
}
```

#### Sample request 3: Downloading an object to a local file via multiple threads

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "object_name";
std::string local_path = "/tmp/object_name";

// appid, bucketname, object, and local path (including the filename) are required for the request
qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, local_path);
qcloud_cos::MultiGetObjectResp resp;
qcloud_cos::CosResult result = cos.GetObject(req, &resp);
if (result.IsSucc()) {
    // The download is successful. You can call the MultiGetObjectResp member functions.
} else {
    // The download failed. You can call the CosResult member functions to get the error information, such as requestID.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | --------------------| -------------------------------------------------------------| ------|
| req  | Request of the `GetObject` operation | GetObjectByFileReq/GetObjectByStreamReq/MultiGetObjectReq | Yes |
| resp | Response of the `GetObject` operation | GetObjectByFileResp/GetObjectByStreamResp/MultiGetObjectResp | Yes |



The member functions are as follows:

```
// Set the Content-Type parameter in the response header.
void SetResponseContentType(const std::string& str);

// Set the Content-Language parameter in the response header.
void SetResponseContentLang(const std::string& str);

// Set the Content-Expires parameter in the response header.
void SetResponseExpires(const std::string& str);

// Set the Cache-Control parameter in the response header.
void SetResponseCacheControl(const std::string& str);

// Set the Content-Disposition parameter in the response header.
void SetResponseContentDisposition(const std::string& str);

// Set the Content-Encoding parameter in the response header.
void SetResponseContentEncoding(const std::string& str);

```

In addition to member functions that read common headers, `GetObjectResp` provides the following member functions:

```cpp
// Get the time an object was last modified, a date in string format, such as "Wed, 28 Oct 2014 20:30:00 GMT"
std::string GetLastModified();

// Obtain the object type, which indicates whether the object is appendable. Enumerated values: normal, appendable
std::string GetXCosObjectType();

// Obtain the storage class of the object. Enumerated values: STANDARD, STANDARD_IA
std::string GetXCosStorageClass();

// Return all custom meta in the form of a map. The key of a map does not contain the "x-cos-meta-" prefix.
std::map<std::string, std::string> GetXCosMetas();

// Get the custom metadata. The parameter can be the asterisk (*) in "x-cos-meta-*".
std::string GetXCosMeta(const std::string& key);

// Get the server-side encryption algorithm.
std::string GetXCosServerSideEncryption(); 
```

### Copying objects

This API (`PUT Object - Copy`) is used to copy a file to the destination path.

#### Method prototype

```cpp
CosResult PutObjectCopy(const PutObjectCopyReq& req, PutObjectCopyResp* resp)
```

#### Sample 1. Copying an object

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "sevenyou";
qcloud_cos::PutObjectCopyReq req(bucket_name, object_name);                                         
req.SetXCosCopySource("sevenyousouthtest-12345656.cn-south.myqcloud.com/sevenyou_source_obj");
qcloud_cos::PutObjectCopyResp resp;
qcloud_cos::CosResult result = cos.PutObjectCopy(req, &resp);
```

#### Sample request 2: Modifying object metadata

```cpp
qcloud_cos::PutObjectCopyReq req(bucket_name, object_name);
req.SetXCosMeta("key1", "val1"); // Custom metadata
req.SetXCosMeta("key2", "val2"); // Custom metadata
req.SetXCosMetadataDirective("Replaced"); // This line must be added
qcloud_cos::PutObjectCopyResp resp;
qcloud_cos::CosResult result = cos.PutObjectCopy(req, &resp);
```

#### Sample 3: modifying storage class

```cpp
qcloud_cos::PutObjectCopyReq req(bucket_name, object_name);
req.SetXCosStorageClass("STANDARD_IA");
req.SetXCosMetadataDirective("Replaced"); // This line must be added
qcloud_cos::PutObjectCopyResp resp;
qcloud_cos::CosResult result = cos.PutObjectCopy(req, &resp);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------| ------------------| ------|
| req  | Request of the `PutObjectCopy` operation | PutObjectCopyReq | Yes |
| resp | Response of the `PutObjectCopy` operation | PutObjectCopyResp | Yes |


`PutObjectCopyReq` contains the following member functions:

```
// URL path of the source file. A previous version can be specified by using the `versionid` subresource.
void SetXCosCopySource(const std::string& str);

// Whether to copy the metadata. Enumerated values: Copy (default), Replaced
// If this field is set to "Copy", the user-defined metadata in the header will be ignored and the metadata will be copied directly.
// If this field is set to "Replaced", the metadata will be modified based on the header information.
// If the destination path and the source path are the same (that is, the user attempts to modify the metadata), set this field to "Replaced".
void SetXCosMetadataDirective(const std::string& str);

// If the object has been modified after the specified time, the operation is performed; otherwise, error code 412 is returned.
// It can be used together with "x-cos-copy-source-If-None-Match". Using it together with other conditions can cause a conflict.
void SetXCosCopySourceIfModifiedSince(const std::string& str);

// If the object has not been modified after the specified time, the operation is performed; otherwise, error code 412 is returned.
// It can be used together with "x-cos-copy-source-If-Match". Using it together with other conditions can cause a conflict.
void SetXCosCopySourceIfUnmodifiedSince(const std::string& str);

// If the Etag of the object is the same as the specified one, the operation is performed; otherwise, error code 412 is returned.
// It can be used together with "x-cos-copy-source-If-Unmodified-Since". Using it together with other conditions can cause a conflict.
void SetXCosCopySourceIfMatch(const std::string& str);

// If the Etag of the object is different from the specified one, the operation is performed; otherwise, error code 412 is returned.
// It can be used together with "x-cos-copy-source-If-Modified-Since". Using it together with other conditions can cause a conflict.
void SetXCosCopySourceIfNoneMatch(const std::string& str);

// x-cos-storage-class: the storage class of an object. Enumerated values: STANDARD, STANDARD_IA
// Default: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Define the ACL attribute of the object. Valid values: private, public-read
// Default: private
void SetXCosAcl(const std::string& str);

// Grant read permission in the format of id="[OwnerUin]".  
void SetXCosGrantRead(const std::string& str);

// Grant full permission in the format of id="[OwnerUin]".
void SetXCosGrantFullControl(const std::string& str);

// Customizable headers, which will be returned as object metadata of up to 2 KB
void SetXCosMeta(const std::string& key, const std::string& value);

/// Set the algorithm for server-side encryption. Currently, AES-256 is supported.
void SetXCosServerSideEncryption(const std::string& str);

```

`PutObjectCopyResp` contains the following member functions:

```
// Return the MD5 checksum of the file. The value of ETag can be used to check whether the object content has changed.
std::string GetEtag();

// Return the time the file was last modified, in GMT.
std::string GetLastModified();

// Return the version ID.
std::string GetVersionId();

/// Get the algorithm for server-side encryption.
std::string GetXCosServerSideEncryption();

```

### Deleting an object

#### Description

This API is used to delete a specified object from a bucket.

#### Method prototype

```cpp
CosResult DeleteObject(const DeleteObjectReq& req, DeleteObjectResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "test_object";

qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
qcloud_cos::DeleteObjectResp resp;
qcloud_cos::CosResult result = cos.DeleteObject(req, &resp);

// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to get the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -------------------- --| ------------------| ------|
| req  | Request of the `DeleteObject` operation | DeleteObjectReq | Yes |
| resp | Response of the `DeleteObject` operation | DeletObjectResp | Yes |


### Deleting multiple objects

#### Description

This API is used to delete multiple objects from a bucket.

#### Method prototype

```cpp
CosResult DeleteObjects(const DeleteObjectsReq& req, DeleteObjectsResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.

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
qcloud_cos::DeleteObjectsReq req(bucket_name, to_be_deleted);  
qcloud_cos::DeleteObjectsResp resp;                 
qcloud_cos::CosResult result = cos.DeleteObjects(req, &resp);
// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to get the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------| ------------------| ------|
| req  | Request of the `DeleteObjects` operation | DeleteObjectsReq | Yes |
| resp | Response of the `DeleteObjects` operation | DeletObjectsResp | Yes |


`DeleteObjectsReq` contains the following member functions:

```cpp
// Add an object and specify the version.
void AddObjectVersion(const std::string& object, const std::string& version)
// Add an object with no versioning information.
void AddObject(const std::string& object)
```

`DeleteObjectsResp` contains the following member functions:

```cpp
// Get the information of successfully deleted objects.
std::vector<DeletedInfo> GetDeletedInfos() const

// Get the information of objects that failed to be deleted.
std::vector<ErrorInfo> GetErrorMsgs() const
```

The structures of `DeletedInfo` and `ErrorInfo` are as follows:

```
struct DeletedInfo{
    std::string m_key; // object key
    std::string m_version_id; //version_id
    bool m_delete_marker; // is delete marker
    std::string m_delete_marker_version_id; // if delete marker, so version id
}
struct ErrorInfo{
    std::string m_key; // object key
    std::string m_code; // error code
    std::string m_message; // error message
    std::string m_version_id; // version id
}
```


### Restoring an archived object 

#### Description

This API is used to restore an archived object for access.

#### Method prototype

```cpp
CosResult PostObjectRestore(const PostObjectRestoreReq& req, PostObjectRestoreResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "sevenyou";

{   
    qcloud_cos::PostObjectRestoreReq req(bucket_name, object_name);
    req.SetExiryDays(30);
    req.SetTier("Standard");
    qcloud_cos::PostObjectRestoreResp resp;
    qcloud_cos::CosResult result = cos.PostObjectRestore(req, &resp);
    // The call is successful. You can call the resp member functions to get the return content.
    if (result.IsSucc()) {
        // ...
    } else {
        // You can call the CosResult member functions to get the error information, such as requestID.
    } 
}   
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ----------------------------| ---------------------| ------|
| req  | Request of the `PostObjectRestore` operation | PostObjectRestoreReq | Yes |
| resp | Response of the `PostObjectRestore` operation | PostObjectRestoreResp | Yes |


`PostObjectRestoreReq` contains the following member functions:

```
// Set the expiration time of the temporary copy.
void SetExiryDays(uint64_t days);

// Enumerated values: Expedited, Standard (default), Bulk
void SetTier(const std::string& tier);
```

## Multipart Upload Operations

Multipart operations include:

- Uploading an object in parts: initializing a multipart upload, uploading parts, and completing a multipart upload
- Deleting uploaded parts


### Querying multipart uploads

#### Description

This API (`List Multipart Uploads`) is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

```cpp
CosResult CosAPI::ListMultipartUpload(const ListMultipartUploadReq& request, ListMultipartUploadResp* response)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "test_object";

qcloud_cos::ListMultipartUploadReq req(bucket_name, object_name);
qcloud_cos::ListMultipartUploadResp resp;
qcloud_cos::CosResult result = cos.ListMultipartUpload(req, &resp);

for (std::vector<qcloud_cos::Upload>::const_iterator itr = rst.begin(); itr != rst.end(); ++itr) {
    const qcloud_cos::Upload& upload = *itr;
    std::cout << "key = " << upload.m_key << ", uploadid= " << upload.m_uploadid << ", storagen class = " << upload.m_storage_class << ", m_initiated= " << upload.m_initiated << std::endl;
}   

// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to get the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------------| -----------------------| ------|
| req  | Request of the `ListMultipartUpload` operation | ListMultipartUploadReq | Yes |
| resp | Response of the `ListMultipartUpload` operation | ListMultipartUploadResp | Yes |


`ListMultipartUploadReq` contains the following member functions:

```
// Specify the prefix that the returned object keys must have. Note that when you query by prefix, the returned keys will contain the prefix.
void SetPrefix(const std::string& prefix);

// Set the delimiter. Objects with identical strings between the specified prefix and the first occurrence of the delimiter are grouped together and defined as common prefixes. If there is no prefix, the string between the start of the path and the first delimiter is compared.
void SetDelimiter(const std::string& delimiter);

// Specify the encoding format for the returned value. Valid value: url
void SetEncodingType(const std::string& encoding_type);

// This field is used together with "upload-id-marker". If "upload-id-marker" is not specified, multipart uploads whose "ObjectName" is lexicographically greater than "key-marker" will be listed. If "upload-id-marker" is specified, multipart uploads whose "ObjectName" is lexicographically greater than "key-marker" will be listed, and multipart uploads whose "ObjectName" is lexicographically equal to "key-marker" with "UploadID" greater than "upload-id-marker" will be listed.
void SetKeyMarker(const std::string& marker);

// Set the maximum number of parts to return. Value range: 1-1000 (default: 1000)
void SetMaxUploads(const std::string& max_uploads);

// This field is used together with "key-marker". If "key-marker" is not specified, "upload-id-marker" will be ignored. If "key-marker" is specified, multipart uploads whose "ObjectName" is lexicographically greater than "key-marker" will be listed, and multipart uploads whose "ObjectName" is lexicographically equal to "key-marker" with "UploadID" greater than "upload-id-marker" will be listed.
void SetUploadIdMarker(const std::string& upload_id_marker);
```

`ListMultipartUploadResp` contains the following member functions:

```
// Get the metadata of an object in a bucket.
std::vector<Upload> GetUpload();
// Bucket name
std::string GetName();
// Encoding format
std::string GetEncodingType() const;
// By default, entries are listed in UTF-8 binary order. The list starts after the marker.
std::string GetMarker() const;
// The entry list starts after UploadId.
std::string GetUploadIdMarker() const;
// If the returned list is truncated, "NextKeyMarker" represents the key after which the next returned list begins.
std::string GetNextKeyMarker() const;
// If the returned list is truncated, "UploadId" represents the upload ID after which the next returned list begins.
std::string GetNextUploadIdMarker() const;
// The maximum number of returned parts allowed. Value range: 0-1000
std::string GetMaxUploads () const;
// Whether the returned list is truncated. The parameter is a boolean (true or false).
bool IsTruncated();
// The prefix of returned objects
std::string GetPrefix() const;
// The delimiter 
std::string GetDelimiter() const;
// Objects with identical paths between the specified prefix and the delimiter are grouped together and defined as common prefixes.
std::vector<std::string> GetCommonPrefixes() const
```

### Initializing a multipart upload

#### Description

This API (`Initiate Multipart Upload`) is used to initialize a multipart upload and obtain its `uploadId`.

#### Method prototype

```cpp
CosResult InitMultiUpload(const InitMultiUploadReq& req, InitMultiUploadResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
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


| Parameter | Description | Type | Required |
| ---- | --------------------------| -------------------| ------|
| req  | Request of the `InitMultiUpload` operation | InitMultiUploadReq | Yes |
| resp | Response of the `InitMultiUpload` operation | InitMultiUploadResp | Yes |


The `InitMultiUploadReq` member functions are as follows:

```
// Cache-Control: cache policy defined in RFC 2616, which is saved as object metadata
void SetCacheControl(const std::string& str);

// Content-Disposition: filename defined in RFC 2616, which is stored as object metadata
void SetContentDisposition(const std::string& str);

// Content-Encoding: encoding format defined in RFC 2616, which is stored as object metadata
void SetContentEncoding(const std::string& str);

// Content-Type: content type (MIME) defined in RFC 2616, which is stored as object metadata
void SetContentType(const std::string& str);

// Expires: expiration time defined in RFC 2616, which is stored as object metadata
void SetExpires(const std::string& str);

// Customizable headers, which will be returned as object metadata of up to 2 KB
void SetXCosMeta(const std::string& key, const std::string& value);

// x-cos-storage-class: the storage class of an object. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE
// Default: STANDARD
void SetXCosStorageClass(const std::string& storage_class);

// Define the ACL attribute of the object. Valid values: private, public-read
// Default: private
void SetXcosAcl(const std::string& str);

// Grant read permission in the format of x-cos-grant-read: id=" ",id=" ".
// To authorize a sub-account, use id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>".
// To authorize the root account, use id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>".
void SetXcosGrantRead(const std::string& str);

// Grant read-write permission in the format of x-cos-grant-full-control: id=" ",id=" ".
// To authorize a sub-account, use id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>".
// To authorize the root account, use id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>".
void SetXcosGrantFullControl(const std::string& str);

/// Set the algorithm for server-side encryption. Currently, AES-256 is supported.
void SetXCosServerSideEncryption(const std::string& str);

```

After the request is successfully executed, the returned response will include `bucket`, `key`, and `uploadId`, which represent the destination bucket of the multipart upload, the object name, and the upload ID (required for the subsequent multipart upload) respectively.

The `InitMultiUploadResp` member functions are as follows:

```cpp
std::string GetBucket();
std::string GetKey();
std::string GetUploadId();

// Algorithm for server-side encryption
std::string GetXCosServerSideEncryption();
```

<span id ="MULIT_UPLOAD_PART"></span>
###  Uploading parts 

This API (`Upload Part`) is used to upload parts.

#### Method prototype

```cpp
CosResult UploadPartData(const UploadPartDataReq& request, UploadPartDataResp* response)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "test_object";

// Upload the first part.
{
    std::fstream is("demo_5M.part1");
    qcloud_cos::UploadPartDataReq req(bucket_name, object_name, upload_id, is);
    req.SetPartNumber(1);
    // Disable MD5 checksum. To enable it, use "req.TurnOnComputeConentMd5()". MD5 checksum is enabled by default.
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

// Upload the second part.
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

| Parameter | Description | Type | Required |
| ---- | -------------------------| ------------------| ------|
| req  | Request of the `UploadPartData` operation | UploadPartDataReq | Yes |
| resp | Response of the `UploadPartData` operation | UploadPartDataResp | Yes |


When you construct `UploadPartDataReq`, you need to specify the `APPID`, `bucket`, `object`, `UploadId`, which you can get from the response of initialization, as well as the data stream to upload (which you should close after the call is completed).

```
UploadPartDataReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id,
                    std::istream& in_stream);

```

In addition, the part number, which is required to complete the multipart upload, needs to be set in the request.

```
void SetPartNumber(uint64_t part_number);

```

`UploadPartDataResp` contains the following member function:

```
/// Algorithm for server-side encryption
std::string GetXCosServerSideEncryption();

```

### Copying an object part

This API is used to copy a part of an object.

#### Method prototype

```cpp
CosResult UploadPartCopyData(const UploadPartCopyDataReq& request,UploadPartCopyDataResp* response)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "test_object";

std::string upload_id;
std::vector<uint64_t> numbers;
std::vector<std::string> etags;
std::string etag1 = "", etag2 = "";
InitMultiUpload(cos, bucket_name, object_name, &upload_id);

// First part
qcloud_cos::UploadPartCopyDataReq req(bucket_name, object_name, upload_id, 1);
req.SetXCosCopySource("sevenyousouth-1251668577.cos.ap-guangzhou.myqcloud.com/seven_10G.tmp");
req.SetXCosCopySourceRange("bytes=0-1048576000");
qcloud_cos::UploadPartCopyDataResp resp;
qcloud_cos::CosResult result = cos.UploadPartCopyData(req, &resp);
if (result.IsSucc()) {
    etag1 = resp.GetEtag();
}
numbers.push_back(1);
etags.push_back(etag1);

// Second part
qcloud_cos::UploadPartCopyDataReq req2(bucket_name, object_name, upload_id, 2);                                                       
req2.SetXCosCopySource("sevenyoutest-7319456.cos.cn-north.myqcloud.com/sevenyou_2G_part");
req2.SetXCosCopySourceRange("bytes=1048576000-2097152000");
qcloud_cos::UploadPartCopyDataResp resp2;
qcloud_cos::CosResult result = cos.UploadPartCopyData(req2, &resp2);
if (result.IsSucc()) {
    etag2 = resp2.GetEtag();
}
numbers.push_back(2);
etags.push_back(etag2);

CompleteMultiUpload(cos, bucket_name, object_name, upload_id, etags, numbers);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -----------------------------| ----------------------| ------|
| req  | Request of the `UploadPartCopyData` operation | UploadPartCopyDataReq | Yes |
| resp | Response of the `UploadPartCopyData` operation | UploadPartCopyDataResp | Yes |


```cpp
/// Set the ID of the multipart copy.
void SetUploadId(const std::string& upload_id)
/// Set the part number.
void SetPartNumber(uint64_t part_number)
/// Set the source file URL for the multipart copy. A previous version can be specified using the versionid sub-resource.
void SetXCosCopySource(const std::string& src)
/// Set the byte range of the source file to copy in the format of bytes=first-last.
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
/// Get the MD5 checksum of the returned file.
std::string GetEtag() const
/// Get the time the file was last modified, in GMT.
std::string GetLastModified() const
/// Get the algorithm for server-side encryption.
std::string GetXCosServerSideEncryption() const
```

### Querying uploaded parts

#### Description

This API is used to query the uploaded parts of a specified multipart upload.

#### Method prototype

```cpp
CosResult ListParts(const ListPartsReq& req, ListPartsResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "test_object";

// uploadId is obtained by calling InitMultiUpload.
qcloud_cos::ListPartsReq req(bucket_name, object_name, upload_id);
req.SetMaxParts(1);                                                                                                                                                               
req.SetPartNumberMarker("1");
qcloud_cos::ListPartsResp resp;
qcloud_cos::CosResult result = cos.ListParts(req, &resp);

// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to get the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | --------------------| -------------| ------|
| req  | Request of the `ListParts` operation | ListPartsReq | Yes |
| resp | Response of the `ListParts` operation | ListPartsResp | Yes |



`ListPartsReq` contains the following member functions:

```
// Constructor: bucket name, object name, and multipart upload ID
ListPartsReq(const std::string& bucket_name,                                                                                                                                      
             const std::string& object_name,
             const std::string& upload_id); 

// \brief The encoding format of the returned value
void SetEncodingType(const std::string& encoding_type);

// \brief Maximum number of entries returned at a time. Default: 1000
void SetMaxParts(uint64_t max_parts);

// \brief By default, entries are listed in UTF-8 binary order. The list starts after the marker.
void SetPartNumberMarker(const std::string& part_number_marker);

```

`ListPartsResp` contains the following member functions:

```
// Destination bucket for the multipart upload
std::string GetBucket();

// Encoding format for the returned value
std::string GetEncodingType();

// Object name
std::string GetKey();

// ID of the multipart upload
std::string GetUploadId();

// The upload initiator
Initiator GetInitiator();

// Part owner
Owner GetOwner();

// By default, entries are listed in UTF-8 binary order. The list starts after the marker.
uint64_t GetPartNumberMarker();

// Get the information of each part.
std::vector<Part> GetParts();

// If the returned list is truncated, "NextMarker" represents the object after which the next returned list begins.
uint64_t GetNextPartNumberMarker();

// Storage class of the parts. Enumerated values: Standard, Standard_IA, Archive
std::string GetStorageClass();

// Maximum number of entries that can be returned at a time
uint64_t GetMaxParts();

// Whether the returned list is truncated. It is a boolean (TRUE or FALSE).
bool IsTruncated();

```

`Initiator`, `Owner`, and `Part` are defined as follows:

```cpp
struct Initiator {
    std::string m_id; // Initiator’s unique ID
    std::string m_display_name; // Initiator name
};

struct Owner {
    std::string m_id; // Owner’s unique ID
    std::string m_display_name; // Owner name
};

struct Part {
    uint64_t m_part_num; // Part number
    uint64_t m_size; // Part size, in bytes
    std::string m_etag; // MD5 checksum of the part
    std::string m_last_modified; // Time the part was last modified
};

```

### Completing a multipart upload

#### Description

This API is used to complete the multipart upload of a file.

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

| Parameter | Description | Type | Required |
| ---- | -----------------------------|------------------------| ------|
| req  | Request of the `CompleteMultiUpload` operation | CompleteMultiUploadReq | Yes |
| resp | Response of the `CompleteMultiUpload` operation | CompleteMultiUploadResp | Yes |


When constructing `CompleteMultiUploadReq`, you need to specify `APPID`, `bucket`, `object`, and `UploadId`, which can be obtained from the response of initialization.

```
CompleteMultiUploadReq(const std::string& bucket_name,
                       const std::string& object_name, const std::string& upload_id)

```

In addition, the numbers and ETag values of all the uploaded parts are required for the request.

```
// When calling the following methods, make sure that the part numbers and ETag are listed in the same order.
void SetPartNumbers(const std::vector<uint64_t>& part_numbers);
void SetEtags(const std::vector<std::string>& etags) ;

// Add a part number and ETag.
void AddPartEtagPair(uint64_t part_number, const std::string& etag);

// Set the algorithm for server-side encryption. Currently, AES-256 is supported.
void SetXCosServerSideEncryption(const std::string& str);
```

The response of `CompleteMultiUploadResp` includes `Location`, `Bucket`, `Key`, and `ETag`, which represent the public network access domain name of the created object, the destination bucket for the multipart upload, the name of the object, and the MD5 checksum of the merged file respectively. You can call the following member functions to access the response.

```
std::string GetLocation();
std::string GetKey();
std::string GetBucket();
std::string GetEtag();

// Algorithm for server-side encryption
std::string GetXCosServerSideEncryption();

```

### Aborting a multipart upload

#### Description

This API is used to abort a multipart upload and delete the uploaded parts.

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

| Parameter | Description | Type | Required |
| ---- | ---------------------------|----------------------| ------|
| req  | Request of the `AbortMultiUpload` operation | AbortMultiUploadReq  | Yes |
| resp | Response of the `AbortMultiUpload` operation | AbortMultiUploadResp | Yes |


When constructing `AbortMultiUploadReq`, you need to specify `Bucket`, `Object`, and `Upload_id`.

```cpp
AbortMultiUploadReq(const std::string& bucket_name,
                    const std::string& object_name, const std::string& upload_id);
```

No specific methods provided. You can call the `BaseResp` member functions to get the common header.

## Advanced APIs (Recommended)

### Composite upload

#### Description

This API is used to upload multiple parts concurrently via multiple threads using the multipart upload APIs.

#### Method prototype

```cpp
CosResult MultiUploadObject(const MultiUploadObjectReq& request, MultiUploadObjectResp* response)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "exampleobject";
std::string local_file = "./test"

qcloud_cos::MultiUploadObjectReq req(bucket_name, object_name, local_file);
// To keep the chunks alive inside the completion API, we recommend setting a longer timeout period.
req.SetRecvTimeoutInms(1000 * 60);
qcloud_cos::MultiUploadObjectResp resp;
qcloud_cos::CosResult result = cos.MultiUploadObject(req, &resp);

// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to get the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ----------------------------|-----------------------| ------|
| req  | Request of the `MultiUploadObject` operation | MultiUploadObjectReq  | Yes |
| resp | Response of the `MultiUploadObject` operation | MultiUploadObjectResp | Yes |


`MultiUploadObjectReq` contains the following member functions:

```cpp
// Set the part size. If it is set to less than 1 MB, 1 MB will be used. If it is set to greater than 5 GB, 5 GB will be used.
void SetPartSize(uint64_t bytes)
// Customizable headers, which will be returned as object metadata of up to 2 KB 
void SetXCosMeta(const std::string& key, const std::string& value)
// Set the algorithm for server-side encryption. Currently, AES-256 is supported.
void SetXCosServerSideEncryption(const std::string& str)
// Set the internal thread pool size.
void SetThreadPoolSize(int size)
```

`MultiUploadObjectResp` contains the following member functions:

```
std::string GetRespTag()
/// Algorithm for server-side encryption 
std::string GetXCosServerSideEncryption() const
```

### Composite download

#### Description

This API is used to download multiple ranges concurrently via multiple threads.

#### Method prototype

```cpp
CosResult GetObject(const MultiGetObjectReq& request, MultiGetObjectResp* response)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "exampleobject";
std::string file_path = "./test";

qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, file_path);  
qcloud_cos::MultiGetObjectResp resp;                                    
qcloud_cos::CosResult result = cos.GetObject(req, &resp); 

// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to get the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -------------------------|--------------------| ------|
| req  | Request of the `MultiGetObject` operation | MultiGetObjectReq  | Yes |
| resp | Response of the `MultiGetObject` operation | MultiGetObjectResp | Yes |


`MultiGetObjectReq` contains the following member functions:

```cpp
// Set the part size.
void SetSliceSize(uint64_t bytes)
// Set the thread pool size.
void SetThreadPoolSize(int size)
```

`MultiGetObjectResp` contains the following member functions:

```cpp
/// Algorithm for server-side encryption
std::string GetXCosServerSideEncryption() const
```

### Resumable download

#### Description

This API is used to download multiple ranges concurrently via resumable download.

#### Method prototype

```cpp
CosResult ResumableGetObject(const MultiGetObjectReq& request, MultiGetObjectResp* response)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "exampleobject";
std::string file_path = "./test";

qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, file_path);  
qcloud_cos::MultiGetObjectResp resp;                                    
qcloud_cos::CosResult result = cos.ResumableGetObject(req, &resp); 

// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to get the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------- | ------------------ | -------- |
| req  | Request of the `MultiGetObject` operation | MultiGetObjectReq  | Yes |
| resp | Response of the `MultiGetObject` operation | MultiGetObjectResp | Yes |

### Batch downloading files (downloading a COS directory)

#### Description

The following example shows how to use the SDK’s basic APIs to download a COS directory to local storage.

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string server_dir_name = "image/"; // COS directory
std::string local_dir_name = "/data/"; // Local directory

qcloud_cos::GetBucketReq get_bucket_req(bucket_name);
get_bucket_req.SetPrefix(server_dir_name);
qcloud_cos::CosResult get_bucket_result;
bool is_truncated = false;

do {
    qcloud_cos::GetBucketResp get_bucket_resp;
    // List objects
    get_bucket_result = cos.GetBucket(get_bucket_req, &get_bucket_resp);
    if (get_bucket_result.IsSucc()) {
        std::vector<Content> contents = get_bucket_resp.GetContents();
        for (auto& content : contents) {
            std::cout << "====process " << content.m_key << std::endl;
            std::string local_file_name = local_dir_name + content.m_key;

            if (StringUtil::StringEndsWith(local_file_name, "/")) {
                continue;
            }

            // Create a local directory
            size_t found_dir = local_file_name.find_last_of("/");
            if (found_dir) {
                std::string dirname = local_file_name.substr(0, found_dir);
                char* p_dirname = const_cast<char*>(dirname.c_str());
                struct stat buffer;
                if (stat(p_dirname, &buffer) != 0) {
                    std::cout << "====mkdir " << dirname << std::endl;
                    std::string mkdir_cmd = "mkdir -p " + dirname;
                    system(mkdir_cmd.c_str());
                }
            }
			// Download an object
            GetObjectByFileReq get_req(bucket_name, content.m_key, local_file_name);
            GetObjectByFileResp get_resp;
            CosResult get_result = cos.GetObject(get_req, &get_resp);
            if (get_result.IsSucc()) {
                std::cout << "====download " << content.m_key << " to "
                    << local_file_name << " succeed" << std::endl;
            } else {
                std::cout << "====download " << content.m_key << " to "
                    << local_file_name << " failed" << std::endl;
            }
        }
        get_bucket_req.SetMarker(
            get_bucket_resp.GetNextMarker());  // Set the start key for the next listing
        is_truncated = get_bucket_resp.IsTruncated();
    }
} while (get_bucket_result.IsSucc() && is_truncated);
```


### 
