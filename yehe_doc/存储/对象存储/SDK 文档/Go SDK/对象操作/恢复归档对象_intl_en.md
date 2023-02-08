## Overview
This document provides an overview of APIs and SDK code samples for restoring an archived object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |

## Restoring an Archived Object 

#### Feature description

This API (`POST Object restore`) is used to restore an archived object for access.

#### Method prototype

```go
func (s *ObjectService) PostRestore(ctx context.Context, key string, opt *ObjectRestoreOptions) (*Response, error) 
```

#### Sample request

[//]: # (.cssg-snippet-restore-object)
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
    key := "example_restore"
    f, err := os.Open("/test")
    if err != nil{
        panic(err)
    }
    opt := &cos.ObjectPutOptions{
        ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
            ContentType:      "text/html",
            XCosStorageClass: "ARCHIVE", //ARCHIVE storage class
        },
        ACLHeaderOptions: &cos.ACLHeaderOptions{
            // Considering the ACL limit, we recommend you not set an object ACL when uploading an object unless required. The object will then inherit the bucket ACL by default.
            XCosACL: "private",
        },
    }
    // Upload an object directly to ARCHIVE storage class
    _, err = client.Object.Put(context.Background(), key, f, opt)
    if err != nil{
        panic(err)
    }

    opts := &cos.ObjectRestoreOptions{
        Days: 2,
        Tier: &cos.CASJobParameters{
            // Standard, Expedited, and Bulk
            Tier: "Expedited",
        },
    }
    // Restore an archived object.
    _, err = client.Object.PostRestore(context.Background(), key, opts)
    if err != nil{
        panic(err)
    }
}
```

#### Field description

```go
type ObjectRestoreOptions struct {        
    Days    int               
    Tier    *CASJobParameters 
}
type CASJobParameters struct {
    Tier    string 
}
```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| ObjectRestoreOptions | Describes rules for retrieved temporary files | Struct | Yes |
| Days | Specifies the number of days before a temporary object expires | Int | Yes |
| CASJobParameters | Specifies the restoration configuration | Struct | No |
| Tier | Object restoration mode. <li>For ARCHIVE, valid values are `Expedited`, `Standard`, and `Bulk`. <li>For DEEP ARCHIVE, valid values are `Standard` and `Bulk`. | String | No |

