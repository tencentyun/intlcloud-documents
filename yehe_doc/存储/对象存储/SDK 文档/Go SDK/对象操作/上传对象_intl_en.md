## Overview

This document provides an overview of APIs and SDK code samples related to object uploads.

**Simple operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | Uploading object using simple upload | Uploads object to bucket. |
| [APPEND Object](https://intl.cloud.tencent.com/document/product/436/7741) | Appending parts  | Uploads object by appending parts.   |


**Multipart upload operations**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | Querying multipart uploads | Queries multipart uploads in progress. |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | Initializing multipart upload operation | Initializes multipart upload operation. |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | Uploading parts | Uploads file in parts. |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | Querying uploaded parts | Queries uploaded parts of multipart upload. |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | Completing multipart upload | Completes multipart upload. |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | Aborting multipart upload | Aborts multipart upload operation and deletes uploaded parts. |

## Advanced API (Recommended)

### Uploading object

#### Feature description

This API automatically divides your data into parts according to the file size. It's easier to use, eliminating the need to follow each step of the multipart upload process. If the file is larger than 16 MB, multipart upload will be used. You can use the `PartSize` parameter to adjust the part size.

#### Method prototype

```go
func (s *ObjectService) Upload(ctx context.Context, key string, filepath string, opt *MultiUploadOptions) (*CompleteMultipartUploadResult, *Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-transfer-upload-file"
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main() {
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })

    key := "exampleobject"

    _, _, err := client.Object.Upload(
        context.Background(), key, "localfile", nil,
    )
    if err != nil {
        panic(err)
    }
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
| -------------- | ------------------------------------------------------------ | ------ | -------- |
| key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string | Yes |
| filepath | Name of the local file. | string | Yes |
| opt | Object attributes. | Struct | No |
| OptIni | Sets the object attributes and ACL. For more information, see [InitiateMultipartUploadOptions](#.E5.88.9D.E5.A7.8B.E5.8C.96.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0). | Struct | No |
| PartSize | Part size in MB. If this parameter is not specified or is set to a value smaller than or equal to 0, its value will be automatically determined. In the new version, the default size is 16 MB. | int | No |
| ThreadPoolSize | Size of the thread pool. Default value: 1. | int | No |
| CheckPoint     | Whether to enable checkpoint restart. Default value: false.  | bool   | No   |

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
| Location | URL | string |
| Bucket               | Bucket name in the format of `BucketName-APPID`, for example, `examplebucket-1250000000`. | string |
| Key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string |
| ETag | Unique tag of a merged object. This value does not represent the MD5 checksum of the object content, but is used only to verify the uniqueness of the object as a whole. To verify the object content, check the `ETag` of each part during the upload process. | string |


## Simple Operations

### Uploading object by using simple upload

#### Feature description

This API is used to upload an object (file) of up to 5 GB to a bucket. For objects larger than 5 GB, use [Multipart Upload](#.E5.88.86.E5.9D.97.E4.B8.8A.E4.BC.A0.E5.AF.B9.E8.B1.A1) or [Advanced API](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89). Simple uploads, creating folders, and batch uploads are supported.


#### Method prototype

```go
func (s *ObjectService) Put(ctx context.Context, key string, r io.Reader, opt *ObjectPutOptions) (*Response, error)
func (s *ObjectService) PutFromFile(ctx context.Context, name string, filePath string, opt *ObjectPutOptions) (*Response, error)
```

#### Sample 1: Uploading an object

[//]: # ".cssg-snippet-put-object"
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "strings"
)

func main() {
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })

    // Sample 1: Using Put to upload an object
    key := "exampleobject"
    f, err := os.Open("../test")
    opt := &cos.ObjectPutOptions{
        ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
            ContentType: "text/html",
        },
        ACLHeaderOptions: &cos.ACLHeaderOptions{
            // Considering the ACL limit, we recommend you not set an object ACL when uploading an object unless required. The object will then inherit the bucket ACL by default.
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
}
```

#### Sample 2: Creating a folder

COS uses slashes to separate object paths to simulate the effect of directories. Therefore, you can upload an empty stream and append a slash to its name to create an empty directory in COS.
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "strings"
)

