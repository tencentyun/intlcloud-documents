## Overview

This document provides an overview of APIs related to simple object operations, multipart upload, and other operations and corresponding SDK sample code.

**Simple operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/30614) | Querying object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Simply uploading an object | Uploads an object (file/object) to a bucket |
[HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries object metadata |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object (file/object) to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Setting object replication | Copies a file to the destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes the specified object (file/object) in a bucket |
| [DELETE Multiple Object](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes objects (files/objects) in a bucket in batches |

**Multipart upload operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Retrieves an archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting object ACL | Sets the ACL for the specified object (file/object) in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying object ACL | Queries the ACL of an object (file/object) |

## Simple Operations

### Querying Object List

#### Feature Description

This API is used to query some or all objects in a bucket.

#### Method Prototype

```go
func (s *BucketService) Get(ctx context.Context, opt *BucketGetOptions) (*BucketGetResult, *Response, error)
```

#### Sample Request

```go
opt := &cos.BucketGetOptions{
	Prefix: "test",
	MaxKeys: 100,                                
}
v, resp, err := client.Bucket.Get(context.Background(), opt)
```

#### Parameter Descriptions

```go
type BucketGetOptions struct {
	Prefix       string 
	Delimiter    string 
	EncodingType string 
	Marker       string 
	MaxKeys      int    
}
```

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Prefix | Filters object keys to match the objects with the same prefix. This parameter is blank by default | string | No |
| Delimiter  | This parameter is blank by default. To simulate a folder, set delimiter `/` | string | No |
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | string | No |
| Marker | Marks the starting position of the list of returned objects. By default, entries are listed in UTF-8 binary order  | string | No |
| MaxKeys | Maximum number of returned objects; default and maximum value: 1,000 | int | No |

#### Return Result Descriptions

```go
type BucketGetResult struct {
	Name           string
	Prefix         string 
	Marker         string 
	NextMarker     string 
	Delimiter      string 
	MaxKeys        int
	IsTruncated    bool
	Contents       []Object 
	CommonPrefixes []string 
	EncodingType   string   
}
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | -------- |
| Name | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000 | string |
| Prefix | Filters object keys to match the objects with the same prefix. This parameter is blank by default | string |
| Marker | Marks the starting position of the list of returned objects. By default, entries are listed in UTF-8 binary order  | string |
| NextMarker  | Marks the starting position of the list of objects returned next time if IsTruncated is true | string |
| Delimiter  | This parameter is blank by default. To simulate a folder, set delimiter `/` | string |
| MaxKeys | Maximum number of returned objects; default and maximum value: 1,000 | int |
| IsTruncated | Indicates whether the returned objects are truncated | bool |
| Contents | A list of all object metadata. Each object type contains information such as ETag, StorageClass, Key, Owner, LastModified, and Size | []Object |
| CommonPrefixes | All keys starting with Prefix and ending in Delimiter are grouped into the same class | []string |
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | string |

### Simply Uploading an Object

#### Feature Description

This API (PUT Object) is used to upload an object (file/object) to a bucket.

#### Method Prototype

```go
func (s *ObjectService) Put(ctx context.Context, key string, r io.Reader, opt *ObjectPutOptions) (*Response, error)
```

#### Sample Request

```go	
key := "put_option.go"
f, err := os.Open("./test")
opt := &cos.ObjectPutOptions{
	ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
		ContentType: "text/html",
	},
	ACLHeaderOptions: &cos.ACLHeaderOptions{
		XCosACL: "private",
	},
}
resp, err = client.Object.Put(context.Background(), key, f, opt)
```

```go
type ObjectPutOptions struct {
	*ACLHeaderOptions       
	*ObjectPutHeaderOptions 
}
type ACLHeaderOptions struct {
	XCosACL              string                           
    XCosGrantRead        string
    XCosGrantWrite       string 
    XCosGrantFullControl string                                           
} 
type ObjectPutHeaderOptions struct {
	CacheControl       string 
	ContentDisposition string 
	ContentEncoding    string 
	ContentType        string 
	ContentLength      int   
	Expires            string 
	// Custom x-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}
```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r | Content of the uploaded file, which can be a file stream or a byte stream. When r is not `bytes.Buffer/bytes.Reader/strings.Reader`, `opt.ObjectPutHeaderOptions.ContentLength` must be specified | io.Reader | Yes |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| XCosACL | Sets the ACL for the file, such as private, public-read, and public-read-write | string | No |
| XCosGrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | string | No |
| XCosGrantRead | Grants the grantee read permission in the format of id="[OwnerUin]" | string | No |
| XCosStorageClass | Sets the storage class of the file; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | string | No |
| Expires | Sets Content-Expires | string | No |
| CacheControl | Cache policy, which sets Cache-Control | string | No |
| ContentType | Content type, which sets Content-Type | string | No |
| ContentDisposition | Filename, which sets Content-Disposition | string | No |
| ContentEncoding | Encoding format, which sets Content-Encoding | string | No |
| ContentLength | Sets transfer length | string | No |
| XCosMetaXXX | User-defined file metadata, which must start with x-cos-meta; otherwise, it will be ignored | http.Header | No |

#### Return Result Descriptions

```go
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```

| Parameter Name | Description | Type |
| ---------------- | -------------------------------- | ------ |
| ETag | MD5 value of the uploaded file | string |
| x-cos-expiration | Returns the file expiration rule after lifecycle is set | string |

### Querying Object Metadata

#### Feature Description

This API (HEAD Object) is used to query the metadata of an object.

#### Method Prototype

```go
func (s *ObjectService) Head(ctx context.Context, key string, opt *ObjectHeadOptions) (*Response, error)
```

#### Sample Request

```go
key := "test/hello.txt"
resp, err := client.Object.Head(context.Background(), key, nil)
```

#### Parameter Descriptions

```go
type ObjectHeadOptions struct {
	IfModifiedSince string 
}
```

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| IfModifiedSince | Returned only if modified after the specified time | string | No |

#### Return Result Descriptions

```go
{
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| File metadata | Gets the file metadata, including information such as Etag and X-Cos-Request-Id and custom metadata | string |

### Downloading an Object

#### Feature Description

This API (GET Object) is used to download an object (file/object) to the local file system.

#### Method Prototype

```go
func (s *ObjectService) Get(ctx context.Context, key string, opt *ObjectGetOptions) (*Response, error)

func (s *ObjectService) GetToFile(ctx context.Context, key, localfile string, opt *ObjectGetOptions) (*Response, error)
```

#### Sample Request

```go
key := "test/hello.txt"
opt := &cos.ObjectGetOptions{
	ResponseContentType: "text/html",
	Range:               "bytes=0-3",
}
// opt is optional and can be set to nil if there are no special settings
// 1. Get object by resp body.
resp, err := client.Object.Get(context.Background(), key, opt)
bs, _ = ioutil.ReadAll(resp.Body)
resp.Body.Close()
fmt.Printf("%s\n", string(bs))

// 2.Get object to local file.
_, err = c.Object.GetToFile(context.Background(), name, "hello_1.txt", nil)
if err != nil {
	panic(err)
}
```

#### Parameter Descriptions

```go
type ObjectGetOptions struct {
	ResponseContentType        string 
	ResponseContentLanguage    string 
	ResponseExpires            string 
	ResponseCacheControl       string 
	ResponseContentDisposition string 
	ResponseContentEncoding    string 
	Range                      string 
	IfModifiedSince            string 
}
```

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ------ | ---- |
|Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| localfile | Sets the response header Content-Type | string | Yes |
| ResponseContentType | Sets the response header Content-Type | string | No |
| ResponseContentLanguage | Sets the response header Content-Language  | string | No |
| ResponseExpires | Sets the response header Content-Expires | string | No |
| ResponseCacheControl | Sets the response header Cache-Control | string | No |
| ResponseContentDisposition | Sets the response header Content-Disposition | string | No |
| ResponseContentEncoding | Sets the response header Content-Encoding | string | No |
| Range | Sets the range of file download in the format of bytes=first-last | string | No |
| IfModifiedSince | Returned only if modified after the specified time | string | No |

#### Return Result Descriptions

```go
{
    'Body': '',
    'Accept-Ranges': 'bytes',
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Range': 'bytes 0-16086/16087',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ---------- |
| Body | Downloaded file content | StreamBody |
| File metadata | Metadata of the downloaded file, including information such as Etag and X-Cos-Request-Id and metadata set by the return | string |

### Setting Object Replication

This API (PUT Object - Copy) is used to copy a file to the destination path.

#### Method Prototype

```go
func (s *ObjectService) Copy(ctx context.Context, key, sourceURL string, opt *ObjectCopyOptions) (*ObjectCopyResult, *Response, error)
```

#### Sample Request

```go
u, _ := url.Parse("http://examplebucket-12500000000.cos.ap-guangzhou.myqcloud.com")
source := "test/objectMove_src"
sourceURL := fmt.Sprintf("%s/%s", u.Host, source)
dest := "test/objectMove_dest"
//opt := &cos.ObjectCopyOptions{}
r, resp, err := client.Object.Copy(context.Background(), dest, sourceURL, nil)
```

#### Parameter Descriptions

```go
type ObjectCopyOptions struct {
	*ObjectCopyHeaderOptions 
	*ACLHeaderOptions        
}
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
type ObjectCopyHeaderOptions struct {
	XCosMetadataDirective           string 
	XCosCopySourceIfModifiedSince   string 
	XCosCopySourceIfUnmodifiedSince string 
	XCosCopySourceIfMatch           string 
	XCosCopySourceIfNoneMatch       string 
	XCosStorageClass                string 
	// Custom x-cos-meta-* header
	XCosMetaXXX    				    *http.Header 
	XCosCopySource 					string      
}
```

| Parameter Name | Description | Type | Required |
| ------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
|Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| sourceURL | Describes the URL of the source file to be copied | string | Yes |
| XCosACL | Sets the ACL for the file, such as private, public-read, and public-read-write | string | No |
| XCosGrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | string | No |
| XCosGrantRead | Grants the grantee read permission in the format of id="[OwnerUin]" | string | No |
| XCosMetadataDirective | Value range: Copy, Replaced. If this parameter is set to Copy, the configured user metadata is ignored and the copy is performed directly; if Replaced, the metadata is modified based on the configured metadata. If the destination path is the same as the source path, this parameter has to be set to Replaced | string | Yes |
| XCosCopySourceIfModifiedSince | If the object is modified after the specified time, the operation is performed; otherwise, 412 is returned. This parameter can be used together with XCosCopySourceIfNoneMatch. If it is used together with other conditions, a conflict is returned | string | No |
| XCosCopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation is performed; otherwise, 412 is returned. This parameter can be used together with XCosCopySourceIfMatch. If it is used together with other conditions, a conflict is returned | string | No |
| XCosCopySourceIfMatch | If the Etag of the object is the same as the specified one, the operation is performed; otherwise, 412 is returned. This parameter can be used together with XCosCopySourceIfUnmodifiedSince. If it is used together with other conditions, a conflict is returned | string | No |
| XCosCopySourceIfNoneMatch | If the Etag of the object is different from the specified one, the operation is performed; otherwise, 412 is returned. This parameter can be used together with XCosCopySourceIfModifiedSince. If it is used together with other conditions, a conflict is returned | string | No |
| XCosStorageClass | Sets the storage class of the file; value range: STANDARD, STANDARD_IA; default value: STANDARD | string | No |
| XCosMetaXXX | Array | User-defined file metadata | http.Header | No |
| XCosCopySource                  | Source file URL path. A previous version can be specified using the versionid sub-resource | string      | No   |

#### Return Result Descriptions

Attributes of the uploaded file:

```go
type ObjectCopyResult struct {
    ETag         string 
    LastModified string
}

```

| Parameter Name | Description | Type |
| ------------ | -------------------------- | ------ |
| ETag | MD5 value of the copied file | string |
| LastModified | Last modified time of the copied file | string |

### Deleting a Single Object

#### Feature Description

This API is used to delete the specified object (file/object) in a bucket.

#### Method Prototype

```go
func (s *ObjectService) Delete(ctx context.Context, key string) (*Response, error)

```

#### Sample Request

```go
key := "test/objectPut.go"
resp, err := client.Object.Delete(context.Background(), name)

```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |

### Deleting Multiple Objects

#### Feature Description

This API is used to delete multiple objects (files/objects) in a bucket. Up to 1,000 objects can be deleted in batches in one single request.

#### Method Prototype

```go
func (s *ObjectService) DeleteMulti(ctx context.Context, opt *ObjectDeleteMultiOptions) (*ObjectDeleteMultiResult, *Response, error)

```

#### Sample Request

```go
var objects []string
objects = append(objects, []string{"a", "b", "c"}...)
obs := []cos.Object{}
for _, v := range names {
	obs = append(obs, cos.Object{Key: v})
}
opt := &cos.ObjectDeleteMultiOptions{
	Objects: obs,
	// A boolean value which determines whether to enable Quiet mode.
	// If the value is true, Quiet mode is enabled; if it is false, Verbose mode is enabled. The default value is false
	// Quiet: true,
}                                       

v, _, err := c.Object.DeleteMulti(ctx, opt)
```

#### Parameter Descriptions

```go
type ObjectDeleteMultiOptions struct {
	Quiet   bool
	Objects []Object   
}
// Object is the meta info of the object
type Object struct {
	Key          string
    // And other params not relate to this api
}
```

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | --------- | ---- |
| Quiet | A boolean value which determines whether to enable Quiet mode. For the response result, COS provides two result modes: Verbose and Quiet. <br>Verbose mode returns the deletion result for each object; while Quiet mode only returns the information of objects for which errors are reported. If the value is true, Quiet mode is enabled; if it is false, Verbose mode is enabled. The default value is false | Boolean | No |
| Objects  | Describes the information of each target object to be deleted | Container | Yes |
| Key | Filename of the destination object | String | Yes |

#### Return Result Descriptions

Attributes of the uploaded file:

```go
// ObjectDeleteMultiResult is the result of DeleteMulti
type ObjectDeleteMultiResult struct {	
	DeletedObjects []Object
	Errors         []struct {
		Key     string
		Code    string
		Message string
	}
}
```

| Parameter Name | Description | Type |
| -------------- | ---------------------------------- | --------- |
| DeletedObjects | Describes the information of each target object to be deleted | Container |
| Errors | Describes the information of objects that failed to be deleted in this operation | Container |
| Key | Name of the object that failed to be deleted | string |
| Code | Error code of the object deletion failure | String |
| Message | Error message of the object deletion failure | string |

## Multipart Upload Operations

### Querying a Multipart Upload

#### Feature Description

This API (List Multipart Uploads) is used to query multipart uploads in progress in the specified bucket.

#### Method Prototype

```go
func (s *BucketService) ListMultipartUploads(ctx context.Context, opt *ListMultipartUploadsOptions) (*ListMultipartUploadsResult, *Response, error)
```

#### Sample Request

```go
v, resp, err := c.Bucket.ListMultipartUploads(context.Background(), opt)
```

#### Parameter Descriptions

```go
type ListMultipartUploadsOptions struct {
	Delimiter      string
	EncodingType   string
	Prefix         string
	MaxUploads     int
	KeyMarker      string
	UploadIDMarker string                                         
}
```

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Delimiter | The delimiter is a symbol. The specified prefix in the object name before the first delimiter character is defined as a set of elements: common prefix. If there is no prefix, it starts at the beginning of the path | string | No |
| EncodingType | Specifies the encoding method of the return value; value range: url | string | No |
| Prefix | Specifies that the returned object key must be prefixed with the "prefix". Note that when a prefix query is used, the returned key will still contain the prefix | string | No |
| MaxUploads | Sets the maximum number of parts returned between 1 and 1,000; default value: 1,000 | string | No |
| KeyMarker | Used together with upload-id-marker. If upload-id-marker is not specified, only the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list; otherwise, the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included, and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker | string | No |
| UploadIDMarker | Used together with key-marker. If key-marker is not specified, upload-id-marker will be ignored; otherwise, the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list, and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker | string | No |

#### Return Result Descriptions

```go
// ListMultipartUploadsResult is the result of ListMultipartUploads
type ListMultipartUploadsResult struct {
	Bucket             string
	EncodingType       string
	KeyMarker          string
	UploadIDMarker     string
    NextKeyMarker      string
    NextUploadIDMarker string
    MaxUploads         int
    IsTruncated        bool
    Uploads            []struct {
    	Key          string
    	UploadID     string
    	StorageClass string
    	Initiator    *Initiator
    	Owner        *Owner
    	Initiated    string
    }
    Prefix         string
    Delimiter      string
    CommonPrefixes []string 
}
// Use the same struct with the Owner
type Initiator Owner
// Owner defines Bucket/Object's owner
type Owner struct {
	ID          string
	DisplayName string
}
```

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | --------- |
| Bucket | Destination bucket for the multipart upload in the format of BucketName, such as examplebucket-1250000000 | String |
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | string |
| KeyMarker      | The entry list starts at this key value                                      | string |
| UploadIDMarker     | The entry list starts at this UploadId value                                      | string |
| NextKeyMarker | If the returned entries are truncated, then NextKeyMarker is the starting point of the next entry | string |
| NextUploadIDMarker | If the returned entries are truncated, then UploadId is the starting point of the next entry | String |
| MaxUploads | Maximum number of returned parts; default and maximum value: 1,000 | string |
| IsTruncated        | Indicates whether the returned parts are truncated | bool |
| Uploads            | Information of each upload                                           | Container |
| Key | Object name | string |
| UploadID           | Identifies the ID of this multipart upload                                        | string    |
| Key | Indicates whether the returned parts are truncated | bool |
| StorageClass       | Indicates the storage class of the parts; enumerated value: STANDARD, STANDARD_IA, ARCHIVE | string    |
| Initiator          | Identifies the initiator of this upload                                 | Container |
| Owner              | Identifies the owner of the parts                                 | Container |
| Initiated          | Start time of the multipart upload                                           | string    |
| Prefix | Specifies that the returned object key must be prefixed with the "prefix". Note that when a prefix query is used, the returned key will still contain the prefix | struct |
| Delimiter | The delimiter is a symbol. The specified prefix in the object name before the first delimiter character is defined as a set of elements: common prefix. If there is no prefix, it starts at the beginning of the path | string |
| CommonPrefixes | The identical paths between prefix and delimiter are grouped into one class and defined as a common prefix | String |
| ID | Unique CAM ID of the user | string |
| DisplayName        | User ID (UIN)                                    | string    |

### Uploading an Object in Parts

With multipart upload, you can do the following:

- Upload an object in parts, including initializing a multipart upload, uploading parts, and completing the multipart upload.
- Delete uploaded parts.

### <span id = "INIT_MULIT_UPLOAD">Initializing a Multipart Upload</span>

#### Feature Description

This API (Initiate Multipart Upload) is used to initialize a multipart upload operation and get the corresponding uploadId.

#### Method Prototype

```go
func (s *ObjectService) InitiateMultipartUpload(ctx context.Context, name string, opt *InitiateMultipartUploadOptions) (*InitiateMultipartUploadResult, *Response, error)
```

#### Sample Request

```go
name := "test_multipart"
// Optional
v, resp, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil）
```

#### Parameter Descriptions

```go
type InitiateMultipartUploadOptions struct {
	*ACLHeaderOptions       
	*ObjectPutHeaderOptions 
}
type ACLHeaderOptions struct {
	XCosACL              string                           
	XCosGrantRead        string
	XCosGrantWrite       string 
	XCosGrantFullControl string                                           
} 
type ObjectPutHeaderOptions struct {
	CacheControl       string 
	ContentDisposition string 
	ContentEncoding    string 
	ContentType        string 
	ContentLength      int   
	Expires            string 
	// Custom x-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}

```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r | Content of the uploaded file, which can be a file stream or a byte stream. When r is not `bytes.Buffer/bytes.Reader/strings.Reader`, `opt.ObjectPutHeaderOptions.ContentLength` must be specified | io.Reader | Yes |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| XCosACL | Sets the ACL for the file, such as private and public-read | string | No |
| XCosGrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | string | No |
| XCosGrantRead | Grants the grantee read permission in the format of id="[OwnerUin]" | string | No |
| XCosStorageClass | Sets the storage class of the file; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | string | No |
| Expires | Sets Content-Expires | string | No |
| CacheControl | Cache policy, which sets Cache-Control | string | No |
| ContentType | Content type, which sets Content-Type | string | No |
| ContentDisposition | Filename, which sets Content-Disposition | string | No |
| ContentEncoding | Encoding format, which sets Content-Encoding | string | No |
| ContentLength | Sets transfer length | string | No |
| XCosMetaXXX | User-defined file metadata, which must start with x-cos-meta; otherwise, it will be ignored | http.Header | No |

#### Return Result Descriptions

```go
type InitiateMultipartUploadResult struct {
	Bucket   string
	Key      string
	UploadID string
} 
```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| UploadId | Identifies the ID of the multipart upload | string |
| Bucket | Bucket name in the format of bucket-appid | String | Yes |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String |

### <span id = "MULIT_UPLOAD_PART">Uploading Parts</span>

This API (Upload Part) is used to upload an object in parts.

#### Method Prototype

```go
func (s *ObjectService) UploadPart(ctx context.Context, key, uploadID string, partNumber int, r io.Reader, opt *ObjectUploadPartOptions) (*Response, error)
```

#### Sample Request

```go
// Note that the number of parts in a multipart upload cannot exceed 10,000
key := "test/test_multi_upload.go"
f := strings.NewReader("test heoo")
// Optional
_, err := client.Object.UploadPart(
    context.Background(), key, uploadID, 1, f, nil,
)
```

#### Parameter Descriptions

```go
type ObjectUploadPartOptions struct {
    ContentLength   int
}
```

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | --------- | ---- |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| UploadId | Identifies the ID of the multipart upload, which is generated by InitiateMultipartUpload | string | Yes |
| PartNumber | Uploaded part number | int | Yes |
| r | Content of the uploaded part, which can be a local file stream or an input stream. When r is not `bytes.Buffer/bytes.Reader/strings.Reader`, opt.ContentLength must be specified | io.Reader | Yes |
| ContentLength | Sets transfer length | int | No |

#### Return Result Descriptions

```go
{
    'ETag': 'string'
}

```

| Parameter Name | Description | Type |
| -------- | ----------------- | ------ |
| ETag | MD5 value of the uploaded part | string |



### <span id = "LIST_MULIT_UPLOAD">Querying Uploaded Parts</span>

#### Feature Description

This API (List Parts) is used to query uploaded parts in the specified multipart upload operation.

#### Method Prototype

```go
func (s *ObjectService) ListParts(ctx context.Context, name, uploadID string, opt *ObjectListPartsOptions) (*ObjectListPartsResult, *Response, error)

```

#### Sample Request

```go
key := "test/test_list_parts.go"
v, resp, err := client.Object.ListParts(context.Background(), key, uploadID, nil) 

```

#### Parameter Descriptions

```go
type ObjectListPartsOptions struct {
	EncodingType     string
	MaxParts         string
	PartNumberMarker string                                      
}
```

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| UploadId | Identifies the ID of the multipart upload, which is generated by InitiateMultipartUpload | string | Yes |
| EncodingType | Specifies the encoding method of the return value | string | No |
| MaxParts | Maximum number of entries returned at a time; 1,000 by default                             | string | No  |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order, and the entry list starts at marker | string | No |

#### Return Result Descriptions

```go
type ObjectListPartsResult struct {
	Bucket               string
	EncodingType         string
	Key                  string
	UploadID             string
	Initiator            *Initiator
	Owner                *Owner
	StorageClass         string
	PartNumberMarker     string
	NextPartNumberMarker string
	MaxParts             string
	IsTruncated          bool
	Parts                []Object
}
type Initiator struct {
	UIN         string
	ID          string
	DisplayName string
}
type Owner struct {
	UIN         string
	ID          string
	DisplayName string
}
type Object struct {
	Key          string
	ETag         string
	Size         int
	PartNumber   int
	LastModified string
	StorageClass string 
	Owner        *Owner
}
```

| Parameter Name | Description | Type |
| -------------------- | ------------------------------------------------------------ | ------ |
| Bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000 | string |
| EncodingType | Specifies the encoding method of the return value; value range: url; no encoding is performed by default | string |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String |
| UploadId | Identifies the ID of the multipart upload, which is generated by InitiateMultipartUpload | string |
| Initiator | Information of the multipart upload initiator, including DisplayName, UIN, and ID | struct |
| Owner | File owner information, including DisplayName, UIN, and ID | struct |
| StorageClass | File storage class; value range: STANDARD, STANDARD_IA, ARCHIVE; default value: STANDARD | string |
| PartNumberMarker | The part list starts from PartNumberMarker, which is 0 by default, i.e., listing parts from the first one | string |
| NextPartNumberMarker | Indicates the starting position of the next listed part | string |
| MaxParts | Maximum number of returned parts; default and maximum value: 1,000 | string |
| IsTruncated        | Indicates whether the returned parts are truncated | bool |
| Part | Information about the uploaded part, including ETag, PartNumber, Size, and LastModified | struct |



### <span id = "COMPLETE_MULIT_UPLOAD">Completing a Multipart Upload</span>

#### Feature Description

The API (Complete Multipart Upload) is used to complete the multipart upload of the entire file.

#### Method Prototype

```go
func (s *ObjectService) CompleteMultipartUpload(ctx context.Context, key, uploadID string, opt *CompleteMultipartUploadOptions) (*CompleteMultipartUploadResult, *Response, error)

```

#### Sample Request

```go
// Encapsulate the etag information returned by the UploadPart API
func uploadPart(c *cos.Client, name string, uploadID string, blockSize, n int) string {
	b := make([]byte, blockSize)
	if _, err := rand.Read(b); err != nil {
		panic(err)
	}
	s := fmt.Sprintf("%X", b)
	f := strings.NewReader(s)

	// When the passed parameter f is not bytes.Buffer/bytes.Reader/strings.Reader, opt.ContentLength must be specified
	// opt := &cos.ObjectUploadPartOptions{
	//	 ContentLength: size,
	// }

	resp, err := c.Object.UploadPart(
		context.Background(), name, uploadID, n, f, nil,
	)
	if err != nil {
		panic(err)
	}
	return resp.Header.Get("Etag")
}

// Init, UploadPart and Complete process
key := "test/test_complete_upload.go"
v, resp, err := client.Object.InitiateMultipartUpload(context.Background(), key, nil)
uploadID := v.UploadID
blockSize := 1024 * 1024 * 3

opt := &cos.CompleteMultipartUploadOptions{}
for i := 1; i < 5; i++ {
	// Call the encapsulated API above to get the etag information
	etag := uploadPart(c, key, uploadID, blockSize, i)
	opt.Parts = append(opt.Parts, cos.Object{
		PartNumber: i, ETag: etag},
	)
}

v, resp, err = client.Object.CompleteMultipartUpload(
	context.Background(), key, uploadID, opt,
)
```

#### Parameter Descriptions

```go
type CompleteMultipartUploadOptions struct {
	Parts   []Object 
}
type Object struct { 
	ETag         string 
	PartNumber   int     
}
```

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
|Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| UploadId | Identifies the ID of the multipart upload, which is generated by InitiateMultipartUpload | string | Yes |
| CompleteMultipartUploadOptions | ETag and PartNumber information of all parts | struct | Yes |

#### Return Result Descriptions

```go
type CompleteMultipartUploadResult struct {
	Location string
	Bucket   string
	Key      string
	ETag     string
}

```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Location | URL address | string |
| Bucket   | Bucket name in the format of BucketName-APPID, such as examplebucket-1250000000 | string |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String |
| ETag | The unique tag value of the merged object, which is not the MD5 checksum of the object's content and can only be used to check the object's uniqueness. To verify the content of the file, check the ETag values of individual parts during the upload process | string |

### <span id = "ABORT_MULIT_UPLOAD">Aborting a Multipart Upload</span>

#### Feature Description

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### Method Prototype

```go
func (s *ObjectService) AbortMultipartUpload(ctx context.Context, key, uploadID string) (*Response, error)
```

#### Sample Request

```go
key := "test_multipart.txt"
v, _, err := client.Object.InitiateMultipartUpload(context.Background(), key, nil)
// Abort
resp, err := client.Object.AbortMultipartUpload(context.Background(), key, v.UploadID)
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| UploadId | Identifies the ID of the multipart upload | string | Yes |

## Other Operations

### Restoring an Archived Object 

#### Feature Description

This API (POST Object restore) is used to retrieve an archived object for access.

#### Method Prototype

```go
func (s *ObjectService) PutRestore(ctx context.Context, key string, opt *ObjectRestoreOptions) (*Response, error) 
```

#### Sample Request

```go
opt := &cos.ObjectRestoreOptions{
	Days: 2,
	Tier: &cos.CASJobParameters{
    		// Standard, Exepdited and Bulk
    		Tier: "Expedited",
	},
}
key := "archivetest"
resp, err := c.Object.PutRestore(context.Background(), key, opt)
```

#### Parameter Descriptions

```go
type ObjectRestoreOptions struct {        
    Days    int               
    Tier    *CASJobParameters 
}
type CASJobParameters struct {
    Tier    string 
}
```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| ObjectRestoreOptions | Describes the rule of the temporary file retrieved | struct | Yes |
| Days | Describes the expiration time of the temporary file | int | Yes |
| CASJobParameters | Describes the configuration information of the restoration type | struct | No |
| Tier | Describes the mode in which the temporary file is retrieved. Value range: Expedited (for expedited mode), Standard (for standard mode), Bulk (for bulk mode) | string | No |

### Setting Object ACL

#### Feature Description

This API (PUT Object acl) is used to set the access control list (ACL) for an object.

#### Method Prototype

```go
func (s *ObjectService) PutACL(ctx context.Context, key string, opt *ObjectPutACLOptions) (*Response, error)
```

#### Sample Request

```go
// 1.Set by header
opt := &cos.ObjectPutACLOptions{
    Header: &cos.ACLHeaderOptions{
        XCosACL: "private",
    },
}
key := "test/hello.txt"
resp, err := client.Object.PutACL(context.Background(), key, opt)
// 2.Set by body
opt = &cos.ObjectPutACLOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            ID: "qcs::cam::uin/100000760461:uin/100000760461",
        },
        AccessControlList: []cos.ACLGrant{
            {
                Grantee: &cos.ACLGrantee{
                    Type: "RootAccount",
                    ID:   "qcs::cam::uin/100000760461:uin/100000760461",
                },

                Permission: "FULL_CONTROL",
            },
        },
    },
}

resp, err = client.Object.PutACL(context.Background(), key, opt)
```

#### Parameter Descriptions

```go
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |
| XCosACL | Sets the ACL for the file, such as private and public-read | string | No |
| XCosGrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | string | No |
| XCosGrantRead | Grants the grantee read permission in the format of id="[OwnerUin]" | string | No |
| ACLXML | Grants the specified account access to the bucket. For detailed format, see the return result descriptions of GET Object acl | struct | No |

### Querying Object ACL

#### Feature Description

This API (GET Object acl) is used to query the ACL of an object (file/object).

#### Method Prototype

```go
func (s *ObjectService) GetACL(ctx context.Context, key string) (*ObjectGetACLResult, *Response, error)
```

#### Sample Request

```go
key := "test/hello.txt"
v, resp, err := client.Object.GetACL(context.Background(), key)
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes |

#### Return Result Descriptions

```go
type ACLXml struct {
	Owner             *Owner
	AccessControlList []ACLGrant 
}
type Owner struct { 
	ID          string 
	DisplayName string
}
type ACLGrant struct {
	Grantee    *ACLGrantee
	Permission string
}
type ACLGrantee struct {
	Type        string 
	ID          string 
	DisplayName string
    UIN         string 
}
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner | Bucket owner information, including DisplayName and ID | struct |
| AccessControlList | Bucket permission grantee information, including Grantee and Permission           | struct |
| Grantee           | Permission grantee information, including DisplayName, Type, ID, and UIN          | struct |
| Type              | Permission grantee type; CanonicalUser or Group            | string |
| ID | If Type is CanonicalUser, this parameter corresponds to the ID of the permission grantee | string |
| DisplayName | Permission grantee name | string |
| UIN | If Type is Group, this parameter corresponds to the UIN of the permission grantee | string |
| Permission | Permission to the bucket owned by the grantee. Value range: FULL_CONTROL (for read/write permission), WRITE (for write permission), READ (for read permission) | string |
