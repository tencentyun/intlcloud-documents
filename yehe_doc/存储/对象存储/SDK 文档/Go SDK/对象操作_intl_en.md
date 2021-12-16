## Overview

This document provides an overview of APIs and SDK code samples related to simple operations, multipart operations, and advanced APIs.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Bucket (List Objects)](https://intl.cloud.tencent.com/document/product/436/30614) | Querying objects | Queries some or all the objects in a bucket. |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading an object using simple upload | Uploads an object to a bucket |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts  | Uploads an object by appending parts   |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object (file) to the local file system |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | Copying an object | Copies a file to the destination path. |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting a single object | Deletes a specified object from a bucket |
| [DELETE Multiple Object](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple objects from a bucket |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |


**Multipart operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries in-progress multipart uploads. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing a multipart upload operation | Initializes a multipart upload operation |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads a file in parts. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries the uploaded parts of a multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing a multipart upload | Completes the multipart upload of a file. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting a multipart upload | Aborts a multipart upload and deletes the uploaded parts. |


## Simple Operations

### Query objects

#### Description

This API is used to query some or all the objects in a bucket.

#### Method prototype

```go
func (s *BucketService) Get(ctx context.Context, opt *BucketGetOptions) (*BucketGetResult, *Response, error)
```

#### Sample 1: requesting the object list

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

#### Sample 2: listing all objects in a directory
COS does not have the concept of folder, but you can use slashes (/) as the delimiter to stimulate folders.

[//]: # (.cssg-snippet-get-bucket2)
```go
var marker string
opt := &cos.BucketGetOptions{
    Prefix:  "folder/",  // "prefix" indicates the directory to query.
    Delimiter: "/", // Set the delimiter to "/" to list objects in the current directory. To list all objects, leave this parameter empty.
    MaxKeys: 1000,       // Set the maximum number of traversed objects (up to 1,000 per `listobject` request).
}
isTruncated := true
for isTruncated {
    opt.Marker = marker
    v, _, err := c.Bucket.Get(context.Background(), opt)
    if err != nil {
        fmt.Println(err)
        break
    }
    for _, content := range v.Contents {
        fmt.Printf("Object: %v\n", content.Key)
    }
    // A common prefix indicates paths that end with the delimiter. If the delimiter is set to "/", the common prefix indicates the paths of all subdirectories.
    for _, commonPrefix := range v.CommonPrefixes {
        fmt.Printf("CommonPrefixes: %v\n", commonPrefix)
    }
    isTruncated = v.IsTruncated    // Whether any data still exists
    marker = v.NextMarker          // Set the start key for the next request
}
```

#### Parameter description

```go
type BucketGetOptions struct {
    Prefix       string 
    Delimiter    string 
    EncodingType   string 
    Marker       string 
    MaxKeys      int    
}
```

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Prefix | Filters the object keys prefixed with the value of this parameter. It is left empty by default. | String | No |
| Delimiter | A separator that is left empty by default. For example, you can specify it as `/` to indicate folders. | String | No |
| EncodingType | Specifies the encoding method of the returned value. It is left empty by default. Valid value: url. | string | No |
| Marker | Marks the starting point of the returned object list. Entries are listed in UTF-8 binary order by default. | String | No |
| MaxKeys | Maximum number of returned objects. Defaults to `1000`. | Int | No |

#### Response description

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

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | -------- |
| Name | Bucket name in the format of `BucketName-APPID`, such as `examplebucket-1250000000`. | String |
| Prefix | Filters the object keys prefixed with the value of this parameter. It is left empty by default. | String |
| Marker | Marks the starting point of the returned object list. Entries are listed in UTF-8 binary order by default. | String |
| NextMarker | Specifies the object after which the next listing should begin if `IsTruncated` is set to `true`. | String |
| Delimiter | A separator that is left empty by default. For example, you can specify it as `/` to indicate folders. | String |
| MaxKeys | Maximum number of returned objects. It defaults to 1000. | Int |
| IsTruncated | Indicates whether the returned objects are truncated | bool |
| Contents | Lists the metadata of all objects, including ETag, StorageClass, Key, Owner, LastModified, and Size. | []Object |
| CommonPrefixes | Groups all keys starting with `Prefix` and ending with `Delimiter` as a common prefix. | []string |
| EncodingType | Encoding type of the returned value. The returned value is not encoded by default. Valid value: `url` | String |

### Uploading an object in whole

#### Description

This API (PUT Object) is used to upload an object (file) of up to 5 GB to a bucket. For objects larger than 5 GB, please use [multipart upload](#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1) or [advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89). Simple uploads, creating folders, and batch uploads are supported.


#### Method prototype

```go
func (s *ObjectService) Put(ctx context.Context, key string, r io.Reader, opt *ObjectPutOptions) (*Response, error)
func (s *ObjectService) PutFromFile(ctx context.Context, name string, filePath string, opt *ObjectPutOptions) (*Response, error)
```

#### Sample 1: uploading an object

[//]: # (.cssg-snippet-put-object)
```go
// Sample 1: Using Put to upload an object
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

// Sample 2: Using PUtFromFile to upload a file to COS
filepath := "./test"
_, err = client.Object.PutFromFile(context.Background(), key, filepath, opt)
if err != nil {
    panic(err)
}

// Sample 3: Uploading a zero-byte file and setting the input stream length to 0 
_, err = client.Object.Put(context.Background(), key, strings.NewReader(""), nil)
if err != nil {
    // ERROR
}
```

#### Sample 2: creating a folder

COS uses slashes (/) to separate object paths to simulate the effect of directories. Therefore, you can upload an empty stream and append a slash to its name to create an empty directory in COS.
```go
// Folder name
name := "folder/"
// Transfer an input stream whose size is 0.
_, err := c.Object.Put(context.Background(), name, strings.NewReader(""), nil)
if err != nil {
	// ERROR
}
```

#### Sample 3: uploading an object to a COS directory

You can upload an object whose name is separated by slashes. In this way, the directory that contains this object will be created automatically. If you need to upload new objects to this COS directory, you can pass the value of this directory to `dir`.
```go
dir := "exampledir/"
filename := "exampleobject"
key := dir + filename
f := strings.NewReader("test file")
_, err = c.Object.Put(context.Background(), key, f, nil)
if err != nil {
    // ERROR
}
```

#### Sample 4: viewing the upload progress

```go
type SelfListener struct {
}
// A custom progress callback, which requires the ProgressChangedCallback method to be implemented.
func (l *SelfListener) ProgressChangedCallback(event *cos.ProgressEvent) {
    switch event.EventType {
    case cos.ProgressDataEvent:
        fmt.Printf("\r[ConsumedBytes/TotalBytes: %d/%d, %d%%]",
                    event.ConsumedBytes, event.TotalBytes, event.ConsumedBytes*100/event.TotalBytes)
    case cos.ProgressFailedEvent:
        fmt.Printf("\nTransfer Failed: %v", event.Err)
    }
}
func main() {
    // Initialize
    ...
 
    // Sample 1: Using the default callback function to view the upload progress
    key := "exampleobject"
    f, err := os.Open("../test")
    opt := &cos.ObjectPutOptions{
        ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
            ContentType: "text/html",
            // Set the default progress callback function.
            Listener:    &cos.DefaultProgressListener{},
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

    // Sample 2: Using a custom way to view the upload progress
    opt.Listener = &SelfListener{}
    filepath := "./test"
    _, err = client.Object.PutFromFile(context.Background(), key, filepath, opt)
    if err != nil {
        panic(err)
    }
}

```

#### Sample 5: uploading objects with multiple threads

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
                        SecretID:  os.Getenv("SECRETID"),
                        SecretKey: os.Getenv("SECRETKEY"),
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

#### Parameter description

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
    // Custom x-cos-meta-* header
    XCosMetaXXX        *http.Header 
    XCosStorageClass   string      
    XCosTrafficLimit   int
    Listener           ProgressListener
}
```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| r | Content of the uploaded file, which can be a file stream or a byte stream. When `r` is not `bytes.Buffer/bytes.Reader/strings.Reader`, `opt.ObjectPutHeaderOptions.ContentLength` must be specified | io.Reader | Yes |
| key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| XCosACL | Sets the file ACL, such as private, public-read, and public-read-write | String | No |
| XCosGrantFullControl | Grants full permission in the format: `id="[OwnerUin]"` | String | No |
| XCosGrantRead | Grants read permission in the format: id="[OwnerUin]" | String | No |
| XCosStorageClass | Sets the object storage class. Valid values: STANDARD (default), STANDARD_IA, ARCHIVE | String | No |
| Expires | Sets `Content-Expires` | String | No |
| CacheControl | Cache policy. Sets `Cache-Control` | String | No |
| ContentType | Content Type. Sets `Content-Type` | String | No |
| ContentDisposition | Filename. Sets `Content-Disposition` | String | No |
| ContentEncoding | Encoding format. Sets `Content-Encoding` | String | No |
| ContentLength | Sets the length of the request content | int64 | No |
| XCosMetaXXX | User-defined file metadata. It must start with x-cos-meta. Otherwise, it will be ignored | http.Header | No |
| XCosTrafficLimit     | Limits the speed for a single URL       | Int    | No |
| Listener             | Progress callback API                        | Struct | No |

#### Response description

```go
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```

The result can be obtained from the response.

```go
resp, err := client.Object.Put(context.Background(), key, f, nil)
etag := resp.Header.Get("ETag")
exp := resp.Header.Get("x-cos-expiration")
```


| Parameter | Description | Type |
| ---------------- | -------------------------------- | ------ |
| ETag | MD5 checksum of the uploaded file  | string |
| x-cos-expiration | Returns the file expiration rule if a lifecycle is configured. | string |

### Appending parts

#### Description

This API is used to upload an object by appending parts.

#### Method prototype

```go
func (s *ObjectService) Append(ctx context.Context, name string, position int, r io.Reader, opt *ObjectPutOptions) (int, *Response, error)
```
#### Sample request
```go
name := "exampleobject"
pos, _, err := c.Object.Append(context.Background(), name, 0, strings.NewReader("test1"), opt)
if err != nil {
    // ERROR
}
_, _, err = c.Object.Append(context.Background(), name, pos, strings.NewReader("test2"), opt)
if err != nil {
    // ERROR
}
```
#### Parameter description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| name  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` |  string |
| position | Starting point for the append operation (in bytes). For the first append, the value of this parameter is 0. For subsequent appends, the value is the `content-length` of the current object. | int |
| r | Content of the uploaded file, which can be a file stream or a byte stream. When `r` is not `bytes.Buffer/bytes.Reader/strings.Reader`, `opt.ObjectPutHeaderOptions.ContentLength` must be specified | io.Reader |
|  opt       |  Upload parameters (see `ObjectPutOptions`) | struct |

#### Response description

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| x-cos-next-append-position | Starting point of the next append, in bytes | int |

### Querying object metadata

#### Description

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
    IfModifiedSince            string 
}
```

| Parameter | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| IfModifiedSince | Returns the object only if it is modified after the specified time | String | No |

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
The result can be obtained from the response.
```go
resp, err := client.Object.Head(context.Background(), key, nil)
contentType := resp.Header.Get("Content-Type")
contentLength := resp.Header.Get("Content-Length")
etag := resp.Header.Get("ETag")
reqid := resp.Header.Get("X-Cos-Request-Id")

```

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| Metadata | Metadata of the queried file, including Etag and X-Cos-Request-Id. The metadata of the configured file is also returned. | String |


### Downloading an object

#### Description

This API (GET Object) is used to download an object (file) to a local file system. Simple downloads and batch downloads are supported.

#### Method prototype

```go
func (s *ObjectService) Get(ctx context.Context, key string, opt *ObjectGetOptions) (*Response, error)

func (s *ObjectService) GetToFile(ctx context.Context, key, localfile string, opt *ObjectGetOptions) (*Response, error)
```

#### Sample 1: downloading an object

[//]: # (.cssg-snippet-get-object)
```go
key := "exampleobject"
opt := &cos.ObjectGetOptions{
    ResponseContentType: "text/html",
    Range:               "bytes=0-3",
}
// `opt` is optional. It can be set to `nil` unless otherwise specified.
// 1. Obtain the object from the response body
resp, err := client.Object.Get(context.Background(), key, opt)
if err != nil {
    panic(err)
}
ioutil.ReadAll(resp.Body)
resp.Body.Close()

// 2. Download the object to the local file system
_, err = client.Object.GetToFile(context.Background(), key, "example.txt", nil)
if err != nil {
    panic(err)
}
```
#### Sample 2: downloading objects with multiple threads
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
                        SecretID:  os.Getenv("SECRETID"),
                        SecretKey: os.Getenv("SECRETKEY"),
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

#### Sample 3: limiting single-URL speed
```go

key := "exampleobject"
opt := &cos.ObjectGetOptions{
    // The speed range is 819200 to 838860800, that is 100 KB/s to 100 MB/s. If the value is not within this range, 400 will be returned.
    XCosTrafficLimit: 819200,
}
// `opt` is optional. It can be set to `nil` unless otherwise specified.
// 1. Obtain the object from the response body
_, err := client.Object.GetToFile(context.Background(), key, "example.txt", opt)
if err != nil {
    panic(err)
}
```

#### Sample 4: obtaining the download progress

The Go SDK allows you to obtain the download progress via a callback. You need to implement the `cos.ProgressListener` API, which is defined as follows:

```go
const (
    // Data transfer starts.
    ProgressStartedEvent ProgressEventType = iota
    // Transferring data
    ProgressDataEvent
    // Data transfer is completed, which does not mean the completion of the API call.
    ProgressCompletedEvent
    // Returned only when an error occurs during data transfer.
    ProgressFailedEvent
)
type ProgressEvent struct {
    EventType     ProgressEventType
    RWBytes       int64  // Number of bytes read at a time
    ConsumedBytes int64  // Number of bytes completed
    TotalBytes    int64  // Total number of bytes
    Err           error  // Error
}
type ProgressListener interface {
    ProgressChangedCallback(event *ProgressEvent)
}
```
```go
type SelfListener struct {
}
// A custom progress callback, which requires the ProgressChangedCallback method to be implemented.
func (l *SelfListener) ProgressChangedCallback(event *cos.ProgressEvent) {
    switch event.EventType {
    case cos.ProgressDataEvent:
        fmt.Printf("\r[ConsumedBytes/TotalBytes: %d/%d, %d%%]",
                    event.ConsumedBytes, event.TotalBytes, event.ConsumedBytes*100/event.TotalBytes)
    case cos.ProgressFailedEvent:
        fmt.Printf("\nTransfer Failed: %v", event.Err)
    }
}
func main() {
    // Initialize
    ... 

    key := "exampleobject"
    opt := &cos.ObjectGetOptions{
        ResponseContentType: "text/html",
        // View the progress using the default progress listener.
	Listener: &cos.DefaultProgressListener{},
    }
    // `opt` is optional. It can be set to `nil` unless otherwise specified.
    // 1. Obtain the object from the response body
    resp, err := client.Object.Get(context.Background(), key, opt)
    if err != nil {
        panic(err)
    }
    ioutil.ReadAll(resp.Body)
    resp.Body.Close()

    // 2. Download the object to the local file system
    // Use the custom progress callback method.
    opt.Listener = &SelfListener{}
    _, err = client.Object.GetToFile(context.Background(), key, "example.txt", opt)
    if err != nil {
        panic(err)
    }
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
    XCosTrafficLimit           int
    Listener                   ProgressListener
}
```

| Parameter | Description | Type | Required |
| -------------------------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| localfile | Name of the file downloaded to the local file system | string | Yes |
| ResponseContentType | Sets `Content-Type` in the response header | String | No |
| ResponseContentLanguage | Sets `Content-Language` in the response header | String | No |
| ResponseExpires | Sets `Expires` in the response header  | String | No |
| ResponseCacheControl | Sets `Cache-Control` in the response header | String | No |
| ResponseContentDisposition | Sets `Content-Disposition` in the response header | String | No |
| ResponseContentEncoding | Sets `Content-Encoding` in the response header | String | No |
| Range | Sets the byte range of the file to download in the format of `bytes=first-last`. | String | No |
| IfModifiedSince | Returns the object only if it is modified after the specified time | String | No |
| XCosTrafficLimit           | Limits the speed for a single URL                            | Int    | No |
| Listener                   | Progress callback API                              | Struct | No |

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
The result can be obtained from the response.
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
| Body | Content of the downloaded file | StreamBody |
| File metadata | Metadata of the downloaded file, including Etag and X-Cos-Request-Id. The metadata of the configured file is also returned. | String |

### Copying an object

This API (PUT Object-Copy) is used to copy an object to a destination path.

#### Method prototype

```go
func (s *ObjectService) Copy(ctx context.Context, key, sourceURL string, opt *ObjectCopyOptions) (*ObjectCopyResult, *Response, error)
```

#### Sample 1: copying an object

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
#### Sample 2: moving an object
```go
source := "test/oldfile"
f := strings.NewReader("test")
// Upload the object
_, err := c.Object.Put(context.Background(), source, f, nil)
if err != nil {
    // Error
}

// Move the object
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

#### Sample 3: modifying storage class

>!You can change STANDARD to STANDARD_IA, INTELLIGENT TIERING, ARCHIVE, or DEEP ARCHIVE. To modify ARCHIVE or DEEP ARCHIVE to other storage classes, you need to call `PostRestore` to restore objects in ARCHIVE or DEEP ARCHIVE first before calling this API. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).

```go
name := "exampleobject"
// Upload the source object
f := strings.NewReader("test")
_, err := client.Object.Put(context.Background(), name, f, nil)
assert.Nil(s.T(), err, "Test Failed")

sourceURL := fmt.Sprintf("%s/%s", client.BaseURL.BucketURL.Host, name)
opt := &cos.ObjectCopyOptions{
    &cos.ObjectCopyHeaderOptions{
        XCosMetadataDirective: "Replaced",
        XCosStorageClass: "Archive",        // Modify the storage class to ARCHIVE.
    },
    nil,
}
_, _, err = client.Object.Copy(context.Background(), name, sourceURL, opt)
if err != nil {
    panic(err)
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
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| sourceURL | URL of the source file to copy | string | Yes |
| XCosACL | Sets the file ACL, such as private, public-read, and public-read-write | string | No |
| XCosGrantFullControl | Grants full permission in the format: `id="[OwnerUin]"` | string | No |
| XCosGrantRead| Grants the read permission in the format: id="[OwnerUin]" | string | No |
|  XCosMetadataDirective | Valid values:</br><li>`Copy`: copies the source object along with its metadata.</br><li>`Replaced`: copies the source object while replacing its metadata.</br>If the destination path is the same as the source path, this parameter must be set to `Replaced`. | String | Yes |
| XCosCopySourceIfModifiedSince | If the object is modified after the specified time, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `XCosCopySourceIfNoneMatch`. If it is used together with other conditions, a conflict will be returned. | String | No |
| XCosCopySourceIfUnmodifiedSince | If the object is not modified after the specified time, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `XCosCopySourceIfMatch`. If it is used together with other conditions, a conflict will be returned. | String | No |
| XCosCopySourceIfMatch | If the `ETag` of the object is the same as the specified one, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `XCosCopySourceIfUnmodifiedSince`. If it is used together with other conditions, a conflict will be returned. | String | No |
| XCosCopySourceIfNoneMatch | If the `Etag` of the object is different from the specified one, the operation will be performed; otherwise, 412 will be returned. This parameter can be used together with `XCosCopySourceIfModifiedSince`. If it is used together with other conditions, a conflict will be returned. | String | No |
| XCosStorageClass | Sets the object storage class. Valid values: STANDARD (default), STANDARD_IA, ARCHIVE. | String | No |
| XCosMetaXXX | User-defined file metadata. | http.Header | No |
| XCosCopySource | Source file URL. You can specify a historical version using the `versionid` sub-resource. | String | No |

#### Response description

Attributes of the uploaded file:

```go
type ObjectCopyResult struct {
    ETag         string 
    LastModified string
}
```


| Parameter | Description | Type |
| ------------ | -------------------------- | ------ |
| ETag | MD5 of the copied file | String |
| LastModified | Last modified time of the copied file | String |

### Deleting an object

#### Description

This API is used to delete an object (folder) from a bucket.

#### Method prototype

```go
func (s *ObjectService) Delete(ctx context.Context, key string) (*Response, error)
```

#### Sample 1: deleting an object

[//]: # (.cssg-snippet-delete-object)
```go
key := "exampleobject"
_, err := client.Object.Delete(context.Background(), key)
if err != nil {
    panic(err)
}
```

#### Sample 2: deleting a folder

This request does not delete objects in the folder but only the specified key.

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
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |

### Deleting multiple objects

#### Description

The API is used to delete multiple objects from a bucket. You can delete up to 1,000 objects in one request.

#### Method prototype

```go
func (s *ObjectService) DeleteMulti(ctx context.Context, opt *ObjectDeleteMultiOptions) (*ObjectDeleteMultiResult, *Response, error)
```

#### Sample 1: deleting multiple specified objects

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
    // Boolean, which indicates whether to enable the Quiet or Verbose mode.
    // `true` indicates the Quiet mode while `false` (default) indicates the Verbose mode.
    // Quiet: true,
}

_, _, err := client.Object.DeleteMulti(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### Sample 2: deleting a folder and the objects contained

COS uses slashes (/) to separate object paths to simulate the effect of a file system. Therefore, deleting a folder in COS means deleting all objects that have a specified prefix. For example, the folder 'prefix/' contains all objects prefixed with 'prefix/'. In other words, you can delete all objects prefixed with 'prefix/' to delete the 'prefix/' folder.
Currently, the COS Go SDK does not provide an API to perform this operation. However, you can still use a combination of basic operations to do so.

```go
dir := "exampledir/"
var marker string
opt := &cos.BucketGetOptions{
    Prefix:  dir,
    MaxKeys: 1000,
}
isTruncated := true
for isTruncated {
    opt.Marker = marker
    v, _, err := c.Bucket.Get(context.Background(), opt)
    if err != nil {
        // Error
        break
    }
    for _, content := range v.Contents {
        _, err = c.Object.Delete(context.Background(), content.Key)
        if err != nil {
            // Error
        }
    }
    isTruncated = v.IsTruncated
    marker = v.NextMarker
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
| Key | Names of the objects that failed to be deleted | String |
| Code | Error code for the deletion failure | String |
| Message | Error message for the deletion failure | String |



### Restoring an archived object 

#### Description

This API (`POST Object restore`) is used to restore an archived object for access.

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
        // Considering the ACL limit, we recommend not setting an object ACL when uploading an object unless required. The object will then inherit the bucket ACL by default.
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
// Restore an archived object.
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
| key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| ObjectRestoreOptions | Describes rules for retrieved temporary files | Struct | Yes |
| Days | Specifies the number of days before a temporary object expires | Int | Yes |
| CASJobParameters | Specifies the restoration configuration | Struct | No |
| Tier | Object restoration mode. For ARCHIVE, valid values are `Expedited`, `Standard`, and `Bulk`. For DEEP ARCHIVE, valid values are `Standard` and `Bulk` | String | No |



## Multipart Operations

### Querying multipart uploads

#### Description

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
    UploadIDMarker     string                                         
}
```

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| delimiter | The delimiter is a symbol. The identical paths between `prefix` or, if no `prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix  | String | No |
| encodingType | Encoding type of the returned value. Valid value: `url` | String | No |
| prefix | Specifies that returned object keys must be prefixed with this value. Note that if you use this parameter, returned keys will contain the prefix | String | No |
| MaxUploads | Sets the maximum number of multipart uploads that can be returned at a time. Value range: 1−1000. Defaults to `1000`. | Int | No |
| KeyMarker | This parameter is used together with `upload-id-marker`: </li><li>If `upload-id-marker` is not specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed.</li><li>If `upload-id-marker` is specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed, and multipart uploads whose `ObjectName` is lexicographically equal to `key-marker` with `UploadID` greater than `upload-id-marker` will be listed. | String | No |
| UploadIDMarker | This parameter is used together with `key-marker`: </li><li>If `key-marker` is not specified, `upload-id-marker` will be ignored. </li><li>If `key-marker` is specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed, and multipart uploads whose `ObjectName` is lexicographically equal to `key-marker` with `UploadID` greater than `upload-id-marker` will be listed.</li> | String | No |


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
        StorageClass         string
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
| Bucket | Destination bucket for multipart upload in the format of `BucketName`, for example, `examplebucket-1250000000` | String |
| EncodingType | Encoding type of the returned value. The returned value is not encoded by default. Valid value: `url` | String |
| KeyMarker | Specifies the key where the list starts | String |
| UploadIDMarker | Specifies the `uploadId` where the list starts | String |
| NextKeyMarker | If the returned list is truncated, the `NextKeyMarker` returned will be the starting point of the subsequent list | String |
| NextUploadIdMarker | If the returned list is truncated, the `UploadId` returned will be the starting point of the subsequent list | String |
| MaxUploads | Maximum number of parts to return at a time. Default value: `1000` | String    |
| IsTruncated | Indicates whether the returned list is truncated | Bool |
| Uploads | Information on each upload | Container |
| Key | Object name | String |
| UploadID | ID that identifies the current multipart upload | String |
| Key | Indicates whether the returned list is truncated | Bool |
| StorageClass | Specifies the storage class for parts. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String |
| Initiator | Indicates information about the initiator of this upload | Container |
| Owner | Indicates information about the owner of these parts | Container |
| Initiated | Start time of the multipart upload | String |
| Prefix | Specifies that returned object keys must be prefixed with this value. Note that if you use this parameter, returned keys will contain the prefix | Struct    |
| Delimiter | A symbol. The identical paths between `Prefix` and the first occurrence of the `Delimiter` are grouped and defined as a common prefix. If no `Prefix` is specified, the common prefix starts with the beginning of the path | String |
| CommonPrefixes | The identical paths between `Prefix` and `Delimiter` are grouped and defined as a common prefix | String    |
| ID | Unique CAM ID of users | String |
| DisplayName | User Identifier (UIN) | String |


### Multipart upload operations

Multipart operations include:

- Multipart upload: initializing a multipart upload operation, uploading parts, and completing a multipart upload operation
- Deleting uploaded parts

>? Uploading the object via multipart upload, you can also use [Advanced APIs](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) to upload (recommended).
>

<span id="INIT_MULIT_UPLOAD"></span>
###  Initializing a multipart upload 

#### Description

This API is used to initialize a multipart upload operation and get its `uploadId`.

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
    // Custom x-cos-meta-* header
    XCosMetaXXX        *http.Header 
    XCosStorageClass   string      
}

```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | ---- |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| XCosACL | Sets the file ACL, such as `private` or `public-read` | String | No |
| XCosGrantFullControl | Grants full permission in the format: `id="[OwnerUin]"` | String | No |
| XCosGrantRead | Grants read permission in the format: id="[OwnerUin]" | String | No |
| XCosStorageClass | Sets the object storage class. Valid values: STANDARD (default), STANDARD_IA, ARCHIVE | String | No |
| Expires | Sets `Content-Expires` | String | No |
| CacheControl | Cache policy. Sets `Cache-Control` | String | No |
| ContentType | Content Type. Sets `Content-Type` | String | No |
| ContentDisposition | Filename. Sets `Content-Disposition` | String | No |
| ContentEncoding | Encoding format. Sets `Content-Encoding` | String | No |
| ContentLength | Sets the length of the request content | int64 | No |
| XCosMetaXXX | User-defined file metadata. It must start with x-cos-meta. Otherwise, it will be ignored | http.Header | No |

#### Response description

```go
type InitiateMultipartUploadResult struct {
    Bucket   string
    Key      string
    UploadID     string
} 
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| UploadId | ID that identifies the multipart upload | string |
| Bucket | Bucket name in the format: `BucketName-APPID` | string |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String |


<span id="MULIT_UPLOAD_PART"></span>
###  Uploading parts 

This API (`Upload Part`) is used to upload an object in parts.

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
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| UploadId | ID that identifies the multipart upload; generated by `InitiateMultipartUpload` | String | Yes |
| PartNumber | Number that identifies the uploaded part | Int | Yes |
| r | Content of the uploaded part, which can be a local file stream or an input stream. When `r` is not `bytes.Buffer/bytes.Reader/strings.Reader`, `opt.ContentLength` must be specified | io.Reader | Yes |
| ContentLength | Sets the length of the request content | int64 | No |

#### Response description

```go
{
    'ETag': 'string'
}
```
The result can be obtained from the response.
```go
resp, err := client.Object.UploadPart(context.Background(), key, UploadID, 1, f, nil)
etag := resp.Header.Get("ETag")
```


| Parameter | Description | Type |
| -------- | ----------------- | ------ |
| ETag | MD5 of the uploaded part | String |


<span id = "LIST_MULIT_UPLOAD"></span>
###  Querying uploaded parts 

#### Description

This API (`List Parts`) is used to query the uploaded parts of a multipart upload.

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
    PartNumberMarker     string                                      
}
```

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| UploadId | ID that identifies the multipart upload; generated by `InitiateMultipartUpload` | String | Yes |
| EncodingType | Encoding type of the returned value | String | No |
| MaxParts | Maximum number of parts to return at a time. Defaults to `1000` | String | No |
| PartNumberMarker | By default, entries are listed in UTF-8 binary order starting with the part number after the marker | String | No |

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
    StorageClass         string 
    Owner        *Owner
}
```

