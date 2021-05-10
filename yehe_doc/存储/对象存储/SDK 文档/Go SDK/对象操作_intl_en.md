## Overview

This document provides an overview of APIs and SDK code samples related to simple operations, multipart operations, and other object operations.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Object)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying an object list | Queries some or all objects in a bucket |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Gets object metadata | Gets the meta information of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object (file) to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies an object to a destination path |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Object](https://cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket |

**Multipart upload operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart upload operations |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload operation | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading a part | Uploads a part in a multipart upload |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of an entire file |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload operation | Aborts a multipart upload operation and deletes the uploaded parts |

**Other operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores archived object for access |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for an object (file) in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object (file) |

## Simple Operations

### Querying an object list

#### API description

This API is used to query some or all objects in a bucket.

#### Method prototype

```go
func (s *BucketService) Get(ctx context.Context, opt *BucketGetOptions) (*BucketGetResult, *Response, error)
```

#### Sample request 

[//]: # (.cssg-snippet-get-bucket)
```go
opt := &cos.BucketGetOptions{
    Prefix:  "test",
    MaxKeys: 100,
}
_, _, err := client.Bucket.Get(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### Parameter description

```go
type BucketGetOptions struct {
	Prefix       string 
	Delimiter    string 
	EncodingType string 
	Marker       string 
	MaxKeys      int    
}
```

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Prefix | Filters object keys prefixed with the value of this parameter. It is left empty by default. | string | No |
| Delimiter | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | string | No |
| EncodingType | Specifies the encoding method of the returned value. It is left empty by default. Valid value: url. | string | No |
| Marker | Specifies the object after which the listing should begin. Objects are listed using UTF-8 binary order by default. | string | No |
| MaxKeys | Maximum number of returned objects. It defaults to 1000. | int | No |

#### Response description

```go
type BucketGetResult struct {
	Name           string
	Prefix         string 
	Marker         string 
	NextMarker     string 
	Delimiter='string', 
	MaxKeys        int
	IsTruncated    bool
	Contents       []Object 
	CommonPrefixes []string 
	EncodingType   string   
}
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | -------- |
| Name           | Bucket name in the format: BucketName-APPID, e.g. examplebucket-1250000000. | string   |
| Prefix | Filters the object keys prefixed with the value of this parameter. It is left empty by default. | string   |
| Marker | Specifies the object after which the listing should begin. Objects are listed using UTF-8 binary order by default. | string |
| NextMarker | Specifies the object after which the next listing should begin if IsTruncated is `true`. | string |
| Delimiter | A separator which is left empty by default. For example, you can specify it as `/` to indicate folders. | string |
| MaxKeys | Maximum number of returned objects. It defaults to 1000. | int |
| IsTruncated | Indicates whether the returned objects are truncated | bool |
| Contents | Lists metadata of all objects, including ETag, StorageClass, Key, Owner, LastModified, and Size. | []Object |
| CommonPrefixes | All keys starting with Prefix and ending with Delimiter are grouped as a common prefix. | []string |
| EncodingType | Specifies the encoding method of the returned value. It is left empty by default. Valid value: url. | string |

### Uploading an object using simple upload

#### API description

This API (PUT Object) is used to upload an object (file) of up to 5 GB to a bucket. For objects larger than 5 GB, please use [multipart upload](#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1) or [advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89). Simple uploads, creating folders, and batch uploads are supported.


#### Method prototype

```go
func (s *ObjectService) Put(ctx context.Context, key string, r io.Reader, opt *ObjectPutOptions) (*Response, error)
```

#### Sample 1. Uploading an object

[//]: # (.cssg-snippet-put-object)
```go	
key := "exampleobject"
f, err := os.Open("../test")
opt := &cos.ObjectPutOptions{
    ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
        ContentType: "text/html",
    },
    ACLHeaderOptions: &cos.ACLHeaderOptions{
        // Considering the ACL limit, we recommend not setting an object ACL when uploading an object unless required. The object will then inherit the bucket ACL by default.
        XCosACL: "private",
    },
}
_, err = client.Object.Put(context.Background(), key, f, opt)
if err != nil {
    panic(err)
}
```
#### Sample 2. Creating a folder
```go
// Folder name
name := "folder/"
// Transfer an input stream whose size is 0.
_, err := c.Object.Put(context.Background(), name, strings.NewReader(""), nil)
if err != nil {
	// ERROR
}
```
#### Sample 3. Uploading objects with multiple threads
```
func upload(wg *sync.WaitGroup, c *cos.Client, files <-chan string) {
    defer wg.Done()
    for file := range files {
        name := "folder/" + file
	fd, err := os.Open(file)
        if err != nil {
            //ERROR
            continue
        }
        _, err = c.Object.Put(context.Background(), name, fd, nil)
        if err != nil {
            //ERROR
        }
    }
}
func main() {
        u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
        b := &cos.BaseURL{BucketURL: u}
        c := cos.NewClient(b, &http.Client{
                Transport: &cos.AuthorizationTransport{
                        SecretID:  os.Getenv("COS_SECRETID"),
                        SecretKey: os.Getenv("COS_SECRETKEY"),
                },
        })
	// Upload files with multiple threads
        filesCh := make(chan string, 2)
        filePaths := []string{"test1", "test2", "test3"}
        var wg sync.WaitGroup
        threadpool := 2
        for i := 0; i < threadpool; i++ {
                wg.Add(1)
                go upload(&wg, c, filesCh)
        }
        for _, filePath := range filePaths {
                filesCh <- filePath
        }
        close(filesCh)
        wg.Wait()
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
	CacheControl       string 
	ContentDisposition string 
	ContentEncoding    string 
	ContentType        string 
	ContentLength      int64  
	Expires            string 
	Custom x-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}
```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r | The content of the uploaded file, which can be a file stream or a byte stream. When r is not bytes.Buffer/bytes.Reader/strings.Reader, opt.ObjectPutHeaderOptions.ContentLength must be specified. | io.Reader | Yes |
| key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| XCosACL | Sets the file ACL, such as private, public-read, and public-read-write. | string | No |
| XCosGrantFullControl | Grants full permission in the format: `id="[OwnerUin]"` | string | No |
| XCosGrantRead | Grants read permission in the format: id="[OwnerUin]" | string | No |
| XCosStorageClass | Sets the object storage class. Valid values: STANDARD (default), STANDARD_IA, ARCHIVE. | string | No |
| Expires | Sets Content-Expires. | string | No |
| CacheControl | Cache policy. Sets Cache-Control. | string | No |
| ContentType | Content Type. Sets Content-Type. | string | No |
| ContentDisposition | File name. Sets Content-Disposition. | string | No |
| ContentEncoding | Encoding format. Sets Content-Encoding. | string | No |
| ContentLength | Sets the length of the request content. | int64 | No |
| XCosMetaXXX | User-defined file metadata. It must start with x-cos-meta. Otherwise, it will be ignored. | http.Header | No |

#### Response description

```go
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```
Return Response class.
```go
resp, err := client.Object.Put(context.Background(), key, f, nil)
etag := resp.Header.Get("ETag")
exp := resp.Header.Get("x-cos-expiration")
```
| Parameter | Description | Type |
| ---------------- | -------------------------------- | ------ |
| ETag | MD5 checksum of the uploaded file  | string |
| x-cos-expiration | Returns the file expiration rule if a lifecycle is configured. | string |

### Querying object metadata

#### API description

The API is used to query object metadata.

#### Method prototype

```go
func (s *ObjectService) Head(ctx context.Context, key string, opt *ObjectHeadOptions) (*Response, error)
```

#### Sample request 

[//]: # (.cssg-snippet-head-object)
```go
key := "exampleobject"
_, err := client.Object.Head(context.Background(), key, nil)
if err != nil {
    panic(err)
}
```

#### Parameter description

```go
type ObjectHeadOptions struct {
	IfModifiedSince string 
}
```

| Parameter | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| IfModifiedSince | Returned only if the object has been modified after the specified time | string | No |

#### Response description

```go
{
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```
Return Response class.
```go
resp, err := client.Object.Head(context.Background(), key, nil)
contentType := resp.Header.Get("Content-Type")
contentLength := resp.Header.Get("Content-Length")
etag := resp.Header.Get("ETag")
reqid := resp.Header.Get("X-Cos-Request-Id")

```

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| Metadata | Includes both predefined object metadata, including Etag and X-Cos-Request-Id, and custom object metadata. | string |

### Downloading an object

#### API description

This API (GET Object) is used to download an object (file) to a local file system. Simple downloads and batch downloads are supported.

#### Method prototype

```go
func (s *ObjectService) Get(ctx context.Context, key string, opt *ObjectGetOptions) (*Response, error)

func (s *ObjectService) GetToFile(ctx context.Context, key, localfile string, opt *ObjectGetOptions) (*Response, error)
```

#### Sample 1. Downloading an object

[//]: # (.cssg-snippet-get-object)
```go
key := "exampleobject"
opt := &cos.ObjectGetOptions{
    ResponseContentType: "text/html",
    Range:               "bytes=0-3",
}
// "opt" is optional. It can be set to “nil” unless otherwise specified.
// 1. Obtain the object from the response body
resp, err := client.Object.Get(context.Background(), key, opt)
if err != nil {
    panic(err)
}
ioutil.ReadAll(resp.Body)
resp.Body.Close()

// 2. Download the object locally
_, err = client.Object.GetToFile(context.Background(), key, "example.txt", nil)
if err != nil {
    panic(err)
}
```
#### Sample 2. Downloading objects with multiple threads
```go
func download(wg *sync.WaitGroup, c *cos.Client, keysCh <-chan string) {
        defer wg.Done()
        for key := range keysCh {
                // Download the file to the current directory. Note that the filename does not contain its directory.
                _, filename := filepath.Split(key)
                _, err := c.Object.GetToFile(context.Background(), key, filename, nil)
                if err != nil {
                	// ERROR
                }
        }
}
func main() {
        u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
        b := &cos.BaseURL{BucketURL: u}
        c := cos.NewClient(b, &http.Client{
                Transport: &cos.AuthorizationTransport{
                        SecretID:  os.Getenv("COS_SECRETID"),
                        SecretKey: os.Getenv("COS_SECRETKEY"),
                },
        })
        keysCh := make(chan string, 2)
        keys := []string{"folder/exampleobject1", "folder/exampleobject2", "folder/exampleobject3"}
        var wg sync.WaitGroup
        threadpool := 2
        for i := 0; i < threadpool; i++ {
                wg.Add(1)
                go download(&wg, c, keysCh)
        }
        for _, key := range keys {
                keysCh <- key
        }
        close(keysCh)
        wg.Wait()
}
```
#### Parameter description

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

| Parameter | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| localfile | Name of the file downloaded to the local file system | string | Yes |
| ResponseContentType | Sets the Content-Type in the response header | string | No |
| ResponseContentLanguage | Sets the Content-Language in the response header | string | No |
| ResponseExpires | Sets the Content-Expires in the response header | string | No |
| ResponseCacheControl | Sets the Cache-Control in the response header | string | No |
| ResponseContentDisposition | Sets the Content-Disposition in the response header | string | No |
| ResponseContentEncoding | Sets the Content-Encoding in the response header | string | No |
| Range | Sets the range of bytes for the file to download in the format of bytes=first-last | string | No |
| IfModifiedSince | Returned only if the object has been modified after the specified time | string | No |

#### Response description

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
Return Response class.
```go
resp, err := client.Object.Get(context.Background(), key, nil)
body, _ := ioutil.ReadAll(resp.Body)
contentType := resp.Header.Get("Content-Type")
contentLength := resp.Header.Get("Content-Length")
etag := resp.Header.Get("ETag")
reqid := resp.Header.Get("X-Cos-Request-Id")

```
| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ---------- |
| Body | The content of the downloaded file | StreamBody |
| File meta information | The meta information of the downloaded file, including Etag and X-Cos-Request-Id. The meta information of the configured file is also returned. | string |

### Copying an object

This API (PUT Object-Copy) is used to copy files to the destination path.

#### Method prototype

```go
func (s *ObjectService) Copy(ctx context.Context, key, sourceURL string, opt *ObjectCopyOptions) (*ObjectCopyResult, *Response, error)
```

#### Sample 1. Copying an object

[//]: # (.cssg-snippet-copy-object)
```go
name := "exampleobject"
// Upload the source object
f := strings.NewReader("test")
_, err := client.Object.Put(context.Background(), name, f, nil)
assert.Nil(s.T(), err, "Test Failed")

sourceURL := fmt.Sprintf("%s/%s", client.BaseURL.BucketURL.Host, name)
dest := "example_dest"
// Considering the ACL limit, we recommend not setting an object ACL when uploading an object unless required. The object will then inherit the bucket ACL by default.
// opt := &cos.ObjectCopyOptions{}
_, _, err = client.Object.Copy(context.Background(), dest, sourceURL, nil)
if err != nil {
    panic(err)
}
```
#### Sample 2. Moving an object
```go
source := "test/oldfile"
f := strings.NewReader("test")
// Upload the object.
_, err := c.Object.Put(context.Background(), source, f, nil)
if err != nil {
    // Error
}

// Move the object.
dest := "test/newfile"
soruceURL := fmt.Sprintf("%s/%s", u.Host, source)
_, _, err := c.Object.Copy(context.Background(), dest, soruceURL, nil)
if err == nil {
	    _, err = c.Object.Delete(context.Background(), source, nil)
 	if err != nil {
 		// Error
 	}
}
```

#### Parameter description

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

| Parameter | Description | Type | Required |
| ------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| sourceURL | URL of the source file to copy | string | Yes |
| XCosACL | Sets the file ACL, such as private, public-read, and public-read-write | string | No |
| XCosGrantFullControl | Grants full permission in the format: `id="[OwnerUin]"` | string | No |
| XCosGrantRead| Grants the read permission in the format: id="[OwnerUin]" | string | No |
|  XCosMetadataDirective | Valid values:</br><li>`Copy`: copies the source object along with its metadata.</br><li>`Replaced`: copies the source object while replacing its metadata.</br>If the destination path is the same as the source path, this parameter must be set to `Replaced`. | string | Yes |
| XCosCopySourceIfModifiedSince | The operation is performed if the object is modified after the specified time; otherwise, error code 412 is returned. It can be used with `XCosCopySourceIfNoneMatch`. Using it with other conditions can cause a conflict. | string | No |
| XCosCopySourceIfUnmodifiedSince | The operation is performed if the object is unmodified after the specified time; otherwise, error code 412 is returned. It can be used with `XCosCopySourceIfMatch`. Using it with other conditions can cause a conflict. | string | No |
| XCosCopySourceIfMatch | The operation is performed if the Etag of the object is the same as the specified one, otherwise error code 412 is returned. It can be used with XCosCopySourceIfUnmodifiedSince. Using it with other conditions can cause a conflict. | string | No |
| XCosCopySourceIfNoneMatch | The operation is performed if the Etag of the object is different from the specified one, otherwise error code 412 is returned. It can be used with XCosCopySourceIfModifiedSince. Using it with other conditions can cause a conflict. | string | No |
| XCosStorageClass | Sets the object storage class. Valid values: STANDARD (default), STANDARD_IA, ARCHIVE. | string | No |
| XCosMetaXXX | User-defined file metadata. | http.Header | No |
| XCosCopySource | Source file URL. You can specify a historical version using the `versionid` sub-resource. | string | No |

#### Response description

Attributes of the uploaded file:

```go
type ObjectCopyResult struct {
    ETag         string 
    'LastModified': 'string',
}
```
| Parameter | Description | Type |
| ------------ | -------------------------- | ------ |
| ETag | MD5 of the copied file | string |
| LastModified | The last time that the copied file was modified | string |

### Deleting a single object

#### API description

This API is used to delete an object (folder) from a bucket.

#### Method prototype

```go
func (s *ObjectService) Delete(ctx context.Context, key string) (*Response, error)
```

#### Sample 1. Deleting an object

[//]: # (.cssg-snippet-delete-object)
```go
key := "exampleobject"
_, err := client.Object.Delete(context.Background(), key)
if err != nil {
    panic(err)
}
```

#### Sample 2. Deleting a folder
```go
key := "folder/"
_, err := c.Object.Delete(context.Background(), key)
if err != nil {
    panic(err)
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |

### Deleting multiple objects

#### API description

The API is used to delete multiple objects from a bucket. You can delete up to 1,000 objects in one request.

#### Method prototype

```go
func (s *ObjectService) DeleteMulti(ctx context.Context, opt *ObjectDeleteMultiOptions) (*ObjectDeleteMultiResult, *Response, error)
```

#### Sample request 

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
    // Boolean, which indicates whether to enable Quiet or Verbose mode.
    // “true” indicates Quiet mode while “false”, the default value, indicates Verbose mode.
    // Quiet: true,
}

_, _, err := client.Object.DeleteMulti(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### Parameter description

```go
type ObjectDeleteMultiOptions struct {
	Quiet   bool
	Objects []Object   
}
// “Object” stores object metadata
type Object struct {
	Key          string
    // Other parameters are not related to this API
}
```

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | --------- | ---- |
| Quiet | Indicates whether to enable Quiet or Verbose mode for the response result. Valid values:</br><li>`true`: enables the Verbose mode that returns the deletion result for each object<br><li>`false` (default): enables the Quiet mode that only returns information on objects that fail | Boolean | No |
| Objects | Describes each destination object to be deleted | Container | Yes |
| Key | Name of the destination object | String | Yes |

#### Response description

Attributes of the uploaded file:

```go
// “ObjectDeleteMultiResult” saves the DeleteMulti result
type ObjectDeleteMultiResult struct {	
	DeletedObjects []Object
	Errors         []struct {
		Key     string
		Code    string
		Message string
	}
}
```

| Parameter | Description | Type |
| -------------- | ---------------------------------- | --------- |
| DeletedObjects |Describes each object deleted | Container |
| Errors| Describes objects that failed to be deleted | Container |
| Key | Names of the objects that failed to be deleted | string |
| Code | Error code for the deletion failure | string |
| Message | Error message for the deletion failure | string |

## Multipart operations

### Querying multipart upload operations

#### API description

This API is used to query in-progress multipart uploads in a specified bucket.

#### Method prototype

```go
func (s *BucketService) ListMultipartUploads(ctx context.Context, opt *ListMultipartUploadsOptions) (*ListMultipartUploadsResult, *Response, error)
```

#### Sample request 

[//]: # (.cssg-snippet-list-multi-upload)
```go
_, _, err := client.Bucket.ListMultipartUploads(context.Background(), nil)
if err != nil {
    panic(err)
}
```

#### Parameter description

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

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| Delimiter | A symbol. The identical paths between `Prefix` and the first occurrence of the `Delimiter` are grouped and defined as a common prefix. If no `Prefix` is specified, the common prefix starts with the beginning of the path | string | No |
| encodingType | Specifies the encoding type of returned values; valid value: `url` | string |No |
| prefix | Specifies that returned object keys must be prefixed with this value. Note that if you use this parameter, returned keys will contain the prefix | string |No |
| MaxUploads | Sets the maximum number of multipart uploads that can be returned at a time. Value range: 1−1000. Defaults to `1000`. | int | No |
| KeyMarker | This parameter is used together with `upload-id-marker`: </li><li>If `upload-id-marker` is not specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed.</li><li>If `upload-id-marker` is specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed, and multipart uploads whose `ObjectName` is lexicographically equal to `key-marker` with `UploadID` greater than `upload-id-marker` will be listed. | string | No |
| UploadIDMarker | This parameter is used together with `key-marker`: </li><li>If `key-marker` is not specified, `upload-id-marker` will be ignored. </li><li>If `key-marker` is specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed, and multipart uploads whose `ObjectName` is lexicographically equal to `key-marker` with `UploadID` greater than `upload-id-marker` will be listed. | string | No |


#### Response description

```go
// ListMultipartUploadsResult saves ListMultipartUploads results
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
// Use the same type as the owner
type Initiator Owner
// “Owner” defines the bucket/object's owner
type Owner struct {
	ID          string
	DisplayName string
}
```

| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | --------- |
| Bucket | Destination bucket for multipart upload in the format of BucketName, e.g. examplebucket-1250000000 | string |
| EncodingType | Specifies the encoding method of the returned value. It is left empty by default. Valid value: url | string |
| KeyMarker | Specifies the key after which the listing should begin | string |
|UploadIDMarker | Specifies the uploadId after which the listing should begin | string |
| NextKeyMarker | Specifies the key after which the next listing should begin if the returned list is truncated | string |
| NextUploadIdMarker | Specifies the uploadId after which the next listing should begin if the returned list is truncated | string |
| MaxUploads | The maximum number of returned multipart uploads. It defaults to 1000. | string    |
| IsTruncated | Indicates whether the returned list is truncated | bool |
| Uploads | Information on each upload | Container |
| Key | Object name | string |
| UploadID | ID that identifies the multipart upload | string |
| Key | Indicates whether the returned list is truncated | bool |
| StorageClass | Specifies the storage class for parts. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | string |
| Initiator | Indicates information about the initiator of this upload | Container |
| Owner | Indicates information about the owner of these parts | Container |
| Initiated | Start time of the multipart upload | string |
| Prefix | Specifies that returned object keys must be prefixed with this value. Note that if you use this parameter, returned keys will contain the prefix | struct    |
| Delimiter | A symbol. The identical paths between `Prefix` and the first occurrence of the `Delimiter` are grouped and defined as a common prefix. If no `Prefix` is specified, the common prefix starts with the beginning of the path | string |
| CommonPrefixes | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | string    |
| ID | Unique CAM ID of users | string |
| DisplayName | User Identifier (UIN) | string |


### Multipart upload operations

Operations related to multipart upload include the following:

- Multipart upload: initializing a multipart upload operation, uploading parts, and completing a multipart upload operation
- Deleting uploaded parts.

>?To perform a multipart upload operation, you can also use the [advanced upload API](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) (recommended).


<span id="INIT_MULIT_UPLOAD"></span>
###  Initializing a multipart upload 

#### API description

This API (Initiate Multipart Upload) is used to initialize a multipart upload operation and get its `UploadID`.

#### Method prototype

```go
func (s *ObjectService) InitiateMultipartUpload(ctx context.Context, name string, opt *InitiateMultipartUploadOptions) (*InitiateMultipartUploadResult, *Response, error)
```

#### Sample request 

[//]: # (.cssg-snippet-init-multi-upload)
```go
name := "exampleobject"
// Optional. Considering the ACL limit, we recommend not setting an object ACL when uploading an object unless required. The object will then inherit bucket ACL by default.
v, _, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil)
if err != nil {
    panic(err)
}
UploadID = v.UploadID
```

#### Parameter description

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
	ContentLength      int64   
	Expires            string 
	Custom x-cos-meta-* header
	XCosMetaXXX        *http.Header 
	XCosStorageClass   string      
}

```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| XCosACL | Sets the file ACL, such as private，public-read | string | No |
| XCosGrantFullControl | Grants full permission in the format: `id="[OwnerUin]"` | string | No |
| XCosGrantRead | Grants read permission in the format: id="[OwnerUin]" | string | No |
| XCosStorageClass | Sets the object storage class. Valid values: STANDARD (default), STANDARD_IA, ARCHIVE. | string | No |
| Expires | Sets Content-Expires. | string | No |
| CacheControl | Cache policy. Sets Cache-Control. | string | No |
| ContentType | Content Type. Sets Content-Type. | string | No |
| ContentDisposition | File name. Sets Content-Disposition. | string | No |
| ContentEncoding | Encoding format. Sets Content-Encoding. | string | No |
| ContentLength | Sets the length of the request content. | int64 | No |
| XCosMetaXXX | User-defined file metadata. It must start with x-cos-meta. Otherwise, it will be ignored. | http.Header | No |

#### Response description

```go
type InitiateMultipartUploadResult struct {
	Bucket   string
	Key      string
	UploadID string
} 
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| UploadId | ID that identifies the multipart upload | string |
| Bucket | Bucket name in the format: `BucketName-APPID` | string |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string |


<span id="MULIT_UPLOAD_PART"></span>
###  Uploading a part 

This API (Upload Part) is used to upload parts in a multipart upload.

#### Method prototype

```go
func (s *ObjectService) UploadPart(ctx context.Context, key, uploadID string, partNumber int, r io.Reader, opt *ObjectUploadPartOptions) (*Response, error)
```

#### Sample request 

[//]: # (.cssg-snippet-upload-part)
```go
// Note: Up to 10,000 parts can be uploaded.
key := "exampleobject"
f := strings.NewReader("test hello")
// "opt" is optional.
resp, err := client.Object.UploadPart(
    context.Background(), key, UploadID, 1, f, nil,
)
if err != nil {
    panic(err)
}
PartETag = resp.Header.Get("ETag")
```

#### Parameter description

```go
type ObjectUploadPartOptions struct {
    ContentLength   int64
}
```

| Parameter | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | --------- | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| UploadId | ID that identifies the multipart upload; generated by InitiateMultipartUpload | string | Yes |
| PartNumber | Number that identifies the uploaded part | int | Yes |
| r | The content of the uploaded part, which can be a local file stream or an input stream. When r is not bytes.Buffer/bytes.Reader/strings.Reader, opt.ContentLength must be specified. | io.Reader | Yes |
| ContentLength | Sets the length of the request content. | int64 | No |

#### Response description

```go
{
    'ETag': 'string'
}
```
Return Response class.
```go
resp, err := client.Object.UploadPart(context.Background(), key, UploadID, 1, f, nil)
etag := resp.Header.Get("ETag")
```
| Parameter | Description | Type |
| -------- | ----------------- | ------ |
| ETag | MD5 of the uploaded part | string |


<span id = "LIST_MULIT_UPLOAD"></span>
###  Querying uploaded parts 

#### API description

This API (List Parts) is used to query the uploaded parts of a multipart upload.

#### Method prototype

```go
func (s *ObjectService) ListParts(ctx context.Context, name, uploadID string, opt *ObjectListPartsOptions) (*ObjectListPartsResult, *Response, error)

```

#### Sample request 

[//]: # (.cssg-snippet-list-parts)
```go
key := "exampleobject"
_, _, err := client.Object.ListParts(context.Background(), key, UploadID, nil)
if err != nil {
    panic(err)
}
```

#### Parameter description

```go
type ObjectListPartsOptions struct {
	EncodingType     string
	MaxParts         string
	PartNumberMarker string                                      
}
```

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| UploadId | ID that identifies the multipart upload; generated by InitiateMultipartUpload | string | Yes |
| EncodingType | Specifies the encoding type of the returned value | string | No |
| MaxParts | Maximum number of parts to return at a time. Defaults to `1000`. | string | No |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting with the part number after the marker | string | No |

#### Response description

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

| Parameter | Description | Type |
| -------------------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket name in the format: BucketName-APPID, e.g. examplebucket-1250000000. | string |
| EncodingType | Specifies the encoding method of the returned value. It is left empty by default. Valid value: url | string |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string |
| UploadId | ID that identifies the multipart upload; generated by InitiateMultipartUpload | string |
| Initiator | Initiator information on the multipart upload, including DisplayName, UIN and ID | struct |
| Owner | Information on the file owner, including DisplayName, UIN and ID | struct |
| StorageClass | Sets the object storage class. Valid values: STANDARD (default), STANDARD_IA, ARCHIVE. | string |
| PartNumberMarker | Specifies the part number after which the listing should begin. It defaults to 0, which means the listing begins with the first part | string |
| NextPartNumberMarker | Specifies the part number after which the next listing should begin | int |
| MaxParts | The maximum number of returned parts. It defaults to 1000. | int |
| IsTruncated | Indicates whether the returned list is truncated | bool |
| Part | Information on the uploaded part, including ETag, PartNumber, Size, and LastModified | struct |


<span id = "COMPLETE_MULIT_UPLOAD"></span>
###  Completing a multipart upload 

#### API description

This API (Complete Multipart Upload) is used to complete the multipart upload of the entire file.

#### Method prototype

```go
func (s *ObjectService) CompleteMultipartUpload(ctx context.Context, key, uploadID string, opt *CompleteMultipartUploadOptions) (*CompleteMultipartUploadResult, *Response, error)

```

#### Sample request 

[//]: # (.cssg-snippet-complete-multi-upload)
```go
// Complete the multipart upload.
key := "exampleobject"
uploadID := UploadID

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

#### Parameter description

```go
type CompleteMultipartUploadOptions struct {
	Parts   []Object 
}
type Object struct { 
	'ETag': 'string', 
	PartNumber   int     
}
```

| Parameter | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| UploadId | ID that identifies the multipart upload; generated by InitiateMultipartUpload | string | Yes |
| CompleteMultipartUploadOptions | ETag and PartNumber for all parts | struct | Yes |

#### Response description

```go
type CompleteMultipartUploadResult struct {
	Location string
	Bucket   string
	Key      string
	ETag     string
}

```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Location | URL address | string |
| Bucket        | Bucket name in the format: BucketName-APPID, e.g. examplebucket-1250000000. | string   |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| ETag | The unique tag of a merged object. This value does not represent the MD5 checksum of the object content, but is used only to verify the uniqueness of the object as a whole. To verify the object content, you can check the ETag of each part during the upload process | string |

<span id = "ABORT_MULIT_UPLOAD"></span>
###  Aborting a multipart upload 

#### API description

This API (Abort Multipart Upload) is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```go
func (s *ObjectService) AbortMultipartUpload(ctx context.Context, key, uploadID string) (*Response, error)
```

#### Sample request 

[//]: # (.cssg-snippet-abort-multi-upload)
```go
$key = "exampleobject";
// Abort
_, err := client.Object.AbortMultipartUpload(context.Background(), key, UploadID)
if err != nil {
    panic(err)
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| UploadId | ID that identifies the multipart upload | string |Yes |

## Other Operations

### Restoring an archived object 

#### API description

This (POST Object restore) API is used to restore an archived object for access.

#### Method prototype

```go
func (s *ObjectService) PostRestore(ctx context.Context, key string, opt *ObjectRestoreOptions) (*Response, error) 
```

#### Sample request 

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
        XCosStorageClass: "ARCHIVE", //ARCHIVE storage class
    },
    ACLHeaderOptions: &cos.ACLHeaderOptions{
        We recommend you not to set permissions on individual files when uploading so as to avoid reaching the limit. Bucket permission sets the default limit.
        XCosACL: "private",
    },
}
// Upload an object directly to ARCHIVE storage class
_, err = client.Object.Put(context.Background(), key, f, opt)
if err != nil {
    panic(err)
}

opts := &cos.ObjectRestoreOptions{
    Days: 2,
    Tier: &cos.CASJobParameters{
        // Standard, Expedited, and Bulk
        Tier: "Expedited",
    },
}
### Restoring an archived object
_, err = client.Object.PostRestore(context.Background(), key, opts)
if err != nil {
    panic(err)
}
```

#### Parameter description

```go
type ObjectRestoreOptions struct {        
    Days    int               
    Tier    *CASJobParameters 
}
type CASJobParameters struct {
    Tier    string 
}
```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| ObjectRestoreOptions | Describes rules for retrieved temporary files | struct | Yes |
| Days | Specifies the number of days before a temporary object expires | int | Yes |
| CASJobParameters |Specifies the restoration configuration | struct | No |
| Tier | Specifies the mode for retrieving temporary files. Valid values: "Expedited", "Standard", and "Bulk" | string | No |

### Setting an object ACL

#### API description

This API is used to set an ACL for an object.

#### Method prototype

```go
func (s *ObjectService) PutACL(ctx context.Context, key string, opt *ObjectPutACLOptions) (*Response, error)
```

#### Sample request 

[//]: # (.cssg-snippet-put-object-acl)
```go
// 1. Configuration via request header
opt := &cos.ObjectPutACLOptions{
    Header: &cos.ACLHeaderOptions{
        XCosACL: "private",
    },
}
key := "exampleobject"
_, err := client.Object.PutACL(context.Background(), key, opt)
if err != nil {
    panic(err)
}
// 2. Configuration using the request body
opt = &cos.ObjectPutACLOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            ID: "qcs::cam::uin/100000000001:uin/100000000001",
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

_, err = client.Object.PutACL(context.Background(), key, opt)
if err != nil {
    panic(err)
}
```

#### Parameter description

```go
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| XCosACL | Sets the object ACL, such as private, public-read | string | No |
| XCosGrantFullControl  | Grants full permission in the format: `id="[OwnerUin]"` | string | No |
| XCosGrantRead  | Grants read permission in the format: id="[OwnerUin]" | string | No |
| ACLXML | Grants the specified account bucket access permission. For more information on the format, see the response to the "GET object acl" request. | struct | No |

### Querying an object ACL

#### API description

This API is used to query the ACL of an object.

#### Method prototype

```go
func (s *ObjectService) GetACL(ctx context.Context, key string) (*ObjectGetACLResult, *Response, error)
```

#### Sample request 

[//]: # (.cssg-snippet-get-object-acl)
```go
key := "exampleobject"
_, _, err := client.Object.GetACL(context.Background(), key)
if err != nil {
    panic(err)
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |

#### Response description

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

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner | Information on the bucket owner, including DisplayName and ID | struct |
| AccessControlList | Information on the granted bucket permissions, including Grantee and Permission | struct |
| Grantee | Information on the grantees, including DisplayName, Type, ID and UIN | struct |
| Type | Type of grantee. Valid values: CanonicalUser and Group | string |
| ID | ID of the grantee if “Type” is set to `CanonicalUser` | string |
| DisplayName | Name of the grantee | string |
| UIN | UIN of the grantee when “Type” is set to `Group` | string |
| Permission | Bucket permission granted. Valid values: FULL_CONTROL (read and write), WRITE, and READ | string |



## Advanced APIs (Recommended)

### Uploading an Object

#### API description

The advanced upload API automatically divides your data into parts based on the size of your file. It’s easier to use, eliminating the need to follow each step of the multipart upload process.

#### Method prototype

```go
func (s *ObjectService) Upload(ctx context.Context, key string, filepath string, opt *MultiUploadOptions) (*CompleteMultipartUploadResult, *Response, error)
```

#### Sample request 

[//]: # (.cssg-snippet-transfer-upload-file)
```go
key := "exampleobject"
file := "../test"

_, _, err := client.Object.Upload(
    context.Background(), key, file, nil,
)
if err != nil {
    panic(err)
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| filepath | Name of the local file | string | Yes |
| opt | Object attributes | Struct | No |
| OptIni | Sets object attributes and ACL. For details, see [InitiateMultipartUploadOptions](#.E6.96.B9.E6.B3.95.E5.8E.9F.E5.9E.8B9) | Struct | No |
| PartSize | Size of each part in MB. It is automatically determined if you do not specify it as <= 0 | int | No |
| ThreadPoolSize | Size of the thread pool. Default: 1 | int | No |

#### Response description

```go
type CompleteMultipartUploadResult struct {
	Location string
	Bucket   string
	Key      string
	ETag     string
}

```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Location | URL address | string |
| Bucket        | Bucket name in the format: BucketName-APPID, e.g. examplebucket-1250000000. | string   |
| key | ObjectKey is the unique identifier of the object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the ObjectKey is doc/pic.jpg | string | Yes |
| ETag | The unique tag of a merged object. This value does not represent the MD5 checksum of the object content, but is used only to verify the uniqueness of the object as a whole. To verify the object content, you can check the ETag of each part during the upload process | string |
