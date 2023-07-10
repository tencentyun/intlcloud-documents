

## Feature Overview

This document provides an overview of APIs and Go SDK code samples related to logging.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting logging | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying logging configuration | Queries the logging configuration of a source bucket |

## Setting Logging Configuration

#### Feature description

This API is used to enable logging for a source bucket and store the access logs in a specified destination bucket.

#### Method prototype

```go
func (s *BucketService) PutLogging(ctx context.Context, opt *BucketPutLoggingOptions) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-logging)
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
    opt := &cos.BucketPutLoggingOptions{
        LoggingEnabled: &cos.BucketLoggingEnabled{
            TargetBucket: "TargetBucket-1250000000",
        },
    }
    _, err := client.Bucket.PutLogging(context.Background(), opt)
    if err != nil{
        // ERROR
    }
}
```

#### Field description

```go
type BucketLoggingEnabled struct {
    TargetBucket string 
    TargetPrefix string 
}

// BucketPutLoggingOptions is the options of PutBucketLogging
type BucketPutLoggingOptions struct {
    XMLName        xml.Name             
    LoggingEnabled *BucketLoggingEnabled 
}
```

| Parameter | Description | Type |
| ----------------------- | ------------------------------------------------------------ | ------ |
| BucketPutLoggingOptions | Log management configuration parameters                                             | Struct |
| LoggingEnabled          | Log management configuration                                                 | Struct |
| TargetBucket             | Destination bucket that stores logs. It can be the source bucket itself (although this is not recommended), or a bucket in the same account or region as the source bucket.                                           | String      |
| TargetPrefix             | The specified path prefix used to store logs in the destination bucket                                           | String      |

## Querying Logging Configuration

#### Feature description

This API is used to query the logging configuration of a specified bucket.

#### Method prototype

```go
func (s *BucketService) GetLogging(ctx context.Context) (*BucketGetLoggingResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-logging)
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
    v, _, err := client.Bucket.GetLogging(context.Background())
    if err != nil{
        // ERROR
    }
    fmt.Println(v)
}
```

#### Response description

```go
type BucketGetLoggingResult BucketPutLoggingOptions
```

| Parameter | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| BucketGetLoggingResult | Log management configuration parameters                                             | Struct |
| LoggingEnabled          | Log management configuration                                                 | Struct |
| TargetBucket             | Destination bucket that stores logs. It can be the source bucket itself (although this is not recommended), or a bucket in the same account or region as the source bucket.                                           | String      |
| TargetPrefix             | The specified path prefix used to store logs in the destination bucket                                           | String      |
