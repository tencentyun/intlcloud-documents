## 简介

本文档提供关于跨域访问的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                       |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | 设置跨域配置 | 设置存储桶的跨域名访问权限     |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | 查询跨域配置 | 查询存储桶的跨域名访问配置信息 |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | 删除跨域配置 | 删除存储桶的跨域名访问配置信息 |

## 设置跨域配置

#### 功能说明

设置指定存储桶的跨域名访问配置信息（PUT Bucket cors）。

#### 方法原型
```go
func (s *BucketService) PutCORS(ctx context.Context, opt *BucketPutCORSOptions) (*Response, error)
```

#### 请求示例
[//]: # ".cssg-snippet-put-bucket-cors"
```go
opt := &cos.BucketPutCORSOptions{
    Rules: []cos.BucketCORSRule{
        {
            AllowedOrigins: []string{"http://www.qq.com"},
            AllowedMethods: []string{"PUT", "GET"},
            AllowedHeaders: []string{"x-cos-meta-test", "x-cos-xx"},
            MaxAgeSeconds:  500,
            ExposeHeaders:  []string{"x-cos-meta-test1"},
        },
        {
            ID:             "1234",
            AllowedOrigins: []string{"http://www.baidu.com", "twitter.com"},
            AllowedMethods: []string{"PUT", "GET"},
            MaxAgeSeconds:  500,
        },
    },
}
_, err := client.Bucket.PutCORS(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### 参数说明

```go
type BucketCORSRule struct {
	ID             string   
	AllowedMethods []string 
	AllowedOrigins []string 
	AllowedHeaders []string 
	MaxAgeSeconds  int      
	ExposeHeaders  []string 
}
```

| 参数名称       | 参数描述                                                     | 类型     | 是否必填 |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | 设置对应的跨域规则，包括 ID，MaxAgeSeconds，AllowedOrigin，AllowedMethod，AllowedHeader，ExposeHeader | struct   | 是   |
| ID             | 设置规则的 ID                                                | string   | 否   |
| AllowedMethods | 设置允许的方法，如 GET，PUT，HEAD，POST，DELETE              | []string | 是   |
| AllowedOrigins | 设置允许的访问来源，如 `"http://cloud.tencent.com"`，支持通配符 * | []string | 是   |
| AllowedHeaders | 设置请求可以使用哪些自定义的 HTTP 请求头部，支持通配符 *     | []string | 否   |
| MaxAgeSeconds  | 设置 OPTIONS 请求得到结果的有效期                            | int      | 否   |
| ExposeHeaders  | 设置浏览器可以接收到的来自服务器端的自定义头部信息           | []string | 否   |


## 查询跨域配置

#### 功能说明

查询指定存储桶的跨域名访问配置信息（GET Bucket cors）。

#### 方法原型
```go
func (s *BucketService) GetCORS(ctx context.Context) (*BucketGetCORSResult, *Response, error)
```

#### 请求示例
[//]: # ".cssg-snippet-get-bucket-cors"
```go
_, _, err := client.Bucket.GetCORS(context.Background())
if err != nil {
    panic(err)
}
```

#### 返回结果说明
通过 GetBucketCORSResult 返回请求结果。

```go
type BucketCORSRule struct {
	ID             string   
	AllowedMethods []string 
	AllowedOrigins []string 
	AllowedHeaders []string 
	MaxAgeSeconds  int      
	ExposeHeaders  []string 
}
```

| 参数名称       | 参数描述                                                     | 类型     | 是否必填 |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | 设置对应的跨域规则，包括 ID，MaxAgeSeconds，AllowedOrigin，AllowedMethod，AllowedHeader，ExposeHeader | struct   | 是   |
| ID             | 设置规则的 ID                                                | string   | 否   |
| AllowedMethods | 设置允许的方法，如 GET，PUT，HEAD，POST，DELETE              | []string | 是   |
| AllowedOrigins | 设置允许的访问来源，如 `"http://cloud.tencent.com"`，支持通配符 * | []string | 是   |
| AllowedHeaders | 设置请求可以使用哪些自定义的 HTTP 请求头部，支持通配符 *     | []string | 否   |
| MaxAgeSeconds  | 设置 OPTIONS 请求得到结果的有效期                            | int      | 否   |
| ExposeHeaders  | 设置浏览器可以接收到的来自服务器端的自定义头部信息           | []string | 否   |                 

## 删除跨域配置

#### 功能说明

删除指定存储桶的跨域名访问配置（DELETE Bucket cors）。

#### 方法原型

```go
func (s *BucketService) DeleteCORS(ctx context.Context) (*Response, error)
```

#### 请求示例
[//]: # ".cssg-snippet-delete-bucket-cors"
```go
_, err := client.Bucket.DeleteCORS(context.Background())
if err != nil {
    panic(err)
}
```
