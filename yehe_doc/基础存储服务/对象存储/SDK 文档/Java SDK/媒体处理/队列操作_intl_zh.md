
## 简介

本文档提供关于数据万象媒体处理队列的相关 API 概览以及 SDK 示例代码。

| API                                                          | 操作名             | 操作描述                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [DescribeMediaQueues](https://intl.cloud.tencent.com/document/product/1045/43672) | 查询队列 | 查询当前账号下对应的队列信息 |
| [UpdateMediaQueue](https://intl.cloud.tencent.com/document/product/1045/43673) | 更新队列 | 接口用于更新队列，修改回调信息 |

## 基本操作

### 查询队列

#### 功能说明

查询当前账号下对应的队列信息。

#### 方法原型

```java
public MediaListQueueResponse describeMediaQueues(MediaQueueRequest mediaQueueRequest);
```

#### 参数说明


| 参数名称   | 描述                                                         | 类型   |必选|
| ---------- | ------------------------------------------------------------ | ------ |---|
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| queueIds   | 队列 ID，以`,`符号分割字符串      | string                                    | 否   |
| state      | <li>Active 表示队列内的作业会被媒体转码服务调度转码执行<br/><li> Paused 表示队列暂停，作业不再会被媒体转码调度转码执行，队列内的所有作业状态维持在暂停状态，已经处于转码中的任务将继续转码，不受影响 | string | 否   |
| pageNumber | 第几页  | string                                                       | 否   |
| pageSize   | 每页个数 | string                                                     | 否   |

#### 返回结果说明

- 成功：返回队列对象集合信息。
- 失败：发生错误（如 Bucket 不存在），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
MediaQueueRequest request = new MediaQueueRequest();
request.setBucketName("examplebucket-1250000000");
MediaListQueueResponse response = client.describeMediaQueues(request);
```

### 更新队列

#### 功能说明

接口用于更新队列，修改回调信息。

#### 方法原型

```java
public MediaQueueResponse updateMediaQueue(MediaQueueRequest mediaQueueRequest);
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   |必选|
| ---------- | ------------------------------------------------------------ | ------ |---|
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| Name   | 模板名称,长度限制100字符    | string| 是  |
| state      | <li>Active 表示队列内的作业会被媒体转码服务调度转码执行<br/><li>Paused 表示队列暂停，作业不再会被媒体转码调度转码执行，<br/>队列内的所有作业状态维持在暂停状态，已经处于转码中的任务将继续转码，不受影响 | string | 是  |
| QueueID | 管道 ID  | string|是 |
| NotifyConfig   | 通知渠道,第三方回调 url	 | Container| 是 |

Container 类型 NotifyConfig 的具体数据描述如下：

| 参数名称   | 描述| 类型   |必选|
| ---------- | --- | ------ |---|
| Url | 回调 url 地址 | String |否|
| Type | 回调类型，普通回调：Url | String |否|
| Event | 回调事件，视频转码完成：TransCodingFinish	 | String |否|
| State | 回调开关，Off，On | String |否|


#### 返回结果说明

- 成功： 返回队列响应实体，包含有关 queue 的描述。
- 失败： 发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
MediaQueueRequest request = new MediaQueueRequest();
request.setBucketName("examplebucket-1250000000");
request.setQueueId("p9900025e4ec44b5e8225e70a521*****");
request.getNotifyConfig().setUrl("cloud.tencent.com");
request.setState("Active");
request.setName("testQueue");
MediaQueueResponse response = client.updateMediaQueue(request);
```
