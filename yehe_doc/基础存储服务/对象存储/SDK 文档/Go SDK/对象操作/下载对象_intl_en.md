## Overview

This document provides an overview of APIs and SDK code samples for downloading an object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | Downloading an object | Downloads an object (file) to the local file system |

## Advanced APIs (Recommended)

### Downloading an object

#### Feature description

The multipart download API automatically downloads data concurrently with `Range` according to the object size. If you use `Range` to download an object larger than 16 MB, you can use the `PartSize` parameter to adjust the part size.

#### Method prototype

```go
func (s *ObjectService) Download(ctx context.Context, name string, filepath string, opt *MultiDownloadOptions) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-download-file)
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })

    key := "exampleobject"
    file := "localfile"

    opt := &cos.MultiDownloadOptions{
        ThreadPoolSize: 5,
    }
    _, err := client.Object.Download(
        context.Background(), key, file, opt,
    )
    if err != nil{
        panic(err)
    }
}
```

#### Field description

```go
type MultiDownloadOptions struct {
    Opt            *ObjectGetOptions
    PartSize       int64
    ThreadPoolSize int
    CheckPoint     bool
    CheckPointFile string
}
```

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | ------ | ---- |
| name | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`. | String | Yes |
| filepath | Name of the local file | String | Yes |
| opt            | Object download parameter             | Struct | No |
| Opt | Request parameter. For more information, please see [ObjectGetOptions](#.E4.B8.8B.E8.BD.BD.E5.AF.B9.E8.B1.A12). | Struct | No |
| PartSize | Part size (in MB). If this parameter is not specified or is set to a value smaller than or equal to 0, its value will be automatically determined. In the new version, the default size is 16 (MB). | int64 | No |
| ThreadPoolSize | Size of the thread pool. Default value: `1` | Int | No |
| CheckPoint     | Whether to enable checkpoint restart. Default value: `false`  | Bool   | No   |
| CheckPointFile | Path to save the download progress file when checkpoint restart is enabled. The default value is `&lt;filepath>.cosresumabletask`. When the download is completed, this progress file will be cleared. | String   | No |

#### Response description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| \*Response| HTTP response, through which you can obtain the response status code, response headers, and other information. | Struct |
| error    | Error message. If no error occurs, `nil` will be returned.                  | Struct |

## Simple Operations

### Downloading an object

#### Feature description

This API (GET Object) is used to download an object (file) to a local file system. Simple downloads and batch downloads are supported.

#### Method prototype

```go
func (s *ObjectService) Get(ctx context.Context, key string, opt *ObjectGetOptions) (*Response, error)

