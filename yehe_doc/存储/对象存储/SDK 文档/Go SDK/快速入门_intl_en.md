## Download and Installation

#### Relevant resources
- Download the source code for the COS XML Go SDK [here](https://github.com/tencentyun/cos-go-sdk-v5).
- Download the demo [here](https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example).
- For more information, see [GitHub](https://godoc.org/github.com/tencentyun/cos-go-sdk-v5).
- For the complete sample code, see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/Go).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-go-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, see [Go SDK](https://intl.cloud.tencent.com/document/product/436/40774).

>? If you encounter errors such as non-existent functions or methods when using the SDK, you can update the SDK to the latest version and try again.
>

#### Environmental dependencies
Golang is used to download and install the Go operating environment; it can be downloaded from the Golang official website.

#### Installing SDK
Execute the following command to install the COS Go SDK:
```sh
go get -u github.com/tencentyun/cos-go-sdk-v5
```

## Getting Started
The section below describes how to use the COS Go SDK to perform basic operations, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, or deleting an object.

### Initialization

>!
>- We recommend you use a sub-account key and environment variables to call the SDK for security purposes. When authorizing a sub-account, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
>- If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.



A COS GO client is generated using the COS domain name.

#### Method prototype
```Go
func NewClient(uri *BaseURL, httpClient *http.Client) *Client
```
#### Field description
```
// `BaseURL` indicates the base URL required for accessing APIs
type BaseURL struct {
    // Base URL (excluding `path`) for accessing bucket and object related APIs: https://examplebucket-1250000000.cos.<Region>.myqcloud.com
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
| BucketURL | Base URL (excluding `path`) for accessing bucket and object related APIs  | String | Yes   |
| ServiceURL| Base URL (excluding `path`) for accessing service APIs              | String | No   |
| BatchURL  | Base URL (excluding `path`) for accessing batch APIs               | String | No   |
| CIURL     | Base URL (excluding `path`) for accessing CI                      | String | No   |

#### Sample request 1: using a permanent key

[//]: # ".cssg-snippet-global-init"
```go
// Replace `examplebucket-1250000000` and `COS_REGION` with the actual information of users
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
// `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
// The following calls the `Get Service` API. By default, all regions (service.cos.myqcloud.com) will be queried.
su, _ := url.Parse("https://cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u, ServiceURL: su}
// 1. Permanent key
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
        SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
    },
})
```

#### Sample request 2: using a temporary key

[//]: # ".cssg-snippet-global-init-sts"
```go
// Replace `examplebucket-1250000000` and `COS_REGION` with the actual information
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
// `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 2. Temporary key
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        // If a temporary key is required, see the instructions at https://intl.cloud.tencent.com/document/product/436/14048 for generating and using a temporary key.
        SecretID:     "SECRETID",
        SecretKey:    "SECRETKEY",
        SessionToken: "SECRETTOKEN",
    },
})
if client != nil {
    // Call the COS request
}

```
>? For more information about how to generate and use a temporary key, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048).
>

#### Sample request 3: setting a domain name

By modifying `BaseURL`, you can directly use a custom domain name or global acceleration domain name to access COS.
```
// Use a global acceleration domain name to access COS
u, _ := url.Parse("http://<BucketName-APPID>.cos.accelerate.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 2. Temporary key
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        // If a temporary key is required, see the instructions at https://intl.cloud.tencent.com/document/product/436/14048 for generating and using a temporary key.
        SecretID:     "SECRETID",
        SecretKey:    "SECRETKEY",
        SessionToken: "SECRETTOKEN",
    },
})
```
#### Sample request 4: CRC64 verification

By default, CRC64 verification is enabled in the COS Go SDK for the uploaded objects.

>! 
>- The COS Go SDK version should be or later than v0.7.23.
>- You are strongly advised not to disable CRC64 verification.
>

```
// Replace `examplebucket-1250000000` and `COS_REGION` with the actual information
// Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
// `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 2. Temporary key
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        // If a temporary key is required, see the instructions at https://intl.cloud.tencent.com/document/product/436/14048 for generating and using a temporary key.
        SecretID:     "SECRETID",
        SecretKey:    "SECRETKEY",
        SessionToken: "SECRETTOKEN",
    },
})
// Disable CRC64 verification.
client.Conf.EnableCRC = false

