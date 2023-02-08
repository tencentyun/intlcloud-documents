## Overview
This document provides an overview of APIs and SDK code samples for creating a bucket.

>!
> - We recommend you use a temporary key as instructed in [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) to call the SDK for security purposes. When you apply for a temporary key, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.


| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |

## Creating a Bucket

#### Feature description

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

        // Sample 1: Creating a bucket
        opt := &cos.BucketGetOptions{
                XCosACL: "private",
        }
        _, err := client.Bucket.Put(context.Background(), opt)
        if err != nil{
                panic(err)
        }

        // Sample 2: Creating an MAZ bucket
        opt.CreateBucketConfiguration = &cos.CreateBucketConfiguration{
                BucketAZConfig: "MAZ",
        }
        _, err = client.Bucket.Put(context.Background(), opt)
        if err != nil{
                panic(err)
        }
}
```

#### Field description
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
| XCosGrantFullControl | Grants a specified account read and write access to a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, use `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`. To authorize a root account, use `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. <br>Example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | String | No |
| XCosGrantRead | Grants a specified account read access to a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, use `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`. To authorize a root account, use `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. <br>Example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | String | No |
| XCosGrantWrite | Grants a specified account write access to a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, use `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`. To authorize a root account, use `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. <br>Example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | String | No |
| BucketAZConfig | Bucket AZ configuration. Set it to `MAZ` to create an MAZ bucket. For the applicable regions of MAZ storage classes, see [MAZ Feature Overview](https://intl.cloud.tencent.com/document/product/436/35208). | Struct | No |
