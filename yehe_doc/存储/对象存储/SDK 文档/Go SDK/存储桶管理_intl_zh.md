## 简介
本文档提供关于跨域访问、生命周期、版本控制、存储桶复制和存储桶策略相关的 API 概览以及 SDK 示例代码。

**跨域访问**

| API                                                          | 操作名       | 操作描述                       |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | 设置跨域配置 | 设置存储桶的跨域访问权限     |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | 查询跨域配置 | 查询存储桶的跨域访问配置信息 |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | 删除跨域配置 | 删除存储桶的跨域访问配置信息 |

**生命周期**

| API                                                          | 操作名       | 操作描述                         |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | 设置生命周期 | 设置存储桶的生命周期管理的配置 |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | 查询生命周期 | 查询存储桶生命周期管理的配置   |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | 删除生命周期 | 删除存储桶生命周期管理的配置   |

**版本控制**

| API | 操作名 | 操作描述 |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | 设置版本控制   | 设置存储桶的版本控制功能 |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | 查询版本控制 | 查询存储桶的版本控制信息 |

**存储桶复制**

| API | 操作名 | 操作描述 |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | 设置存储桶复制   | 设置存储桶的跨地域复制规则 |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | 查询存储桶复制 | 查询存储桶的跨地域复制规则 |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | 删除存储桶复制 | 删除存储桶的跨地域复制规则 |

**存储桶策略**

| API                                                          | 操作名       | 操作描述                 |
| ----------------------------------------------------------- | ----------- | ----------------------- |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | 设置存储桶策略 | 设置存储桶的权限策略规则 |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | 查询存储桶策略 | 查询存储桶的权限策略规则 |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | 删除存储桶策略 | 删除存储桶的权限策略规则 |

## 跨域访问
### 设置跨域配置

#### 功能说明

设置指定存储桶的跨域访问配置信息（PUT Bucket cors）。

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

| 参数名称       | 参数描述                                                     | 类型     | 必填 |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | 设置对应的跨域规则，包括 ID，MaxAgeSeconds，AllowedOrigin，AllowedMethod，AllowedHeader，ExposeHeader | struct   | 是   |
| ID             | 设置规则的 ID                                                | string   | 否   |
| AllowedMethods | 设置允许的方法，如 GET，PUT，HEAD，POST，DELETE              | []string | 是   |
| AllowedOrigins | 设置允许的访问来源，如 `"http://cloud.tencent.com"`，支持通配符 * | []string | 是   |
| AllowedHeaders | 设置请求可以使用哪些自定义的 HTTP 请求头部，支持通配符 *     | []string | 否   |
| MaxAgeSeconds  | 设置 OPTIONS 请求得到结果的有效期                            | int      | 否   |
| ExposeHeaders  | 设置浏览器可以接收到的来自服务器端的自定义头部信息           | []string | 否   |


### 查询跨域配置

#### 功能说明

查询存储桶的跨域访问配置信息（GET Bucket cors）。

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

| 参数名称       | 参数描述                                                     | 类型     | 必填 |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | 设置对应的跨域规则，包括 ID，MaxAgeSeconds，AllowedOrigin，AllowedMethod，AllowedHeader，ExposeHeader | struct   | 是   |
| ID             | 设置规则的 ID                                                | string   | 否   |
| AllowedMethods | 设置允许的方法，如 GET，PUT，HEAD，POST，DELETE              | []string | 是   |
| AllowedOrigins | 设置允许的访问来源，如 `"http://cloud.tencent.com"`，支持通配符 * | []string | 是   |
| AllowedHeaders | 设置请求可以使用哪些自定义的 HTTP 请求头部，支持通配符 *     | []string | 否   |
| MaxAgeSeconds  | 设置 OPTIONS 请求得到结果的有效期                            | int      | 否   |
| ExposeHeaders  | 设置浏览器可以接收到的来自服务器端的自定义头部信息           | []string | 否   |                 |

### 删除跨域配置

#### 功能说明

删除指定存储桶的跨域访问配置（DELETE Bucket cors）。

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

## 生命周期
### 设置生命周期

#### 功能说明

设置指定存储桶的生命周期配置信息（PUT Bucket lifecycle）。

#### 方法原型
```go
func (s *BucketService) PutLifecycle(ctx context.Context, opt *BucketPutLifecycleOptions) (*Response, error)
```

