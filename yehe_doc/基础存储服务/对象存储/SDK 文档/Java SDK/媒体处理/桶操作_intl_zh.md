
## 简介

本文档提供关于数据万象媒体处理桶的相关 API 概览以及 SDK 示例代码。

| API                                                          | 操作名             | 操作描述                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [DescribeMediaBuckets](https://intl.cloud.tencent.com/document/product/1045/43671) | 查询媒体 Bucket | 查询当前账号下已经开通媒体处理功能的桶列表 |

## 基本操作

### 查询开通媒体处理功能的桶列表

#### 功能说明

查询当前账号下已经开通媒体处理功能的桶列表。

#### 方法原型

```java
public MediaBucketResponse describeMediaBuckets(MediaBucketRequest mediaBucketRequest);
```

#### 参数说明


| 参数名称   | 描述                                                         | 类型   |必选|
| ---------- | ------------------------------------------------------------ | ------ |---|
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| bucketNames |  bucket 名字，以`,`分隔，支持多 bucket，精确搜索 | String |否|
| regions |  地区信息，以`,`分隔字符串，支持 All，ap-shanghai，ap-beijing | String |否|
| pageNumber |  第几页 | String |否|
| pageSize | 每页个数 | String |否|

#### 返回结果说明

- 成功：返回 bucket 对象信息。
- 失败：发生错误（如 Bucket 不存在），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
 //1.创建模板请求对象
MediaBucketRequest request = new MediaBucketRequest();
//2.添加请求参数 参数详情请见api接口文档
request.setBucketName("examplebucket-1250000000");
//3.调用接口,获取桶响应对象
MediaBucketResponse response = client.describeMediaBuckets(request);
```
