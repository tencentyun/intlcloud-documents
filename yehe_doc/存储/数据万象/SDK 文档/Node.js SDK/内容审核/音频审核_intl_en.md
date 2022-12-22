## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for audio moderation.
>! The COS Node.js SDK version must be at least v2.11.2.
>

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
|[Submitting audio moderation job](https://intl.cloud.tencent.com/document/product/436/48262) | Submits audio moderation job.   |
|[Querying audio moderation job result](https://intl.cloud.tencent.com/document/product/436/48263)  | Queries the result of specified audio moderation job. |


## Submitting Audio Moderation Job

#### Feature description

This API is used to submit an audio moderation job.

#### Sample request

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket (required) */
  Region: 'COS_REGION', /* Bucket region (required) */
};
function postAudioAuditing() {
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com';
  var url = 'https://' + host + '/audio/auditing';
  var body = COS.util.json2xml({
    Request: {
      Input: {
        Object: '1.mp3', /* Path of the audio file to be moderated in the bucket */
      },
      Conf: {
        BizType: '',
        DetectType: 'Porn',
      }
    }
  });
  cos.request({
      Bucket: config.Bucket,
      Region: config.Region,
      Method: 'POST',
      Url: url,
      Key: '/audio/auditing', /** Fixed value (required) */
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
| :----------------- | :------ | :------------- | :-------- | :------- |
| Input | Request | Content to be moderated. | Container | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Object | Request.Input | Name of the audio file stored in the COS bucket; for example, if the file is `audio.mp3` in the `test` directory, then the filename is `test/audio.mp3`. Either `Object` or `Url` can be selected at a time. | String | No |
| Url | Request.Input | Full URL of the audio file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/audio.mp3`. Either `Object` or `Url` can be selected at a time. | String | No |

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :------- |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography), `Ads` (advertising), `Illegal` (illegal), and `Abuse` (abusive). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |
| CallbackVersion | Request.Conf | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | string | No |
| BizType            | Request.Conf | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console. For more information, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). | String | No |

#### Response description

For more information, see [Submitting Audio Moderation Job](https://intl.cloud.tencent.com/document/product/436/48262#.E5.93.8D.E5.BA.94).


## Querying Audio Moderation Job

#### Feature description
This API is used to query the status and result of an audio moderation job.

#### Sample request

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket (required) */
  Region: 'COS_REGION', /* Bucket region (required) */
};
function getAudioAuditingResult() {
  var jobId = 'sa0c28d41daff411ecb23352540078cxxx'; // `jobId`, which is returned after an audio moderation job is submitted.
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com';
  var url = 'https://' + host + '/audio/auditing/' + jobId;
  cos.request({
      Bucket: config.Bucket,
      Region: config.Region,
      Method: 'GET',
      Key: '/audio/auditing/' + jobId,
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

For more information, see [Querying Audio Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48263#.E5.93.8D.E5.BA.94).

