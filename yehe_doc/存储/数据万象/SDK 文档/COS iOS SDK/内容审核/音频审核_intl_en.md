## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for audio moderation.

| API | Description |
| :------------------------------------------------------------ | :------------------------- |
| [Submitting an audio moderation job](https://intl.cloud.tencent.com/document/product/436/48262) | Submits an audio moderation job.   |
| [Querying the audio moderation job result](https://intl.cloud.tencent.com/document/product/436/48263)  | Queries the result of the specified audio moderation job. |

## Creating a Task

#### Feature description

This API (`QCloudPostAudioRecognitionRequest`) is used to submit an audio moderation job. You can receive the moderation result by setting the callback address or querying by `JobId`.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request

**Objective-C**

[//]: # (.cssg-snippet-post-audio-recognition)

```objective-c
QCloudPostAudioRecognitionRequest * request = [[QCloudPostAudioRecognitionRequest alloc]init];

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = @"exampleobject";

// File region
request.regionName = @"regionName";

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// Moderation type, such as `porn` (pornography), `terrorist` (terrorism), `politics` (politically sensitive), and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionPorn | QCloudRecognitionAds;

request.bizType = BizType;

request.finishBlock = ^(QCloudPostAudioRecognitionResult * outputObject, NSError *error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudPostAudioRecognitionResult` class
};
[[QCloudCOSXMLService defaultCOSXML] PostAudioRecognition:request];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/AudioRecognition.m).

**Swift**

[//]: # (.cssg-snippet-post-audio-recognition)

```swift
let request = QCloudPostAudioRecognitionRequest();

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = "exampleobject";

// File region
request.regionName = "regionName";

// Bucket name in the format of BucketName-APPID
request.bucket = "examplebucket-1250000000";

// Moderation type, such as `porn` (pornography), `terrorist` (terrorism), `politics` (politically sensitive), and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionEnum(rawValue: QCloudRecognitionEnum.porn.rawValue | QCloudRecognitionEnum.ads.rawValue)!

request.bizType = BizType;

request.setFinish { outputObject, error in
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudPostAudioRecognitionResult` class
};
QCloudCOSXMLService.defaultCOSXML().postAudioRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/AudioRecognition.swift).

## Querying Job

#### Feature description

This API (`QCloudGetAudioRecognitionRequest`) is used to query the result of the specified audio moderation job by `JobId`.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request

**Objective-C**

[//]: # (.cssg-snippet-get-audio-recognition)

```objective-c
QCloudGetAudioRecognitionRequest * request = [[QCloudGetAudioRecognitionRequest alloc]init];

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// File region
request.regionName = @"regionName";

// The `jobid` returned by the `QCloudPostAudioRecognitionRequest` API
request.jobId = @"jobid";

request.finishBlock = ^(QCloudAudioRecognitionResult * outputObject, NSError *error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudAudioRecognitionResult` class
};
[[QCloudCOSXMLService defaultCOSXML] GetAudioRecognition:request];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/AudioRecognition.m).

**Swift**

[//]: # (.cssg-snippet-get-audio-recognition)

```swift
let request = QCloudGetAudioRecognitionRequest();

// Bucket name in the format of BucketName-APPID
request.bucket = "examplebucket-1250000000";

// File region
request.regionName = "regionName";

// The `jobid` returned by the `QCloudPostAudioRecognitionRequest` API
request.jobId = "jobid";

request.setFinish { outputObject, error in
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudAudioRecognitionResult` class
}
QCloudCOSXMLService.defaultCOSXML().getAudioRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/AudioRecognition.swift).
