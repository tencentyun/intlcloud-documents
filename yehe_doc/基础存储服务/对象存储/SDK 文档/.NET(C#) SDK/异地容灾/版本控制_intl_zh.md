## 简介

本文档提供关于版本控制的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                 |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | 设置版本控制 | 设置存储桶的版本控制功能 |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | 查询版本控制 | 查询存储桶的版本控制信息 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置版本控制

#### 功能说明

设置指定存储桶的版本控制功能。开启版本控制功能后，只能暂停，不能关闭。

#### 示例代码

[//]: # ".cssg-snippet-put-bucket-versioning"
```cs
// 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
string bucket = "examplebucket-1250000000";
PutBucketVersioningRequest request = new PutBucketVersioningRequest(bucket);
request.IsEnableVersionConfig(true); //true: 开启版本控制; false:暂停版本控制

try
{
  PutBucketVersioningResult result = cosXml.PutBucketVersioning(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketVersioning.cs) 查看。

## 查询版本控制

#### 功能说明

查询指定存储桶的版本控制信息。

- 获取存储桶版本控制的状态，需要有该存储桶的读权限。
- 有三种版本控制状态：未启用版本控制、启用版本控制和暂停版本控制。

#### 示例代码

[//]: # ".cssg-snippet-get-bucket-versioning"
```cs
// 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
string bucket = "examplebucket-1250000000";
GetBucketVersioningRequest request = new GetBucketVersioningRequest(bucket);

try
{
  GetBucketVersioningResult result = cosXml.GetBucketVersioning(request);
  // 存储桶的生命周期配置
  VersioningConfiguration conf =  result.versioningConfiguration;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketVersioning.cs) 查看。

