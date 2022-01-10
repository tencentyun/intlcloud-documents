## Overview

This document provides an overview of the API and sample code for getting an object access URL.

## Getting an Object Access URL

#### Description

The API is used to get object access URLs for anonymous download or distribution.

>! The COS Go SDK version should not be earlier than v0.7.26.

#### Method prototype

```
func (s *ObjectService) GetObjectURL(key string) *url.URL
```

#### Sample request


[//]: # (.cssg-snippet-get-object-url-alias)
```go
package main

import (
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
            SecretID:  os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's SecretId, which can be viewed at https://console.cloud.tencent.com/cam/capi
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    key := "exampleobject"
    ourl := client.Object.GetObjectURL(key)
    fmt.Println(ourl)
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |

#### Response description

An object access URL is returned upon success.
