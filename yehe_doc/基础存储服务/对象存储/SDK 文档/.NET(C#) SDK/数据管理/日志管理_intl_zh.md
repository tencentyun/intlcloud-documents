## 简介

本文档提供关于日志管理的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                   |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | 设置日志管理 | 为源存储桶开启日志记录     |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | 查询日志管理 | 查询源存储桶的日志配置信息 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置日志管理

#### 功能说明

PUT Bucket logging 用于为源存储桶开启日志记录，将源存储桶的访问日志保存到指定的目标存储桶中。

#### 示例代码

[//]: # (.cssg-snippet-put-bucket-logging)
```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  PutBucketLoggingRequest request = new PutBucketLoggingRequest(bucket);
  // 设置保存日志的目标路径
  request.SetTarget("targetbucket-1250000000", "logs/");
  //执行请求
  PutBucketLoggingResult result = cosXml.PutBucketLogging(request);
  //请求成功
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLogging.cs) 查看。

## 查询日志管理

#### 功能说明

GET Bucket logging 用于查询指定存储桶的日志配置信息。

#### 示例代码

[//]: # (.cssg-snippet-get-bucket-logging)
```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  GetBucketLoggingRequest request = new GetBucketLoggingRequest(bucket);
  //执行请求
  GetBucketLoggingResult getResult = cosXml.GetBucketLogging(request);
  //请求成功
  BucketLoggingStatus status = getResult.bucketLoggingStatus;
  if (status != null && status.loggingEnabled != null) {
    string targetBucket = status.loggingEnabled.targetBucket;
    string targetPrefix = status.loggingEnabled.targetPrefix;
  }
}
catch (COSXML.CosException.CosClientException clientEx)
{
  //请求失败
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  //请求失败
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLogging.cs) 查看。

