## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for text moderation.

| API | Description |
| :------------------------------------------------------------ | :------------------------- |
| [Submitting a text moderation job](https://intl.cloud.tencent.com/document/product/436/48188)  | Submits a text moderation job.   |
| [Querying the text moderation job result](https://intl.cloud.tencent.com/document/product/436/48189)  | Queries the result of the specified text moderation job. |

## SDK API References

For parameters and method description of all APIs in the SDK, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Creating a Task

#### Feature description

This API (`QCloudPostTextRecognitionRequest`) is used to submit a text moderation job. You can receive the moderation result by setting the callback address or querying by `JobId`.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request

**Objective-C**

[//]: # ".cssg-snippet-post-text-recognition"

```objective-c
QCloudPostTextRecognitionRequest * request = [[QCloudPostTextRecognitionRequest alloc]init];

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = @"exampleobject";

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// File region
request.regionName = @"regionName";

// Moderation type, such as `porn` (pornography), `terrorist` (terrorism), `politics` (politically sensitive), and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionPorn | QCloudRecognitionAds | QCloudRecognitionPolitics | QCloudRecognitionTerrorist;

// Moderation policy. If this parameter is not specified, the default policy will be used. For more information, visit https://cloud.tencent.com/document/product/460/56345.
request.bizType = BizType;

request.finishBlock = ^(QCloudPostTextRecognitionResult * outputObject, NSError *error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudPostTextRecognitionResult` class
};
[[QCloudCOSXMLService defaultCOSXML] PostTextRecognition:request];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TextRecognition.m).

**Swift**

[//]: # ".cssg-snippet-post-text-recognition"

```swift
let request = QCloudPostTextRecognitionRequest();

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = "exampleobject";

// Bucket name in the format of BucketName-APPID
request.bucket = "examplebucket-1250000000";

// File region
request.regionName = "regionName";

// Moderation type, such as `porn` (pornography), `terrorist` (terrorism), `politics` (politically sensitive), and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionEnum(rawValue: QCloudRecognitionEnum.porn.rawValue | QCloudRecognitionEnum.ads.rawValue)!

// Moderation policy. If this parameter is not specified, the default policy will be used. For more information, visit https://cloud.tencent.com/document/product/460/56345.
request.setFinish { outputObject, error in
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudPostTextRecognitionResult` class
}
QCloudCOSXMLService.defaultCOSXML().postTextRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TextRecognition.swift).

## Querying Job

#### Feature description

This API (`QCloudGetTextRecognitionRequest`) is used to query the result of the specified text moderation job by `JobId`.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request

**Objective-C**

[//]: # ".cssg-snippet-get-text-recognition"

```objective-c
QCloudGetTextRecognitionRequest * request = [[QCloudGetTextRecognitionRequest alloc]init];

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// File region
request.regionName = @"regionName";

// The `jobid` returned by the `QCloudPostTextRecognitionRequest` API
request.jobId = @"jobid";

request.finishBlock = ^(QCloudTextRecognitionResult * outputObject, NSError *error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudTextRecognitionResult` class
};
[[QCloudCOSXMLService defaultCOSXML] GetTextRecognition:request];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TextRecognition.m).

**Swift**

[//]: # ".cssg-snippet-post-text-recognition"

```swift
let request = QCloudGetTextRecognitionRequest();

// Bucket name in the format of BucketName-APPID
request.bucket = "examplebucket-1250000000";

// File region
request.regionName = "regionName";

// The `jobid` returned by the `QCloudPostTextRecognitionRequest` API
request.jobId = "jobid";

request.setFinish { outputObject, error in
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudTextRecognitionResult` class
};
QCloudCOSXMLService.defaultCOSXML().getTextRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TextRecognition.swift).