```

### Creating a bucket

```Go
package main


import (
    "context"
    "net/http"
    "net/url"
    "os"


    "github.com/tencentyun/cos-go-sdk-v5"
)


func main(){
    // Replace `examplebucket-1250000000` and `COS_REGION` with the actual information
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
        },
    })


    _, err := c.Bucket.Put(context.Background(), nil)
    if err != nil{
        panic(err)
    }
}
```


### Querying the bucket list
```go
package main


import (
    "context"
    "fmt"
    "net/http"
    "os"


    "github.com/tencentyun/cos-go-sdk-v5"
)


func main(){
    c := cos.NewClient(nil, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
        },
    })


    s, _, err := c.Service.Get(context.Background())
    if err != nil{
        panic(err)
    }


    for _, b := range s.Buckets {
        fmt.Printf("%#v\n", b)
    }
}
```

### Uploading an object
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


func main(){
    // Replace `examplebucket-1250000000` and `COS_REGION` with the actual information
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
        },
    })
    // An object key is the unique identifier of an object in a bucket
    // For example, in the access domain name `examplebucket-1250000000.cos.COS_REGION.myqcloud.com/test/objectPut.go`, the object key is `test/objectPut.go`
    name := "test/objectPut.go"
    // 1. Upload the object with a string.
    f := strings.NewReader("test")


    _, err := c.Object.Put(context.Background(), name, f, nil)
    if err != nil{
        panic(err)
    }
    // 2. Upload the object with a local file.
    _, err = c.Object.PutFromFile(context.Background(), name, "../test", nil)
    if err != nil{
        panic(err)
    }
    // 3. Upload the object with a file stream.
    fd, err := os.Open("./test")
    if err != nil{
        panic(err)
    }
    defer fd.Close()
    _, err = c.Object.Put(context.Background(), name, fd, nil)
    if err != nil{
        panic(err)
    }
}
```

### Querying objects
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


func main(){
    // Replace `examplebucket-1250000000` and `COS_REGION` with the actual information
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
        },
    })


    opt := &cos.BucketGetOptions{
        Prefix:  "test",
        MaxKeys: 3,
    }
    v, _, err := c.Bucket.Get(context.Background(), opt)
    if err != nil{
        panic(err)
    }


    for _, c := range v.Contents {
        fmt.Printf("%s, %d\n", c.Key, c.Size)
    }
}
```

### Download an object
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


func main(){
    // Replace `examplebucket-1250000000` and `COS_REGION` with the actual information
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
        },
    })
    // 1. Obtain the object through response body
    name := "test/objectPut.go"
    resp, err := c.Object.Get(context.Background(), name, nil)
    if err != nil{
        panic(err)
    }
    bs, _ := ioutil.ReadAll(resp.Body)
    resp.Body.Close()
    fmt.Printf("%s\n", string(bs))
    // 2. Download the object to the local file system
    _, err = c.Object.GetToFile(context.Background(), name, "exampleobject", nil)
    if err != nil{
        panic(err)
    }
}
```

### Deleting an object
```go
package main


import (
    "context"
    "net/http"
    "net/url"
    "os"

    "github.com/tencentyun/cos-go-sdk-v5"
)


func main(){
    // Replace `examplebucket-1250000000` and `COS_REGION` with the actual information
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // `COS_REGION` can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
        },
    })
    name := "test/objectPut.go"
    _, err := c.Object.Delete(context.Background(), name)
    if err != nil{
        panic(err)
    }
}
```
