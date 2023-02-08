

## Feature Overview

This document provides an overview of APIs and SDK code samples for custom domains.

| API | Operation | Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting a custom domain | Sets a custom domain for a bucket |
| GET Bucket domain    | Querying a custom domain | Queries the custom domain of a bucket |
| DELETE Bucket domain | Deleting custom domains | Deletes custom domains from a bucket |

## Setting Custom Domains

#### Feature description

This API is used to set a custom domain for a bucket.

#### Method prototype

```go
func (s *BucketService) PutDomain(ctx context.Context, opt *BucketPutDomainOptions) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-domain)
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
    opt := &cos.BucketPutDomainOptions{
        Rules: []cos.BucketDomainRule{
            {
                Status:            "ENABLED",
                Name:              "www.example.com",
                Type:              "REST",
                ForcedReplacement: "CNAME",
            },
        },
    }
    _, err := client.Bucket.PutDomain(context.Background(), opt)
    if err != nil{
        fmt.Println(err)
    }
}
```

#### Field description

```go
type BucketDomainRule struct {
    Status            string
    Name              string
    Type              string
    ForcedReplacement string
}

type BucketPutDomainOptions struct {
    XMLName                xml.Name
    Rules   []BucketDomainRule
}
```

| Parameter | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| BucketPutDomainOptions | Custom domain configurations                                   | Struct |
| Rules                  | Domain configuration rules                                     | Array  |
| Status                 | Domain status. Valid values: `ENABLED`, `DISABLED`             | String |
| Name                   | Custom domain. Letters, digits, and dots (.) are supported.          | String |
| Type                   | Type of the origin server to bind. Valid values: `REST`, `WEBSITE`                          | String |
| ForcedReplacement      | Replaces existing configurations. Valid values: `CNAME`, `TXT`. If this parameter is specified, configurations will only be delivered after the domain ownership is verified. | String |

#### Error codes

The following describes some common errors that may occur when you call this API:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The domain record already exists, and forced overwrite is not specified in the request; OR the domain record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The domain does not have an ICP filing in the Chinese mainland                          |

## Querying a Custom Domain

#### Feature description

This API is used to query the custom domain set for a bucket.

#### Method prototype

```go
func (s *BucketService) GetDomain(ctx context.Context) (*BucketGetDomainResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-domain)
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
    v, _, err := client.Bucket.GetDomain(context.Background())
    if err != nil{
        fmt.Println(err)
    }
    fmt.Println(v)
}
```

#### Response description

```go
type BucketGetDomainResult BucketPutDomainOptions
```

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| BucketGetDomainResult | Custom domain configurations                                          | Struct |
| Rules                 | Domain configuration rules                            | Array  |
| Status                | Domain status. Valid values: `ENABLED`, `DISABLED`                   | String |
| Name                  | Custom domain. Letters, digits, and dots (.) are supported. | String |
| Type                  | Type of the origin server bound. Valid values: `REST`, `WEBSITE`                          | String |
| ForcedReplacement      | Replaces existing configurations. Valid values: `CNAME`, `TXT`. If this parameter is specified, configurations will only be delivered after the domain ownership is verified. | String |

## Deleting Custom Domains

This API (DELETE  Bucket domain) is used to delete all custom domains bound to a bucket.

#### Method prototype

```go
func (s *BucketService) DeleteDomain(ctx context.Context) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-domain)
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
    _, err := client.Bucket.DeleteDomain(context.Background())
    if err != nil{
        fmt.Println(err)
    }
}
```
