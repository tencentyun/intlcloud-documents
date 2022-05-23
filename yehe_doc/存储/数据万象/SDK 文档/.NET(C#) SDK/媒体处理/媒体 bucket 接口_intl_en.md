## Overview

This document provides an overview of APIs and SDK code samples for media buckets.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ |---------------------------------- |
| [DescribeMediaBuckets](https://intl.cloud.tencent.com/document/product/436/46909) | Querying media processing activation status	 | Queries buckets with media processing enabled   |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see the [API documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Querying Media Processing Activation Status

#### Feature description

This API is used to query buckets with media processing enabled.

>?
> - The `DescribeMediaBuckets` API is supported since v5.4.24. To download the new version of SDK, go to [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases) or see [Getting Started](https://intl.cloud.tencent.com/document/product/436/30594).
> - For the SDK version changelog, see [Changelog](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).
>


#### Sample code

[//]: #	".cssg-snippet-DescribeMediaBucketModel"

```cs
using COSXML.Model.CI;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class DescribeMediaBucketModel {

      private CosXml cosXml;

      DescribeMediaBucketModel() {
        CosXmlConfig config = new CosXmlConfig.Builder()
          .SetRegion("COS_REGION") // Set the default region. For abbreviations of COS regions, visit https://intl.cloud.tencent.com/document/product/436/6224. 
          .Build();
        
        string secretId = "SECRET_ID";   // TencentCloud API `SecretId`. For more information on how to get it, visit https://console.cloud.tencent.com/cam/capi.
        string secretKey = "SECRET_KEY"; // TencentCloud API `SecretKey`. For more information on how to get it, visit https://console.cloud.tencent.com/cam/capi.
        long durationSecond = 600;          // Validity period of the request signature in seconds
        QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
          secretKey, durationSecond);
        
        this.cosXml = new CosXmlServer(config, qCloudCredentialProvider);
      }

      /// Get the list of buckets with CI enabled
      public void DescribeMediaBucket()
      {
        //.cssg-snippet-body-start:[DescribeMediaBucket]
        DescribeMediaBucketsRequest request = new DescribeMediaBucketsRequest();
        // Execute the request
        DescribeMediaBucketsResult result = cosXml.DescribeMediaBuckets(request);
        Console.WriteLine(result.GetResultInfo());
        // Traverse the bucket list
        for (int i = 0; i < result.mediaBuckets.MediaBucketList.Count; i++)
        {
          Console.WriteLine(result.mediaBuckets.MediaBucketList[i].BucketId);
          Console.WriteLine(result.mediaBuckets.MediaBucketList[i].Region);
          Console.WriteLine(result.mediaBuckets.MediaBucketList[i].CreateTime);
        }
        //.cssg-snippet-body-end
      }

      static void Main(string[] args)
      {
        DescribeMediaBucketModel m = new DescribeMediaBucketModel();
        /// Get the list of media buckets
        m.DescribeMediaBucket();
        // .cssg-methods-pragma
      }
    }
}

```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/blob/master/dotnet/dist/DescribeMediaBucket.cs).
>