func main() {
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })

    // Folder name
    name := "folder/"
    // Transfer an input stream of 0 in size.
    _, err := client.Object.Put(context.Background(), name, strings.NewReader(""), nil)
    if err != nil {
        // ERROR
    }
}
```

#### Sample 3: Uploading an object to a COS directory

You can upload an object whose name is separated by slashes. In this way, the directory that contains this object will be created automatically. To upload new objects to this COS directory, enter the value of `Key` as the directory's prefix.
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "strings"
)

func main() {
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })

    dir := "exampledir/"
    filename := "exampleobject"
    key := dir + filename
    f := strings.NewReader("test file")
    _, err = client.Object.Put(context.Background(), key, f, nil)
    if err != nil {
        // ERROR
    }
}
```

#### Sample 4: Viewing the upload progress

```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

type SelfListener struct {
}

// A custom progress callback, which requires the `ProgressChangedCallback` method to be implemented.
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
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    // Sample 1: Using the default callback function to view the upload progress
    key := "exampleobject"
    f, err := os.Open("test")
    opt := &cos.ObjectPutOptions{
        ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
            ContentType: "text/html",
            // Set the default progress callback function.
            Listener: &cos.DefaultProgressListener{},
        },
        ACLHeaderOptions: &cos.ACLHeaderOptions{
            // Considering the ACL limit, we recommend you not set an object ACL when uploading an object unless required. The object will then inherit the bucket ACL by default.
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

#### Sample 5: Uploading objects with multiple threads

```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "sync"
)

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
    // Upload files with multiple threads.
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

#### Sample 6: Performing MD5 check
CRC64 check is enabled by default for file uploads in the Go SDK v0.7.23 or later. You can also perform MD5 check on your own.

```go
package main
import (
    "context"
    "crypto/md5"
    "encoding/base64"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "io/ioutil"
    "net/http"
    "net/url"
    "os"
    "strings"
)

func calMD5Digest(msg []byte) []byte {
    m := md5.New()
    m.Write(msg)
    return m.Sum(nil)
}

func main() {
    u, _ := url.Parse("https://test-1259654469.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    // CRC64 check is enabled by default in the Go SDK v0.7.23 or later.
	// c.Conf.EnableCRC = false // Manually disable CRC64 check, which is not recommended.

    // Calculate MD5.
    content := "test content"
    bs1 := calMD5Digest([]byte(content))
    md5str := fmt.Sprintf("%x", bs1)

    name := "exampleobject"
    f := strings.NewReader(content)
    opt := &cos.ObjectPutOptions{
        ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
            ContentMD5:  base64.StdEncoding.EncodeToString(bs1), // The server can perform a check based on the received file and this value during upload
            XCosMetaXXX: &http.Header{},
        },
        ACLHeaderOptions: nil,
    }
    opt.XCosMetaXXX.Add("x-cos-meta-md5", md5str) // The business can use this value for file check during download

    // Upload a file.
    _, err := c.Object.Put(context.Background(), name, f, opt)
    if err != nil {
        // ERROR
    }

    // Download a file.
    resp, err := c.Object.Get(context.Background(), name, nil)
    if err != nil {
        // ERROR
    }
    defer resp.Body.Close()

    meta_md5 := resp.Header.Get("x-cos-meta-md5")
    body, _ := ioutil.ReadAll(resp.Body)
    bs2 := calMD5Digest(body)
    if fmt.Sprintf("%x", bs2) != meta_md5 {
        fmt.Printf("md5 is not consistent\n")
    }
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
    ContentMD5         string 
    ContentLength      int64  
    Expires            string 
    // Custom x-cos-meta-* header.
    XCosMetaXXX        *http.Header 
    XCosStorageClass   string      
    XCosTrafficLimit   int
    Listener           ProgressListener
}
```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | -------- |
| r | Content of the uploaded file, which can be a file stream or a byte stream. When `r` is not `bytes.Buffer/bytes.Reader/strings.Reader`, `opt.ObjectPutHeaderOptions.ContentLength` must be specified. | io.Reader | Yes |
| key | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string | Yes |
| XCosACL | Sets the file ACL. Valid values: private; public-read; public-read-write. | string | No |
| XCosGrantFullControl | Grants full permission in the format of `id="[OwnerUin]"`. | string | No |
| XCosGrantRead | Grants read permission in the format of `id="[OwnerUin]"`. | string | No |
| XCosStorageClass | Storage class of the object. Valid values: STANDARD; STANDARD_IA; ARCHIVE. Default value: STANDARD. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | string | No |
| Expires | Sets `Content-Expires`. | string | No |
| CacheControl | Cache policy. Sets `Cache-Control`. | string | No |
| ContentType | Content type. Sets `Content-Type`. | string | No |
| ContentMD5           | Base64-encoded 16-byte binary MD5 checksum of the request body content defined in RFC 1864. This value is a 24-character string, such as `ZzD3iDJdrMAAb00lgLLeig==`, and is used to verify whether the request body experienced any changes during transfer.      | string      | No       |
| ContentDisposition | Filename. Sets `Content-Disposition`. | string | No |
| ContentEncoding | Encoding format. Sets `Content-Encoding`. | string | No |
| ContentLength | Sets the length of the request content. | int64 | No |
| XCosMetaXXX | User-defined file metadata. It must start with `x-cos-meta`; otherwise, it will be ignored. | http.Header | No |
| XCosTrafficLimit           | Speed limit for a single URL.                            | int    | No |
| Listener                   | Progress callback API.                              | Struct | No |

