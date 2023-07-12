## Overview

This document provides sample code for quickly checking whether a bucket exists.

The sample code actually calls the [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) COS API and is a simplified version of the API.

In addition to checking whether a bucket exists, `HEAD Bucket` also checks whether you have permission to access the bucket. Possible scenarios are as follows:

- If the bucket exists and you have permission to read it, HTTP status code 200 will be returned.
- If you do not have permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.


## Checking Whether a Bucket Exists

#### Feature description

You can check whether a bucket exists by using the shortcut API provided by the SDK.

>! The COS Go SDK version should not be earlier than v0.7.33.
>

#### Method prototype
```go
func (s *BucketService) IsExist(ctx context.Context) (isExist bool, err error)
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

        ok, err := client.Bucket.IsExist(context.Background())
        if err == nil && ok {
                fmt.Printf("bucket exists\n")
        } else if err != nil {
                fmt.Printf("head bucket failed: %v\n", err)
        } else {
                fmt.Printf("bucket does not exist\n")
        }
}
```
#### Response description
| Parameter | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| isExist | Whether the bucket exists                    | bool |
| err | Whether the request is successful | Struct |
