## Overview

This document provides an overview of APIs and SDK code samples for media screenshot.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
|   [GetSnapshot](https://intl.cloud.tencent.com/document/product/436/46912)     |  Querying screenshot	 |   Query the screenshot of media file at some time point     |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see the [API documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Querying Screenshot

#### Feature description

This API is used to query the screenshot of a media file at some time point.

>?
> - The `GetSnapshot` API is supported since v5.4.24. To download the new version of SDK, go to [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases) or see [Getting Started](https://intl.cloud.tencent.com/document/product/436/30594).
> - For the SDK version changelog, see [Changelog](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).
> 


#### Sample code

[//]: #	".cssg-snippet-GetSnapshotModel"

```cs
using COSXML.Model.CI;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class GetSnapshotModel {

      private CosXml cosXml;

      GetSnapshotModel() {
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

      /// Capture video frames
      public void GetSnapshot()
      {
        // Bucket name in the format of `BucketName-APPID`. You can get the `APPID` by referring to https://console.cloud.tencent.com/developer.
        string bucket = "examplebucket-1250000000";
        string key = "video.mp4"; // Object key of the media file, which should be replaced with the actual object key of the media file existing in the bucket
        float time = 1.5F; // Screenshot time point expressed as a floating point number
        string destPath = @"temp-source-file"; // The path to save the screenshot file, which needs to be replaced with a local specific path, such as "/usr/local/"
        GetSnapshotRequest request = new GetSnapshotRequest(bucket, key, time, destPath);
        // Execute the request
        GetSnapshotResult result = cosXml.GetSnapshot(request);
        Console.WriteLine(result.GetResultInfo());
      }

      static void Main(string[] args)
      {
        GetSnapshotModel m = new GetSnapshotModel();
        /// Capture video frames
        m.GetSnapshot();
      }
    }
}
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/blob/master/dotnet/dist/GetSnapshot.cs).
>

