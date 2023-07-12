## Overview

This document provides an overview of APIs and SDK code samples related to how to query a bucket list.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under a specified account |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Querying a Bucket List

#### Description

This API is used to query the list of all buckets under a specified account.

#### Sample code

[//]: # (.cssg-snippet-get-service)
```cs
using COSXML.Model.Tag;
using COSXML.Model.Service;
using COSXML.Auth;
using System;
using COSXML;
using System.Collections.Generic;

namespace COSSnippet
{
    public class GetServiceModel {

      private CosXml cosXml;

      GetServiceModel() {
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

      /// Get the bucket list.
      public void GetService()
      {
        //.cssg-snippet-body-start:[get-service]
        try
        {
          GetServiceRequest request = new GetServiceRequest();
          // Execute the request
          GetServiceResult result = cosXml.GetService(request);
          // Get the list of all buckets.
          List<ListAllMyBuckets.Bucket> allBuckets = result.listAllMyBuckets.buckets;
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

      /// Get the list of buckets residing in this region.
      public void GetRegionalService()
      {
        //.cssg-snippet-body-start:[get-regional-service]
        try
        {
          GetServiceRequest request = new GetServiceRequest();
          string region = "ap-guangzhou";
          request.host = $"cos.{region}.myqcloud.com";
          // Execute the request
          GetServiceResult result = cosXml.GetService(request);
          // Get the list of all buckets.
          List<ListAllMyBuckets.Bucket> allBuckets = result.listAllMyBuckets.buckets;
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
        GetServiceModel m = new GetServiceModel();

        /// Get the bucket list.
        m.GetService();
        /// Get the list of buckets residing in this region.
        m.GetRegionalService();
        // .cssg-methods-pragma
      }
    }
}

```

>? For the complete sample, please go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/GetService.cs).
>

