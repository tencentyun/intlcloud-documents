
## 简介

本文档提供关于数据万象媒体截图的相关 API 概览以及 SDK 示例代码。

| API                                                          | 操作名             | 操作描述                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GenerateSnapshot](https://intl.cloud.tencent.com/document/product/436/46913) | 获取媒体文件某个时间的截图  | 获取媒体文件某个时间的截图  |

## 基本操作

### 获取媒体文件某个时间的截图

#### 功能说明

获取媒体文件某个时间的截图。

#### 方法原型

```java
public SnapshotResponse generateSnapshot(SnapshotRequest request);
```

#### 参数说明

| 参数名称 | 描述                                                         | 类型      | 是否必选 |
| :----------------- | :----------------------------------------------------------- | :-------- | :------- |
| bucketName | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |是|
| Input      | 媒体文件的位置信息                                           | Container | 是       |
| Time       | 截取哪个时间点的内容，单位为秒                               | Float     | 是       |
| Output     | 截图保存的位置信息                                           | Container | 是       |
| Width      | 截图的宽。默认为0                                          | Int       | 否       |
| Height     | 截图的高。默认为0。<br/>Width 和 Height 都为0时，表示使用视频的宽高。<br/>如果单个为0，则以另外一个值按视频宽高比例自动适应 | Int       | 否       |
| Format     | 截图的格式，支持 jpg 和 png，默认 jpg                     | String    | 否       |
| Mode       | 截帧方式<br><li>keyframe：截取指定时间点之前的最近的一个关键帧<br><li>exactframe：截取指定时间点的帧<br/>默认值为 exactframe | String    | 否       |
| Rotate     | 图片旋转方式<br><li>auto：按视频旋转信息进行自动旋转<br><li>off：不旋转<br/>默认值为 auto | String    | 否       |

Input 的内容：

| 参数名称 | 父节点        | 描述       | 类型   | 是否必选 |
| :----------------- | :------------ | :--------- | :----- | :------- |
| Object             | Request.Input | 文件的名称 | String | 是       |

Output 的内容：

| 参数名称） | 父节点         | 描述                  | 类型   | 是否必选 |
| :----------------- | :------------- | :-------------------- | :----- | :------- |
| Region             | Request.Output | 存储桶所在的地域      | String | 是       |
| Bucket             | Request.Output | 文件所属的 COS 存储桶 | String | 是       |
| Object             | Request.Output | 文件的名称            | String | 是       |

#### 返回结果说明

- 成功：返回截图实体信息。
- 失败：发生错误（如 Bucket 不存在），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

#### 请求示例

```java
//1.创建截图请求对象
SnapshotRequest request = new SnapshotRequest();
//2.添加请求参数 参数详情请见api接口文档
request.setBucketName("examplebucket-1250000000");
request.getInput().setObject("1.mp4");
request.getOutput().setBucket("examplebucket-1250000000");
request.getOutput().setRegion("ap-chongqing");
request.getOutput().setObject("test/1.jpg");
request.setTime("15");
//3.调用接口,获取截图响应对象
SnapshotResponse response = client.generateSnapshot(request);
```
