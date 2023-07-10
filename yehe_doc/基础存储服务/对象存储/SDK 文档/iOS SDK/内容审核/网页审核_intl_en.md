
## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for webpage moderation.

| API | Description |
| :--------------- | :------------------ |
| [Submitting webpage moderation job](https://intl.cloud.tencent.com/document/product/436/48282)  | Submits webpage moderation job.   |
| [Querying webpage moderation job result](https://intl.cloud.tencent.com/document/product/436/48283)  | Queries the result of specified webpage moderation job. |

## SDK API References
For the parameters and method description of all the APIs in the SDK, see [QCloudCOSXML SDK for iOS v5.7.4 Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Creating Job
#### Feature description
This API (`QCloudPostWebRecognitionRequest`) is used to submit a webpage moderation job. The job can be queried by `JobId`.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request

**Objective-C**

[//]: # ".cssg-snippet-post-web-recognition"
```objective-c
QCloudPostWebRecognitionRequest * request = [[QCloudPostWebRecognitionRequest alloc]init];

// Bucket name in the format of `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// File region
request.regionName = @"regionName";

request.url = @"www.****.com";
// Moderation type, such as `porn` (pornography), `terrorist` (terrorism), `politics` (politically sensitive), and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionPorn | QCloudRecognitionAds | QCloudRecognitionPolitics | QCloudRecognitionTerrorist;

// Moderation policy. If this parameter is not specified, the default policy will be used. For more information, visit https://cloud.tencent.com/document/product/460/56345.
request.bizType = BizType;

request.finishBlock = ^(QCloudPostWebRecognitionResult * outputObject, NSError *error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudPostTextRecognitionResult` class:
};
[[QCloudCOSXMLService defaultCOSXML] PostWebRecognition:request];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/WebRecognition.m).


**Swift**

[//]: # ".cssg-snippet-post-web-recognition"
```swift
let request = QCloudPostWebRecognitionRequest();

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.url = "www.***.com";

// File region
request.regionName = "regionName";

// Bucket name in the format of `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

// Moderation type, such as `porn` (pornography), `terrorist` (terrorism), `politics` (politically sensitive), and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionEnum(rawValue: QCloudRecognitionEnum.porn.rawValue | QCloudRecognitionEnum.ads.rawValue)!

// Moderation policy. If this parameter is not specified, the default policy will be used. For more information, visit https://cloud.tencent.com/document/product/460/56345.
request.setFinish { outputObject, error in
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudPostTextRecognitionResult` class:
}
QCloudCOSXMLService.defaultCOSXML().postWebRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/WebRecognition.swift).


## Querying Job
#### Feature description
This API (`QCloudGetWebRecognitionRequest`) is used to query the result of the specified webpage moderation job by `JobId`.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request
**Objective-C**

[//]: # ".cssg-snippet-get-web-recognition"
```objective-c
QCloudGetWebRecognitionRequest * request = [[QCloudGetWebRecognitionRequest alloc]init];

// Bucket name in the format of `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

// File region
request.regionName = @"regionName";

// The `jobid` returned by the `QCloudPostWebRecognitionRequest` API
request.jobId = @"jobid";

request.finishBlock = ^(QCloudWebRecognitionResult * outputObject, NSError *error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudWebRecognitionResult` class:
};
[[QCloudCOSXMLService defaultCOSXML] GetWebRecognition:request];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/WebRecognition.m).

**Swift**

[//]: # ".cssg-snippet-get-web-recognition"
```swift
let request = QCloudGetWebRecognitionRequest();

// Bucket name in the format of `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

// File region
request.regionName = "regionName";

// The `jobid` returned by the `QCloudPostWebRecognitionRequest` API
request.jobId = "jobid";

request.setFinish { outputObject, error in
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudWebRecognitionResult` class:
};
QCloudCOSXMLService.defaultCOSXML().getWebRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/WebRecognition.swift).


