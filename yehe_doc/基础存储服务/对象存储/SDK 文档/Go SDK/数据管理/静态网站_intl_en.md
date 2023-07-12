

## Feature Overview

This document provides an overview of APIs and SDK code samples for static website.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Configuring a static website configuration | Configures a static website for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying a static website configuration | Queries the static website configuration of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting a static website configuration | Deletes the static website configuration of a bucket |

## Setting Static Website Configuration

#### Feature description

This API is used to configure a static website for a bucket.

#### Method prototype

```go
func (s *BucketService) PutWebsite(ctx context.Context, opt *BucketPutWebsiteOptions) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-website)
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
    opt := &cos.BucketPutWebsiteOptions{
        Index: "index.html",
        Error: &cos.ErrorDocument{"index_backup.html"},
        RoutingRules: &cos.WebsiteRoutingRules{
            []cos.WebsiteRoutingRule{
                {
                    ConditionErrorCode: "404",
                    RedirectProtocol:   "https",
                    RedirectReplaceKey: "404.html",
                },
                {
                    ConditionPrefix:          "docs/",
                    RedirectProtocol:         "https",
                    RedirectReplaceKeyPrefix: "documents/",
                },
            },
        },
    }
    _, err := client.Bucket.PutWebsite(context.Background(), opt)
    if err != nil{
        // ERROR
    }
}
```

#### Field description

```go
type WebsiteRoutingRule struct {
    ConditionErrorCode string 
    ConditionPrefix    string 

    RedirectProtocol         string 
    RedirectReplaceKey       string 
    RedirectReplaceKeyPrefix string 
}

type WebsiteRoutingRules struct {
    Rules []WebsiteRoutingRule
}

type ErrorDocument struct {
    Key string 
}

type RedirectRequestsProtocol struct {
    Protocol string 
}

type BucketPutWebsiteOptions struct {
    XMLName          xml.Name                  
    Index            string                    
    RedirectProtocol *RedirectRequestsProtocol
    Error            *ErrorDocument            
    RoutingRules     *WebsiteRoutingRules
}
```

| Parameter | Description | Type |
| ------------------------ | ------------------------------------------------------------ | ------ |
| BucketPutWebsiteOptions  | Static website configuration parameters                                             | Struct |
| Index                    | Index document                                                 | String |
| RedirectProtocol         | Site-wide redirect protocol                                             | Struct |
| Protocol                    | Site-wide redirect protocol. Only HTTPS is supported.                       | String   |
| Error                    | Error document                                                     | Struct |
| Key                         | Common error response                                             | String   |
| RoutingRules                | Multiple redirect rules. Up to 100 redirect rules can be set.                    | Struct    |
| ConditionErrorCode       | Redirect error code. Only 4xx status codes are supported. This has a higher priority than `Error.Key`.   | String |
| ConditionPrefix          | Redirect path prefix to replace with the specified "folder/" for the redirect.                     | String |
| RedirectProtocol         | Redirect protocol. Only HTTPS is supported.                       | String |
| RedirectReplaceKey       | Content that is used to replace the entire key.                                    | String |
| RedirectReplaceKeyPrefix | Content that is used to replace the key prefix. The replacement is allowed only when `Condition` is `KeyPrefixEquals`. | String |

## Querying Static Website Configuration

#### Feature description

This API (`GET Bucket website`) is used to query the static website configuration associated with a bucket.

#### Method prototype

```go
func (s *BucketService) GetWebsite(ctx context.Context) (*BucketGetWebsiteResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-website)
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
    res, _, err := client.Bucket.GetWebsite(context.Background())
    if err != nil{
        // ERROR
    }
    fmt.Println(res)
}
```

#### Response description

```go
type BucketGetWebsiteResult BucketPutWebsiteOptions
```

| Parameter | Description | Type |
| ------------------------ | ------------------------------------------------------------ | ------ |
| BucketGetWebsiteResult   | Static website configuration parameters                                             | Struct |
| Index                    | Index document                                                 | String |
| RedirectProtocol         | Site-wide redirect protocol                                             | Struct |
| Protocol                    | Site-wide redirect protocol. Only HTTPS is supported.                       | String   |
| Error                    | Common error response                                                 | Struct |
| Key                         | Common error response                                             | String   |
| RoutingRules                | Multiple redirect rules. Up to 100 redirect rules can be set.                    | Struct    |
| ConditionErrorCode       | Redirect error code. Only 4xx status codes are supported. This has a higher priority than `Error.Key`.   | String |
| ConditionPrefix          | Redirect path prefix to replace with the specified "folder/" for the redirect.                     | String |
| RedirectProtocol         | Redirect protocol. Only HTTPS is supported.                       | String |
| RedirectReplaceKey       | Content that is used to replace the entire key.                                    | String |
| RedirectReplaceKeyPrefix | Content that is used to replace the key prefix. The replacement is allowed only when `Condition` is `KeyPrefixEquals`. | String |

## Deleting Static Website Configuration

#### Feature description

This API (`DELETE Bucket website`) is used to delete the static website configuration of a bucket.

#### Method prototype

```go
func (s *BucketService) DeleteWebsite(ctx context.Context) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-website)
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
    _, err := client.Bucket.DeleteWebsite(context.Background())
    if err != nil{
        // ERROR
    }
}
```
