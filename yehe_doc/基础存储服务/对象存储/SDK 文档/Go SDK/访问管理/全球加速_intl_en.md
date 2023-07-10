
## Overview

This document provides an overview of APIs and SDK code samples related to global acceleration.

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :------------------------------- |
| [PUT Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33411)| Setting global acceleration | Enables/Suspends global acceleration for a bucket |
| [GET Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33412)| Querying global acceleration | Queries the global acceleration configuration of a bucket |


## Setting Global Acceleration

#### Feature description

This API is used to enable or suspend global acceleration.

#### Method prototype

```go
func (s *BucketService) PutAccelerate(ctx context.Context, opt *BucketPutAccelerateOptions) (*Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-put-accelerate"
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
    opt := &cos.BucketPutAccelerateOptions{
        Status: "Enabled",
        Type:   "COS",
    }
    _, err := client.Bucket.PutAccelerate(context.Background(), opt)
    if err != nil{
        // ERROR
    }
}
```
#### Field description

```go
type BucketPutAccelerateOptions struct {
    Status  string
}
```

| Parameter | Description | Type | Required |
| -------- | ---------------------------------------------------- | ------ | ---- |
| Status   | Whether to enable global acceleration. Valid values: `Suspended`, `Enabled` | string | Yes   |

## Querying Global Acceleration

#### Feature description

This API is used to query the global acceleration configuration of a bucket.

#### Method prototype

```go
func (s *BucketService) GetAccelerate(ctx context.Context) (*BucketGetAccelerateResult, *Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-get-accelerate"
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
    res, _, err := client.Bucket.GetAccelerate(context.Background())
    if err != nil{
        // ERROR
    }
    fmt.Println(res)
}
```
#### Response description

```go
type BucketGetAccelerateResult struct {
    Status  string
}
```

| Parameter | Description | Type | Required |
| -------- | ---------------------------------------------------- | ------ | ---- |
| Status   | Whether to enable global acceleration. Valid values: `Suspended`, `Enabled` | string | Yes   |
