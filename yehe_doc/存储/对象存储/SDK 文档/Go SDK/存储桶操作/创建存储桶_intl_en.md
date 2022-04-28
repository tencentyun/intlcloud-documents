## Overview
This document provides an overview of APIs and SDK code samples related to how to create a bucket.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |

## Creating a Bucket

#### Description

This API is used to create a bucket under the specified account. You can create multiple buckets under the same user account. The maximum number is 200 (regardless of region). There is no limit to the number of objects in the bucket. Bucket creation is a low-frequency operation. We recommended you create a bucket in the console and perform object operations in the SDK.

#### Method prototype

```go
func (s *BucketService) Put(ctx context.Context, opt *BucketPutOptions) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket)
```go
package main

import (
        "context"
        "github.com/tencentyun/cos-go-sdk-v5"
        "net/http"
        "net/url"
        "os"
)

func main() {
        // Bucket name in the format of `BucketName-APPID` (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
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

        // Sample 1. Creating a bucket
        opt := &cos.BucketPutOptions{
                XCosACL: "private",
        }
        _, err := client.Bucket.Put(context.Background(), opt)
        if err != nil {
                panic(err)
        }

}
```

#### Parameter description
```go
type BucketPutOptions struct {
	XCosACL              string 
	XCosGrantRead        string  
	XCosGrantWrite       string  
	XCosGrantFullControl string 
    CreateBucketConfiguration *CreateBucketConfiguration
}
type CreateBucketConfiguration struct {
    BucketAZConfig string
}
```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL | Sets the bucket ACL, such as private, public-read, and public-read-write | String | No |
| XCosGrantFullControl | Grants the specified account the permission to read and write buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"`. | string | No |
| XCosGrantRead | Grants the specified account the permission to read buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"`. | string | No |
| XCosGrantWrite | Grants the specified account the permission to write buckets. Format: `id=" ",id=" "`. For authorization to a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; for authorization to a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"`. | string | No |
