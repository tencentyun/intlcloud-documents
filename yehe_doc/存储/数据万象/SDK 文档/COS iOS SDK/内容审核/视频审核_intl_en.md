## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for video moderation.

| API | Description |
| :------------------------------------------------------------------------ | :------------------------- |
| [Submitting a video moderation job](https://intl.cloud.tencent.com/document/product/436/48249) | Submits a video moderation job.   |
|[Querying the video moderation job result](https://intl.cloud.tencent.com/document/product/436/48250)  | Queries the result of the specified video moderation job. |

## SDK API References

For parameters and method description of all APIs in the SDK, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Creating a Task

#### Feature description

This API (`QCloudPostVideoRecognitionRequest`) is used to submit a video moderation job. You can receive the moderation result by setting the callback address or querying by `JobId`.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request
<dx-tabs>
::: Objective-C
```objectivec
QCloudPostVideoRecognitionRequest * request = [[QCloudPostVideoRecognitionRequest alloc]init];

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = @"exampleobject";

// File region
request.regionName = @"regionName";

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// Moderation type, such as `porn` (pornography) and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionPorn | QCloudRecognitionAds;

// Frame capturing mode. Valid values: `Interval` (interval mode), `Average` (average mode), `Fps` (fixed frame rate mode).
// `Interval` mode: The `TimeInterval` and `Count` parameters take effect. If `Count` is set but `TimeInterval` is not, all frames will be captured to generate a total of `Count` images.
// `Average` mode: The `Count` parameter takes effect, indicating to capture a total of `Count` images at an average interval in the entire video.
// `Fps` mode: `TimeInterval` indicates how many frames to capture per second, and `Count` indicates how many frames to capture in total.
request.mode = QCloudVideoRecognitionModeFps;

// Video frame capturing frequency. Value range: (0.000, 60.000] seconds. The value supports the float format, accurate to the millisecond.
request.timeInterval = 1;

// The number of captured frames. Value range: (0, 10000].
request.count = 10;

// Moderation policy. If this parameter is not specified, the default policy will be used. For more information, visit https://cloud.tencent.com/document/product/460/56345.
request.bizType = @"BizType";

// Specify whether to moderate video sound. Valid values: `0` (moderates the video image only), `1` (moderates both the video image and video sound). Default value: `0`.
request.detectContent = YES;

request.finishBlock = ^(QCloudPostVideoRecognitionResult * outputObject, NSError *error) {
// The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
// `QCloudPostVideoRecognitionResult` class
};
[[QCloudCOSXMLService defaultCOSXML] PostVideoRecognition:request];

```
**Note:** For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/VideoOperation.m).

:::
::: Swift
```swift
let request : QCloudPostVideoRecognitionRequest = QCloudPostVideoRecognitionRequest();

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = "exampleobject";

// File region
request.regionName = "regionName";

// Bucket name in the format of BucketName-APPID
request.bucket = "examplebucket-1250000000";

// Moderation type, such as `porn` (pornography) and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionEnum(rawValue: QCloudRecognitionEnum.porn.rawValue | QCloudRecognitionEnum.ads.rawValue!

// Frame capturing mode. Valid values: `Interval` (interval mode), `Average` (average mode), `Fps` (fixed frame rate mode).
// `Interval` mode: The `TimeInterval` and `Count` parameters take effect. If `Count` is set but `TimeInterval` is not, all frames will be captured to generate a total of `Count` images.
// `Average` mode: The `Count` parameter takes effect, indicating to capture a total of `Count` images at an average interval in the entire video.
// `Fps` mode: `TimeInterval` indicates how many frames to capture per second, and `Count` indicates how many frames to capture in total.
request.mode = QCloudVideoRecognitionMode.fps;

// Video frame capturing frequency. Value range: (0.000, 60.000] seconds. The value supports the float format, accurate to the millisecond.
request.timeInterval = 1;

// The number of captured frames. Value range: (0, 10000].
request.count = 10;

// Moderation policy. If this parameter is not specified, the default policy will be used. For more information, visit https://cloud.tencent.com/document/product/460/56345.
request.bizType = "BizType";

// Specify whether to moderate video sound. Valid values: `0` (moderates the video image only), `1` (moderates both the video image and video sound). Default value: `0`.
request.detectContent = true;
  
request.finishBlock = { (result, error) in
        // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudPostVideoRecognitionResult` class
}
QCloudCOSXMLService.defaultCOSXML().postVideoRecognition(request);
```

**Note:** For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/VideoOperation.swift).
:::
</dx-tabs>

## Querying Job

#### Feature description

This API (`QCloudGetVideoRecognitionRequest`) is used to query the result of the specified video moderation job by job ID.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request

<dx-tabs>
::: Objective-C
```objectivec
QCloudGetVideoRecognitionRequest * request = [[QCloudGetVideoRecognitionRequest alloc]init];

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// The `jobid` returned by the `QCloudPostVideoRecognitionRequest` API
request.jobId = @"jobid";
[request setFinishBlock:^(QCloudVideoRecognitionResult * _Nullable result, NSError * _Nullable error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudVideoRecognitionResult` class
}];
[[QCloudCOSXMLService defaultCOSXML] GetVideoRecognition:request];

```
**Note:** For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/VideoOperation.m).

:::
::: Swift
```swift
let request : QCloudGetVideoRecognitionRequest = QCloudGetVideoRecognitionRequest();

// Bucket name in the format of BucketName-APPID
request.bucket = "examplebucket-1250000000";

// The `jobid` returned by the `QCloudPostVideoRecognitionRequest` API
request.jobId = "jobid";
    
request.finishBlock = { (result, error) in
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudVideoRecognitionResult` class
}
QCloudCOSXMLService.defaultCOSXML().getVideoRecognition(request);
```

**Note:** For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/VideoOperation.swift).
:::
</dx-tabs>


