## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for video moderation.
>! The COS Node.js SDK version must be at least v2.11.2.
>

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
|[Submitting video moderation job](https://intl.cloud.tencent.com/document/product/436/48249) | Submits video moderation job.   |
|[Querying video moderation job result](https://intl.cloud.tencent.com/document/product/436/48250)  | Queries the result of specified video moderation job. |


## Submitting Video Moderation Job

#### Feature description

This API is used to submit a video moderation job.

#### Sample request

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket (required) */
  Region: 'COS_REGION', /* Bucket region (required) */
};
function postVideoAuditing() {
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com';
  var url = 'https://' + host + '/video/auditing';
  var body = COS.util.json2xml({
    Request: {
      Input: {
        Object: '1.mp4', /* Path of the video file to be moderated in the bucket */
      },
      Conf: {
        BizType: '',
        DetectType: 'Porn',
        Snapshot: {
          Count: 1000, // Number of frames captured
        },
        DetectContent: 1, // Whether to moderate the video sound. Valid values: `0` (moderates video image only); `1` (moderates both video image and sound)
      }
    }
  });
  cos.request({
      Bucket: config.Bucket,
      Region: config.Region,
      Method: 'POST',
      Url: url,
      Key: '/video/auditing', /** Fixed value (required) */
      ContentType: 'application/xml', /** Fixed value (required) */
      Body: body
  },
  function(err, data){
      console.log(err || data);
  });
}
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
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. | String | No |
| Snapshot           | Request.Conf | Video image moderation is implemented by taking a certain number of screenshots based on the video frame capturing capability and then moderating the screenshots one by one. This parameter is used to specify the configuration of video frame capturing. | Container | Yes |
| Callback           | Request.Conf | Callback address, which must start with `http://` or `https://`.              | String    | No       |
| CallbackVersion | Request.Conf | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | String | No |
| BizType            | Request.Conf | Moderation policy. If this parameter is not specified, the default policy will be used.                       | String    | No       |
| DetectContent | Request.Conf | Whether to moderate video sound. Valid values: `0` (moderates the video image only), `1` (moderates both the video image and video sound). Default value: `0`. | Integer | No |

`Snapshot` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :-------------------- | ------------------------------------------------------------ | --------- | -------- |
| Mode               | Request.Conf.Snapshot | Frame capturing mode. Valid values: `Interval` (interval mode), `Average` (average mode), `Fps` (fixed frame rate mode). <ul  style="margin: 0;"><li>`Interval` mode: The `TimeInterval` and `Count` parameters take effect. If `Count` is set but `TimeInterval` is not, all frames will be captured to generate a total of `Count` images. </li><li>`Average` mode: The `Count` parameter takes effect, indicating to capture a total of `Count` images at an average interval in the entire video. </li><li>`Fps` mode: `TimeInterval` indicates how many frames to capture per second, and `Count` indicates how many frames to capture in total.</li></ul> | String | No |
| Count              | Request.Conf.Snapshot | The number of captured frames. Value range: (0, 10000]. | String | No       |
| TimeInterval       | Request.Conf.Snapshot | Video frame capturing frequency. Value range: (0.000, 60.000] seconds. The value supports the float format, accurate to the millisecond. | Float  | No |

#### Response description

For more information, see [Submitting Video Moderation Job](https://intl.cloud.tencent.com/document/product/436/48249#.E5.93.8D.E5.BA.94).

## Querying Video Moderation Job Result

#### Feature description

This API is used to query the status and result of a video moderation job.

#### Sample request

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket (required) */
  Region: 'COS_REGION', /* Bucket region (required) */
};
function getVideoAuditingResult() {
  var jobId = 'av14d9ca15af3a11eca0d6525400d88xxx'; // `jobId`, which is returned after a video moderation job is submitted.
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com';
  var url = 'https://' + host + '/video/auditing/' + jobId;
  cos.request({
      Bucket: config.Bucket,
      Region: config.Region,
      Method: 'GET',
      Key: '/video/auditing/' + jobId,
      Url: url,
  },
  function(err, data){
      console.log(err || data);
  });
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |-----|
| jobId | ID of the job to be queried. | String | Yes |

#### Response description

For more information, see [Querying Video Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48250#.E5.93.8D.E5.BA.94).
