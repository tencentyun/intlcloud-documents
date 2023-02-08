## Overview

This document provides an overview of APIs and SDK code samples for versioning.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

## Setting Versioning

#### Feature description

This API (`PUT Bucket versioning`) is used to set the versioning configuration for a bucket.

#### Method prototype
```go
func (s *BucketService) PutVersioning(ctx context.Context, opt *BucketPutVersionOptions) (*Response, error)
```

#### Sample request
[//]: # (.cssg-snippet-put-bucket-versioning)
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
    u, _ := url.Parse("https://examplebucket-12500000000.cos.ap-guangzhou.myqcloud.com")
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
    opt := &cos.BucketPutVersionOptions{
        // `Enabled` or `Suspended`; once enabled, versioning can only be paused but not deleted.
        Status: "Enabled",
    }
    _, err := client.Bucket.PutVersioning(context.Background(), opt)
    if err != nil{
        panic(err)
    }
}
```

#### Field description
```go
type BucketPutVersionOptions struct {
	Status  string
}
```

| Parameter | Description | Type |
| ----| ---- | ---- |
| BucketPutVersionOptions | Versioning policies | Struct |
| Status | Indicates whether versioning is enabled. Enumerated values: `Suspended` (versioning is paused), `Enabled` (versioning is enabled) | String |

## Querying Versioning

#### Feature description

This API (`GET Bucket versioning`) is used to query the versioning configuration of a bucket.

#### Method prototype
```go
func (s *BucketService) GetVersioning(ctx context.Context) (*BucketGetVersionResult, *Response, error)
```

#### Sample request
[//]: # (.cssg-snippet-get-bucket-versioning)
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
    u, _ := url.Parse("https://examplebucket-12500000000.cos.ap-guangzhou.myqcloud.com")
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
    _, _, err := client.Bucket.GetVersioning(context.Background())
    if err != nil{
        panic(err)
    }
}
```

#### Response description
```go
type BucketGetVersionResult struct {
	Status  string
}
```

| Parameter | Description | Type |
| ----| ---- | ---- |
| BucketGetVersionResult | Versioning policies | Struct |
| Status | Indicates whether versioning is enabled. Enumerated values: `Suspended` (versioning is paused), `Enabled` (versioning is enabled) | String |

