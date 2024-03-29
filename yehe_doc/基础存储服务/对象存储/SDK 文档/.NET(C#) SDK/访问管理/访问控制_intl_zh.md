## 简介

本文档提供关于存储桶、对象的访问控制列表（ACL）的相关 API 概览以及 SDK 示例代码。

**存储桶 ACL**

| API                                                          | 操作名         | 操作描述                                |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 设置存储桶 ACL | 设置指定存储桶的访问权限控制列表（ACL） |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | 查询存储桶 ACL | 查询指定存储桶的访问权限控制列表（ACL） |

**对象 ACL**

| API                                                          | 操作名       | 操作描述                                      |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 设置对象 ACL | 设置存储桶中某个对象的访问控制列表 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 查询对象 ACL | 查询对象的访问控制列表                |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)。


## 存储桶 ACL

### 设置存储桶 ACL

#### 功能说明

设置指定存储桶的访问权限控制列表（ACL）。

#### 示例代码

[//]: # (.cssg-snippet-put-bucket-acl)
```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  PutBucketACLRequest request = new PutBucketACLRequest(bucket);
  //设置私有读写权限
  request.SetCosACL(CosACL.Private);
  //授予1131975903账号读权限
  COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
  readAccount.AddGrantAccount("1131975903", "1131975903");
  request.SetXCosGrantRead(readAccount);
  //执行请求
  PutBucketACLResult result = cosXml.PutBucketACL(request);
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketACL.cs) 查看。

### 查询存储桶 ACL

#### 功能说明

查询指定存储桶的访问权限控制列表（ACL）。

#### 示例代码

[//]: # (.cssg-snippet-get-bucket-acl)
```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  GetBucketACLRequest request = new GetBucketACLRequest(bucket);
  //执行请求
  GetBucketACLResult result = cosXml.GetBucketACL(request);
  //存储桶的 ACL 信息
  AccessControlPolicy acl = result.accessControlPolicy;
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketACL.cs) 查看。

## 对象 ACL

### 设置对象 ACL

#### 功能说明

设置存储桶中某个对象的访问控制列表（ACL）。

#### 示例代码

[//]: # (.cssg-snippet-put-object-acl)
```cs
// 因为存储桶 ACL 最多1000条，为避免 ACL 达到上限，
// 非必须情况不建议给对象单独设置 ACL(对象默认继承 bucket 权限).
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //对象键
  PutObjectACLRequest request = new PutObjectACLRequest(bucket, key);
  //设置私有读写权限 
  request.SetCosACL(CosACL.Private);
  //授予1131975903账号读权限 
  COSXML.Model.Tag.GrantAccount readAccount = new COSXML.Model.Tag.GrantAccount();
  readAccount.AddGrantAccount("1131975903", "1131975903");
  request.SetXCosGrantRead(readAccount);
  //执行请求
  PutObjectACLResult result = cosXml.PutObjectACL(request);
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

>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectACL.cs) 查看。

### 查询对象 ACL

#### 功能说明

查询对象的访问控制列表。

#### 示例代码

[//]: # (.cssg-snippet-get-object-acl)
```cs
try
{
  // 存储桶名称，此处填入格式必须为 bucketname-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
  string bucket = "examplebucket-1250000000";
  string key = "exampleobject"; //对象键
  GetObjectACLRequest request = new GetObjectACLRequest(bucket, key);
  //执行请求
  GetObjectACLResult result = cosXml.GetObjectACL(request);
  //对象的 ACL 信息
  AccessControlPolicy acl = result.accessControlPolicy;
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
>?更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectACL.cs) 查看。



