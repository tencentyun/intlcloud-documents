## Overview

This document provides an overview of APIs and SDK code samples related to checking whether a bucket exists.


| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and whether you have permission to access it |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Checking Whether a Bucket Exists

#### Description

This API (`DoesBucketExist`) is used to check whether a bucket exists.

>?
> - The `DoesBucketExist` API is a simple version of the `HEAD Bucket` API provided by the .NET SDK. It can only be used to check whether a bucket exists and return a Boolean value.
> - To get the details of a bucket, use the [bucket extraction](https://intl.cloud.tencent.com/document/product/436/43270) API.

#### Sample code

[//]: # (.cssg-snippet-head-bucket)
```cs
using COSXML.Model.Bucket;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class DoesBucketExistModel {

      private CosXml cosXml;

      DoesBucketExistModel() {
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

      /// Check whether a bucket exists
      public void DoesBucketExist()
      {
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          DoesBucketExistRequest request = new DoesBucketExistRequest(bucket);
          // Execute the request
          bool existState = cosXml.DoesBucketExist(request);
          // Request succeeded
          Console.WriteLine("bucket exist state is: " + existState);
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
        
      }

      static void Main(string[] args)
      {
        DoesBucketExistModel m = new DoesBucketExistModel();

        /// Check whether a bucket exists
        m.DoesBucketExist();
      }
    }
}
```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/HeadBucket.cs).
>
