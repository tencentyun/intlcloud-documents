## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for file moderation.

| API | Description |
| ----------------------------------| ---------------------------------- |
| [Submitting file moderation job](https://intl.cloud.tencent.com/document/product/436/48258) | Submits a file moderation job.   |
| [Querying file moderation job result](https://intl.cloud.tencent.com/document/product/436/48259)  | Queries the result of a specified file moderation job. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [API Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Submitting a File Moderation Job

#### Feature description

This API is used to submit a file moderation job, which can check your file for sensitive or non-compliant information. The file moderation feature combines the file preview feature of COS to moderate files by converting them into images and leveraging image content moderation and OCR capabilities.

The following example shows how to submit a file moderation job and then query the result by `JobId`.

>?
> - To perform this operation, the bucket should have CI features enabled.
> - File moderation APIs are supported starting from v5.4.24. To download the latest SDK, go to [Releases](https://github.com/tencentyun/qcloud-sdk-dotnet/releases) or see [Getting Started](https://intl.cloud.tencent.com/document/product/436/30594).
> - To view the version change log, go to [GitHub](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/CHANGELOG.md).
> 


#### Sample code

[//]: #	".cssg-snippet-SubmitDocumentCensorJobModel"

```cs
using COSXML.Model.CI;
using COSXML.Auth;
using System;
using System.Threading;
using COSXML;

namespace COSSnippet
{
    public class SubmitDocumentCensorJobModel {

      private CosXml cosXml;

      SubmitDocumentCensorJobModel() {
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

      /// Submit the file moderation job
      public string SubmitDocumentCensorJob()
      {
        // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
        string bucket = "examplebucket-1250000000"; // Note: To perform this operation, the bucket should have the content moderation feature enabled.
        SubmitDocumentCensorJobRequest request = new SubmitDocumentCensorJobRequest(bucket);
        request.SetUrl("url"); // URL of the file to be moderated, which should be replaced with that of the actual file.
        // The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`.
        request.SetDetectType("Porn,Ads");
        // Execute the request
        SubmitCensorJobResult result = cosXml.SubmitDocumentCensorJob(request);
        Console.WriteLine(result.GetResultInfo());
        Console.WriteLine(result.censorJobsResponse.JobsDetail.JobId);
        Console.WriteLine(result.censorJobsResponse.JobsDetail.State);
        Console.WriteLine(result.censorJobsResponse.JobsDetail.CreationTime);
        return result.censorJobsResponse.JobsDetail.JobId;
      }

      static void Main(string[] args)
      {
        SubmitDocumentCensorJobModel m = new SubmitDocumentCensorJobModel();
        /// Submit the moderation job
        string JobId = m.SubmitDocumentCensorJob();
      }
    }
}

```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/blob/master/dotnet/dist/SubmitDocumentCensorJob.cs).
>

## Querying File Moderation Job

#### Feature description

This API is used to query the status and result of a file moderation job.

#### Sample code

[//]: #	".cssg-snippet-SubmitDocumentCensorJobModel"

```cs
using COSXML.Model.CI;
using COSXML.Auth;
using System;
using System.Threading;
using COSXML;

namespace COSSnippet
{
    public class SubmitDocumentCensorJobModel {

      private CosXml cosXml;

      SubmitDocumentCensorJobModel() {
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

      /// Query the file moderation job result
      public void GetDocumentCensorJobResult(string JobId)
      {
        // Bucket name in the format of `BucketName-APPID`. You can get APPID by referring to https://console.cloud.tencent.com/developer.
        string bucket = "examplebucket-1250000000"; // Note: To perform this operation, the bucket should have the content moderation feature enabled.
        GetDocumentCensorJobRequest request = new GetDocumentCensorJobRequest(bucket, JobId);
        // Execute the request
        GetDocumentCensorJobResult result = cosXml.GetDocumentCensorJob(request);
        Console.WriteLine(result.GetResultInfo());

        // Read the moderation result
        Console.WriteLine(result.resultStruct.JobsDetail.State);
        Console.WriteLine(result.resultStruct.JobsDetail.JobId);
        Console.WriteLine(result.resultStruct.JobsDetail.Suggestion);
        Console.WriteLine(result.resultStruct.JobsDetail.CreationTime);
        Console.WriteLine(result.resultStruct.JobsDetail.Url);
        Console.WriteLine(result.resultStruct.JobsDetail.PageCount);
        Console.WriteLine(result.resultStruct.JobsDetail.Labels);
        Console.WriteLine(result.resultStruct.JobsDetail.Labels.PornInfo.HitFlag);
        Console.WriteLine(result.resultStruct.JobsDetail.Labels.PornInfo.Score);
        Console.WriteLine(result.resultStruct.JobsDetail.PageSegment.Results.Url);
        Console.WriteLine(result.resultStruct.JobsDetail.PageSegment.Results.Text);
        Console.WriteLine(result.resultStruct.JobsDetail.PageSegment.Results.PageNumber);
        Console.WriteLine(result.resultStruct.JobsDetail.PageSegment.Results.PornInfo.HitFlag);
        Console.WriteLine(result.resultStruct.JobsDetail.PageSegment.Results.PornInfo.SubLabel);
        Console.WriteLine(result.resultStruct.JobsDetail.PageSegment.Results.PornInfo.Score);
      }

      static void Main(string[] args)
      {
        SubmitDocumentCensorJobModel m = new SubmitDocumentCensorJobModel();
        /// Enter the `JobId` that is returned during moderation job submission and uniquely identifies this moderation job
        string JobId = "xxx";
        /// Query the moderation job result
        m.GetDocumentCensorJobResult(JobId);
      }
    }
}

```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/blob/master/dotnet/dist/SubmitDocumentCensorJob.cs).
>
