## Download and installation

#### Relevant Resources
- Download the source code of COS XML Go SDK: (https://github.com/tencentyun/cos-wx-sdk-v5).
- Download the demo: (https://github.com/tencentyun/cos-wx-sdk-v5/tree/master/demo).
- For more information, see [COS Go SDK API](https://godoc.org/github.com/tencentyun/cos-go-sdk-v5).

#### Environmental Requirements
- Golang: Used to download and install the Go environment, which can be downloaded from Golang’s official website

#### Installing the SDK
Execute the following command to install COS Go SDK:
```sh
go get -u github.com/tencentyun/cos-go-sdk-v5/
```

## Getting Started
The section below describes how to use COS SDK for Go to perform basic operations, such as initializing a client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object..

### Initialization
The COS GO client structure is generated using the COS domain name.

#### Method Prototype
```Go
func NewClient(uri *BaseURL, httpClient *http.Client) *Client
```

#### Request Samples
Use a permanent key:

[//]: # (.cssg-snippet-global-init)
```go
// Change examplebucket-1250000000 and COS_REGION into actual information
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 1. Permanent key
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretId: 'COS_SECRETID',
        SecretKey: 'COS_SECRETKEY'
    },
})
```

Use a temporary key:

[//]: # (.cssg-snippet-global-init-sts)
```go
// Change examplebucket-1250000000 and COS_REGION into actual information
u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
// 2. Temporary key
client := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretId: 'COS_SECRETID',
        SecretKey: 'COS_SECRETKEY'
        SessionToken："COS_SECRETTOKEN",
    },
})
if client != nil {
    // Call COS request
}
```

For more information on how to generate and use a temporary key, see [Generating and using temporary keys](https://intl.cloud.tencent.com/document/product/436/14048).

### Creating a Bucket

[//]: # (.cssg-snippet-put-bucket-comp)
```Go
package main

import(
    "context"
    "net/http"
    "net/url"
    [os]

    "github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
    // Change examplebucket-1250000000 and COS_REGION into actual information
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretId: 'COS_SECRETID',
            SecretKey: 'COS_SECRETKEY'
        },
    })

    _, err := c.Bucket.Put(context.Background(), nil)
    if err != nil {
        panic(err)
    }
}
```


### Querying the Bucket List
[//]: # (.cssg-snippet-get-service-comp)
```go
package main

import(
    "context"
    "fmt"
    "net/http"
    [os]

    "github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
    c := cos.NewClient(nil, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretId: 'COS_SECRETID',
            SecretKey: 'COS_SECRETKEY'
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

### Uploading an Object
[//]: # (.cssg-snippet-put-object-comp)
```Go
package main

import(
    "context"
    "net/http"
    "net/url"
    [os]
    "strings"

    "github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
    // Change examplebucket-1250000000 and COS_REGION into actual information
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretId: 'COS_SECRETID',
            SecretKey: 'COS_SECRETKEY'
        },
    })
    Object key is the unique identifier of the object in the bucket.
    // For example, in the access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/test/objectPut.go`, the object key is test/objectPut.go
    name := "test/objectPut.go"
    // 1. Upload the object using key
    f := strings.NewReader("test")

    _, err := c.Object.Put(context.Background(), name, f, nil)
    if err != nil {
        panic(err)
    }
    // 2. Upload the object through local files
    _, err = c.Object.PutFromFile(context.Background(), name, "./test", nil)
    if err != nil {
        panic(err)
    }
}
```

### Querying the Object List
[//]: # (.cssg-snippet-get-bucket-comp)
```go
package main

import(
    "context"
    "fmt"
    "net/http"
    "net/url"
    [os]

    "github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
    // Change examplebucket-1250000000 and COS_REGION into actual information
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretId: 'COS_SECRETID',
            SecretKey: 'COS_SECRETKEY'
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

### Downloading an Object
[//]: # (.cssg-snippet-get-object-comp)
```Go
package main

import(
    "context"
    "fmt"
    "io/ioutil"
    "net/http"
    "net/url"
    [os]

    "github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
    // Change examplebucket-1250000000 and COS_REGION into actual information
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretId: 'COS_SECRETID',
            SecretKey: 'COS_SECRETKEY'
        },
    })
    // 1. Obtain the object through response body
    name := "test/objectPut.go"
    resp, err := c.Object.Get(context.Background(), name, nil)
    if err != nil {
        panic(err)
    }
    bs, _ := ioutil.ReadAll(resp.Body)
    resp.Body.Close()
    fmt.Printf("%s\n", string(bs))
    // 2. Obtain the object to local files
    _, err = c.Object.GetToFile(context.Background(), name, "example", nil)
    if err != nil {
        panic(err)
    }
}
```

### Deleting an object
[//]: # (.cssg-snippet-delete-object-comp)
```go
package main

import(
    "context"
    "net/http"
    "net/url"
    [os]

    "github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
    // Change examplebucket-1250000000 and COS_REGION into actual information
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretId: 'COS_SECRETID',
            SecretKey: 'COS_SECRETKEY'
        },
    })
    name := "test/objectPut.go"
    _, err := c.Object.Delete(context.Background(), name)
    if err != nil {
        panic(err)
    }
}
```
