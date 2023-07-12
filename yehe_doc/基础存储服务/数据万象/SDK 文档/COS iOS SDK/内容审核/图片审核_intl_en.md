## Overview 
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for image moderation. 

| API | Description |
| --------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| [Moderating single image](https://intl.cloud.tencent.com/document/product/436/48537) |  Scans existing data stored in COS for pornographic, illegal, and advertising images. |
| [Batch moderating images](https://intl.cloud.tencent.com/document/product/436/48538) |  Moderates multiple images in batches. |
| [Querying the image moderation job result](https://intl.cloud.tencent.com/document/product/436/48539) | Queries the result of the specified image moderation job.                                                  |

## SDK API References

For parameters and method description of all APIs in the SDK, see [SDK API Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Single Image Moderation

#### Feature description

This API (`QCloudSyncImageRecognitionRequest`) is used to submit an image moderation job. You can receive the moderation result by setting the callback address or querying by `JobId`.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request

**Objective-C**

[//]: # ".cssg-snippet-sync-image-recognition"
```objective-c
QCloudSyncImageRecognitionRequest * request = [[QCloudSyncImageRecognitionRequest alloc]init];

// Bucket name in the format of BucketName-APPID
request.bucket = @"bucket";

// File region
request.regionName = @"regionName";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = @"***.jpg";

// Moderation type, such as `porn` (pornography) and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionPorn | QCloudRecognitionTerrorist | QCloudRecognitionPolitics | QCloudRecognitionAds;
[request setFinishBlock:^(QCloudImageRecognitionResult * _Nullable result, NSError * _Nullable error) {
// `outputObject` is the moderation result. For detailed fields, see the API documentation or SDK source code.
// `QCloudImageRecognitionResult` class
}];
[[QCloudCOSXMLService defaultCOSXML] SyncImageRecognition:request];

```

> ?For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PictureOperation.m).

**Swift**

[//]: # ".cssg-snippet-sync-image-recognition"
```swift
let request : QCloudSyncImageRecognitionRequest = QCloudSyncImageRecognitionRequest();

// Bucket name in the format of BucketName-APPID
request.bucket = "bucket";

// File region
request.regionName = "regionName";

// Object key, i.e., the full path of a COS object. If the object is in a directory, the path should be "dir1/object1".
request.object = "***.jpg";

// Moderation type, such as `porn` (pornography) and `ads` (advertising).
// You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for pornographic and advertising information.
// You can use multiple parameters together, such as `QCloudRecognitionPorn | QCloudRecognitionTerrorist`.
request.detectType = QCloudRecognitionEnum(rawValue: QCloudRecognitionEnum.porn.rawValue | QCloudRecognitionEnum.ads.rawValue)!
    
request.finishBlock = { (result, error) in
        // `outputObject` is the moderation result. For detailed fields, see the API documentation or SDK source code.
    // `QCloudImageRecognitionResult` class
}
QCloudCOSXMLService.defaultCOSXML().syncImageRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PictureOperation.swift).

## Batch Image Moderation

#### Feature description

The batch image moderation API adopts a sync POST request method. You can use this API to perform content moderation on multiple image files.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request

**Objective-C**

[//]: # ".cssg-snippet-batch-image-recognition"
```objective-c

QCloudBatchimageRecognitionRequest * request = [[QCloudBatchimageRecognitionRequest alloc]init];

request.bucket = @"bucket";
// File region
request.regionName = @"regionName";

NSMutableArray * input = [NSMutableArray new];

// The image object to be moderated
QCloudBatchRecognitionImageInfo * input1 = [QCloudBatchRecognitionImageInfo new];
input1.Object = @"***.jpg";
[input addObject:input1];

QCloudBatchRecognitionImageInfo * input2 = [QCloudBatchRecognitionImageInfo new];
input2.Object = @"***.jpg";
[input addObject:input2];

// The array of image objects to be moderated
request.input = input;
request.detectType = QCloudRecognitionPorn | QCloudRecognitionTerrorist | QCloudRecognitionPolitics | QCloudRecognitionAds;
[request setFinishBlock:^(QCloudBatchImageRecognitionResult * _Nullable result, NSError * _Nullable error) {
// `outputObject` is the moderation result. For detailed fields, see the API documentation or SDK source code.
// `QCloudBatchImageRecognitionResult` class
}];
[[QCloudCOSXMLService defaultCOSXML] BatchImageRecognition:request];

```

> ?For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PictureOperation.m).

**Swift**

[//]: # ".cssg-snippet-batch-image-recognition"
```swift
let request = QCloudBatchimageRecognitionRequest();
request.bucket = "bucket";

// File region
request.regionName = "regionName";

// The image object to be moderated
let input1 = QCloudBatchRecognitionImageInfo();
input1.object = "***.jpg";

let input2 = QCloudBatchRecognitionImageInfo();
input2.object = "***.jpg";

// The array of image objects to be moderated
request.input = [input1,input2];
request.detectType = QCloudRecognitionEnum(rawValue: QCloudRecognitionEnum.porn.rawValue | QCloudRecognitionEnum.ads.rawValue)!
request.setFinish { outputObject, error in
// `outputObject` is the moderation result. For detailed fields, see the API documentation or SDK source code.
// `QCloudBatchImageRecognitionResult` class
}
QCloudCOSXMLService.defaultCOSXML().batchImageRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PictureOperation.swift).

## Querying Image Moderation Job Result

#### Feature description

This API (`QCloudGetImageRecognitionRequest`) is used to query the result of the specified sync or batch image moderation job by `JobId`.

> ! The COS iOS SDK version must be at least v6.0.9.

#### Sample request

**Objective-C**

[//]: # ".cssg-snippet-get-image-recognition"
```objective-c
QCloudGetImageRecognitionRequest * request = [[QCloudGetImageRecognitionRequest alloc]init];

// Bucket name in the format of BucketName-APPID
request.bucket = @"examplebucket-1250000000";

// File region
request.regionName = @"regionName";

// The `jobid` of the sync or batch moderation job
request.jobId = @"jobid";

request.finishBlock = ^(QCloudImageRecognitionResult * outputObject, NSError *error) {
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudImageRecognitionResult` class
};
[[QCloudCOSXMLService defaultCOSXML] GetImageRecognition:request];
```

> ?For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/PictureOperation.m).

**Swift**

[//]: # ".cssg-snippet-get-image-recognition"
```swift
let request = QCloudGetImageRecognitionRequest();

// Bucket name in the format of BucketName-APPID
request.bucket = "examplebucket-1250000000";

request.regionName = "regionName";

// The `jobid` of the sync or batch moderation job
request.jobId = "jobid";

request.setFinish { outputObject, error in
    // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
    // `QCloudWebRecognitionResult` class
};
QCloudCOSXMLService.defaultCOSXML().getImageRecognition(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/PictureOperation.swift).
