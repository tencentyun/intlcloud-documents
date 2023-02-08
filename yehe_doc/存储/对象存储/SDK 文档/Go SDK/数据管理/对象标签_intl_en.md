## Overview

This document provides an overview of APIs and SDK code samples for object tagging.

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Tagging an object | Tags an uploaded object. |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all tags of an object. |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes all tags of an object. |


## Tagging an Object

#### Feature description

This API is used to set tags for an existing object. It can help you group and manage existing object resources by adding key-value pairs as object tags. For more information, please see [Object Tagging Overview](https://intl.cloud.tencent.com/document/product/436/35665).

#### Method prototype

```go
func (s *ObjectService) PutTagging(ctx context.Context, name string, opt *ObjectPutTaggingOptions, id ...string) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-object-tagging)
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "strings"
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
    // Sample 1. Use PutTagging to tag in-cloud objects
    opt := &cos.ObjectPutTaggingOptions{
        TagSet: []cos.ObjectTaggingTag{
            {
                Key:   "test_k2",
                Value: "test_v2",
            },
            {
                Key:   "test_k3",
                Value: "test_v3",
            },
        },
    }
    name := "example"
    _, err := client.Object.PutTagging(context.Background(), name, opt)
    if err != nil{
        //ERROR
    }    
    // Sample 2. Tag an object when it is uploaded
    name = "test/example"
    f := strings.NewReader("test")
    popt := &cos.ObjectPutOptions{
        ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
            XOptionHeader: &http.Header{},
        },
    }
    popt.XOptionHeader.Add("x-cos-tagging", "Key1=Value1&Key2=Value2")
    _, err = client.Object.Put(context.Background(), name, f, popt)
} 
```

#### Field description

```go
type ObjectPutTaggingOptions struct {
    TagSet  []ObjectTaggingTag
}
type BucketTaggingTag struct {
    Key   string
    Value string
}
```

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| name  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| TagSet   | A set of up to 10 tags | Array  | Yes |
| Key | Tag key. A tag key must not exceed 128 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String | Yes |
| Value | Tag value. A tag value must not exceed 256 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String | Yes |

## Querying Object Tags

#### Feature description

This API is used to query the existing tags of an object.

#### Method prototype

```go
func (s *ObjectService) GetTagging(ctx context.Context, name string, id ...string) (*ObjectGetTaggingResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-object-tagging)
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
    name := "example"
    res, _, err := client.Object.GetTagging(context.Background(), name)
    if err != nil{
        //ERROR
    }
    fmt.Println(res)
}
```

#### Response description
```go
type ObjectGetTaggingResult struct {
    TagSet  []ObjectTaggingTag
}
type BucketTaggingTag struct {
    Key   string
    Value string
}
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| TagSet   | A set of up to 10 tags    | Array  |
| Key | Tag key. A tag key must not exceed 128 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |
| Value | Tag value. A tag value must not exceed 256 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |

## Deleting Object Tags

#### Feature description

This API is used to delete existing tags of an object.

#### Method prototype

```go
func (s *ObjectService) DeleteTagging(ctx context.Context, name string, id ...string) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-delete-object-tagging)
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
    name := "example"
    _, err := client.Object.DeleteTagging(context.Background(), name)
    if err != nil{
        //ERROR
    }
}
```
