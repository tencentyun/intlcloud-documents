
## 简介

本文档提供关于数据万象处理媒体信息的相关 API 概览以及 SDK 示例代码。

| API                                                          | 操作名             | 操作描述                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| GenerateMediainfo | 获取媒体文件的信息 | 查询 Bucket 中文件的媒体信息详情 |

## 基本操作

### 获取媒体文件的信息

#### 功能说明

查询 Bucket 中文件的媒体信息详情。

#### 方法原型

```java
public MediaInfoResponse generateMediainfo(MediaInfoRequest request);
```

#### 参数说明


| 参数名称   | 描述                                                         | 类型   |必选|
| ---------- | ------------------------------------------------------------ | ------ |---|
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| object |  input.objet 查询的对象在 Bucket 中的位置信息 | String |是|

#### 返回结果说明

- 成功：返回媒体对象信息。
- 失败：发生错误（如 Bucket 不存在），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
//1.创建媒体信息请求对象
MediaInfoRequest request = new MediaInfoRequest();
//2.添加请求参数 参数详情请见api接口文档
request.setBucketName("examplebucket-1250000000");
request.getInput().setObject("1.mp3");
//3.调用接口,获取媒体信息响应对象
MediaInfoResponse response = client.generateMediainfo(request);
```
