## 简介

本文档提供关于检索存储桶的 API 概览以及 SDK 示例代码。


| API                                                          | 操作名             | 操作描述                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | 检索存储桶及其权限 | 检索存储桶是否存在且是否有权限访问 |

## SDK API 参考

SDK 所有接口的具体参数与方法说明，请参考 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)。

## 检索存储桶及其权限

#### 功能说明

HEAD Bucket 请求可以确认该存储桶是否存在，是否有权限访问。有以下几种情况：

- 存储桶存在且有读取权限，返回 HTTP 状态码为200。
- 无存储桶读取权限，返回 HTTP 状态码为403。
- 存储桶不存在，返回 HTTP 状态码为404。

#### 示例代码

[//]: # (.cssg-snippet-head-bucket)
```cs
using COSXML.Model.Bucket;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class HeadBucketModel {

      private CosXml cosXml;

      HeadBucketModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // 设置默认的地域, COS 地域的简称请参照 https://cloud.tencent.com/document/product/436/6224 
          .Build();
        
        string secretId = "SECRET_ID";   // 云 API 密钥 SecretId, 获取 API 密钥请参照 https://console.cloud.tencent.com/cam/capi
        string secretKey = "SECRET_KEY"; // 云 API 密钥 SecretKey, 获取 API 密钥请参照 https://console.cloud.tencent.com/cam/capi
        long durationSecond = 600;          //每次请求签名有效时长，单位为秒
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// 获取存储桶信息
      public void HeadBucket()
      {
        //.cssg-snippet-body-start:[head-bucket]
        try
        {
          // 存储桶名称，此处填入格式必须为 BucketName-APPID, 其中 APPID 获取参考 https://console.cloud.tencent.com/developer
          string bucket = "examplebucket-1250000000";
          HeadBucketRequest request = new HeadBucketRequest(bucket);
          //执行请求
          HeadBucketResult result = cosXml.HeadBucket(request);
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
        
        //.cssg-snippet-body-end
      }
      // .cssg-methods-pragma

      static void Main(string[] args)
      {
        HeadBucketModel m = new HeadBucketModel();

        /// 获取存储桶信息
        m.HeadBucket();
        // .cssg-methods-pragma
      }
    }
}
```

>? 更多完整示例，请前往 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/HeadBucket.cs) 查看。
>