| Parameter | Description | Type |
| -------------------- | ------------------------------------------------------------ | ------ |
| Bucket               | Bucket name in the format: `BucketName-APPID`, for example, `examplebucket-1250000000` | String |
| EncodingType | Encoding type of the returned value. The returned value is not encoded by default. Valid value: `url` | String |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String |
| UploadId | ID that identifies the multipart upload; generated by `InitiateMultipartUpload` | String |
| Initiator | Initiator of the multipart upload, including `DisplayName`, `UIN` and `ID` | Struct |
| Owner | Information on the file owner, including `DisplayName`, `UIN` and `ID` | Struct |
| StorageClass | Object storage class. Valid values: `STANDARD` (default), `STANDARD_IA`, `ARCHIVE` | String |
| PartNumberMarker | Specifies the part number after which the listing should begin. It defaults to 0, which means the listing begins with the first part | String |
| NextPartNumberMarker | Specifies the part number after which the next listing should begin | Int |
| MaxParts | Maximum number of parts to return at a time. Default value: `1000` | Int |
| IsTruncated | Indicates whether the returned list is truncated | Bool |
| Part | Information on the uploaded part, including `ETag`, `PartNumber`, `Size`, and `LastModified` | Struct |


<span id = "COMPLETE_MULIT_UPLOAD"></span>
###  Completing a multipart upload 

