## Introduction

This document provides an overview of APIs and SDK sample codes related to simple operations, multipart operations and other operations on objects.

**Simple Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | Querying object list | Queries a part of or all objects in a bucket |
| [PUT Object](https://cloud.tencent.com/document/product/436/7749) | Uploads an object | Uploads an object (file) to the bucket |
| [HEAD Object](https://cloud.tencent.com/document/product/436/7745) | Gets object metadata | Gets the meta information of an object |
| [GET Object](https://cloud.tencent.com/document/product/436/7753) | Gets an object | Downloads an object (file) locally |
| [PUT Object - Copy](https://cloud.tencent.com/document/product/436/10881) | Sets object replication | Copies a file to the destination path |
| [DELETE Object](https://cloud.tencent.com/document/product/436/7743) | Deletes a single object | Deletes the specified object in the bucket |
| [DELETE Object](https://cloud.tencent.com/document/product/436/7743) | Deletes a single object | Deletes multiple objects in the bucket |

**Multipart Upload Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://cloud.tencent.com/document/product/436/7736) | Querying a multipart upload | Queries the information of a multipart upload in progress |
| [Initiate Multipart Upload](https://cloud.tencent.com/document/product/436/7746) | Initializes multipart upload | Initializes a multipart upload operation |
| [Upload Part](https://cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file parts |
| [List Parts](https://cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts in the specified multipart upload operation |
| [Complete Multipart Upload](https://cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of the entire file |
| [Abort Multipart Upload](https://cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload operation and deletes the uploaded parts |

**Other Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://cloud.tencent.com/document/product/436/12633) | Restores an archived object | Restores an archived object for access |
| [PUT Object acl](https://cloud.tencent.com/document/product/436/7748) | Sets the object ACL | Sets an ACL for an object (file) in the bucket |
| [GET Object acl](https://cloud.tencent.com/document/product/436/7744) | Gets the object ACL | Gets the ACL of an object (file) |

## Simple Operations

### Querying the object list

#### Feature

This API (GET Bucket (List Object)) is used to query some or all objects in a bucket.

#### Method Prototype

```go
func (s *BucketService) Get(ctx context.Context, opt *BucketGetOptions) (*BucketGetResult, *Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-get-bucket)
```go
opt := &cos.BucketGetOptions{
    Prefix:  "test",
    MaxKeys: 100,
}
v, _, err := c.Bucket.Get(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### Parameter Description

```go
type BucketGetOptions struct {
	Prefix       string 
	Delimiter='string', 
	EncodingType string 
	Marker='string', 
	MaxKeys      int    
}
```

| Parameter Name | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Prefix | Filters object keys prefixed with the value of this parameter. It is left empty by default. | string | No |
| Delimiter | Sets a delimiter. It is left empty by default. | string | No |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | string | No |
| Marker | Marks the starting point of the list of returned objects. Entries are listed using UTF-8 binary order by default. | string | No |
| MaxKeys | Maximum number of returned objects. It defaults to 1000. | int | No |

#### Returned Result

```go
type BucketGetResult struct {
	Name           string
	Prefix         string 
	Marker='string', 
	'NextMarker': 'string', 
	Delimiter='string', 
	MaxKeys        int
	IsTruncated    bool
	Contents       []Object 
	CommonPrefixes []string 
	EncodingType   string   
}
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | -------- |
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
| Prefix | Filters the object keys prefixed with the value of this parameter. It is left empty by default. | string   |
| Marker | Marks the starting point of the list of returned objects. Entries are listed using UTF-8 binary order by default. | string |
| NextMarker | Marks the starting point of the next list of returned objects if IsTruncated is true. | string |
| Delimiter | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | string |
| MaxKeys | Maximum number of returned objects. It defaults to 1000. | int |
| IsTruncated | Indicates whether the returned objects are truncated | bool |
| Contents | The list containing the meta information of all objects, including ETag, StorageClass, Key, Owner, LastModified, and Size. | []Object |
| CommonPrefixes | All keys starting with Prefix and ending with Delimiter are grouped into the same type. | []string |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | string |

### Uploading an object using simple upload

#### Feature

Upload an object or file to the bucket (PUT Object). Up to 5GM (inclusive) is supported, please use [multipart upload (#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1) or [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) if more than 5GB。 

#### Method Prototype

```go
func (s *ObjectService) Put(ctx context.Context, key string, r io.Reader, opt *ObjectPutOptions) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-put-object)
```go	
$key = "exampleobject";
f, err := os.Open("../test")
opt := &cos.ObjectPutOptions{
    ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
        ContentType: "text/html",
    },
    ACLHeaderOptions: &cos.ACLHeaderOptions{
        We recommend you not to set permissions on individual files when uploading so as to avoid reaching the limit. Bucket permission sets the default limit.
        XCosACL: "private",
    },
}
_, err = client.Object.Put(context.Background(), key, f, opt)
if err != nil {
    panic(err)
}
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
	CacheControl='string', 
	ContentDisposition='string', 
	ContentEncoding='string', 
	ContentType='string', 
	'ContentLength' => 'int',   
	'Expires' => 'string', 
	Custom x-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}
```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r | The content of the uploaded file, which can be a file stream or a byte stream. When r is not bytes.Buffer/bytes.Reader/strings.Reader, opt.ObjectPutHeaderOptions.ContentLength must be specified. | io.Reader | Yes |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| XCosACL | Sets the file ACL, such as private, public-read, and public-read-write | string | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="[OwnerUin]"` | String | No |
| GrantRead | Grants the grantee the read permission in the format of id="[OwnerUin]" | String | No |
| StorageClass | Sets the object storage class; value range: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | String | No |
| Expires | Sets Content-Expires. | string | No |
| CacheControl | Cache policy. Sets Cache-Control. | string | No |
| ContentType | Content Type. Sets Content-Type. | string | No |
| ContentDisposition | File name. Sets Content-Disposition. | string | No |
| ContentEncoding | Encoding format. Sets Content-Encoding. | string | No |
| ContentLength | Sets transmission length | string | No |
| XCosMetaXXX | User-defined file meta information. It must start with x-cos-meta. Otherwise, it will be ignored. | http.Header | No |

#### Returned Result

```go
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```

| Parameter Name | Description | Type |
| ---------------- | -------------------------------- | ------ |
| ETag | MD5 of the upload File | string |
| x-cos-expiration | After the lifecycle is set, the file expiration rule is returned. | string |

### Querying object metadata

#### Feature

The API (HEAD Object) is used to query object metadata.

#### Method Prototype

```go
func (s *ObjectService) Head(ctx context.Context, key string, opt *ObjectHeadOptions) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-head-object)
```go
$key = "exampleobject";
_, err := client.Object.Head(context.Background(), key, nil)
if err != nil {
    panic(err)
}
```

#### Parameter Description

```go
type ObjectHeadOptions struct {
	IfModifiedSince string 
}
```

| Parameter Name | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| IfModifiedSince | The file is returned only if it has been modified after the specified time | string | No |

#### Returned Result

```go
{
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| File meta information | The meta information of the file obtained, including Etag and X-Cos-Request-Id. The meta information of the configured file is also included. | string |

### Downloading an object

#### Feature

This API (Get Object) is used to download an object.

#### Method Prototype

```go
func (s *ObjectService) Get(ctx context.Context, key string, opt *ObjectGetOptions) (*Response, error)

func (s *ObjectService) GetToFile(ctx context.Context, key, localfile string, opt *ObjectGetOptions) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-get-object)
```go
$key = "exampleobject";
opt := &cos.ObjectGetOptions{
    ResponseContentType: "text/html",
    Range:               "bytes=0-3",
}
"opt" is optional. It can be set to nil unless otherwise specified.
// 1. Obtain the object from response body
resp, err := c.Object.Get(context.Background(), name, nil)
if err != nil {
    panic(err)
}
bs, _ := ioutil.ReadAll(resp.Body)
resp.Body.Close()

// 2. Download the object to local files
_, err = c.Object.GetToFile(context.Background(), name, "example", nil)
if err != nil {
    panic(err)
}
```

#### Parameter Description

```go
type ObjectGetOptions struct {
	ResponseContentType='string', 
	ResponseContentLanguage='string', 
	ResponseExpires='string', 
	ResponseCacheControl='string', 
	ResponseContentDisposition='string', 
	ResponseContentEncoding='string', 
	Range                      string 
	IfModifiedSince            string 
}
```

| Parameter Name | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| localfile | Sets the Content-Type in the response header | string | Yes |
| ResponseContentType | Sets the Content-Type in the response header | string | No |
| ResponseContentLanguage | Sets the Content-Language in the response header | string | No |
| ResponseExpires | Sets the Content-Expires in the response header | string | No |
| ResponseCacheControl | Sets the Cache-Control in the response header | string | No |
| ResponseContentDisposition | Sets the Content-Disposition in the response header | string | No |
| ResponseContentEncoding | Sets the Content-Encoding in the response header | string | No |
| Range | Sets the range of bytes of the file to be downloaded in the format of bytes=first-last | string | No |
| IfModifiedSince | The file is returned only if it has been modified after the specified time | string | No |

#### Returned Result

```go
{
    Body: '',
    'Accept-Ranges': 'bytes',
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Range': 'bytes 0-16086/16087',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```

| Parameter Name | Description | Type |
| ---------- | ------------------------------------------------------------ | ---------- |
| Body | The content of the downloaded file | StreamBody |
| File meta information | The meta information of the downloaded file, including Etag and X-Cos-Request-Id. The meta information of the configured file is also returned. | string |

### Set object Replication

This API (PUT Object - Copy) is used to copy files to the destination path.

#### Method Prototype

```go
func (s *ObjectService) Copy(ctx context.Context, key, sourceURL string, opt *ObjectCopyOptions) (*ObjectCopyResult, *Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-copy-object)
```go
name := "exampleobject"
// Uploading the source object
f := strings.NewReader("test")
_, err := c.Object.Put(context.Background(), name, f, nil)
assert.Nil(s.T(), err, "Test Failed")

soruceURL := fmt.Sprintf("%s/%s", client.BaseURL.BucketURL.Host, name)
dest := "example_dest"
We recommend you not to set permissions on individual files when uploading so as to avoid reaching the limit. Bucket permission sets the default limit.
// opt := &cos.ObjectCopyOptions{}
_, _, err = client.Object.Copy(context.Background(), dest, soruceURL, nil)
if err != nil {
    panic(err)
}
```

#### Parameter Description

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
	Custom x-cos-meta-* header
	XCosMetaXXX    				    *http.Header 
	XCosCopySource 					string      
}
```

| Parameter Name | Description | Type | Required |
| ------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| sourceURL | The URL of the copied source file | string | Yes |
| XCosACL | Sets the file ACL, such as private, public-read, and public-read-write | string | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="[OwnerUin]"` | String | No |
| GrantRead | Grants the grantee the read permission in the format of id="[OwnerUin]" | String | No |
| XCosMetadataDirective | Available values: Copy and Replaced. When it is set to Copy, ignore the configured user metadata information and copy the file directly. When it is set to Replaced, modify the metadata according to the configured meta information. If the destination path is identical to the source path, it must be set to Replaced. | string | Yes |
| XCosCopySourceIfModifiedSince | The operation is performed if the object is modified after the specified time, otherwise error code 412 is returned. It can be used with XCosCopySourceIfNoneMatch. Using it with other conditions can cause a conflict. | string | No |
| XCosCopySourceIfUnmodifiedSince | The operation is performed if the object is not modified after the specified time, otherwise error code 412 is returned. It can be used with XCosCopySourceIfMatch. Using it with other conditions can cause a conflict. | string | No |
| XCosCopySourceIfMatch | The operation is performed if the Etag of the object is the same as the given one, otherwise error code 412 is returned. It can be used with XCosCopySourceIfUnmodifiedSince. Using it with other conditions can cause a conflict. | string | No |
| XCosCopySourceIfNoneMatch | The operation is performed if the Etag of the object is different from the given one, otherwise error code 412 is returned. It can be used with XCosCopySourceIfModifiedSince. Using it with other conditions can cause a conflict. | string | No |
| XCosStorageClass | Sets file storage type: STANDARD and STANDARD_IA. Default: STANDARD | string | No |
| XCosMetaXXX | User-defined file meta information. | http.Header | No |
| XCosCopySource | Source file URL path. You can specify the history version with the versionid subresource. | string | No |

#### Returned Result

Attributes of the uploaded file:

```go
type ObjectCopyResult struct {
    'ETag': 'string', 
    'LastModified': 'string',
}
```

| Parameter Name | Description | Type |
| ------------ | -------------------------- | ------ |
| ETag | MD5 of the copied file | string |
| LastModified | The time when the copied file was last modified. | string |

### Deleting a single object

#### Feature

This API is used to delete a specified object in the bucket.

#### Method Prototype

```go
func (s *ObjectService) Delete(ctx context.Context, key string) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-delete-object)
```go
$key = "exampleobject";
_, err := c.Object.Delete(context.Background(), name)
if err != nil {
    panic(err)
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |

### Deleting multiple objects

#### Feature

The API is used to delete multiple objects in a bucket. Up to 1000 objects can be deleted in a batch in one request.

#### Method Prototype

```go
func (s *ObjectService) DeleteMulti(ctx context.Context, opt *ObjectDeleteMultiOptions) (*ObjectDeleteMultiResult, *Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-delete-multi-object)
```go
var objects []string
objects = append(objects, []string{"a", "b", "c"}...)
obs := []cos.Object{}
for _, v := range objects {
    obs = append(obs, cos.Object{Key: v})
}
opt := &cos.ObjectDeleteMultiOptions{
    Objects: obs,
    Boolean. Indicates whether the Quiet mode is enabled.
    True means Quiet mode is enabled, and False means Verbose mode is enabled. The default is False | No |
    // Quiet: true,
}

_, _, err := client.Object.DeleteMulti(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### Parameter Description

```go
type ObjectDeleteMultiOptions struct {
	Quiet   bool
	Objects []Object   
}
// Object stores object information
type Object struct {
	Key          string
    // Other parameters are not related to this API
}
```

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | --------- | ---- |
| Quiet | Boolean value determines whether to enable Quiet mode. For the response result, COS offers Verbose and Quiet modes: <br><li>Verbose mode returns the deletion result of each object<br><li>Quiet mode only returns information about object errors<br>If the value is true, Quiet mode is enabled; If the value is false, Verbose mode is enabled. The value is false by default. | Boolean | No |
| Objects | Provides the information of each target object to be deleted | List | Yes |
| Key | Destination object file name | String | Yes |

#### Returned Result

Attributes of the uploaded file:

```go
// ObjectDeleteMultiResult saves the DeleteMulti result
type ObjectDeleteMultiResult struct {	
	DeletedObjects []Object
	Errors         []struct {
		Key     string
		'Code': 'string',
		'Message': 'string'
	}
}
```

| Parameter Name | Description | Type |
| -------------- | ---------------------------------- | --------- |
| Object |DELETE | Information on the objects to be deleted | Container | Yes |
| Error| DeleteResult | Information on objects that have not been deleted in this operation | Container |
| Key | The path of the object that failed to be deleted | string |
| - - Code | Error code of the deletion failure | String |
| - - Message | Error message of the deletion failure | String |

## Multipart Operations

### Querying multipart upload

#### Feature

This API (List Multipart Uploads) is used to query in-progress multipart uploads in the specified bucket.

#### Method Prototype

```go
func (s *BucketService) ListMultipartUploads(ctx context.Context, opt *ListMultipartUploadsOptions) (*ListMultipartUploadsResult, *Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-list-multi-upload)
```go
_, _, err := client.Bucket.ListMultipartUploads(context.Background(), nil)
if err != nil {
    panic(err)
}
```

#### Parameter Description

```go
type ListMultipartUploadsOptions struct {
	Delimiter='string',
	EncodingType   string
	Prefix         string
	MaxUploads     int
	KeyMarker='string',
	UploadIdMarker='string',                                         
}
```

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| delimiter | The delimiter is a symbol. The delimiter is a symbol. The identical paths between `prefix` or, if no `prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix  | String | No |
| EncodingType | Specifies the encoding method of the return value; value range: url | String | No |
| prefix | The returned Object key must be prefixed with Prefix. Note that the returned key will still contain Prefix when querying with prefix. | NSString * | No |
| max-uploads | Sets the maximum number of multipart uploads returned. Value range: [1, 1,000]. Default value: 1,000 | String | No |
| key-marker | Used together with `upload-id-marker`. <Br>If `upload-id-marker` is not specified, only the multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed; <Br/>If `upload-id-marker` is specified, the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed, and any multipart upload whose `ObjectName` lexicographically equals `key-marker` and whose `UploadID` is greater than `upload-id-marker` will also be listed | String | No |
| upload-id-marker | Used together with `key-marker`. <Br>If `key-marker` is not specified, `upload-id-marker` will be ignored; <Br/>If `key-marker` is specified, the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed, and any multipart upload whose `ObjectName` lexicographically equals `key-marker` and whose `UploadID` is greater than `upload-id-marker` will also be listed | String | No |


#### Returned Result

```go
// ListMultipartUploadsResult saves ListMultipartUploads results
type ListMultipartUploadsResult struct {
	Bucket             string
	EncodingType       string
	KeyMarker          string
	UploadIDMarker     string
    'NextKeyMarker': 'string',
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
// Use the same type as the owner
type Initiator Owner
// Owner defines the Bucket/Object's owner
type Owner struct {
	ID          string
	DisplayName string
}
```

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | --------- |
| Bucket | Target bucket for multipart upload, format is BucketName. For example, examplebucket-1250000000 | string |
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | string |
| - KeyMarker | The key value where the entry list starts | String |
| - UploadIdMarker | The `UploadId` value where the entry list starts | String |
| - NextKeyMarker | If the returned list is truncated, the `NextKeyMarker` returned will be the starting point of the subsequent list | String |
| - NextUploadIdMarker | If the returned list is truncated, the `UploadId` returned will be the starting point of the subsequent list | String |
| MaxUploads | The maximum number of returned multipart uploads. It defaults to 1000. | int |
| IsTruncated | Indicates whether the returned parts are truncated | bool |
| Uploads | Information for each upload | Container |
| - - Key | Object name | String |
| - UploadId | Identifies the ID of this multipart upload | String |
| Key | Indicates whether the returned parts are truncated | bool |
| - - StorageClass | Indicates part storage class; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String |
| Initiator | Indicates information about the initiator of this upload | Container |
| Owner | Indicates information about the owner of these parts | Container |
| - - Initiated | Starting time of the multipart upload | String |
| prefix | The returned Object key must be prefixed with Prefix. Note that the returned key will still contain Prefix when querying with prefix. | NSString * | No |
| delimiter | The delimiter is a symbol. The delimiter is a symbol. The identical paths between `prefix` or, if no `prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix  | String | No |
| - CommonPrefixes | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | ObjectArray |
| ID | Unique CAM ID of users | string |
| DisplayName | User Identifier (UIN) | string |

### Uploading the object via multipart upload

This includes the following operations:

- Multipart upload objects: Initializing multipart upload, uploading parts, and completing all multipart uploads
- Delete the part uploaded

> Uploading the object via multipart upload, you can also use [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) to upload (recommended).

### <span id = "INIT_MULIT_UPLOAD"> Initializing multipart upload</span>

#### Feature

Initializing multipart upload, obtaining corresponding uploadId (Initiate Multipart Upload).

#### Method Prototype

```go
func (s *ObjectService) InitiateMultipartUpload(ctx context.Context, name string, opt *InitiateMultipartUploadOptions) (*InitiateMultipartUploadResult, *Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-init-multi-upload)
```go
name := "exampleobject"
We recommend you not to set permissions on individual files when uploading so as to avoid reaching the limit. Bucket permission sets the default limit.
v, _, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil)
if err != nil {
    panic(err)
}
UploadId=uploadid,
```

#### Parameter Description

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
	CacheControl='string', 
	ContentDisposition='string', 
	ContentEncoding='string', 
	ContentType='string', 
	'ContentLength' => 'int',   
	'Expires' => 'string', 
	Custom x-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}

```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r | The content of the uploaded file, which can be a file stream or a byte stream. When r is not bytes.Buffer/bytes.Reader/strings.Reader, opt.ObjectPutHeaderOptions.ContentLength must be specified. | io.Reader | Yes |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| XCosACL | Sets file ACL, such as private，public-read | string | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="[OwnerUin]"` | String | No |
| GrantRead | Grants the grantee the read permission in the format of id="[OwnerUin]" | String | No |
| StorageClass | Sets the object storage class; value range: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | String | No |
| Expires | Sets Content-Expires. | string | No |
| CacheControl | Cache policy. Sets Cache-Control. | string | No |
| ContentType | Content Type. Sets Content-Type. | string | No |
| ContentDisposition | File name. Sets Content-Disposition. | string | No |
| ContentEncoding | Encoding format. Sets Content-Encoding. | string | No |
| ContentLength | Sets transmission length | string | No |
| XCosMetaXXX | User-defined file meta information. It must start with x-cos-meta. Otherwise, it will be ignored. | http.Header | No |

#### Returned Result

```go
<InitiateMultipartUploadResult>
	Bucket   string
	Key      string
	UploadID string
} 
```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| UploadId | Indicates the ID of multipart upload | string |
| Bucket | Bucket name, which is in a format of bucket-appid | string |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |

### <span id = "MULIT_UPLOAD_PART"> Uploading parts</span>

This API (Upload Part) is used to upload a part.

#### Method Prototype

```go
func (s *ObjectService) UploadPart(ctx context.Context, key, uploadID string, partNumber int, r io.Reader, opt *ObjectUploadPartOptions) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-upload-part)
```go
# Note: The maximum number of parts to be uploaded is 10,000.
$key = "exampleobject";
f := strings.NewReader("test")
"opt" is optional.
resp, err := client.Object.UploadPart(
    context.Background(), key, UploadID, 1, f, nil,
)
if err != nil {
    panic(err)
}
PartETag = resp.Header.Get("ETag")
```

#### Parameter Description

```go
type ObjectUploadPartOptions struct {
    'ContentLength' => 'int',
}
```

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | --------- | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| UploadId | Indicates the ID of multipart upload, which is generated by InitiateMultipartUpload. | string | Yes |
| PartNumber | Indicates the number of the uploaded part | int | Yes |
| r | The content of the uploaded part, which can be a local file stream or an input stream. When r is not bytes.Buffer/bytes.Reader/strings.Reader, opt.ContentLength must be specified. | io.Reader | Yes |
| ContentLength | Sets transmission length. | int | No |

#### Returned Result

```go
{
    'ETag': 'string'
}

```

| Parameter Name | Description | Type |
| -------- | ----------------- | ------ |
| ETag | MD5 of the uploaded part | string |



### <span id = "LIST_MULIT_UPLOAD"> Querying uploaded parts</span>

#### Feature

This API (List Parts) is used to query the uploaded parts in a specific multipart upload process.

#### Method Prototype

```go
func (s *ObjectService) ListParts(ctx context.Context, name, uploadID string, opt *ObjectListPartsOptions) (*ObjectListPartsResult, *Response, error)

```

#### Request Samples

[//]: # (.cssg-snippet-list-parts)
```go
$key = "exampleobject";
_, _, err := client.Object.ListParts(context.Background(), key, UploadID, nil)
if err != nil {
    panic(err)
}
```

#### Parameter Description

```go
type ObjectListPartsOptions struct {
	EncodingType     string
	MaxParts         string
	PartNumberMarker string                                      
}
```

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| UploadId | Indicates the ID of multipart upload, which is generated by InitiateMultipartUpload. | string | Yes |
| EncodingType | Specifies the encoding type of the returned value | String | No |
| MaxParts | Maximum number of entries returned at a time. Default is 1,000. | String | No |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting from the marker | String | No |

#### Returned Result

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
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
| EncodingType | Indicates the encoding method of the returned value. The value is not encoded by default. Available value: url | string |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| UploadId | Indicates the ID of multipart upload, which is generated by InitiateMultipartUpload. | string |
| Initiator | Creator of the multipart upload, including DisplayName, UIN and ID | struct |
| Owner | Information of the file owner, including DisplayName, UIN and ID | struct |
| StorageClass | Sets the object storage class; value range: STANDARD, STANDARD_IA, ARCHIVE. Default value: STANDARD | String | No |
| PartNumberMarker | Indicates that the parts are listed from the one following PartNumberMarker. It defaults to 0, which means the parts are listed from the first one. | String |
| NextPartNumberMarker | Marks the starting point of the next list of parts | int |
| MaxParts | The maximum number of returned parts. It defaults to 1000. | int |
| IsTruncated | Indicates whether the returned parts are truncated | bool |
| Part | Information of the uploaded part, including ETag, PartNumber, Size, and LastModified | struct |



### <span id = "COMPLETE_MULIT_UPLOAD">Completing multipart upload</span>

#### Feature

This API (Complete Multipart Upload) is used to complete the entire multipart upload.

#### Method Prototype

```go
func (s *ObjectService) CompleteMultipartUpload(ctx context.Context, key, uploadID string, opt *CompleteMultipartUploadOptions) (*CompleteMultipartUploadResult, *Response, error)

```

#### Request Samples

[//]: # (.cssg-snippet-complete-multi-upload)
```go
# Complete the multipart upload
$key = "exampleobject";
UploadId=uploadid

opt := &cos.CompleteMultipartUploadOptions{}
opt.Parts = append(opt.Parts, cos.Object{
	PartNumber: 1, ETag: PartETag},
)

_, _, err := client.Object.CompleteMultipartUpload(
	context.Background(), key, uploadID, opt,
)
if err != nil {
	panic(err)
}
```

#### Parameter Description

```go
type CompleteMultipartUploadOptions struct {
	Parts   []Object 
}
type Object struct { 
	'ETag': 'string', 
	PartNumber   int     
}
```

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| UploadId | Indicates the ID of multipart upload, which is generated by InitiateMultipartUpload. | string | Yes |
| CompleteMultipartUploadOptions | ETag and PartNumber information for all parts | struct | Yes |

#### Returned Result

```go
<CompleteMultipartUploadResult>
	Location string
	Bucket   string
	Key      string
	ETag     string
}

```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Location | URL address | string |
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| ETag | The unique tag of the resulting object. It is not the MD5 check value for the object content, but is only used to check the uniqueness of the object. To verify the file content, you can check the ETag of each part during the process of upload. | string |

### <span id = "ABORT_MULIT_UPLOAD"> Terminating multipart upload</span>

#### Feature

This API (Abort Multipart Upload) is used to abort a multipart upload operation and delete the uploaded parts.

#### Method Prototype

```go
func (s *ObjectService) AbortMultipartUpload(ctx context.Context, key, uploadID string) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-abort-multi-upload)
```go
$key = "exampleobject";
Abort
_, err := client.Object.AbortMultipartUpload(context.Background(), key, UploadID)
if err != nil {
    panic(err)
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| UploadId | Indicates the ID of multipart upload | string | Yes |

## Other Operations

### Restoring an archived object 

#### Feature

This API (POST Object restore) is used to restore an archived object.

#### Method Prototype

```go
func (s *ObjectService) PostRestore(ctx context.Context, key string, opt *ObjectRestoreOptions) (*Response, error) 
```

#### Request Samples

[//]: # (.cssg-snippet-restore-object)
```go
key := "example_restore"
f, err := os.Open("../test")
if err != nil {
    panic(err)
}
opt := &cos.ObjectPutOptions{
    ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
        ContentType:      "text/html",
        XCosStorageClass: "ARCHIVE", //Archive type
    },
    ACLHeaderOptions: &cos.ACLHeaderOptions{
        We recommend you not to set permissions on individual files when uploading so as to avoid reaching the limit. Bucket permission sets the default limit.
        XCosACL: "private",
    },
}
// Uploading an archived object
_, err = client.Object.Put(context.Background(), key, f, opt)
if err != nil {
    panic(err)
}

opts := &cos.ObjectRestoreOptions{
    Days: 2,
    Tier: &cos.CASJobParameters{
        // Standard, Exepdited and Bulk
        Tier: 'Expedited'
    },
}
### Restoring an archived object
_, err = client.Object.PostRestore(context.Background(), key, opts)
if err != nil {
    panic(err)
}
```

#### Parameter Description

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
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| ObjectRestoreOptions | Describes rules for retrieved temporary files | struct | Yes |
| Days | Describes the expiration time of the temporary object | int | Yes |
| CASJobParameters | Describes the configuration of the restoration type | struct | No |
| Tier | Describes the mode for retrieving temporary files. Possible values are "Expedited", "Standard", and "Bulk", which correspond to speed mode, standard mode, and batch mode | string | No |

### Setting object ACL

#### Feature

This API (Put Object ACL) is used to set an ACL for an object.

#### Method Prototype

```go
func (s *ObjectService) PutACL(ctx context.Context, key string, opt *ObjectPutACLOptions) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-put-object-acl)
```go
// 1. Configuration via request header
opt := &cos.ObjectPutACLOptions{
    Header: &cos.ACLHeaderOptions{
        XCosACL: "private",
    },
}
$key = "exampleobject";
_, err := client.Object.PutACL(context.Background(), key, opt)
if err != nil {
    panic(err)
}
// 2. Configuration via request body
opt = &cos.ObjectPutACLOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            "ID": "qcs::cam::uin/100000000001:uin/100000000001",
        },
        AccessControlList: []cos.ACLGrant{
            {
                Grantee: &cos.ACLGrantee{
                    Type: "RootAccount",
                    "ID": "qcs::cam::uin/100000000001:uin/100000000001",
                },

                Permission: "FULL_CONTROL",
            },
        },
    },
}

_, err = client.Object.PutACL(context.Background(), key, opt)
if err != nil {
    panic(err)
}
```

#### Parameter Description

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
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| XCosACL | Sets object ACL, such as private, public-read | string | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="[OwnerUin]"` | String | No |
| GrantRead | Grants the grantee the read permission in the format of id="[OwnerUin]" | String | No |
| ACLXML | Grants the specified account the access to buckets. For more information on the format, see the response for "get object acl". | struct | No |

### Querying object ACL

#### Feature

This API (GET Object acl) is used to query object (or file) ACL.

#### Method Prototype

```go
func (s *ObjectService) GetACL(ctx context.Context, key string) (*ObjectGetACLResult, *Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-get-object-acl)
```go
$key = "exampleobject";
_, _, err := client.Object.GetACL(context.Background(), key)
if err != nil {
    panic(err)
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |

#### Returned Result

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
| Owner | Information of the bucket owner, including DisplayName and ID | struct |
| AccessControlList | Information of the user granted the bucket permissions, including Grantee and Permission | struct |
| Grantee | Information of grantee, including DisplayName, Type, ID and UIN | struct |
| Type | Type of grantee: CanonicalUser or Group | string |
| ID | ID of grantee when Type is CanonicalUser | string |
| DisplayName | Name of grantee | string |
| UIN | UIN of grantee when Type is Group | string |
| Permission | Bucket permissions of grantee. Available values: FULL_CONTROL (read and write permissions), WRITE (write permission), and READ (read permission) | string |



## Advanced APIs (Recommended)

### Uploading an object

#### Feature

The upload API automatically divides the data based on the length of the user file to facilitate usage, and the user does not need to worry about every step of the multipart upload.

#### Method Prototype

```go
func (s *ObjectService) Upload(ctx context.Context, key string, filepath string, opt *MultiUploadOptions) (*CompleteMultipartUploadResult, *Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-transfer-upload-object)
```go
$key = "exampleobject";
file := "../test"

_, _, err := client.Object.Upload(
    context.Background(), key, file, nil,
)
if err != nil {
    panic(err)
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| filepath | Name of the local file | string | Yes |
| opt | Object attributes | Struct | No |
| OptIni | Sets object attributes and ACL. For details, refer to [InitiateMultipartUploadOptions](#.E6.96.B9.E6.B3.95.E5.8E.9F.E5.9E.8B9) | Struct | No |
| PartSize | Size of parts, unit in MB, Go SDK automatically divides the parts if not specified by users or specified as partSize <= 0 | int | No |
| ThreadPoolSize | Size of the thread pool, default size is 1 | int | No |

#### Returned Result

```go
<CompleteMultipartUploadResult>
	Location string
	Bucket   string
	Key      string
	ETag     string
}

```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Location | URL address | string |
String bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| ETag | The unique tag of the resulting object. It is not the MD5 check value for the object content, but is only used to check the uniqueness of the object. To verify the file content, you can check the ETag of each part during the process of upload. | string |
