## Overview

This document provides an overview of APIs and SDK code samples related to bucket referer allowlist or blocklist.


| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting bucket referer configuration | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying bucket referer configuration | Queries a bucket referer allowlist or blocklist |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Setting Bucket Referer Configuration

#### Description

This API is used to use the .NET SDK to set the referer allowlist or blocklist of a bucket and read the referer configuration of the bucket.

>?
> - Hotlink protection configuration of buckets is supported from v5.4.24. To download the latest version of SDK, go to [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases) or refer to [Getting Started](https://intl.cloud.tencent.com/document/product/436/30594).
> - For the SDK version changelog, please see [Changelog](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).
> 

#### Sample code

[//]: # ".cssg-snippet-get-service"
```cs
using COSXML.Model.Tag;
using COSXML.Model.Bucket;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class BucketRefererModel {

      private CosXml cosXml;

      BucketRefererModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://cloud.tencent.com/document/product/436/6224.
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Set bucket hotlink protection
      public void PutBucketReferer()
      {
        //.cssg-snippet-body-start:[put-bucket-cors]
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          PutBucketRefererRequest request = new PutBucketRefererRequest(bucket);
          // Set the hotlink protection rule
          RefererConfiguration configuration = new RefererConfiguration();
          // Whether to enable hotlink protection. Enumerated values: `Enabled`, `Disabled`
          configuration.Status = "Enabled"; 
          // Hotlink protection type. Enumerated values: `Black-List`, `White-List`
          configuration.RefererType = "White-List"; 
          // List of domain names in the blocklist/allowlist. Using a prefix to specify multiple domains is supported. Domain names and IPs with ports are supported. A wildcard (*) is supported for second-level or multi-level domains.
          configuration.domainList = new DomainList(); 
          // A single domain name, for example, `www.qq.com/example`, `192.168.1.2:8080`, or `*.qq.com`
          configuration.domainList.AddDomain("*.domain1.com");
          configuration.domainList.AddDomain("*.domain2.com");
          // Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` (default) 
          configuration.EmptyReferConfiguration = "Deny";
          request.SetRefererConfiguration(configuration);
          // Execute the request
          PutBucketRefererResult result = cosXml.PutBucketReferer(request);
          // Request succeeded
          Console.WriteLine(result.GetResultInfo());
        }
        catch (COSXML.CosException.CosClientException clientEx)
        {
          // Request failed
          Console.WriteLine("CosClientException: " + clientEx);
        }
        catch (COSXML.CosException.CosServerException serverEx)
        {
          // Request failed
          Console.WriteLine("CosServerException: " + serverEx.GetInfo());
        }
        
        //.cssg-snippet-body-end
      }

      /// Get the bucket hotlink protection rule
      public void GetBucketReferer()
      {
        //.cssg-snippet-body-start:[get-bucket-cors]
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          GetBucketRefererRequest request = new GetBucketRefererRequest(bucket);
          // Execute the request
          GetBucketRefererResult result = cosXml.GetBucketReferer(request);
          Console.WriteLine(result.GetResultInfo());
          // Status parameter
          Console.WriteLine(result.refererConfiguration.Status);
          // Referer list type
          Console.WriteLine(result.refererConfiguration.RefererType);
          // Domain names in the list
          foreach (string domain in result.refererConfiguration.domainList.domains)
          {
            Console.WriteLine(domain);
          }
        }
        catch (COSXML.CosException.CosClientException clientEx)
        {
          // Request failed
          Console.WriteLine("CosClientException: " + clientEx);
        }
        catch (COSXML.CosException.CosServerException serverEx)
        {
          // Request failed
          Console.WriteLine("CosServerException: " + serverEx.GetInfo());
        }
        
        //.cssg-snippet-body-end
      }
    
      // .cssg-methods-pragma

      static void Main(string[] args)
      {
        BucketRefererModel m = new BucketRefererModel();
        /// Set the CORS rules for the bucket
        m.PutBucketReferer();
        /// Get the CORS rules of the bucket
        m.GetBucketReferer();
        // .cssg-methods-pragma
      }
    }
}

```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/BucketReferer.cs).
>
