
## 简介

本文档提供关于数据万象媒体处理工作流的相关 API 概览以及 SDK 示例代码，此处以动图任务举例。

| API                                                          | 操作名             | 操作描述                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [DeleteWorkflow](https://intl.cloud.tencent.com/document/product/1045/43734) | 删除工作流 | 删除一个工作流 |
| [DescribeWorkflow](https://intl.cloud.tencent.com/document/product/1045/43735) | 查询工作流 | 查询一个工作流 |
| [DescribeWorkflowExecution](https://intl.cloud.tencent.com/document/product/1045/43736) | 查询工作流实例详情 | 查询一个工作流实例详情 |
| [DescribeWorkflowExecutions](https://intl.cloud.tencent.com/document/product/1045/43737) | 查询工作流详情列表 | 获取工作流实例列表 |
| [TriggerWorkflowList](https://intl.cloud.tencent.com/document/product/1045/47032) | 触发工作流 | 工作流执行 |


## 删除工作流

#### 功能说明

删除一个工作流。

#### 方法原型

```java
public Boolean deleteWorkflow(MediaWorkflowListRequest request);
```

#### 参数说明

Request中的具体数据描述如下：

| 节点名称（关键字） | 描述                                                     | 类型      | 必选 |
| ------------------ |-------------------------------------------------------- | --------- | ---- |
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| workflowId         | 工作流 ID | String    | 是   |

#### 返回结果说明

- 成功：成功则返回 true。
- 失败：发生错误（如 Bucket 不存在），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
//1.创建工作流请求对象
MediaWorkflowListRequest request = new MediaWorkflowListRequest();
//2.添加请求参数 参数详情请见api接口文档
request.setBucketName("examplebucket-1250000000");
request.setWorkflowId("aaaa");
Boolean response = client.deleteWorkflow(request);
```

## 查询工作流

#### 功能说明
用于搜索工作流。

#### 方法原型

```java
public MediaWorkflowListResponse describeWorkflow(MediaWorkflowListRequest request);
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   | 必选|
| ---------- | ------------------------------------------------------------ | ------ |-----|
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| ids                | 工作流 ID，以`,`符号分割字符串 | String | 否       |
| name               | 工作流名称                   | String | 否       |
| pageNumber         | 第几页                       | String | 否       |
| pageSize           | 每页个数                     | String | 否       |

#### 返回结果说明

- 成功： 返回工作流集合响应对象，其中包含一个工作流对象集合。
- 失败： 发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
//1.创建工作流请求对象
MediaWorkflowListRequest request = new MediaWorkflowListRequest();
//2.添加请求参数 参数详情请见api接口文档
request.setBucketName("examplebucket-1250000000");
MediaWorkflowListResponse response = client.describeWorkflow(request);
List<MediaWorkflowObject> mediaWorkflowList = response.getMediaWorkflowList();
```

## 查询工作流实例详情

#### 功能说明
查询工作流实例详情。

#### 方法原型

```java
public MediaWorkflowExecutionResponse describeWorkflowExecution(MediaWorkflowListRequest request);
```

#### 参数说明

| 参数名称   | 描述                                                         | 类型   | 必选|
| ---------- | ------------------------------------------------------------ | ------ |-----|
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| runId | 工作流实例 ID | String | 是 |

#### 返回结果说明

- 成功： 返回工作流实例响应包装类，类中包含一个工作流实例详情对象。 
- 失败： 发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
//1.创建工作流请求对象
MediaWorkflowListRequest request = new MediaWorkflowListRequest();
//2.添加请求参数 参数详情请见api接口文档
request.setBucketName("examplebucket-1250000000");
request.setRunId("i34bfd8d7eae711ea89fe525400c******");
MediaWorkflowExecutionResponse response = client.describeWorkflowExecution(request);
```


## 查询工作流详情列表

#### 功能说明
查询工作流详情列表。

#### 方法原型

```java
public MediaWorkflowExecutionsResponse describeWorkflowExecutions(MediaWorkflowListRequest request);   
```

#### 参数说明

|节点名称|描述|类型|必选|
|:---|:--|:--|:--|
| bucketName|Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| workflowId         | 工作流 ID                                                    | String | 是       |
| name               | 文件名称                                                     | String | 否       |
| orderByTime        | Desc 或者 Asc。默认为 Desc                                 | String | 否       |
| size               | 拉取的最大任务数。默认为10。最大为100                      | String | 否       |
| states             | 工作流实例状态，以`,`分割支持多状态<br> All，Success，Failed，Running，Cancel。默认为 All | String | 否       |
| startCreationTime  | 拉取创建时间大于该时间。格式为：`%Y-%m-%dT%H:%m:%S%z`        | String | 否       |
| endCreationTime    | 拉取创建时间小于该时间。格式为：`%Y-%m-%dT%H:%m:%S%z`        | String | 否       |
| nextToken          | 请求的上下文，用于翻页。下一页输入 token                   | String | 否       |

#### 返回结果说明

- 成功： 返回工作流实例集合响应对象，其中包含一个工作流对象实例集合。
- 失败： 发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
//1.创建工作流请求对象
MediaWorkflowListRequest request = new MediaWorkflowListRequest();
//2.添加请求参数 参数详情请见api接口文档
request.setBucketName("examplebucket-1250000000");
request.setWorkflowId("w4e6963a18e2446ed8bc8f09410e******");
MediaWorkflowExecutionsResponse response = client.describeWorkflowExecutions(request);
List<MediaWorkflowExecutionObject> workflowExecutionList = response.getWorkflowExecutionList();
```

## 手动触发工作流

#### 功能说明
用于手动触发工作流。

#### 方法原型

```java
public MediaWorkflowListResponse triggerWorkflowList(MediaWorkflowListRequest request);   
```

#### 请求示例
```java
//1.创建工作流请求对象
MediaWorkflowListRequest request = new MediaWorkflowListRequest();
//2.添加请求参数 参数详情请见api接口文档
request.setBucketName("DemoBucket-123456789");
request.setWorkflowId("we32f75950afe4a4682463d8158d*****");
request.setObject("1.mp4");
MediaWorkflowListResponse response = client.triggerWorkflowList(request);
```

#### 参数说明

|节点名称|描述|类型|必选|
|:---|:--|:--|:--|
| bucketName|Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| object          | 需要进行工作流处理的对象名称	                  | String | 是       |
| workflowId          | 需要触发的工作流 ID		                  | String | 是    |
| name          | 存量触发任务名称，支持中文、英文、数字、—和_，长度限制128字符，默认为空 | String | 否       |

#### 返回结果说明

- 成功： 返回 MediaWorkflowListResponse 实例。
- 失败： 发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

