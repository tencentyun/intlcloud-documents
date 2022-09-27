

## Overview

This document provides an overview of APIs and SDK code samples for querying and updating speech recognition queues.

| API | Description |
| ------------------------------------------------------------ | ----------------------------------------- |
| Querying a speech recognition queue | Queries a speech recognition queue. |
| Updating a speech recognition queue | Updates a speech recognition queue. |

## SDK API References

For the parameters and method description of all the APIs in the SDK, see [QCloudCOSXML SDK for iOS v5.7.4 Reference](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com/).

## Querying Speech Recognition Queue

#### Feature description

This API is used to query a speech recognition queue.

>! The COS iOS SDK version must be at least v6.1.3.
>

#### Sample code

**Objective-C**

[//]: # ".cssg-snippet-get-audiodiscern-taskqueue"
```objective-c
    QCloudGetAudioDiscernTaskQueueRequest * request = [[QCloudGetAudioDiscernTaskQueueRequest alloc]init];

    // Bucket name in the format of `BucketName-APPID`
    request.bucket = @"examplebucket-1250000000";

    request.regionName = @"regionName";
    // Queue ID. If you enter multiple IDs, separate them by comma.
    request.queueIds = @"1,2,3";

    // 1. Active: Jobs in the queue will be scheduled and executed by the speech recognition service.
    // 2. Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will continue without being affected.
    request.state = 1;

    request.finishBlock = ^(QCloudAudioAsrqueueResult * outputObject, NSError *error) {
        // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
        // `QCloudAudioAsrqueueResult` class
    };
    [[QCloudCOSXMLService defaultCOSXML] GetAudioDiscernTaskQueue:request];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/AudioDiscernTaskQueue.m).
>

**Swift**

[//]: # ".cssg-snippet-get-audiodiscern-taskqueue"
```swift
    let  request = QCloudGetAudioDiscernTaskQueueRequest.init();

    // Bucket name in the format of `BucketName-APPID`
    request.bucket = "examplebucket-1250000000";

    request.regionName = "regionName";
    // Queue ID. If you enter multiple IDs, separate them by comma.
    request.queueIds = "1,2,3";

    // 1. Active: Jobs in the queue will be scheduled and executed by the speech recognition service.
    // 2. Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will continue without being affected.
    request.state = 1;

    request.setFinish { outputObject, error in
        // The moderation result `outputObject` contains the job ID used for query. For detailed fields, see the API documentation or SDK source code.
        // `QCloudAudioAsrqueueResult` class
    };
    QCloudCOSXMLService.defaultCOSXML().getAudioDiscernTaskQueue(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/AudioDiscernTaskQueue.swift).
>

## Updating Speech Recognition Queue

#### Feature description

This API is used to update a speech recognition queue.

>! The COS iOS SDK version must be at least v6.1.3.
>

#### Sample code

**Objective-C**

[//]: # ".cssg-snippet-update-audiodiscern-taskqueue"
```objective-c
QCloudUpdateAudioDiscernTaskQueueRequest * request = [[QCloudUpdateAudioDiscernTaskQueueRequest alloc]init];

// Bucket name in the format of `BucketName-APPID`
request.bucket = @"examplebucket-1250000000";

request.regionName = @"regionName";
// Template name
request.name = @"name";
// 1. Active: Jobs in the queue will be scheduled and executed by the speech recognition service.
// 2. Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will continue without being affected.
request.state = 1;
// Queue ID
request.queueID = @"queueID";

// For other parameters, see the SDK documentation or source code comments.

request.finishBlock = ^(QCloudAudioAsrqueueUpdateResult * outputObject, NSError *error) {
    // `outputObject`. For detailed fields, see the API documentation or SDK source code.
    // `QCloudAudioAsrqueueUpdateResult` class
};
[[QCloudCOSXMLService defaultCOSXML] UpdateAudioDiscernTaskQueue:request];
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/AudioDiscernTaskQueue.m).
>

**Swift**

[//]: # ".cssg-snippet-update-audiodiscern-taskqueue"
```swift
let request = QCloudUpdateAudioDiscernTaskQueueRequest.init();

// Bucket name in the format of `BucketName-APPID`
request.bucket = "examplebucket-1250000000";

request.regionName = "regionName";
// Template name
request.name = "name";
// 1. Active: Jobs in the queue will be scheduled and executed by the speech recognition service.
// 2. Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will continue without being affected.
request.state = 1;
// Queue ID
request.queueID = "queueID";

// For other parameters, see the SDK documentation or source code comments.

request.setFinish { outputObject, error in
    // `outputObject`. For detailed fields, see the API documentation or SDK source code.
    // `QCloudAudioAsrqueueUpdateResult` class
};
QCloudCOSXMLService.defaultCOSXML().updateAudioDiscernTaskQueue(request);
```

>? For more complete samples, visit [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/AudioDiscernTaskQueue.swift).
>
