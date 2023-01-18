## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for video moderation.

| API | Description |
| ----------------------------------| ---------------------------------- |
| [Submitting video moderation job](https://intl.cloud.tencent.com/document/product/436/48249) | Submits a video moderation job.   |
| [Querying video moderation job result](https://intl.cloud.tencent.com/document/product/436/48250)  | Queries the result of a specified video moderation job. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Submitting a Video Moderation Job

#### Feature description

The video moderation feature is async. You can submit a job to moderate your video files, and then use the API for querying video moderation job result to query the moderation results.

The following example shows how to submit a video moderation job and then query the result by `JobId`.

>?
> - To perform this operation, the bucket should have CI features enabled.
> - Video moderation APIs are supported starting from v5.4.24. To download the latest SDK, go to [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases) or see [Getting Started](https://intl.cloud.tencent.com/document/product/436/30594).
> - To view the version change log, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).
> 


#### Sample code

[//]: #	".cssg-snippet-SubmitVideoCensorJobModel"

```cs
using COSXML.Model.CI;
using COSXML.Auth;
using System;
using System.Threading;
using COSXML;

namespace COSSnippet
{
    public class SubmitVideoCensorJobModel {

      private CosXml cosXml;

      SubmitVideoCensorJobModel() {
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

      /// Submit the video moderation job
      public string SubmitVideoCensorJob()
      {
        // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
        string bucket = "examplebucket-1250000000"; // Note: To perform this operation, the bucket should have the content moderation feature enabled.
        SubmitVideoCensorJobRequest request = new SubmitVideoCensorJobRequest(bucket);
        request.SetCensorObject("video.mp4"); // Object key of the media file, which should be replaced with that of the actual media file in the bucket.
        // The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`.
        request.SetDetectType("Porn,Ads");
        // Video image moderation is implemented by taking a certain number of screenshots based on the video frame capturing capability and then moderating the screenshots one by one. This parameter is used to specify the configuration of video frame capturing.
        request.SetSnapshotMode("Average"); // Frame capturing mode. Valid values: `Interval` (interval mode), `Average` (average mode), `Fps` (fixed frame rate mode).
        request.SetSnapshotCount("100"); // The number of captured frames. Value range: (0, 10000].
        request.SetSnapshotTimeInterval("1.0"); // Video frame capturing frequency. Value range: (0.000, 60.000] seconds. The value supports the float format, accurate to the millisecond.
        // Execute the request
        SubmitCensorJobResult result = cosXml.SubmitVideoCensorJob(request);
        Console.WriteLine(result.GetResultInfo());
        Console.WriteLine(result.censorJobsResponse.JobsDetail.JobId);
        Console.WriteLine(result.censorJobsResponse.JobsDetail.State);
        Console.WriteLine(result.censorJobsResponse.JobsDetail.CreationTime);
        return result.censorJobsResponse.JobsDetail.JobId;
      }

      static void Main(string[] args)
      {
        SubmitVideoCensorJobModel m = new SubmitVideoCensorJobModel();
        /// Submit the moderation job. The `JobId` uniquely identifies the result of the submitted job.
        string JobId = m.SubmitVideoCensorJob();
        /// Print the `JobId`
        Console.WriteLine("JobId : " + JobId);
      }
    }
}

```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/blob/master/dotnet/dist/SubmitVideoCensorJob.cs).
> 


## Querying Video Moderation Job Result

#### Feature description

This API is used to query the status and result of a video moderation job.

#### Sample code

[//]: #	".cssg-snippet-SubmitVideoCensorJobModel"

```cs
using COSXML.Model.CI;
using COSXML.Auth;
using System;
using System.Threading;
using COSXML;

namespace COSSnippet
{
    public class SubmitVideoCensorJobModel {

      private CosXml cosXml;

      SubmitVideoCensorJobModel() {
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

      /// Query the video moderation job result
      public void GetVideoCensorJobResult(string JobId)
      {
        // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
        string bucket = "examplebucket-1250000000"; // Note: To perform this operation, the bucket should have the content moderation feature enabled.
        GetVideoCensorJobRequest request = new GetVideoCensorJobRequest(bucket, JobId);
        // Execute the request
        GetVideoCensorJobResult result = cosXml.GetVideoCensorJob(request);
        Console.WriteLine(result.GetResultInfo());

        // Read the moderation result
        Console.WriteLine(result.resultStruct.JobsDetail.JobId);
        Console.WriteLine(result.resultStruct.JobsDetail.State);
        Console.WriteLine(result.resultStruct.JobsDetail.CreationTime);
        Console.WriteLine(result.resultStruct.JobsDetail.Object);
        Console.WriteLine(result.resultStruct.JobsDetail.SnapshotCount);
        Console.WriteLine(result.resultStruct.JobsDetail.Result);

        Console.WriteLine(result.resultStruct.JobsDetail.PornInfo.HitFlag);
        Console.WriteLine(result.resultStruct.JobsDetail.PornInfo.Count);
                
        Console.WriteLine(result.resultStruct.JobsDetail.AdsInfo.HitFlag);
        Console.WriteLine(result.resultStruct.JobsDetail.AdsInfo.Count);

        // Moderate video screenshots
        for(int i = 0; i < result.resultStruct.JobsDetail.Snapshot.Count; i++)
        {
            Console.WriteLine(result.resultStruct.JobsDetail.Snapshot[i].Url);
            Console.WriteLine(result.resultStruct.JobsDetail.Snapshot[i].Text);
            Console.WriteLine(result.resultStruct.JobsDetail.Snapshot[i].SnapshotTime);
            Console.WriteLine(result.resultStruct.JobsDetail.Snapshot[i].PornInfo.HitFlag);
            Console.WriteLine(result.resultStruct.JobsDetail.Snapshot[i].PornInfo.Score);
            Console.WriteLine(result.resultStruct.JobsDetail.Snapshot[i].PornInfo.Label);
            Console.WriteLine(result.resultStruct.JobsDetail.Snapshot[i].PornInfo.SubLabel);

            Console.WriteLine(result.resultStruct.JobsDetail.Snapshot[i].AdsInfo.HitFlag);
            Console.WriteLine(result.resultStruct.JobsDetail.Snapshot[i].AdsInfo.Score);
            Console.WriteLine(result.resultStruct.JobsDetail.Snapshot[i].AdsInfo.Label);
            Console.WriteLine(result.resultStruct.JobsDetail.Snapshot[i].AdsInfo.SubLabel);
        }
      }

      static void Main(string[] args)
      {
        SubmitVideoCensorJobModel m = new SubmitVideoCensorJobModel();
        // Enter the `JobId` obtained when you submit the moderation job
        string JobId = "xxx";
        /// Query the moderation job
        m.GetVideoCensorJobResult(JobId);
      }
    }
}

```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/blob/master/dotnet/dist/SubmitVideoCensorJob.cs).
>

