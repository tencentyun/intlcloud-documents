## Overview
This document provides an overview of APIs and SDK code samples related to archived object restoration.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring archived object | Restores ARCHIVE object. |

## Restoring Archived Object 

#### Feature description

This API is used to restore an ARCHIVE object.

#### Method prototype

```go
func (s *ObjectService) PostRestore(ctx context.Context, key string, opt *ObjectRestoreOptions) (*Response, error) 
```

#### Sample request

[//]: # ".cssg-snippet-restore-object"
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
    // Bucket name in the format of `bucketname-appid` (`appid` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your `region`, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information on regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables.
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    key := "example_restore"
    f, err := os.Open("/test")
    if err != nil {
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
    // Upload an object directly to ARCHIVE storage class.
    _, err = client.Object.Put(context.Background(), key, f, opt)
    if err != nil {
        panic(err)
    }

    opts := &cos.ObjectRestoreOptions{
        Days: 2,
        Tier: &cos.CASJobParameters{
            // Standard, Exepdited and Bulk
            Tier: "Expedited",
        },
    }
    // Restore an archived object.
    _, err = client.Object.PostRestore(context.Background(), key, opts)
    if err != nil {
        panic(err)
    }
}
```

#### Parameter description

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
| key | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string | Yes |
| ObjectRestoreOptions | Describes rules for retrieved temporary files. | struct | Yes |
| Days | Specifies the number of days before a temporary object expires. | int | Yes |
| CASJobParameters | Specifies the restoration configuration. | struct | No |
| Tier | Object restoration mode. For ARCHIVE, valid values are `Expedited`, `Standard`, and `Bulk`. For DEEP ARCHIVE, valid values are `Standard` and `Bulk`. | string | No |

