

## Overview

This document provides an overview of APIs and SDK code samples for bucket tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes the tags of a bucket |

## Setting Bucket Tags

#### Feature description

This API is used to set tags for an existing bucket.

#### Method prototype

```go
func (s *BucketService) PutTagging(ctx context.Context, opt *BucketPutTaggingOptions) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-tagging)
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
    opt := &cos.BucketPutTaggingOptions{
        TagSet: []cos.BucketTaggingTag{
            {
                Key:   "testk1",
                Value: "testv1",
            },
            {
                Key:   "testk2",
                Value: "testv2",
            },
        },
    }
    _, err := client.Bucket.PutTagging(context.Background(), opt)
    if err != nil{
        // ERROR
    }
}
```

#### Field description

```go
type BucketTaggingTag struct {
    Key   string
    Value string
}
type BucketPutTaggingOptions struct {
    XMLName                xml.Name           
    TagSet  []BucketTaggingTag 
}
```

| Parameter | Description | Type |
| ----------------------- | ------------------------------------------------------------ | ------ |
| BucketPutTaggingOptions | Bucket tag configuration parameters                                           | Struct |
| TagSet                  | Bucket tag configuration                                           | Struct |
| key | Tag key. A tag key must not exceed 128 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |
| value | Tag value. A tag value must not exceed 256 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |

## Querying Bucket Tags

#### Feature description

This API is used to query the existing tags of a specified bucket.

#### Method prototype

```go
func (s *BucketService) GetTagging(ctx context.Context) (*BucketGetTaggingResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-tagging)
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
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, see https://intl.cloud.tencent.com/document/product/436/6224.
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
    v, _, err := client.Bucket.GetTagging(context.Background())
    if err != nil{
        fmt.Println(err)
    }
    fmt.Println(v)
}
```

#### Response description

```go
type BucketTaggingTag struct {
    Key   string
    Value string
}
type BucketGetTaggingResult struct {
    XMLName                xml.Name           
    TagSet  []BucketTaggingTag 
}

```

| Parameter | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| BucketGetTaggingResult | Bucket tag configuration parameters                                           | Struct |
| TagSet                  | Bucket tag configuration                                           | Struct |
| key | Tag key. A tag key must not exceed 128 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |
| value | Tag value. A tag value must not exceed 256 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |

## Deleting Bucket Tags

#### Feature description

This API (`DELETE Bucket tagging`) is used to delete the existing tags from a bucket.

#### Method prototype

[//]: # (.cssg-snippet-delete-bucket-tagging)
```go
func (s *BucketService) DeleteTagging(ctx context.Context) (*Response, error)
```

#### Sample request

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
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, see https://intl.cloud.tencent.com/document/product/436/6224.
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
    resp, err := client.Bucket.DeleteTagging(context.Background())
    if err != nil{
        fmt.Println(err)
    }
    fmt.Println(resp.Header)
}
```
