

## 简介

本文档提供关于存储桶标签的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                         |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | 设置存储桶标签 | 为已存在的存储桶设置标签         |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | 查询存储桶标签 | 查询指定存储桶下已有的存储桶标签 |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | 删除存储桶标签 | 删除指定的存储桶标签             |

## 设置存储桶标签

#### 功能说明

PUT Bucket tagging 用于为已存在的存储桶设置标签。

#### 方法原型

```go
func (s *BucketService) PutTagging(ctx context.Context, opt *BucketPutTaggingOptions) (*Response, error)
```

#### 请求示例

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

func main() {
    // 存储桶名称，由 bucketname-appid 组成，appid 必须填入，可以在 COS 控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
    // 替换为用户的 region，存储桶 region 可以在 COS 控制台“存储桶概览”查看 https://console.cloud.tencent.com/ ，关于地域的详情见 https://cloud.tencent.com/document/product/436/6224 。
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // 通过环境变量获取密钥
            // 环境变量 SECRETID 表示用户的 SecretId，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretID: os.Getenv("SECRETID"),  // 用户的 SecretId，建议使用子账号密钥，授权遵循最小权限指引，降低使用风险。子账号密钥获取可参见 https://cloud.tencent.com/document/product/598/37140
            // 环境变量 SECRETKEY 表示用户的 SecretKey，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretKey: os.Getenv("SECRETKEY"),  // 用户的 SecretKey，建议使用子账号密钥，授权遵循最小权限指引，降低使用风险。子账号密钥获取可参见 https://cloud.tencent.com/document/product/598/37140
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
    if err != nil {
        // ERROR
    }
}
```

#### 参数说明

```go
type BucketTaggingTag struct {
    Key   string
    Value string
}
type BucketPutTaggingOptions struct {
    XMLName xml.Name           
    TagSet  []BucketTaggingTag 
}
```

| 参数名称                | 描述                                                         | 类型   |
| ----------------------- | ------------------------------------------------------------ | ------ |
| BucketPutTaggingOptions | 存储桶标签配置参数                                           | Struct |
| TagSet                  | 存储桶标签配置信息                                           | Struct |
| key                     | 标签的 Key，长度不超过128字节，支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | String |
| value                   | 标签的 Value，长度不超过256字节，支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | String |

## 查询存储桶标签

#### 功能说明

GET Bucket tagging 用于查询指定存储桶下已有的存储桶标签。

#### 方法原型

```go
func (s *BucketService) GetTagging(ctx context.Context) (*BucketGetTaggingResult, *Response, error)
```

#### 请求示例

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

func main() {
    // 存储桶名称，由 bucketname-appid 组成，appid 必须填入，可以在 COS 控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
    // 替换为用户的 region，存储桶region可以在COS控制台“存储桶概览”查看 https://console.cloud.tencent.com/ ，关于地域的详情见 https://cloud.tencent.com/document/product/436/6224 。
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // 通过环境变量获取密钥
            // 环境变量 SECRETID 表示用户的 SecretId，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretID: os.Getenv("SECRETID"),  // 用户的 SecretId，建议使用子账号密钥，授权遵循最小权限指引，降低使用风险。子账号密钥获取可参见 https://cloud.tencent.com/document/product/598/37140
            // 环境变量 SECRETKEY 表示用户的 SecretKey，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretKey: os.Getenv("SECRETKEY"),  // 用户的 SecretKey，建议使用子账号密钥，授权遵循最小权限指引，降低使用风险。子账号密钥获取可参见 https://cloud.tencent.com/document/product/598/37140
        },
    })
    v, _, err := client.Bucket.GetTagging(context.Background())
    if err != nil {
        fmt.Println(err)
    }
    fmt.Println(v)
}
```

#### 返回结果说明

```go
type BucketTaggingTag struct {
    Key   string
    Value string
}
type BucketGetTaggingResult struct {
    XMLName xml.Name           
    TagSet  []BucketTaggingTag 
}

```

| 参数名称               | 描述                                                         | 类型   |
| ---------------------- | ------------------------------------------------------------ | ------ |
| BucketGetTaggingResult | 存储桶标签配置参数                                           | Struct |
| TagSet                 | 存储桶标签配置信息                                           | Struct |
| key                    | 标签的 Key，长度不超过128字节，支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | String |
| value                  | 标签的 Value，长度不超过256字节，支持英文字母、数字、空格、加号、减号、下划线、等号、点号、冒号、斜线 | String |

## 删除存储桶标签

#### 功能说明

DELETE Bucket tagging 用于删除指定存储桶下已有的存储桶标签。

#### 方法原型

[//]: # (.cssg-snippet-delete-bucket-tagging)
```go
func (s *BucketService) DeleteTagging(ctx context.Context) (*Response, error)
```

#### 请求示例

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

func main() {
    // 存储桶名称，由 bucketname-appid 组成，appid 必须填入，可以在 COS 控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
    // 替换为用户的 region，存储桶region可以在COS控制台“存储桶概览”查看 https://console.cloud.tencent.com/ ，关于地域的详情见 https://cloud.tencent.com/document/product/436/6224 。
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // 通过环境变量获取密钥
            // 环境变量 SECRETID 表示用户的 SecretId，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretID: os.Getenv("SECRETID"),  // 用户的 SecretId，建议使用子账号密钥，授权遵循最小权限指引，降低使用风险。子账号密钥获取可参见 https://cloud.tencent.com/document/product/598/37140
            // 环境变量 SECRETKEY 表示用户的 SecretKey，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretKey: os.Getenv("SECRETKEY"),  // 用户的 SecretKey，建议使用子账号密钥，授权遵循最小权限指引，降低使用风险。子账号密钥获取可参见 https://cloud.tencent.com/document/product/598/37140
        },
    })
    resp, err := client.Bucket.DeleteTagging(context.Background())
    if err != nil {
        fmt.Println(err)
    }
    fmt.Println(resp.Header)
}
```
