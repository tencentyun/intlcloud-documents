## Download and Installation

#### Relevant Resources
- Download the source code for the COS XML Go SDK [here](https://github.com/tencentyun/cos-wx-sdk-v5).
- Download the demo [here](https://github.com/tencentyun/cos-wx-sdk-v5/tree/master/demo).
- For more information, see [COS Go SDK API](https://godoc.org/github.com/tencentyun/cos-go-sdk-v5).
- Find all code samples for this SDK [here](https://github.com/tencentyun/cos-snippets/tree/master/Go).

#### Environmental dependencies
- Golang is used to download and install the Go operating environment; it can be downloaded from the Golang official website.

### Installing the SDK
Execute the following command to install the COS Go SDK:
```sh
go get -u github.com/tencentyun/cos-go-sdk-v5
```

## Getting started
The section below describes how to use the COS Go SDK to perform basic operations, such as initializing a client, creating a bucket, querying a bucket list, uploading an object, querying an object list, downloading an object, and deleting an object..

### Initialization
A COS GO client is generated using the COS domain name.

#### Method prototype
```Go
func NewClient(uri *BaseURL, httpClient *http.Client) *Client
```

#### Sample request 
Using a permanent key:

[//]: # (.cssg-snippet-global-init)
```go
// Replace examplebucket-1250000000 and COS_REGION with your information
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

Using a temporary key:

[//]: # (.cssg-snippet-global-init-sts)
```go
// Replace examplebucket-1250000000 and COS_REGION with your information
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
    // Call the COS request
}
```

For more information on how to generate and use a temporary key, see [Generating and using temporary keys](https://intl.cloud.tencent.com/document/product/436/14048).

### Creating a bucket


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
    // Replace examplebucket-1250000000 and COS_REGION with your information
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


### Querying a bucket list

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

### Uploading an object

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
    // Replace examplebucket-1250000000 and COS_REGION with your information
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretId: 'COS_SECRETID',
            SecretKey: 'COS_SECRETKEY'
        },
    })
    // An object key is the unique identifier of an object in a bucket.
    // For example, in the access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/test/objectPut.go`, the object key is `test/objectPut.go`
    name := "test/objectPut.go"
    // 1. Uploading an object using a key
    f := strings.NewReader("test")

    _, err := c.Object.Put(context.Background(), name, f, nil)
    if err != nil {
        panic(err)
    }
    // 2. Uploading an object through local files
    _, err = c.Object.PutFromFile(context.Background(), name, "./test", nil)
    if err != nil {
        panic(err)
    }
}
```

### Querying an object list

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
    // Replace examplebucket-1250000000 and COS_REGION with your information
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

### Downloading an object

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
    // Replace examplebucket-1250000000 and COS_REGION with your information
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    c := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretId: 'COS_SECRETID',
            SecretKey: 'COS_SECRETKEY'
        },
    })
    // 1. Getting the object through the response body
    name := "test/objectPut.go"
    resp, err := c.Object.Get(context.Background(), name, nil)
    if err != nil {
        panic(err)
    }
    bs, _ := ioutil.ReadAll(resp.Body)
    resp.Body.Close()
    fmt.Printf("%s\n", string(bs))
    // 2. Downloading the object to the local file system
    _, err = c.Object.GetToFile(context.Background(), name, "example", nil)
    if err != nil {
        panic(err)
    }
}
```

### Deleting an object

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
    // Replace examplebucket-1250000000 and COS_REGION with your information
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
