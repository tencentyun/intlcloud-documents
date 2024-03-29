## 简介

本文档提供关于列出对象操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名                   | 操作描述                                       |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614) | 查询对象列表             | 查询存储桶下的部分或者全部对象                 |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | 查询对象及其历史版本列表 | 查询存储桶下的部分或者全部对象及其历史版本信息 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)。

## 查询对象列表

#### 功能说明

查询存储桶下的部分或者全部对象。

#### 示例代码一: 获取第一页数据

[//]: #	".cssg-snippet-get-bucket"

```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  GetBucketRequest request = new GetBucketRequest(bucket);
  //执行请求
  GetBucketResult result = cosXml.GetBucket(request);
  //bucket的相关信息
  ListBucket info = result.listBucket;
  if (info.isTruncated) {
    // 数据被截断，记录下数据下标
    this.nextMarker = info.nextMarker;
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

> ?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs) 查看。

#### 示例代码二：请求下一页数据

[//]: #	".cssg-snippet-get-bucket-next-page"

```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  GetBucketRequest request = new GetBucketRequest(bucket);
  //上一次拉取数据的下标
  request.SetMarker(this.nextMarker);
  //执行请求
  GetBucketResult result = cosXml.GetBucket(request);
  //bucket的相关信息
  ListBucket info = result.listBucket;
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

> ?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs) 查看。

#### 示例代码三：获取对象列表与子目录

[//]: #	".cssg-snippet-get-bucket-with-delimiter"

```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  GetBucketRequest request = new GetBucketRequest(bucket);
  //获取 a/ 下的对象以及子目录
  request.SetPrefix("a/");
  request.SetDelimiter("/");
  //执行请求
  GetBucketResult result = cosXml.GetBucket(request);
  //bucket的相关信息
  ListBucket info = result.listBucket;
  // 对象列表
  List<ListBucket.Contents> objects = info.contentsList;
  // 子目录列表
  List<ListBucket.CommonPrefixes> subDirs = info.commonPrefixesList;
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

> ?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjects.cs) 查看。

## 查询对象历史版本列表

#### 功能说明

查询开启版本控制的存储桶下的部分或者全部对象。

#### 示例代码一：获取对象历史版本列表第一页数据

[//]: #	".cssg-snippet-list-objects-versioning"

```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  ListBucketVersionsRequest request = new ListBucketVersionsRequest(bucket);
  //执行请求
  ListBucketVersionsResult result = cosXml.ListBucketVersions(request);
  //bucket的相关信息
  ListBucketVersions info = result.listBucketVersions;

  List<ListBucketVersions.Version> objects = info.objectVersionList;
  List<ListBucketVersions.CommonPrefixes> prefixes = info.commonPrefixesList;

  if (info.isTruncated) {
    // 数据被截断，记录下数据下标
    this.keyMarker = info.nextKeyMarker;
    this.versionIdMarker = info.nextVersionIdMarker;
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

> ?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjectsVersioning.cs) 查看。

#### 示例代码二：获取对象历史版本列表下一页数据

[//]: #	".cssg-snippet-list-objects-versioning-next-page"

```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  ListBucketVersionsRequest request = new ListBucketVersionsRequest(bucket);

  // 上一页的数据结束下标
  request.SetKeyMarker(this.keyMarker);
  request.SetVersionIdMarker(this.versionIdMarker);

  //执行请求
  ListBucketVersionsResult result = cosXml.ListBucketVersions(request);
  ListBucketVersions info = result.listBucketVersions;

  if (info.isTruncated) {
    // 数据被截断，记录下数据下标
    this.keyMarker = info.nextKeyMarker;
    this.versionIdMarker = info.nextVersionIdMarker;
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

> ?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ListObjectsVersioning.cs) 查看。