#### Description

This API (`Complete Multipart Upload`) is used to complete the multipart upload of a file.

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
    ETag         string 
    PartNumber   int     
}
```

| Parameter | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| UploadId | ID that identifies the multipart upload; generated by `InitiateMultipartUpload` | String | Yes |
| CompleteMultipartUploadOptions | Information on all parts, including `ETag` and `PartNumber` | Struct | Yes |

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
| Location | URL address | String |
| Bucket               | Bucket name in the format: `BucketName-APPID`, for example, `examplebucket-1250000000` | String |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String |
| ETag | Unique tag of a merged object. This value does not represent the MD5 checksum of the object content, but is used only to verify the uniqueness of the object as a whole. To verify the object content, you can check the ETag of each part during the upload process | String |

<span id = "ABORT_MULIT_UPLOAD"></span>
###  Aborting a multipart upload 

#### Description

This API (`Abort Multipart Upload`) is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```go
func (s *ObjectService) AbortMultipartUpload(ctx context.Context, key, uploadID string) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-abort-multi-upload)
```go
key := "exampleobject"
// Abort
_, err := client.Object.AbortMultipartUpload(context.Background(), key, UploadID)
if err != nil {
    panic(err)
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| UploadId | ID of the multipart upload | String | Yes |



## Advanced APIs (Recommended)

### Uploading an object

#### Description

The advanced upload API automatically divides your data into parts according to the file size. It’s easier to use, eliminating the need to follow each step of the multipart upload process. If the file is larger than 16 MB, multipart upload will be used. You can use the `PartSize` parameter to adjust the part size.

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

```go
type MultiUploadOptions struct {
    OptIni             *InitiateMultipartUploadOptions
    PartSize           int64
    ThreadPoolSize     int
    CheckPoint         bool
}
```

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| filepath | Name of the local file | String | Yes |
| opt | Object attributes | Struct | No |
| OptIni | Sets object attributes and ACL. For details, see [InitiateMultipartUploadOptions](#.E6.96.B9.E6.B3.95.E5.8E.9F.E5.9E.8B9) | Struct | No |
| PartSize | Part size (in MB). If this parameter is not specified or is set to a value smaller than or equal to 0, its value will be automatically determined. In the new version, the default size is 16 (MB). | int | No |
| ThreadPoolSize | Size of the thread pool. Default: 1 | Int | No |
| CheckPoint     | Whether to enable checkpoint restart. Default value: `false`  | Bool   | No   |

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
| Location | URL address | String |
| Bucket               | Bucket name in the format: `BucketName-APPID`, for example, `examplebucket-1250000000` | String |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String |
| ETag | Unique tag of a merged object. This value does not represent the MD5 checksum of the object content, but is used only to verify the uniqueness of the object as a whole. To verify the object content, you can check the ETag of each part during the upload process | String |

### Downloading an object

#### Description

The multipart download API automatically downloads data concurrently with `Range` according to the object size. If you use `Range` to download an object larger than 16 MB, you can use the `PartSize` parameter to adjust the part size.

#### Method prototype

```go
func (s *ObjectService) Download(ctx context.Context, name string, filepath string, opt *MultiDownloadOptions) (*Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-download-file"
```go
key := "exampleobject"
file := "localfile"

opt := &cos.MultiDownloadOptions{
	ThreadPoolSize: 5,
}
_, err := c.Object.Download(
	context.Background(), key, file, opt,
)
if err != nil {
    panic(err)
}
```

#### Parameter description

```go
type MultiDownloadOptions struct {
    Opt            *ObjectGetOptions
    PartSize       int64
    ThreadPoolSize     int
    CheckPoint     bool
    CheckPointFile string
}
```

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| name | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| filepath | Name of the local file | String | Yes |
| opt            | Object download parameter             | Struct | No |
| Opt | Request parameter. For more information, please see [ObjectGetOptions](#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A1). | Struct | No |
| PartSize | Part size (in MB). If this parameter is not specified or is set to a value smaller than or equal to 0, its value will be automatically determined. In the new version, the default size is 16 (MB). | int64 | No |
| ThreadPoolSize | Size of the thread pool. Default: 1 | Int | No |
| CheckPoint     | Whether to enable checkpoint restart. Default value: `false`  | Bool   | No   |
| CheckPointFile | Path to save the download progress file when checkpoint restart is enabled. The default value is `&lt;filepath>.cosresumabletask`. When the download is completed, this progress file will be cleared. | String   | No |

#### Response description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| \*Response| HTTP response, through which you can obtain the response status code, response headers, and other information. | Struct |
| error    | Error message. If no error occurs, `nil` will be returned.                  | Struct |



### Moving an object

#### Description

Object movement can be implemented using the object copy API and object delete API.

#### Sample request

```go
source := "test/oldfile"
f := strings.NewReader("test")
// Upload the object
_, err := c.Object.Put(context.Background(), source, f, nil)
if err != nil {
   // Error
}
// Move the object
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


