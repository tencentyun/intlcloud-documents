## 简介

本文档提供关于原图保护的 API 概览以及 SDK 示例代码。

| API                                                          | 操作描述                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [开通原图保护](https://intl.cloud.tencent.com/document/product/1045/33711) | 对 Bucket 开通原图保护功能。 |
| [查询原图保护状态](https://intl.cloud.tencent.com/document/product/1045/33710) | 用于查询原图保护功能是否开启。   |
| [关闭原图保护](https://intl.cloud.tencent.com/document/product/1045/33712) | 用于关闭原图保护功能。 |


## 开通原图保护

#### 功能说明

对 Bucket 开通原图保护功能。

#### 方法原型

```go
func (s *CIService) OpenOriginProtect(ctx context.Context) (*Response, error)
```

#### 请求示例

```go
_, err := c.CI.OpenOriginProtect(context.Background())
```

## 查询原图保护状态

#### 功能说明

用于查询原图保护功能是否开启。

#### 方法原型

```go
func (s *CIService) GetOriginProtect(ctx context.Context) (*OriginProtectResult, *Response, error)
```

#### 请求示例

```go
res, _, err := c.CI.GetOriginProtect(context.Background())
```

#### 参数说明

| 参数名称  | 参数描述                                                     |
| --------- | ------------------------------------------------------------ |
| OriginProtectResult  | 查询原图保护的结果 |

## 关闭原图保护

#### 功能说明

用于关闭原图保护功能。

#### 方法原型

```go
func (s *CIService) CloseOriginProtect(ctx context.Context) (*Response, error)
```

#### 请求示例

```go
_, err := c.CI.CloseOriginProtect(context.Background())
```
