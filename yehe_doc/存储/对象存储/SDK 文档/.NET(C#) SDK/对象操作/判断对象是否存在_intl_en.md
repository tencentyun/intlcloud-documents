## Overview

This document provides an overview of APIs and SDK code samples related to checking whether an object exists.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | Querying object metadata | Queries the metadata of an object. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Checking Whether an Object Exists

#### Description

This API accepts the bucket name and object name parameters as input parameters and return a Boolean value. It is in fact the encapsulation of the `HeadObject` (querying object metadata) API. To get the detailed metadata of an object, use the API for [querying object metadata](https://intl.cloud.tencent.com/document/product/436/38067).

#### Sample code

[//]: # (.cssg-snippet-head-object)
```cs
using COSXML.Model.Object;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class DoesObjectExistModel {

      private CosXml cosXml;

      DoesObjectExistModel() {
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

      /// Check whether an object exists
      public void DoesObjectExist()
      {
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; // Object key
          DoesObjectExistRequest request = new DoesObjectExistRequest(bucket, key);
          // Execute the request
          bool exist = cosXml.DoesObjectExist(request);
          // Request succeeded
          Console.WriteLine("object exist state is: " + exist);
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
        DoesObjectExistModel m = new DoesObjectExistModel();

        /// Check whether an object exists
        m.DoesObjectExist();
        // .cssg-methods-pragma
      }
    }
}

```
>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/HeadObject.cs).
>

