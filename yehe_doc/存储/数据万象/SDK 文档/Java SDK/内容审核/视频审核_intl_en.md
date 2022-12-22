## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for video moderation.

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
| [Submitting video moderation job](https://www.tencentcloud.com/document/product/1045/48254) | Submits video moderation job.   |
| [Querying video moderation job result](https://www.tencentcloud.com/document/product/1045/48255)  | Queries the result of specified video moderation job. |


## Submitting Video Moderation Job

#### Feature description

This API is used to submit a video moderation job.

#### Method prototype

```java
VideoAuditingResponse createVideoAuditingJob(VideoAuditingRequest request);
```

#### Sample request

```java
//1. Create a job request object
VideoAuditingRequest request = new VideoAuditingRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.getInput().setObject("1.mp4");
request.getConf().setDetectType("Porn,Ads");
request.getConf().getSnapshot().setCount("10");
request.getConf().getSnapshot().setMode("Interval");
request.getConf().getSnapshot().setTimeInterval("10");
//3. Call the API to get the job response object
VideoAuditingResponse response = client.createVideoAuditingJob(request);
```


#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ---------------- | --------- | -------- |
| Input | Request | Video to be moderated. | Container | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | ------------------------------------------------------------ | ------ | -------- |
| Object | Request.Input | Name of the video file stored in the COS bucket; for example, if the file is `video.mp4` in the `test` directory, then the filename is `test/video.mp4`. | String | Yes |
| Url | Request.Input | Full URL of the video file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/test.mp4`. Either `Object` or `Url` can be selected at a time. | String | No |

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------ | ------------------------------------------------------------ | --------- | -------- |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. | String | Yes |
| Snapshot           | Request.Conf | Video image moderation is implemented by taking a certain number of screenshots based on the video frame capturing capability and then moderating the screenshots one by one. This parameter is used to specify the configuration of video frame capturing. | Container | Yes |
| Callback           | Request.Conf | Callback address, which must start with `http://` or `https://`.              | String    | No       |
| CallbackVersion | Request.Conf | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | String | No |
| BizType            | Request.Conf | Moderation policy. If this parameter is not specified, the default policy will be used.                       | String    | No       |
| DetectContent | Request.Conf | Whether to moderate video sound. Valid values: `0` (moderates the video image only), `1` (moderates both the video image and video sound). Default value: `0`. | Integer | No |

`Snapshot` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :-------------------- | ------------------------------------------------------------ | --------- | -------- |
| Mode               | Request.Conf.Snapshot | Frame capturing mode. Valid values: `Interval` (interval mode), `Average` (average mode), `Fps` (fixed frame rate mode). </br><li>`Interval` mode: The `TimeInterval` and `Count` parameters take effect. If `Count` is set but `TimeInterval` is not, all frames will be captured to generate a total of `Count` images. </br><li>`Average` mode: The `Count` parameter takes effect, indicating to capture a total of `Count` images at an average interval in the entire video. </br><li>`Fps` mode: `TimeInterval` indicates how many frames to capture per second, and `Count` indicates how many frames to capture in total.</li> | String | No |
| Count              | Request.Conf.Snapshot | The number of captured frames. Value range: (0, 10000]. | String | No       |
| TimeInterval       | Request.Conf.Snapshot | Video frame capturing frequency. Value range: (0.000, 60.000] seconds. The value supports the float format, accurate to the millisecond. | Float  | No |

#### Response description

- Success: The `VideoAuditingResponse` media moderation job result object is returned upon success.
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).


## Querying Video Moderation Job Result

#### Feature description

This API is used to query the status and result of a video moderation job.

#### Method prototype

```java
VideoAuditingResponse describeAuditingJob(VideoAuditingRequest request);
```

#### Sample request

```java
//1. Create a job request object
VideoAuditingRequest request = new VideoAuditingRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.setJobId("av81591b4bbd2211eb80235254008*****");
//3. Call the API to get the job response object
VideoAuditingResponse response = client.describeAuditingJob(request);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |-----|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| jobId | ID of the job to be queried. | String | Yes |

#### Response description

- Success: The `VideoAuditingResponse` moderation job result object is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
