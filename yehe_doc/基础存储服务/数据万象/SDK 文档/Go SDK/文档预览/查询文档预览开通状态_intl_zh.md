## 简介

本文档提供关于查询文档预览开通状态的 API 概览以及 SDK 示例代码。

| API  |	说明  |
|----|-----|
|  [查询文档预览开通状态](https://intl.cloud.tencent.com/document/product/1045/47928)  |用于查询存储桶是否已开通文档预览功能  |


## 查询文档预览开通状态

#### 功能说明

DescribeDocProcessBuckets 接口用于查询存储桶是否已开通文档预览功能。

#### 方法原型

```go
func (s *CIService) DescribeDocProcessBuckets(ctx context.Context, opt *DescribeDocProcessBucketsOptions) (*DescribeDocProcessBucketsResult, *Response, error)
```

#### 请求示例

```go
BucketsOpt := &cos.DescribeDocProcessBucketsOptions{
	Regions: "ap-shanghai",
}
res, _, err := c.CI.DescribeDocProcessBuckets(context.Background(), BucketsOpt)
```

#### 参数说明

```go
type DescribeDocProcessBucketsOptions struct {
    Regions     string
    BucketNames string 
    BucketName  string
    PageNumber  int
    PageSize    int
}
```

| 参数名称    | 描述                                                         | 类型   |
| ----------- | ------------------------------------------------------------ | ------ |
| Regions     | 地域信息，例如 ap-shanghai、ap-beijing，若查询多个地域以“,”分隔字符串，支持中国大陆地域，详情请参见 [地域与域名](https://intl.cloud.tencent.com/document/product/1045/33423) | string |
| BucketNames | 存储桶名称，以“,”分隔，支持多个存储桶，精确搜索              | string |
| BucketName  | 存储桶名称前缀，前缀搜索                                     | string |
| PageNumber  | 第几页                                                       | int |
| pageSize    | 每页个数                                                     | int |

#### 返回结果说明

```go
type DescribeDocProcessBucketsResult struct {
    RequestId     string
    TotalCount    int
    PageNumber    int
    PageSize      int
    DocBucketList []DocProcessBucket
}
type DocProcessBucket struct {
    BucketId      string
    Name          string
    Region        string
    CreateTime    string
    AliasBucketId string
}
```

| 参数名称      | 描述                            | 类型      |
| ------------- | ------------------------------- | --------- |
| RequestId     | 请求的唯一 ID                   | string    |
| TotalCount    | 文档预览 Bucket 总数            | int       |
| PageNumber    | 当前页数，同请求中的 pageNumber | int       |
| PageSize      | 每页个数，同请求中的 pageSize   | int       |
| DocBucketList | 文档预览 Bucket 列表            | Container |
| BucketId      | 存储桶 ID               | string |
| Name          | 存储桶名称，同 BucketId | string |
| Region        | 所在的地域              | string |
| CreateTime    | 创建时间                | string |
| AliasBucketId | 存储桶别名              | string |
