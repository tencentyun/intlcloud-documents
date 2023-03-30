## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://www.tencentcloud.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples related to live stream moderation.

| API | Description  |
| :------------------------------------------------------------------------ | :------------------------- |
|[Submitting a live stream moderation job](https://www.tencentcloud.com/document/product/436/48277) | Submits a live stream moderation job.   |
|[Querying live stream moderation job result](https://www.tencentcloud.com/document/product/436/48279)  | Queries the result of a specified live stream moderation job. |
|[Canceling a live stream moderation job](https://www.tencentcloud.com/document/product/436/48278)  | Cancels a specified live stream moderation job. |

## SDK API References

For parameters and method description of all APIs in the SDK, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Creating a Job

#### Feature description

This API (`QCloudPostLiveVideoRecognitionRequest`) is used to submit a live stream moderation job. You can receive the moderation result by setting the callback address or querying by `JobId`.

> ! The COS iOS SDK version should be v6.1.6 or later.

#### Request example

**Objective-C**

[//]: # ".cssg-snippet-post-video-recognition"

```objective-c

QCloudPostLiveVideoRecognitionRequest * request = [[QCloudPostLiveVideoRecognitionRequest alloc]init];

request.regionName = @"regionName";

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// The path where to dump the live stream. The TS and M3U8 files of the live stream will be saved in this directory of the bucket. The saved M3U8 file will be named Path/{$JobId}.m3u8, and the saved TS file will be named Path/{$JobId}-{$Realtime}.ts, where `Realtime` is the 17-digit time of `year, month, day, hour, minute, second, and millisecond`.
request.path = @"test";

// The URL of the live stream to be moderated, such as `rtmp://example.com/live/123`.
request.url = @"test";

// Moderation policy. If this parameter is not specified, the default policy will be used. For more information, visit https://www.tencentcloud.com/document/product/1045/52107.
request.bizType = BizType;

request.finishBlock = ^(QCloudPostVideoRecognitionResult * outputObject, NSError *error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudPostVideoRecognitionResult` class
};
[[QCloudCOSXMLService defaultCOSXML] PostLiveVideoRecognition:request];

```

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/LiveVideoOperation.m).

## Querying a Job

#### Feature description

This API (`QCloudGetLiveVideoRecognitionRequest`) is used to query the result of a specified live stream moderation job by `JobId`.

> ! The COS iOS SDK version should be v6.1.6 or later.

#### Request example

**Objective-C**

[//]: # ".cssg-snippet-get-video-recognition"

```objective-c
QCloudGetLiveVideoRecognitionRequest * request = [[QCloudGetLiveVideoRecognitionRequest alloc]init];

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// The `jobid` returned by the `QCloudPostLiveVideoRecognitionRequest` API
request.jobId = @"jobid";

request.regionName = @"regionName";

request.finishBlock = ^(QCloudGetVideoRecognitionRequest * outputObject, NSError *error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudVideoRecognitionResult` class
};
[[QCloudCOSXMLService defaultCOSXML] GetLiveVideoRecognition:request];

```

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/LiveVideoOperation.m).

## Canceling a Job

#### Feature description

This API (`QCloudCancelLiveVideoRecognitionRequest`) is used to cancel a specified live stream moderation job by `JobId`.

> ! The COS iOS SDK version should be v6.1.6 or later.

#### Request example

**Objective-C**

[//]: # ".cssg-snippet-get-video-recognition"

```objective-c

QCloudCancelLiveVideoRecognitionRequest * request = [[QCloudCancelLiveVideoRecognitionRequest alloc]init];

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// The `jobid` returned by the `QCloudPostLiveVideoRecognitionRequest` API
request.jobId = @"jobid";

request.regionName = @"regionName";

request.finishBlock = ^(QCloudPostVideoRecognitionResult * outputObject, NSError *error) {
// The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
// `QCloudPostVideoRecognitionResult` class
};
[[QCloudCOSXMLService defaultCOSXML] CancelLiveVideoRecognition:request];

```

> ?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/LiveVideoOperation.m).
