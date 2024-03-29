## 简介
本文档提供关于生命周期的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                       |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | 设置生命周期 | 设置存储桶的生命周期管理的配置 |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | 查询生命周期 | 查询存储桶生命周期管理的配置   |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | 删除生命周期 | 删除存储桶生命周期管理的配置   |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)。

## 设置生命周期

#### 功能说明

设置指定存储桶的生命周期配置信息。

#### 示例代码

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  PutBucketLifecycleRequest request = new PutBucketLifecycleRequest(bucket);
  //设置 lifecycle
  LifecycleConfiguration.Rule rule = new LifecycleConfiguration.Rule();
  rule.id = "lfiecycleConfigureId";
  rule.status = "Enabled"; //Enabled，Disabled

  rule.filter = new COSXML.Model.Tag.LifecycleConfiguration.Filter();
  rule.filter.prefix = "2/";

  //指定分片过期删除操作
  rule.abortIncompleteMultiUpload = new LifecycleConfiguration.AbortIncompleteMultiUpload();
  rule.abortIncompleteMultiUpload.daysAfterInitiation = 2;

  request.SetRule(rule);

  //执行请求
  PutBucketLifecycleResult result = cosXml.PutBucketLifecycle(request);
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLifecycle.cs) 查看。


## 查询生命周期

#### 功能说明

查询存储桶的生命周期管理配置。

#### 示例代码

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  GetBucketLifecycleRequest request = new GetBucketLifecycleRequest(bucket);
  //执行请求
  GetBucketLifecycleResult result = cosXml.GetBucketLifecycle(request);
  //存储桶的生命周期配置
  LifecycleConfiguration conf = result.lifecycleConfiguration;
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLifecycle.cs) 查看。

## 删除生命周期

#### 功能说明

删除存储桶生命周期管理的配置。

#### 示例代码

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  DeleteBucketLifecycleRequest request = new DeleteBucketLifecycleRequest(bucket);
  //执行请求
  DeleteBucketLifecycleResult result = cosXml.DeleteBucketLifecycle(request);
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketLifecycle.cs) 查看。

