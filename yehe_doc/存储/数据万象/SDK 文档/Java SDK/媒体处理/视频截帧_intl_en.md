
## Overview

This document provides an overview of APIs and SDK code samples related to media file screencapturing in CI.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| GenerateSnapshot | Getting a screenshot of a media file at some time point  | Gets a screenshot of a media file at some time point  |

## Basic operations

### Getting a screenshot of a media file at some time point

#### Feature description

This API is used to get a screenshot of a media file at some time point.

#### Method prototype

```java
public SnapshotResponse generateSnapshot(SnapshotRequest request);
```

#### Parameter description

| Parameter | Description | Type | Required |
| :----------------- | :----------------------------------------------------------- | :-------- | :------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String |Yes|
| Input      | Media file location information.                                           | Container | Yes       |
| Time       | Screenshot time point in seconds.                               | Float     | Yes       |
| Output     | Screenshot storage location information.                                           | Container | Yes       |
| Width      | Screenshot width. Default value: 0.                                          | Int       | No       |
| Height | Screenshot height. Default value: 0.<br/>If `Width` and `Height` are both `0`, the width and height of the video are used. <br/>If one of them is `0`, the other value is used to automatically adapt to the aspect ratio of the video. | Int | No |
| Format | Screenshot format. Valid values: jpg, png. Default value: jpg. | String | No |
| Mode | Frame capturing method.<br><li>keyframe: Capture the last keyframe before the specified time point.<br><li>exactframe: Capture the frame at a specified time point.<br/>Default value: exactframe. | String | No |
| Rotate | Image rotation method.<br><li>auto: Rotate automatically according to the video rotation information.<br><li>off: Do not rotate.<br/>Default value: auto. | String | No |

`Input` has the following sub-nodes:

| Parameter | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :--------- | :----- | :------- |
| Object             | Request.Input | Filename | String | Yes       |

`Output` has the following sub-nodes:

| Parameter | Parent Node | Description | Type | Required |
| :----------------- | :------------- | :-------------------- | :----- | :------- |
| Region             | Request.Output | Bucket region      | String | Yes       |
| Bucket             | Request.Output | File bucket | String | Yes       |
| Object             | Request.Output | Filename            | String | Yes       |

#### Response description

- Success: The screenshot entity information is returned.
- Failure: An error (such as the bucket does not exist) occurs, throwing the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
//1. Create a screenshot request object
SnapshotRequest request = new SnapshotRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.getInput().setObject("1.mp4");
request.getOutput().setBucket("examplebucket-1250000000");
request.getOutput().setRegion("ap-chongqing");
request.getOutput().setObject("test/1.jpg");
request.setTime("15");
//3. Call the API to get the screenshot response object
SnapshotResponse response = client.generateSnapshot(request);
```
