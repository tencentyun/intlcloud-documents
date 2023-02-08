## Overview

This document provides an overview of APIs and SDK code samples related to bucket referer allowlist or blocklist.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting bucket referer configuration | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying bucket referer configuration | Queries a bucket referer allowlist or blocklist |

## Setting Bucket Referer Configuration

#### Feature description

This API (PUT Bucket referer) is used to set a referer allowlist/blocklist for a bucket.

#### Method prototype

```go
func (s *BucketService) PutReferer(ctx context.Context, opt *BucketPutRefererOptions) (*Response, error)
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
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://www.tencentcloud.com/document/product/598/32675.
        },
    })
    opt := &cos.BucketPutRefererOptions{
        Status:      "Enabled",
        RefererType: "White-List",
        DomainList: []string{
            "*.qq.com",
            "*.qcloud.com",
        },
        EmptyReferConfiguration: "Allow",
    }

    _, err := client.Bucket.PutReferer(context.Background(), opt)
}
```

#### Field description

```go
type BucketPutRefererOptions struct {
    Status                  string 
    RefererType             string 
    DomainList              []string 
    EmptyReferConfiguration string
}
```

| Parameter  | Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| Status   | Whether hotlink protection is enabled. Enumerated values: `Enabled, `Disabled` | String                                   |
| RefererType    | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String |
| DomainList | A list of domains, which can include ports, IPs, or asterisks (\*). You can set multiple domains. | Array |
| EmptyReferConfiguration | Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` | String |

## Querying Bucket Referer Configuration

#### Feature description

This API (GET Bucket referer) is used to query the referer allowlist/blocklist of a bucket.

#### Method prototype

```go
func (s *BucketService) GetReferer(ctx context.Context) (*BucketGetRefererResult, *Response, error)
```

#### Sample request

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
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://www.tencentcloud.com/document/product/598/32675.
        },
    })
    res, _, err := client.Bucket.GetReferer(context.Background())
    if err != nil{
        fmt.Println(err)
    }
    fmt.Println(res)
}
```

#### Response description

```go
type BucketGetRefererResult struct {
    Status                  string 
    RefererType             string 
    DomainList              []string 
    EmptyReferConfiguration string
}
```

| Parameter  | Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| Status   | Whether hotlink protection is enabled. Enumerated values: `Enabled, `Disabled` | String                                   |
| RefererType    | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String |
| DomainList | A list of domains, which can include ports, IPs, or asterisks (\*). You can set multiple domains. | Array |
| EmptyReferConfiguration | Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` | String |
