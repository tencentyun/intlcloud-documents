## 简介

本文档提供关于存储桶基本操作的相关 API 概览以及 SDK 示例代码。

| API                                                          | 操作名             | 操作描述                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service（List Buckets）](https://intl.cloud.tencent.com/document/product/436/8291) | 查询存储桶列表     | 查询指定账号下所有的存储桶列表     |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | 创建存储桶         | 在指定账号下创建一个存储桶         |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | 检索存储桶及其权限 | 检索存储桶是否存在且是否有权限访问 |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | 删除存储桶         | 删除指定账号下的空存储桶           |

## 查询存储桶列表

#### 功能说明

用于查询指定账号下所有存储桶列表。

#### 示例代码

```dart
try {
  ListAllMyBuckets listAllMyBuckets = await Cos().getDefaultService().getService();
  // 存储桶列表详情请查看 ListAllMyBuckets 类
} catch (e) {
  // 失败后会抛异常 根据异常进行业务处理
  print(e);
}
```

#### 参数说明

无

#### 返回结果说明

- 成功：返回 ListAllMyBuckets 包含：存储桶列表和存储桶持有者信息。
- 失败：发生错误（如身份认证失败），抛出异常 CosXmlClientException 或者 CosXmlServiceException。详情请参见 [异常处理](https://www.tencentcloud.com/document/product/436/53963)。

ListAllMyBuckets 响应包体具体数据内容如下：

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| buckets | 存储桶列表 | List&lt;Bucket&gt; |
| owner | 存储桶持有者信息 | Owner |

存储桶（Bucket）中包含如下内容：

| 参数名称   | 描述                                                        | 类型   |
| ---------- | ----------------------------------------------------------- | ------ |
| name       | 存储桶的名称                                                | String |
| location   | 存储桶所在地域                                              | String |
| createDate | 存储桶的创建时间，为 ISO8601 格式，例如2019-05-24T10:56:40Z | String |

存储桶持有者信息（Owner）中包含如下内容：

| 参数名称    | 描述               | 类型   |
| ----------- | ------------------ | ------ |
| id          | 完整 ID            | String |
| disPlayName | 存储桶持有者的名字 | String |

## 创建存储桶

#### 功能说明

创建一个存储桶（PUT Bucket）。

#### 示例代码

```dart
// 存储桶名称，由 bucketname-appid 组成，appid 必须填入，可以在 COS 控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
// 存储桶所在地域简称，例如广州地区是 ap-guangzhou
String region = "COS_REGION";
// 是否开启多 AZ
bool enableMAZ = false;
try {
  await Cos().getDefaultService().putBucket(
      bucket, 
      region: region,
      enableMAZ: enableMAZ
  );
} catch (e) {
  // 失败后会抛异常 根据异常进行业务处理
  print(e);
}
```

#### 参数说明

| 参数名称  | 描述                                                         | 类型   | 是否必选 |
| --------- | ------------------------------------------------------------ | ------ | -------- |
| bucket    | 桶名称，Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String | 是       |
| enableMAZ | 是否创建多 AZ 存储桶                                         | String | 否       |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败），抛出异常 CosXmlClientException 或者 CosXmlServiceException。详情请参见 [异常处理](https://www.tencentcloud.com/document/product/436/53963)。

## 检索存储桶及其权限

#### 功能说明

HEAD Bucket 请求可以确认该存储桶是否存在，是否有权限访问。有以下几种情况：

- 存储桶存在且有读取权限，返回 HTTP 状态码为200。
- 无存储桶读取权限，返回 HTTP 状态码为403。
- 存储桶不存在，返回 HTTP 状态码为404。

#### 示例代码

```dart
// 存储桶名称，由 bucketname-appid 组成，appid 必须填入，可以在 COS 控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
// 存储桶所在地域简称，例如广州地区是 ap-guangzhou
String region = "COS_REGION";
try {
  Map<String?, String?> header = await Cos().getDefaultService().headBucket(
      bucket,
      region: region
  );
  // HTTP 状态码为200，HTTP 头为 header
} catch (e) {
  // e.statusCode 查看具体的 HTTP 状态码
  print(e);
}
```

#### 参数说明

| 参数名称 | 描述                                                         | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| bucket   | 桶名称，Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

- 成功：返回 HTTP Header。
- 失败：发生错误（如身份认证失败），抛出异常 CosXmlClientException 或者 CosXmlServiceException。详情请参见 [异常处理](https://www.tencentcloud.com/document/product/436/53963)。

## 删除存储桶

#### 功能说明

删除指定的存储桶（DELETE Bucket）。

>! 删除存储桶前，请确保存储桶内的数据和未完成上传的分块数据已全部清空，否则会无法删除存储桶。

#### 示例代码

```dart
// 存储桶名称，由 bucketname-appid 组成，appid 必须填入，可以在 COS 控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
String bucket = "examplebucket-1250000000";
// 存储桶所在地域简称，例如广州地区是 ap-guangzhou
String region = "COS_REGION";
try {
  await Cos().getDefaultService().deleteBucket(
      bucket,
      region: region
  );
} catch (e) {
  // 失败后会抛异常 根据异常进行业务处理
  print(e);
}
```

#### 参数说明

| 参数名称 | 描述                                                         | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| bucket   | 桶名称，Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败），抛出异常 CosXmlClientException 或者 CosXmlServiceException。详情请参见 [异常处理](https://www.tencentcloud.com/document/product/436/53963)。
