## Download and Installation

#### Related resources
- Download the COS XML Go SDK source code from [GitHub](https://github.com/tencentyun/cos-go-sdk-v5).
- Download the XML Go SDK demo from [GitHub](https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example).
- For more information, see [COS Go SDK](https://godoc.org/github.com/tencentyun/cos-go-sdk-v5).
- For all the code samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/Go).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-go-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, see [Go SDK](https://intl.cloud.tencent.com/document/product/436/40774).

>? If you encounter errors such as non-existent functions or methods when using the SDK, update the SDK to the latest version and try again.
>

#### Environmental dependencies
Go is used to download and install the SDK compilation and runtime environment. It can be downloaded from the Go official website.

#### Installing SDK
Run the following command to install the COS Go SDK:
```sh
go get -u github.com/tencentyun/cos-go-sdk-v5
```

## Getting Started
The section below describes how to use the COS Go SDK to perform basic operations, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, or deleting an object.

### Initialization
Use the COS domain name to generate a COS Go client.

#### Method prototype
```Go
func NewClient(uri *BaseURL, httpClient *http.Client) *Client
```
#### Parameter description
```
// `BaseURL` indicates the base URL required for accessing APIs
type BaseURL struct {
    // Base URL (excluding `path`) for accessing bucket and object APIs: https://examplebucket-1250000000.cos.<Region>.myqcloud.com
    BucketURL *url.URL
    // Base URL (excluding `path`) for accessing service APIs: https://cos.<Region>.myqcloud.com
    ServiceURL *url.URL
    // Base URL (excluding `path`) for accessing batch APIs: https://<UIN>.cos-control.<Region>.myqcloud.com
    BatchURL *url.URL
    // Base URL (excluding `path`) for accessing CI: https://examplebucket-1250000000.ci.<Region>.myqcloud.com
    CIURL *url.URL
}
```

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| BucketURL | Base URL (excluding `path`) for accessing bucket and object APIs  | String | Yes   |
| ServiceURL| Base URL (excluding `path`) for accessing service APIs              | String | No   |
| BatchURL  | Base URL (excluding `path`) for accessing batch APIs               | String | No   |
| CIURL     | Base URL (excluding `path`) for accessing CI                      | String | No   |

#### Sample request 1: Using a permanent key

[//]: # (.cssg-snippet-global-init)
```go
// Replace `examplebucket-1250000000` and `COS_REGION` with your actual information
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
// `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
// The following calls the `Get Service` API. By default, all regions (service.cos.myqcloud.com) will be queried.
su, _ := url.Parse("https://cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u, ServiceURL: su}
// 1. Permanent key
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretID:  "SECRETID",  // Replace it with your actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
        SecretKey: "SECRETKEY", // Replace it with your actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
    },
})
```

#### Sample request 2: Using a temporary key

[//]: # (.cssg-snippet-global-init-sts)
```go
// Replace `examplebucket-1250000000` and `COS_REGION` with your actual information
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
// `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 2. Temporary key
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        // This is required for temporary keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
        SecretID:     "SECRETID",
        SecretKey:    "SECRETKEY",
        SessionToken: "SECRETTOKEN",
    },
})
if client != nil {
    // Make a request to COS
}

```
>? For more information on how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

#### Sample request 3: Setting a domain name

By modifying `BaseURL`, you can directly use a custom domain name or global acceleration domain name to access COS.
```
// Use a global acceleration domain name to access COS
u, _ := url.Parse("http://<BucketName-APPID>.cos.accelerate.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 2. Temporary key
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        // This is required for temporary keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
        SecretID:     "SECRETID",
        SecretKey:    "SECRETKEY",
        SessionToken: "SECRETTOKEN",
    },
})
```
#### Sample request 4: Performing CRC64 check

CRC64 check is enabled in the COS Go SDK for uploaded objects by default.

>! 
>- The COS Go SDK should be on v0.7.23 or later.
>- We strongly recommend you keep CRC64 check enabled.
>

```
// Replace `examplebucket-1250000000` and `COS_REGION` with your actual information
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
// `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 2. Temporary key
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        // This is required for temporary keys. For more information on how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
        SecretID:     "SECRETID",
        SecretKey:    "SECRETKEY",
        SessionToken: "SECRETTOKEN",
    },
})
// Disable CRC64 check
client.Conf.EnableCRC = false

