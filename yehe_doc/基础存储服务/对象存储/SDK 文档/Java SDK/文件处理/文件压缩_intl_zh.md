## 简介

本文档提供关于数据万象文件处理压缩任务的相关 API 概览以及 SDK 示例代码。

| API                                                                            | 操作描述                           |
|--------------------------------------------------------------------------------| ---------------------------------- |
| [提交多文件打包压缩任务](https://intl.cloud.tencent.com/document/product/436/53995) |  创建一个多文件打包压缩任务 |
| [查询多文件打包压缩结果](https://intl.cloud.tencent.com/document/product/436/53996) |  查询指定的多文件打包压缩任务结果 |

## 提交多文件打包压缩任务

### 功能说明

多文件打包压缩功能可以将您的多个文件，打包为 zip 等压缩包格式，以提交任务的方式进行多文件打包压缩，异步返回打包后的文件。

### 方法原型

```java
public FileProcessJobResponse createFileProcessJob(FileProcessRequest request);
```

### 参数说明

Request 的具体数据描述如下：

| 节点名称（关键字）        | 父节点  | 描述                                                         | 类型      | 是否必选 |
|:-----------------| :------ | :----------------------------------------------------------- | :-------- | :------- |
| tag              | Request | 表示任务的类型，多文件打包压缩默认为：FileCompress。               | String    | 是       |
| operation        | Request | 包含文件打包压缩的处理规则。                                 | Container | 是       |
| queueId          | Request | 任务所在的队列 ID。                                          | String    | 是       |
| callBackFormat   | Request | 任务回调格式，JSON 或 XML，默认 XML，优先级高于队列的回调格式。 | String    | 否       |
| callBackType     | Request | 任务回调类型，Url 或 TDMQ，默认 Url，优先级高于队列的回调类型。 | String    | 否       |
| callBack         | Request | 任务回调的地址，优先级高于队列的回调地址。                   | String    | 否       |
| callBackMqConfig | Request | 任务回调 TDMQ 配置，当 CallBackType 为 TDMQ 时必填。详情请参见 [CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945) | Container | 否       |

Container 类型 Operation 的具体数据描述如下：

| 节点名称（关键字）          | 父节点            | 描述                                            | 类型      | 是否必选 |
|:-------------------| :---------------- | :---------------------------------------------- | :-------- | :------- |
| fileCompressConfig | Request.Operation | 指定文件打包压缩的处理规则。                    | Container | 是       |
| userData           | Request.Operation | 透传用户信息, 可打印的 ASCII 码, 长度不超过1024 | String    | 否       |
| output             | Request.Operation | 指定打包压缩后的文件保存的地址信息。            | Container | 是       |

Container 类型 FileCompressConfig 的具体数据描述如下：

| 节点名称（关键字） | 父节点                               | 描述                                                         | 类型       | 是否必选 |
|:----------| :----------------------------------- | :----------------------------------------------------------- | :--------- | :------- |
| flatten   | Request.Operation.FileCompressConfig | 文件打包时，是否需要去除源文件已有的目录结构，有效值：<br><li>0：不需要去除目录结构，打包后压缩包中的文件会保留原有的目录结构；<br><li>1：需要，打包后压缩包内的文件会去除原有的目录结构，所有文件都在同一层级。<br>例如：源文件 URL 为 https://domain/source/test.mp4, 则源文件路径为 source/test.mp4，如果为 1，则 ZIP 包中该文件路径为 test.mp4；如果为0， ZIP 包中该文件路径为 source/test.mp4。 | String     | 是       |
| format    | Request.Operation.FileCompressConfig | 打包压缩的类型，有效值：zip、tar、tar.gz。                   | String     | 是       |
| urlList   | Request.Operation.FileCompressConfig | <li>支持将需要打包的文件整理成索引文件，后台将根据索引文件内提供的文件 url，打包为一个压缩包文件。<li>索引文件需要保存在当前存储桶中，本字段需要提供索引文件的对象地址，例如：/test/index.csv。<br><li>索引文件格式：仅支持 CSV 文件，一行一条 URL（仅支持本存储桶文件），如有多列字段，默认取第一列作为 URL。最多不超过10000个文件, 总大小不超过50G, 否则会导致任务失败。 | String     | 否       |
| prefix    | Request.Operation.FileCompressConfig | 支持对存储桶中的某个前缀进行打包，如果需要对某个目录进行打包，需要加/，例如 test 目录打包，则值为：test/。最多不超过10000个文件，总大小不超过50G，否则会导致任务失败。 | String     | 否       |
| key       | Request.Operation.FileCompressConfig | 支持对存储桶中的多个文件进行打包，个数不能超过 1000, 总大小不超过50G，否则会导致任务失败。 | String 数组 | 否       |

> !UrlList、Prefix、Key 三者仅能选择一个，不能都为空，也不会同时生效。如果填了多个，会按优先级 UrlList > Prefix > Key 取最高优先级执行。

Container 类型 Output 的具体数据描述如下：

| 节点名称（关键字） | 父节点                   | 描述                     | 类型   | 是否必选 |
|:----------| :----------------------- | :----------------------- | :----- | :------- |
| region    | Request.Operation.Output | 存储桶的地域。           | String | 是       |
| bucket    | Request.Operation.Output | 保存压缩后文件的存储桶。 | String | 是       |
| object    | Request.Operation.Output | 压缩后文件的文件名       | String | 是       |

### 返回结果说明

- 成功：返回 FileProcessJobResponse 对象响应信息。
- 失败：发生错误（如 Bucket 不存在），抛出异常 CosClientException 或者
  CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

### 请求示例

```java
//1.创建任务请求对象
FileProcessRequest request=new FileProcessRequest();
//2.添加请求参数 参数详情请见 API 接口文档
request.setBucketName("demo-1234567890");
request.setTag(FileProcessJobType.FileCompress);
FileCompressConfig fileCompressConfig=request.getOperation().getFileCompressConfig();
fileCompressConfig.setFormat("zip");
fileCompressConfig.setFlatten("0");
List<String> keyList=fileCompressConfig.getKey();
keyList.add("mark/pic-1.jpg");
keyList.add("mark/pic-1.pdf");
//QueueId 需要从控制台获取
request.setQueueId("p1ff062b35a494cf0ac4b572df22****");
MediaOutputObject output=request.getOperation().getOutput();
output.setBucket("demo-1234567890");
output.setRegion("ap-shanghai");
output.setObject("output/demo.zip");
//3.调用接口,获取任务响应对象
FileProcessJobResponse response=client.createFileProcessJob(request);
```

## 查询多文件打包压缩结果

### 功能说明

查询一个文件处理任务,根据任务 ID 查询任务详情。

### 方法原型

```java
public FileProcessJobResponse describeFileProcessJob(FileProcessRequest request);
```

### 参数说明

| 参数名称   | 描述                                                                                                 | 类型   | 是否必选|
| ---------- |----------------------------------------------------------------------------------------------------| ------ |-----|
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| jobId | 要查询的任务 ID                                                                                          | String | 是 |

### 返回结果说明

- 成功： 返回任务详情响应包装类，类中包含一个 FileProcessJobResponse 任务详情对象。
- 失败： 发生错误（如身份认证失败），抛出异常 CosClientException 或者
  CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

### 请求示例

```java
//1.创建任务请求对象
FileProcessRequest request = new FileProcessRequest();
//2.添加请求参数 参数详情请见 API 接口文档
request.setBucketName("demo-1234567890");
request.setJobId("fda7eb1607b8411ed8c182156726*****");
//3.调用接口,获取任务响应对象
FileProcessJobResponse response = client.describeFileProcessJob(request);
```
