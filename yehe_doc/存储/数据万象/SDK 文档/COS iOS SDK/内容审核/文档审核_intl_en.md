## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for file moderation.

| API | Description |
| :------------------------------------------------------------ | :------------------------- |
| [Submitting a file moderation job](https://intl.cloud.tencent.com/document/product/436/48258) | Submits a file moderation job.   |
| [Querying the file moderation job result](https://intl.cloud.tencent.com/document/product/436/48259)  | Queries the result of the specified file moderation job. |

## SDK API References

For parameters and method description of all APIs in the SDK, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Creating a Task

#### Feature description

This API (`QCloudPostDocRecognitionRequest`) is used to submit a file moderation job. You can receive the moderation result by setting the callback address or querying by `JobId`.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request

**Objective-C**

[//]: # ".cssg-snippet-post-doc-recognition"

```objective-c
QCloudPostDocRecognitionRequest * request = [[QCloudPostDocRecognitionRequest alloc]init];

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = @"exampleobject";

// File region
request.regionName = @"regionName";

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

request.type = @"doc";

// Moderation type, such as `porn` (pornography), `terrorist` (terrorism), `politics` (politically sensitive), and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionPorn | QCloudRecognitionAds | QCloudRecognitionPolitics | QCloudRecognitionTerrorist;

// Moderation policy. If this parameter is not specified, the default policy will be used. For more information, visit https://cloud.tencent.com/document/product/460/56345.
request.bizType = BizType;

request.finishBlock = ^(QCloudPostDocRecognitionResult * outputObject, NSError *error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudPostDocRecognitionResult` class
};
[[QCloudCOSXMLService defaultCOSXML] PostDocRecognition:request];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DocRecognition.m).

**Swift**

[//]: # ".cssg-snippet-post-doc-recognition"

```swift
let request = QCloudPostDocRecognitionRequest();

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = "exampleobject";

// File region
request.regionName = "regionName";

// Bucket name in the format of BucketName-APPID
request.bucket = "examplebucket-1250000000";

request.type = "doc";

// Moderation type, such as `porn` (pornography), `terrorist` (terrorism), `politics` (politically sensitive), and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionEnum(rawValue: QCloudRecognitionEnum.porn.rawValue | QCloudRecognitionEnum.ads.rawValue)!

// Moderation policy. If this parameter is not specified, the default policy will be used. For more information, visit https://cloud.tencent.com/document/product/460/56345.
request.setFinish { outputObject, error in
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudPostDocRecognitionResult` class
}
QCloudCOSXMLService.defaultCOSXML().postDocRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DocRecognition.swift).

## Querying Job

#### Feature description

This API (`QCloudGetDocRecognitionRequest`) is used to query the result of the specified file moderation job by `JobId`.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request

**Objective-C**

[//]: # ".cssg-snippet-get-doc-recognition"

```objective-c
QCloudGetDocRecognitionRequest * request = [[QCloudGetDocRecognitionRequest alloc]init];

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// File region
request.regionName = @"regionName";

// The `jobid` returned by the `QCloudPostDocRecognitionRequest` API
request.jobId = @"jobid";

request.finishBlock = ^(QCloudDocRecognitionResult * outputObject, NSError *error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudDocRecognitionResult` class
};
[[QCloudCOSXMLService defaultCOSXML] GetDocRecognition:request];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/DocRecognition.m).

**Swift**

[//]: # ".cssg-snippet-get-doc-recognition"

```swift
let request = QCloudGetDocRecognitionRequest();

// Bucket name in the format of BucketName-APPID
request.bucket = "examplebucket-1250000000";

// File region
request.regionName = "regionName";

// The `jobid` returned by the `QCloudPostDocRecognitionRequest` API
request.jobId = "jobid";

request.setFinish { outputObject, error in
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudDocRecognitionResult` class
};
QCloudCOSXMLService.defaultCOSXML().getDocRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/DocRecognition.swift).