#### Response description

```go
{
    'ETag': 'string',
    'x-cos-expiration': 'string'
}
```

The returned result can be obtained from `Response`.

```go
resp, err := client.Object.Put(context.Background(), key, f, nil)
etag := resp.Header.Get("ETag")
exp := resp.Header.Get("x-cos-expiration")
```


| Parameter | Description | Type |
| ---------------- | -------------------------------- | ------ |
| ETag | MD5 checksum of the uploaded file.  | string |
| x-cos-expiration | Returns the file expiration rule if a lifecycle is configured. | string |

### Appending parts

#### Feature description

This API is used to upload an object by appending parts.

#### Method prototype

```go
func (s *ObjectService) Append(ctx context.Context, name string, position int, r io.Reader, opt *ObjectPutOptions) (int, *Response, error)
```
#### Sample request
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "strings"
)

func main() {
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })

    name := "exampleobject"
    pos, _, err := client.Object.Append(context.Background(), name, 0, strings.NewReader("test1"), nil)
    if err != nil {
        // ERROR
    }
    _, _, err = client.Object.Append(context.Background(), name, pos, strings.NewReader("test2"), nil)
    if err != nil {
        // ERROR
    }
}
```
#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | --------- |
| name  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. |  string |
| position | Starting point for the append operation in bytes. For the first append, the value of this parameter is 0. For subsequent appends, the value is the `content-length` of the current object. | int |
| r | Content of the uploaded file, which can be a file stream or a byte stream. When `r` is not `bytes.Buffer/bytes.Reader/strings.Reader`, `opt.ObjectPutHeaderOptions.ContentLength` must be specified. | io.Reader |
| opt      | Uploaded parameter. For more information, see ObjectPutOptions.                               | struct    |

#### Response description

| Parameter | Description | Type |
| -------------------------- | ---------------------------------- | ---- |
| x-cos-next-append-position | Starting point of the next append in bytes. | int |




## Multipart Upload Operations

### Querying multipart upload

#### Feature description

This API is used to query multipart uploads in progress in a specified bucket.

#### Method prototype

```go
func (s *BucketService) ListMultipartUploads(ctx context.Context, opt *ListMultipartUploadsOptions) (*ListMultipartUploadsResult, *Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-list-multi-upload"
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main() {
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    _, _, err := client.Bucket.ListMultipartUploads(context.Background(), nil)
    if err != nil {
        panic(err)
    }
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
| -------------- | ------------------------------------------------------------ | ------ | -------- |
| Delimiter | A symbol. The identical paths between `prefix` or, if no `prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix.  | string | No |
| EncodingType | Encoding type of the returned value. Valid value: url. | string | No |
| Prefix | Specifies that returned object keys must be prefixed with the value of this parameter. Note that if you use this parameter, returned keys will contain the prefix. | string | No |
| MaxUploads | Sets the maximum number of multipart uploads that can be returned at a time. Value range: 1−1000. Default value: 1000. | int | No |
| KeyMarker | This parameter is used together with `upload-id-marker`: </li><li>If `upload-id-marker` is not specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed.</li><li>If `upload-id-marker` is specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed, and multipart uploads whose `ObjectName` is lexicographically equal to `key-marker` with `UploadID` greater than `upload-id-marker` will be listed. | string | No |
| UploadIDMarker | This parameter is used together with `key-marker`: </li><li>If `key-marker` is not specified, `upload-id-marker` will be ignored. </li><li>If `key-marker` is specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed, and multipart uploads whose `ObjectName` is lexicographically equal to `key-marker` with `UploadID` greater than `upload-id-marker` will be listed.</li> | string | No |


#### Response description

```go
// `ListMultipartUploadsResult` saves the result of `ListMultipartUploads`.
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
// Use the same type as the owner.
type Initiator Owner
// `Owner` defines the bucket/object's owner.
type Owner struct {
    ID          string
    DisplayName string
}
```

| Parameter | Description | Type |
| ------------------ | ------------------------------------------------------------ | --------- |
| Bucket | Destination bucket for multipart upload in the format of `BucketName`, for example, `examplebucket-1250000000`. | string |
| EncodingType | Encoding type of the returned value. The returned value is not encoded by default. Valid value: url. | string |
| KeyMarker | Specifies the key where the list starts. | string |
| UploadIDMarker | Specifies the `UploadId` where the list starts. | string |
| NextKeyMarker | If the returned list is truncated, the returned `NextKeyMarker` will be the starting point of the subsequent list. | string |
| NextUploadIDMarker | If the returned list is truncated, the returned `UploadId` will be the starting point of the subsequent list. | string |
| MaxUploads | Maximum number of multipart uploads that can be returned at a time. Default value: 1000. | string    |
| IsTruncated | Indicates whether the returned list is truncated. | bool |
| Uploads | Information of each upload. | Container |
| Key | Object name. | string |
| UploadID | ID that identifies the current multipart upload. | string |
| Key | Indicates whether the returned list is truncated. | bool |
| StorageClass | Storage class of the part. Valid values: STANDARD; STANDARD_IA; ARCHIVE. Default value: STANDARD. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | string |
| Initiator | Indicates the initiator information of the upload. | Container |
| Owner | Indicates the owner information of the parts. | Container |
| Initiated | Start time of the multipart upload | string. |
| Prefix | Specifies that returned object keys must be prefixed with the value of this parameter. Note that if you use this parameter, returned keys will contain the prefix. | struct    |
| Delimiter | A symbol. The identical paths between `prefix` or, if no `prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. | string |
| CommonPrefixes | The identical paths between `prefix` and `delimiter` are grouped and defined as a common prefix. | string    |
| ID | Unique CAM ID of the user. | string |
| DisplayName | User ID (UIN). | string |


### Uploading object in parts

With multipart upload, you can do the following:

- Multipart upload: Initializing a multipart upload operation, uploading parts, and completing a multipart upload operation.
- Deleting uploaded parts.

>? To perform a multipart upload operation, you can also use the [Advanced API](#.E9.AB.98.E7.BA.A7.E6.8E.A5.E5.8F.A3.EF.BC.88.E6.8E.A8.E8.8D.90.EF.BC.89) (recommended).
>

<span id="INIT_MULIT_UPLOAD"></span>
###  Initializing multipart upload 

#### Feature description

This API is used to initialize a multipart upload operation and get its `uploadId`.

#### Method prototype

```go
func (s *ObjectService) InitiateMultipartUpload(ctx context.Context, name string, opt *InitiateMultipartUploadOptions) (*InitiateMultipartUploadResult, *Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-init-multi-upload"
```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main() {
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    name := "exampleobject"
    // Optional. Considering the ACL limit, we recommend you not set an object ACL when uploading an object unless required. The object will then inherit the bucket ACL by default.
    v, _, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil)
    if err != nil {
        panic(err)
    }
    UploadID := v.UploadID
    fmt.Println(UploadID)
}
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
    // Custom x-cos-meta-* header.
    XCosMetaXXX        *http.Header 
    XCosStorageClass   string      
}

```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ----------- | -------- |
| key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string | Yes |
| XCosACL | Sets the file ACL. Valid values: private; public-read | string. | No |
| XCosGrantFullControl | Grants full permission in the format of `id="[OwnerUin]"`. | string | No |
| XCosGrantRead | Grants read permission in the format of `id="[OwnerUin]"`. | string | No |
| XCosStorageClass | Storage class of the object. Valid values: STANDARD; STANDARD_IA; ARCHIVE. Default value: STANDARD. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | string | No |
| Expires | Sets `Content-Expires`. | string | No |
| CacheControl | Cache policy. Sets `Cache-Control`. | string | No |
| ContentType | Content type. Sets `Content-Type`. | string | No |
| ContentDisposition | Filename. Sets `Content-Disposition`. | string | No |
| ContentEncoding | Encoding format. Sets `Content-Encoding`. | string | No |
| ContentLength | Sets the length of the request content. | int64 | No |
| XCosMetaXXX | User-defined file metadata. It must start with `x-cos-meta`; otherwise, it will be ignored. | http.Header | No |

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
| UploadId | ID that identifies the multipart upload. | string |
| Bucket | Bucket name in the format of `bucket-appid`. | string |
| Key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string |


<span id="MULIT_UPLOAD_PART"></span>
### Uploading parts 

This API is used to upload an object in parts.

#### Method prototype

```go
func (s *ObjectService) UploadPart(ctx context.Context, key, uploadID string, partNumber int, r io.Reader, opt *ObjectUploadPartOptions) (*Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-upload-part"
```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "strings"
)

func main() {
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    name := "exampleobject"
    // Optional. Considering the ACL limit, we recommend you not set an object ACL when uploading an object unless required. The object will then inherit the bucket ACL by default.
    v, _, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil)
    if err != nil {
        panic(err)
    }
    UploadID := v.UploadID
    fmt.Println(UploadID)
    // Note: Up to 10,000 parts can be uploaded.
    key := "exampleobject"
    f := strings.NewReader("test hello")
    // `opt` is optional.
    resp, err := client.Object.UploadPart(
        context.Background(), key, UploadID, 1, f, nil,
    )
    if err != nil {
        panic(err)
    }
    PartETag := resp.Header.Get("ETag")
    fmt.Println(PartETag)
}
```

#### Parameter description

```go
type ObjectUploadPartOptions struct {
    ContentLength   int64
    ContentMD5      string
}
```

| Parameter | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | --------- | -------- |
| key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string | Yes |
| UploadId | ID that identifies the multipart upload. It is generated by `InitiateMultipartUpload`. | string | Yes |
| PartNumber | Number that identifies the uploaded part. | int | Yes |
| r | Content of the uploaded part, which can be a local file stream or an input stream. When `r` is not `bytes.Buffer/bytes.Reader/strings.Reader`, `opt.ContentLength` must be specified. | io.Reader | Yes |
| ContentLength | Sets the length of the request content. | int64 | No |
| ContentMD5    | Base64-encoded 16-byte binary MD5 checksum of the request body content defined in RFC 1864. This value is a 24-character string, such as `ZzD3iDJdrMAAb00lgLLeig==`, and is used to verify whether the request body experienced any changes during transfer.      | string      | No       |

#### Response description

```go
{
    'ETag': 'string'
}
```
The returned result can be obtained from `Response`.
```go
resp, err := client.Object.UploadPart(context.Background(), key, UploadID, 1, f, nil)
etag := resp.Header.Get("ETag")
```


| Parameter | Description | Type |
| -------- | ----------------- | ------ |
| ETag | MD5 checksum of the uploaded part. | string |


<span id = "LIST_MULIT_UPLOAD"></span>
### Querying uploaded parts 

#### Feature description

This API is used to query the uploaded parts of a multipart upload.

#### Method prototype

```go
func (s *ObjectService) ListParts(ctx context.Context, name, uploadID string, opt *ObjectListPartsOptions) (*ObjectListPartsResult, *Response, error)

```

#### Sample request

[//]: # ".cssg-snippet-list-parts"
```go
package main                                                                                                                                                                                   

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main() {
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    key := "exampleobject"
    v, _, err := client.Object.InitiateMultipartUpload(context.Background(), key, nil)
    if err != nil {
        panic(err)
    }
    UploadID := v.UploadID
    fmt.Println(UploadID)
    _, _, err = client.Object.ListParts(context.Background(), key, UploadID, nil)
    if err != nil {
        panic(err)
    }
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
| ---------------- | ------------------------------------------------------------ | ------ | -------- |
| key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string | Yes |
| UploadId | ID that identifies the multipart upload. It is generated by `InitiateMultipartUpload`. | string | Yes |
| EncodingType | Encoding type of the returned value. | string | No |
| MaxParts | Maximum number of parts that can be returned at a time. Default value: 1000. | string | No |
| PartNumberMarker | The marker after which the returned list begins. By default, entries are listed in UTF-8 binary order. | string | No |

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
| Bucket               | Bucket name in the format of `BucketName-APPID`, for example, `examplebucket-1250000000`. | string |
| EncodingType | Encoding type of the returned value. The returned value is not encoded by default. Valid value: url. | string |
| Key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string |
| UploadId | ID that identifies the multipart upload. It is generated by `InitiateMultipartUpload`. | string |
| Initiator | Initiator of the multipart upload, including `DisplayName`, `UIN`, and `ID`. | struct |
| Owner | Information of the file owner, including `DisplayName`, `UIN`, and `ID`. | struct |
| StorageClass | Storage class of the object. Valid values: STANDARD; STANDARD_IA; ARCHIVE. Default value: STANDARD. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | string |
| PartNumberMarker | Specifies the part number after which the listing should begin. The default value is `0`, which means the listing begins with the first part. | string |
| NextPartNumberMarker | Specifies the part number after which the next listing should begin. | string |
| MaxParts | Maximum number of parts that can be returned at a time. Default value: 1000. | string |
| IsTruncated | Indicates whether the returned list is truncated. | bool |
| Part | Information of the uploaded part, including `ETag`, `PartNumber`, `Size`, and `LastModified`. | struct |


<span id = "COMPLETE_MULIT_UPLOAD"></span>
###  Completing multipart upload 

#### Feature description

This API is used to complete a multipart upload.

#### Method prototype

```go
func (s *ObjectService) CompleteMultipartUpload(ctx context.Context, key, uploadID string, opt *CompleteMultipartUploadOptions) (*CompleteMultipartUploadResult, *Response, error)

```

#### Sample request

[//]: # ".cssg-snippet-complete-multi-upload"
```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "strings"
)

func main() {
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    name := "exampleobject"
    // Optional. Considering the ACL limit, we recommend you not set an object ACL when uploading an object unless required. The object will then inherit the bucket ACL by default.
    v, _, err := client.Object.InitiateMultipartUpload(context.Background(), name, nil)
    if err != nil {
        panic(err)
    }
    UploadID := v.UploadID
    fmt.Println(UploadID)
    // Note: Up to 10,000 parts can be uploaded.
    key := "exampleobject"
    f := strings.NewReader("test hello")
    // `opt` is optional.
    resp, err := client.Object.UploadPart(
        context.Background(), key, UploadID, 1, f, nil,
    )
    if err != nil {
        panic(err)
    }
    PartETag := resp.Header.Get("ETag")
    fmt.Println(PartETag)

    opt := &cos.CompleteMultipartUploadOptions{}
    opt.Parts = append(opt.Parts, cos.Object{
        PartNumber: 1, ETag: PartETag},
    )
    _, _, err = client.Object.CompleteMultipartUpload(
        context.Background(), key, UploadID, opt,
    )
    if err != nil {
        panic(err)
    }
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
| ------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| key | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string | Yes |
| UploadId | ID that identifies the multipart upload. It is generated by `InitiateMultipartUpload`. | string | Yes |
| CompleteMultipartUploadOptions | Information of all parts, including `ETag` and `PartNumber`. | struct | Yes |

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
| Location | URL | string |
| Bucket               | Bucket name in the format of `BucketName-APPID`, for example, `examplebucket-1250000000`. | string |
| Key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string |
| ETag | Unique tag of a merged object. This value does not represent the MD5 checksum of the object content, but is used only to verify the uniqueness of the object as a whole. To verify the object content, check the `ETag` of each part during the upload process. | string |


### Aborting multipart upload 

#### Feature description

This API is used to abort a multipart upload and delete the uploaded parts.

#### Method prototype

```go
func (s *ObjectService) AbortMultipartUpload(ctx context.Context, key, uploadID string) (*Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-abort-multi-upload"
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main() {
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    key := "exampleobject"
    v, _, err := client.Object.InitiateMultipartUpload(context.Background(), key, nil)
    if err != nil {
        panic(err)
    }
    UploadID := v.UploadID
    // Abort
    _, err = client.Object.AbortMultipartUpload(context.Background(), key, UploadID)
    if err != nil {
        panic(err)
    }
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string | Yes |
| UploadId | ID that identifies the multipart upload. | string | Yes |


