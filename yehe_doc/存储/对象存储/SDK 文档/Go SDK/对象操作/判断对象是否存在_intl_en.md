## Overview

This document provides sample code for quickly checking whether an object exists in a bucket. 

The sample code actually calls the [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) COS API and is a simplified version of the API.

In addition to checking whether an object exists, `HEAD Object` returns object metadata. To view the SDK API that contains the full functionality of `HEAD Object`, please see [Querying Object Metadata](https://intl.cloud.tencent.com/document/product/436/44069).


## Checking Whether an Object Exists

#### Description

You can check whether an object exists by using the shortcut API provided by the SDK.

>! The COS Go SDK version should not be earlier than v0.7.33.
>

#### Method prototype
```go
func (s *ObjectService) IsExist(ctx context.Context, key string, id ...string) (isExist bool, err error)
```
#### Sample code

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

func main() {
    // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, see https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's SecretId, which can be viewed at https://console.cloud.tencent.com/cam/capi
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's SecretKey, which can be viewed at https://console.cloud.tencent.com/cam/capi
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    key := "exampleobject"
    ok, err := client.Object.IsExist(context.Background(), key)
    if err == nil && ok {
        fmt.Printf("object exists\n")
    } else if err != nil {
        fmt.Printf("head object failed: %v\n", err)
    } else {
        fmt.Printf("object does not exist\n")
    }
}
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`. | String | Yes |
| id  | `VersionId` of the object | String | No |

#### Response description

| Parameter | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| isExist | Whether the object exists                    | Bool |
| err | Whether the request is successful | Struct |