func (s *ObjectService) GetToFile(ctx context.Context, key, localfile string, opt *ObjectGetOptions) (*Response, error)
```

#### Sample 1: downloading an object

[//]: # (.cssg-snippet-get-object)
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "io/ioutil"
    "os"
)

func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })

    key := "exampleobject"
    opt := &cos.ObjectGetOptions{
        ResponseContentType: "text/html",
        Range:               "bytes=0-3", // Download the first 4 bytes of data
    }
    // `opt` is optional. It can be set to `nil` unless otherwise specified.
    // 1. Obtain the object from the response body
    resp, err := client.Object.Get(context.Background(), key, opt)
    if err != nil{
        panic(err)
    }
    ioutil.ReadAll(resp.Body)
    resp.Body.Close()

    // 2. Download the object to the local file system
    _, err = client.Object.GetToFile(context.Background(), key, "example.txt", nil)
    if err != nil{
        panic(err)
    }
}
```
#### Sample 2: batch downloading files (downloading a COS directory)
```go
package main
import (
    "context"
    "fmt"
    "net/http"
    "net/url"
    "os"
    "path"
    "strings"
    "sync"

    "github.com/tencentyun/cos-go-sdk-v5"
)

func download(wg *sync.WaitGroup, c *cos.Client, keysCh <-chan []string) {
    defer wg.Done()
    for keys := range keysCh {
        key := keys[0]
        filename := keys[1]
        _, err := c.Object.GetToFile(context.Background(), key, filename, nil)
        if err != nil{
            fmt.Println(err)
        }
    }
}
func main(){
    u, _ := url.Parse("https://test-1259654469.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
            Transport: &cos.AuthorizationTransport{
				// os.Getenv indicates to get the key from environment variables
                SecretID:  os.Getenv("SECRETID"),   // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
                SecretKey: os.Getenv("SECRETKEY"),// User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
            },
    })
    // Multi-thread execution
    keysCh := make(chan []string, 3)
    var wg sync.WaitGroup
    threadpool := 3
    for i := 0; i < threadpool; i++ {
            wg.Add(1)
            go download(&wg, c, keysCh)
    }
    isTruncated := true
    prefix := "dir" // Download all files in the `dir` directory
    marker := ""
    localDir := "./local/"
    for isTruncated {
        opt := &cos.BucketGetOptions{
            Prefix:       prefix,
            Marker:       marker,
            EncodingType: "url", // URL code
        }
        // List directories
        v, _, err := c.Bucket.Get(context.Background(), opt)
        if err != nil{
            fmt.Println(err)
            break
        }
        for _, c := range v.Contents {
            key, _ := cos.DecodeURIComponent(c.Key) //EncodingType: "url". Perform URL decoding on the key first.
            localfile := localDir + key
            if _, err := os.Stat(path.Dir(localfile)); err != nil && os.IsNotExist(err) {
                os.MkdirAll(path.Dir(localfile), os.ModePerm)
            }
            // Keys (directories and files) ended with a slash (/) do not need to be downloaded
            if strings.HasSuffix(localfile, "/") {
                continue
            }
            keysCh <- []string{key, localfile}
        }
        marker, _ = cos.DecodeURIComponent(v.NextMarker) // EncodingType: "url". Perform URL decoding on NextMarker first.
        isTruncated = v.IsTruncated
    }
    close(keysCh)
    wg.Wait()
}
```

#### Sample 3: limiting single-URL speed
```go

package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })

    key := "exampleobject"
    opt := &cos.ObjectGetOptions{
        // The speed range is 819200 to 838860800, that is 100 KB/s to 100 MB/s. If the value is not within this range, 400 will be returned.
        XCosTrafficLimit: 819200,
    }
    // `opt` is optional. It can be set to `nil` unless otherwise specified.
    // 1. Obtain the object from the response body
    _, err := client.Object.GetToFile(context.Background(), key, "example.txt", opt)
    if err != nil{
        panic(err)
    }
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
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "io/ioutil"
    "net/http"
    "net/url"
    "os"
)

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
func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })
    key := "exampleobject"
    opt := &cos.ObjectGetOptions{
        ResponseContentType: "text/html",
        // View the progress using the default progress listener.
	Listener: &cos.DefaultProgressListener{},
    }
    // `opt` is optional. It can be set to `nil` unless otherwise specified.
    // 1. Obtain the object from the response body
    resp, err := client.Object.Get(context.Background(), key, opt)
    if err != nil{
        panic(err)
    }
    ioutil.ReadAll(resp.Body)
    resp.Body.Close()

    // 2. Download the object to the local file system
    // Use the custom progress callback method.
    opt.Listener = &SelfListener{}
    _, err = client.Object.GetToFile(context.Background(), key, "example.txt", opt)
    if err != nil{
        panic(err)
    }
}
```

#### Field description

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
| key  | `ObjectKey` is the unique identifier of an object in a bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the `ObjectKey` is `doc/pic.jpg`. | string | Yes |
| localfile | Name of the file downloaded to the local file system | string | Yes |
| ResponseContentType | `Content-Type` of the response header | string | No |
| ResponseContentLanguage | `Content-Language` of the response header | string | No |
| ResponseExpires | `Content-Expires` of the response header | string | No |
| ResponseCacheControl | `Cache-Control` of the response header | string | No |
| ResponseContentDisposition | `Content-Disposition` of the response header | string | No |
| ResponseContentEncoding | `Content-Encoding` of the response header | string | No |
| Range | Byte range of the file to download. Format: `bytes=first-last` | string | No |
| IfModifiedSince | Returned only if the object is modified after the specified time | string | No |
| XCosTrafficLimit           | Speed limit for a single URL                            | int    | No |
| Listener                   | Progress callback API                              | struct | No |

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
| File metadata | Metadata of the downloaded file, including `ETag` and `X-Cos-Request-Id`. The metadata of the configured file is also returned. | String |
