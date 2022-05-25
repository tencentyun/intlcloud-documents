## Overview

This document provides an overview of APIs and SDK code samples related to object tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Tagging an object | Tags an existing object. |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all existing tags of an object. |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes specified tags of an object. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Tagging an Object

#### Description

This API is used to tag an existing object.

#### Sample code

[//]: # ".cssg-snippet-put-object-tagging"
```cs
using COSXML.Model;
using COSXML.Model.Object;
using COSXML.Model.Tag;
using COSXML.Auth;
using System;
using COSXML;
using System.Linq;

namespace COSSnippet
{
    public class ObjectTaggingModel {

      private CosXml cosXml;

      ObjectTaggingModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Set object tags. This API is supported from v5.4.25.
      public void PutObjectTagging()
      {
        //.cssg-snippet-body-start:[put-object-tagging]
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; // Object key
          PutObjectTaggingRequest request = new PutObjectTaggingRequest(bucket, key);
          // Add a tag key-value pair 
          request.AddTag("tag1", "value1");
          // Execute the request
          PutObjectTaggingResult result = cosXml.PutObjectTagging(request);
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
        
      }

      // .cssg-methods-pragma

      static void Main(string[] args)
      {
        ObjectTaggingModel m = new ObjectTaggingModel();

        /// Set an object tag
        m.PutObjectTagging();
        // .cssg-methods-pragma
      }
    }
}

```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectTagging.cs).
>

## Querying Bucket Tags

#### Description

This API (GET Object tagging) is used to query the existing tags of an object.

#### Sample code

[//]: # ".cssg-snippet-get-bucket-tagging"
```cs
using COSXML.Model;
using COSXML.Model.Object;
using COSXML.Model.Tag;
using COSXML.Auth;
using System;
using COSXML;
using System.Linq;

namespace COSSnippet
{
    public class ObjectTaggingModel {

      private CosXml cosXml;

      ObjectTaggingModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Get object tags. This API is supported from v5.4.25.
      public void GetObjectTagging()
      {
        //.cssg-snippet-body-start:[get-object-tagging]
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; // Object key
          GetObjectTaggingRequest request = new GetObjectTaggingRequest(bucket, key);
          // Execute the request
          GetObjectTaggingResult result = cosXml.GetObjectTagging(request);
          // Request succeeded
          Console.WriteLine(result.GetResultInfo());
          // Traverse the output tagging list
          for (int i = 0; i < result.tagging.tagSet.tags.Count; i++) {
            Console.WriteLine(result.tagging.tagSet.tags[i].key);
            Console.WriteLine(result.tagging.tagSet.tags[i].value);
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
        ObjectTaggingModel m = new ObjectTaggingModel();

        /// Get object tags
        m.GetObjectTagging();
        // .cssg-methods-pragma
      }
    }
}

```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectTagging.cs).
>


## Deleting Object Tags

#### Description

This API is used to delete the existing object tags from an object.

#### Sample code

[//]: # ".cssg-snippet-delete-object-tagging"
```cs
using COSXML.Model;
using COSXML.Model.Object;
using COSXML.Model.Tag;
using COSXML.Auth;
using System;
using COSXML;
using System.Linq;

namespace COSSnippet
{
    public class ObjectTaggingModel {

      private CosXml cosXml;

      ObjectTaggingModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
          .Build();
        
        string secretId = "SECRET_ID";   // SecretId of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // SecretKey of the TencentCloud API. For more information about how to obtain the API key, see https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Delete object tags. This API is supported from v5.4.25.
      public void DeleteObjectTagging()
      {
        //.cssg-snippet-body-start:[delete-object-tagging]
        try
        {
          // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
          string bucket = "examplebucket-1250000000";
          string key = "exampleobject"; // Object key
          DeleteObjectTaggingRequest request = new DeleteObjectTaggingRequest(bucket, key);
          // Execute the request
          DeleteObjectTaggingResult result = cosXml.DeleteObjectTagging(request);
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

      // .cssg-methods-pragma

      static void Main(string[] args)
      {
        ObjectTaggingModel m = new ObjectTaggingModel();

        /// Delete object tags
        m.DeleteObjectTagging();
        // .cssg-methods-pragma
      }
    }
}

```

>? For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/ObjectTagging.cs).
>

