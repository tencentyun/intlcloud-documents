## Overview

This document provides an overview of APIs and SDK code samples related to bucket policies.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for a specified bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying a bucket policy | Queries the permission policy of a bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting a bucket policy | Deletes the permission policy of a bucket |

## Setting a bucket policy

#### Feature description

This API is used to write a permission policy for a bucket. The policy passed in this API will overwrite the existing one (if any) in the bucket.

#### Method prototype
```go
func (s *BucketService) PutPolicy(ctx context.Context, opt *BucketPutPolicyOptions) (*Response, error)
```

#### Sample request
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
    opt := &cos.BucketPutPolicyOptions{
        Version: "2.0",
        Statement: []cos.BucketStatement{
            {
                Principal: map[string][]string{
                    "qcs": []string{
                        "qcs::cam::uin/100000000001:uin/100000000011", // Replace with the uin of the account to be granted the permission.
                    },
                },
                Action: []string{
                    "name/cos:GetObject",
                },
                Effect: "allow",
                Resource: []string{
                    // Change it to the allowed path prefix (such as "a.jpg", "a/*", or "*"). You can determine the upload path based on your login status. (Keep in mind that using asterisks (*) could bring high risks.)
                    "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/exampleobject",
                },
                Condition: map[string]map[string]interface{}{
                    "ip_not_equal": map[string]interface{}{
                        "qcs:ip": []string{
                            "192.168.1.1",
                        },
                    },
                },
            },
        },
    }
    _, err := client.Bucket.PutPolicy(context.Background(), opt)
    if err != nil{
        // ERROR
    }
}
```

#### Field description

```go
type BucketStatement struct {
    Principal map[string][]string
    Action    []string
    Effect    string
    Resource  []string
    Condition map[string]map[string]interface{}
}

type BucketPutPolicyOptions struct {
    Statement []BucketStatement
    Version   string
    Principal map[string][]string
}
```

| Parameter | Description | Type |
| ----| ---- | ---- |
| Statement | Detailed information about one or more permissions | Struct |
| Version | Policy syntax version | Struct            |
| Principal | Entity to which the permission is granted. For more information, please see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023) | String |
| action | COS API. You can specify one, several, or all (`*`) COS APIs as needed, e.g., set `action` to `name/cos:GetService`. **Note that this parameter is case-sensitive**. |
| Effect | Allow or explicitly deny | String |
| resource | Specific data authorized to be operated on. It can be any resource, a resource whose path prefix is specified, a resource with a specified absolute path, or a combination thereof. | Array |
| condition | Condition (optional). For more information, please see [Condition](https://intl.cloud.tencent.com/document/product/598/10603) | Struct |

## Querying a bucket policy

#### Feature description

This API is used to read the permission policy of a bucket.

#### Method prototype

```go
func (s *BucketService) GetPolicy(ctx context.Context) (*BucketGetPolicyResult, *Response, error)
```

#### Sample request
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
    res, _, err := client.Bucket.GetPolicy(context.Background())
    if err != nil{
        // ERROR
    }
    fmt.Println(res)
}
```

#### Response description

```go
type BucketGetPolicyResult BucketPutPolicyOptions
// For details, see `BucketPutPolicyOptions`.
```

## Deleting a bucket policy

#### Feature description

This API (DELETE Bucket policy) is used to delete the permission policy of a bucket.

#### Method prototype

```go
func (s *BucketService) DeletePolicy(ctx context.Context) (*Response, error)
```

#### Sample request

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
    _, err := client.Bucket.DeletePolicy(context.Background())
    if err != nil{
        // ERROR
    }
}
```