```

### Creating bucket

```Go
package main


import (
    "context"
    "net/http"
    "net/url"
    "os"


    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    // Replace `examplebucket-1250000000` and `COS_REGION` with your actual information
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",   // Replace it with your actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: "SECRETKEY",  // Replace it with your actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
        },
    })


    _, err := c.Bucket.Put(context.Background(), nil)
    if err != nil {
        panic(err)
    }
}
```


### Querying bucket list
```go
package main


import (
    "context"
    "fmt"
    "net/http"
    "os"


    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    c := cos.NewClient(nil, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",   // Replace it with your actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: "SECRETKEY",  // Replace it with your actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
        },
    })


    s, _, err := c.Service.Get(context.Background())
    if err != nil {
        panic(err)
    }


    for _, b := range s.Buckets {
        fmt.Printf("%#v\n", b)
    }
}
```

### Uploading object
```Go
package main


import (
    "context"
    "net/http"
    "net/url"
    "os"
    "strings"

    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    // Replace `examplebucket-1250000000` and `COS_REGION` with your actual information
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",   // Replace it with your actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: "SECRETKEY",  // Replace it with your actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
        },
    })
    // Object key, which is the unique identifier of the object in the bucket.
    // For example, in the access domain name `examplebucket-1250000000.cos.COS_REGION.myqcloud.com/test/objectPut.go`, the object key is `test/objectPut.go`.
    name := "test/objectPut.go"
    // 1. Upload an object through a string
    f := strings.NewReader("test")


    _, err := c.Object.Put(context.Background(), name, f, nil)
    if err != nil {
        panic(err)
    }
    // 2. Upload an object through a local file
    _, err = c.Object.PutFromFile(context.Background(), name, "../test", nil)
    if err != nil {
        panic(err)
    }
    // 3. Upload an object through a file stream
    fd, err := os.Open("./test")
    if err != nil {
        panic(err)
    }
    defer fd.Close()
    _, err = c.Object.Put(context.Background(), name, fd, nil)
    if err != nil {
        panic(err)
    }
}
```

### Querying object list
```go
package main


import (
    "context"
    "fmt"
    "net/http"
    "net/url"
    "os"

    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    // Replace `examplebucket-1250000000` and `COS_REGION` with your actual information
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",   // Replace it with your actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: "SECRETKEY",  // Replace it with your actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
        },
    })


    opt := &cos.BucketGetOptions{
        Prefix:  "test",
        MaxKeys: 3,
    }
    v, _, err := c.Bucket.Get(context.Background(), opt)
    if err != nil {
        panic(err)
    }


    for _, c := range v.Contents {
        fmt.Printf("%s, %d\n", c.Key, c.Size)
    }
}
```

### Downloading object
```Go
package main


import (
    "context"
    "fmt"
    "io/ioutil"
    "net/http"
    "net/url"
    "os"

    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    // Replace `examplebucket-1250000000` and `COS_REGION` with your actual information
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",   // Replace it with your actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: "SECRETKEY",  // Replace it with your actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
        },
    })
    // 1. Get an object through the response body
    name := "test/objectPut.go"
    resp, err := c.Object.Get(context.Background(), name, nil)
    if err != nil {
        panic(err)
    }
    bs, _ := ioutil.ReadAll(resp.Body)
    resp.Body.Close()
    fmt.Printf("%s\n", string(bs))
    // 2. Download an object to the local file system
    _, err = c.Object.GetToFile(context.Background(), name, "exampleobject", nil)
    if err != nil {
        panic(err)
    }
}
```

### Deleting object
```go
package main


import (
    "context"
    "net/http"
    "net/url"
    "os"

    "github.com/tencentyun/cos-go-sdk-v5"
)


func main() {
    // Replace `examplebucket-1250000000` and `COS_REGION` with your actual information
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. For more information on regions, visit https://cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",   // Replace it with your actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: "SECRETKEY",  // Replace it with your actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
        },
    })
    name := "test/objectPut.go"
    _, err := c.Object.Delete(context.Background(), name)
    if err != nil {
        panic(err)
    }
}
```
