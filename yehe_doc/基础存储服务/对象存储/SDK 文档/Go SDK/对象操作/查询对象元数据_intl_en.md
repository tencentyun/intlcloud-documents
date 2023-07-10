## Overview

This document provides an overview of APIs and SDK code samples for querying object metadata.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |

## Querying Object Metadata

#### Feature description

The API (`HEAD Object`) is used to query object metadata.

#### Method prototype

```go
func (s *ObjectService) Head(ctx context.Context, key string, opt *ObjectHeadOptions) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-head-object)
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
    _, err := client.Object.Head(context.Background(), key, nil)
    if err != nil{
        panic(err)
    }
}
```

#### Field description

```go
type ObjectHeadOptions struct {
    IfModifiedSince string 
}
```

| Parameter | Description | Type | Required |
| --------------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| IfModifiedSince | Returned only if the object is modified after the specified time | String | No |

#### Response description

```go
{
    'Content-Type': 'application/octet-stream',
    'Content-Length': '16807',
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'X-Cos-Request-Id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```
The result can be obtained from the `response`.
```go
resp, err := client.Object.Head(context.Background(), key, nil)
contentType := resp.Header.Get("Content-Type")
contentLength := resp.Header.Get("Content-Length")
etag := resp.Header.Get("ETag")
reqid := resp.Header.Get("X-Cos-Request-Id")

```

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | ------ |
| Metadata | Metadata of the queried file, including `ETag` and `X-Cos-Request-Id`. The metadata of the configured file is also returned. | String |
