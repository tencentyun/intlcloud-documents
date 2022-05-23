## Overview

This document provides an overview of APIs and SDK code samples for media information.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
|  [GetMediaInfo](https://intl.cloud.tencent.com/document/product/436/46915)    |   Querying file information	 | Queries media file information      |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see the [API documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Querying File Information

#### Feature description

This API is used to query the information of a media file. To use this API, you must enable media processing for the bucket in the console.

>?
> - The `GetMediainfo` API is supported since v5.4.24. To download the new version of SDK, go to [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases) or see [Getting Started](https://intl.cloud.tencent.com/document/product/436/30594).
> - For the SDK version changelog, see [Changelog](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).
> 


#### Sample code

[//]: #	".cssg-snippet-GetMediaInfoModel"

```cs
using COSXML.Model.CI;
using COSXML.Auth;
using System;
using COSXML;

namespace COSSnippet
{
    public class GetMediaInfoModel {

      private CosXml cosXml;

      GetMediaInfoModel() {
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

      /// Get media file information
      public void GetMediaInfo()
      {
        //.cssg-snippet-body-start:[GetMediaInfo]
        // Bucket name in the format of `BucketName-APPID`. You can get the `APPID` by referring to https://console.cloud.tencent.com/developer.
        string bucket = "examplebucket-1250000000";
        string key = "mediafile"; // Object key of the media file, which should be replaced with the actual object key of the media file existing in the bucket
        GetMediaInfoRequest request = new GetMediaInfoRequest(bucket, key);
        // Execute the request
        GetMediaInfoResult result = cosXml.GetMediaInfo(request);
        Console.WriteLine(result.GetResultInfo());
        // Get video media information
        Console.WriteLine(result.mediaInfoResult.MediaInfo.Stream);
        Console.WriteLine(result.mediaInfoResult.MediaInfo.Stream.Video);
        Console.WriteLine(result.mediaInfoResult.MediaInfo.Stream.Video.Index);
        Console.WriteLine(result.mediaInfoResult.MediaInfo.Stream.Video.CodecName);
        // Get audio information
        Console.WriteLine(result.mediaInfoResult.MediaInfo.Stream.Audio);
        Console.WriteLine(result.mediaInfoResult.MediaInfo.Stream.Audio.Index);
        Console.WriteLine(result.mediaInfoResult.MediaInfo.Stream.Audio.CodecName);
        Console.WriteLine(result.mediaInfoResult.MediaInfo.Stream.Audio.CodecLongName);
        // Get the `Format` field
        Console.WriteLine(result.mediaInfoResult.MediaInfo.Format);
        Console.WriteLine(result.mediaInfoResult.MediaInfo.Format.NumStream);
        Console.WriteLine(result.mediaInfoResult.MediaInfo.Format.NumProgram);
        //.cssg-snippet-body-end
      }

      static void Main(string[] args)
      {
        GetMediaInfoModel m = new GetMediaInfoModel();
        /// Get media file information
        m.GetMediaInfo();
        // .cssg-methods-pragma
      }
    }
}
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/blob/master/dotnet/dist/GetMediaInfo.cs).
>