#### 请求示例
[//]: # ".cssg-snippet-put-bucket-lifecycle"
```go
lc := &cos.BucketPutLifecycleOptions{
    Rules: []cos.BucketLifecycleRule{
        {
            ID:     "1234",
            Filter: &cos.BucketLifecycleFilter{Prefix: "test"},
            Status: "Enabled",
            Transition: &cos.BucketLifecycleTransition{
                Days:         10,
                StorageClass: "Standard",
            },
        },
        {
            ID:     "123422",
            Filter: &cos.BucketLifecycleFilter{Prefix: "gg"},
            Status: "Disabled",
            Expiration: &cos.BucketLifecycleExpiration{
                Days: 10,
            },
        },
    },
}
_, err := client.Bucket.PutLifecycle(context.Background(), lc)
if err != nil {
    panic(err)
}
```

#### 参数说明
```go
type BucketLifecycleRule struct {
	ID                             string
	Status                         string
	Filter                         *BucketLifecycleFilter
	Transition                     *BucketLifecycleTransition
	Expiration                     *BucketLifecycleExpiration
	AbortIncompleteMultipartUpload  *BucketLifecycleAbortIncompleteMultipartUpload 
}
type BucketLifecycleFilter struct {
	Prefix       string 
}
type BucketLifecycleTransition struct {
	Date         string 
	Days         int    
	StorageClass string
}
type BucketLifecycleExpiration struct {
	Date string 
	Days int    
}
type BucketLifecycleAbortIncompleteMultipartUpload struct {
	DaysAfterInitiation string 
}
```

| 参数名称                       | 参数描述                                                     | 类型   | 必填 |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule            | 设置对应的规则，包括 ID，Filter，Status，Expiration，Transition，AbortIncompleteMultipartUpload | List   | 是   |
| ID                             | 设置规则的 ID                                                | string | 否   |
| Status                         | 设置 Rule 是否启用，可选值为 Enabled 或者 Disabled           | string | 是   |
| Filter                         | 用于描述规则影响的 Object 集合，如需设置 Bucket 中的所有 objects，请设置 Prefix 为空 | struct | 是   |
| Transition                     | 设置 Object 转换存储类型规则，可以指定天数 Days 或者指定日期 Date，Date 的格式必须是 GMT ISO 8601。StorageClass 可选 Standard_IA，Archive，可以同时设置多条此类规则 | struct | 否   |
| Expiration                     | 设置 Object 过期规则，可以指定天数 Days 或者指定日期 Date，Date 的格式必须是 GMT ISO 8601 | struct | 否   |
| AbortIncompleteMultipartUpload | 指明分块上传开始后多少天内必须完成上传                       | struct | 否   |

### 查询生命周期

#### 功能说明

查询存储桶生命周期管理的配置（GET Bucket lifecycle）。

#### 方法原型
```go
func (s *BucketService) GetLifecycle(ctx context.Context) (*BucketGetLifecycleResult, *Response, error)
```

#### 请求示例

[//]: # ".cssg-snippet-get-bucket-lifecycle"
```go
_, _, err := client.Bucket.GetLifecycle(context.Background())
if err != nil {
    panic(err)
}
```

#### 返回结果说明

通过 GetBucketLifecycleResult 返回请求结果。

```go
type BucketLifecycleRule struct {
	ID                             string
	Status                         string
	Filter                         *BucketLifecycleFilter
	Transition                     *BucketLifecycleTransition
	Expiration                     *BucketLifecycleExpiration
	AbortIncompleteMultipartUpload  *BucketLifecycleAbortIncompleteMultipartUpload 
}
type BucketLifecycleFilter struct {
	Prefix       string 
}
type BucketLifecycleTransition struct {
	Date         string 
	Days         int    
	StorageClass string
}
type BucketLifecycleExpiration struct {
	Date string 
	Days int    
}
type BucketLifecycleAbortIncompleteMultipartUpload struct {
	DaysAfterInitiation string 
}
```

| 参数名称                       | 参数描述                                                     | 类型   | 必填 |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule            | 设置对应的规则，包括 ID，Filter，Status，Expiration，Transition，AbortIncompleteMultipartUpload | List   | 是   |
| ID                             | 设置规则的 ID                                                | string | 否   |
| Status                         | 设置 Rule 是否启用，可选值为 Enabled 或者 Disabled           | string | 是   |
| Filter                         | 用于描述规则影响的 Object 集合，如需设置 Bucket 中的所有 objects，请设置 Prefix 为空 | struct | 是   |
| Transition                     | 设置 Object 转换存储类型规则，可以指定天数 Days 或者指定日期 Date，Date 的格式必须是 GMT ISO 8601。StorageClass 可选 Standard_IA，Archive，可以同时设置多条此类规则 | struct | 否   |
| Expiration                     | 设置 Object 过期规则，可以指定天数 Days 或者指定日期 Date，Date 的格式必须是 GMT ISO 8601 | struct | 否   |
| AbortIncompleteMultipartUpload | 指明分块上传开始后多少天内必须完成上传                       | struct | 否   |


### 删除生命周期

#### 功能说明

删除存储桶生命周期管理的配置（DELETE Bucket lifecycle）。

#### 方法原型

```go
func (s *BucketService) DeleteLifecycle(ctx context.Context) (*Response, error)
```

#### 请求示例

[//]: # ".cssg-snippet-delete-bucket-lifecycle"
```go
_, err := client.Bucket.DeleteLifecycle(context.Background())
if err != nil {
    panic(err)
}
```

## 版本控制
### 设置版本控制

#### 功能说明

设置指定存储桶的版本控制功能（PUT Bucket versioning）。

#### 方法原型
```go
func (s *BucketService) PutVersioning(ctx context.Context, opt *BucketPutVersionOptions) (*Response, error)
```

#### 请求示例
[//]: # ".cssg-snippet-put-bucket-versioning"
```go
opt := &cos.BucketPutVersionOptions{
    // Enabled 或者 Suspended, 版本控制配置一旦开启就不能删除，只能暂停
    Status: "Enabled",
}
_, err := client.Bucket.PutVersioning(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### 参数说明
```go
type BucketPutVersionOptions struct {
	Status  string
}
```
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| BucketPutVersionOptions | 版本控制策略  | struct |
| Status | 说明版本是否开启，枚举值：Suspended（暂停版本控制）、Enabled（开启版本控制）  | string |

### 查询版本控制

#### 功能说明

查询指定存储桶的版本控制信息（GET Bucket versioning）。

#### 方法原型
```go
func (s *BucketService) GetVersioning(ctx context.Context) (*BucketGetVersionResult, *Response, error)
```

#### 请求示例
[//]: # ".cssg-snippet-get-bucket-versioning"
```go
_, _, err := client.Bucket.GetVersioning(context.Background())
if err != nil {
    panic(err)
}
```

#### 返回结果说明
```go
type BucketGetVersionResult struct {
	Status  string
}
```
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| BucketGetVersionResult | 版本控制策略  | struct |
| Status | 说明版本是否开启，枚举值：Suspended（暂停版本控制）、Enabled（开启版本控制）  | string |

## 存储桶复制
### 设置存储桶复制

#### 功能说明

设置指定存储桶的跨地域复制规则（PUT Bucket replication）。

#### 方法原型
```go
func (s *BucketService) PutBucketReplication(ctx context.Context, opt *PutBucketReplicationOptions) (*Response, error)
```

#### 请求示例
[//]: # ".cssg-snippet-put-bucket-replication"
```go
opt := &cos.PutBucketReplicationOptions{
    // qcs::cam::uin/[UIN]:uin/[Subaccount]
    Role: "qcs::cam::uin/100000000001:uin/100000000001",
    Rule: []cos.BucketReplicationRule{
        {
            ID: "1",
            // Enabled or Disabled
            Status: "Enabled",
            Destination: &cos.ReplicationDestination{
                // qcs::cos:[Region]::[Bucketname-Appid]
                Bucket: "qcs::cos:ap-beijing::destinationbucket-1250000000",
            },
        },
    },
}
_, err := client.Bucket.PutBucketReplication(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### 参数说明
```go
type PutBucketReplicationOptions struct {
	Role    string
	Rule    []BucketReplicationRule
}
type BucketReplicationRule struct {
	ID          string
	Status      string
	Prefix      string
	Destination *ReplicationDestination
}
type ReplicationDestination struct {
	Bucket       string
	StorageClass string
}
```
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| PutBucketReplicationOptions  | 存储桶复制规则 | struct                         |
| Role | 发起者身份标示：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>`  | string |
| Rule | 具体配置信息，最多支持1000个，所有策略只能指向一个目标存储桶  | struct |
| ID | 	用来标注具体 Rule 的名称  | string |
| Status | 标识 Rule 是否生效，枚举值：Enabled, Disabled  | string |
| Prefix | 	前缀匹配策略，不可重叠，重叠返回错误。前缀匹配根目录为空  | string |
| Destination | 目标存储桶信息  | struct |
| Bucket | 资源标识符：`qcs::cos:[region]::[bucketname-AppId]`  | string |
| StorageClass |  存储级别，枚举值：STANDARD，TANDARD_IA。默认值：原存储桶级别  | string |

### 查询存储桶复制

#### 功能说明

查询指定存储桶的跨地域复制规则（GET Bucket replication）。

#### 方法原型
```go
func (s *BucketService) GetBucketReplication(ctx context.Context) (*GetBucketReplicationResult, *Response, error)
```

#### 请求示例
[//]: # ".cssg-snippet-get-bucket-replication"
```go
_, _, err := client.Bucket.GetBucketReplication(context.Background())
if err != nil {
    panic(err)
}
```

#### 返回结果说明
```go
type GetBucketReplicationResult struct {
	Role    string
	Rule    []BucketReplicationRule
}
type BucketReplicationRule struct {
	ID          string
	Status      string
	Prefix      string
	Destination *ReplicationDestination
}
type ReplicationDestination struct {
	Bucket       string
	StorageClass string
}
```
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| GetBucketReplicationResult  | 存储桶复制规则 | struct                         |
| Role | 发起者身份标示：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>`  | string |
| Rule | 具体配置信息，最多支持1000个，所有策略只能指向一个目标存储桶  | struct |
| ID | 	用来标注具体 Rule 的名称  | string |
| Status | 标识 Rule 是否生效，枚举值：Enabled，isabled  | string |
| Prefix | 	前缀匹配策略，不可重叠，重叠返回错误。前缀匹配根目录为空  | string |
| Destination | 目标存储桶信息  | struct |
| Bucket | 资源标识符：`qcs::cos:[region]::[bucketname-AppId]`  | string |
| StorageClass |  存储级别，枚举值：STANDARD，ANDARD_IA。默认值：原存储桶级别  | string |


### 删除存储桶复制

#### 功能说明

删除指定存储桶的跨地域复制规则（DELETE Bucket replication）。

#### 方法原型
```go
func (s *BucketService) DeleteBucketReplication(ctx context.Context) (*Response, error)
```

#### 请求示例
[//]: # ".cssg-snippet-delete-bucket-replication"
```go
_, err := client.Bucket.DeleteBucketReplication(context.Background())
if err != nil {
    panic(err)
}
```

## 存储桶策略

### 设置存储桶策略

#### 功能说明

PUT Bucket policy 请求可以向 Bucket 写入权限策略，当存储桶已存在权限策略时，该请求上传的策略将覆盖原有的权限策略。

#### 方法原型
```go
func (s *BucketService) PutPolicy(ctx context.Context, opt *BucketPutPolicyOptions) (*Response, error)
```

#### 请求示例
```go
opt := &cos.BucketPutPolicyOptions{
	Version: "2.0",
	Statement: []cos.BucketStatement{
	{
		Principal: map[string][]string{
			"qcs": []string{
				"qcs::cam::uin/100000000001:uin/100000000011", //替换成您想授予权限的账户uin
			},
		},
		Action: []string{
			"name/cos:GetObject",
		},
		Effect: "allow",
		Resource: []string{
			//这里改成允许的路径前缀，可以根据自己网站的用户登录态判断允许上传的具体路径，例子： a.jpg 或者 a/* 或者 * (使用通配符*存在重大安全风险, 请谨慎评估使用)
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
_, err := c.Bucket.PutPolicy(context.Background(), opt)
```

#### 参数说明

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
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| Statement | 描述一条或多条权限的详细信息 | Struct                   |
| Version | 策略语法版本 | Struct            |
| Principal | 描述策略授权的实体，详情请参见 [访问策略语言概述](https://intl.cloud.tencent.com/document/product/436/18023) | String |
| Action | 此处是指 COS API，根据需求指定一个或者一序列操作的组合或所有操作(`*`)，例如 action 为 name/cos:GetService，**请注意区分英文大小写** | Array       |
| Effect | 有 allow（允许）和 deny（显式拒绝）两种情况 | String |
| Resource | 授权操作的具体数据，可以是任意资源、指定路径前缀的资源、指定绝对路径的资源或它们的组合 | Array |
| Condition | 约束条件，可以不填，具体说明请参见 [condition](https://intl.cloud.tencent.com/document/product/598/10603) 说明 | Struct |

### 查询存储桶策略

#### 功能说明

 GET Bucket policy 请求可以向 Bucket 读取权限策略 。

#### 方法原型

```go
func (s *BucketService) GetPolicy(ctx context.Context) (*BucketGetPolicyResult, *Response, error)
```

#### 请求示例
```go
res, resp, err := c.Bucket.GetPolicy(context.Background())
```

#### 返回结果说明

```go
type BucketGetPolicyResult BucketPutPolicyOptions
// 详情见BucketPutPolicyOptions
```

### 删除存储桶策略

#### 功能说明

  DELETE Bucket policy 请求可以向 Bucket 删除权限策略 。

#### 方法原型

```go
func (s *BucketService) DeletePolicy(ctx context.Context) (*Response, error)
```

#### 请求示例

```go
resp, err := c.Bucket.DeletePolicy(context.Background())
```
