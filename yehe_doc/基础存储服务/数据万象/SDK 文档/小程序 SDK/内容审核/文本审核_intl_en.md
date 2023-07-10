## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for text moderation.
>! The COS Mini Program SDK version should be or later than v1.1.1.
>

| API | Description    |
| :----------------------------------------------------------- | :------------------------- |
|[Submitting text moderation job](https://intl.cloud.tencent.com/document/product/436/48188)  | Submits a text moderation job.   |
|[Querying text moderation job result](https://intl.cloud.tencent.com/document/product/436/48189)  | Queries the result of a specified text moderation job. |


## Submitting a Text Moderation Job

#### Feature description

This API is used to submit a text moderation job.

#### Sample request

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket. Required */
  Region: 'COS_REGION',     /* Bucket region. Required */
};
function postTextAuditing() {
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com';
  var url = 'https://' + host + '/text/auditing';
  var body = COS.util.json2xml({
    Request: {
      Input: {
        Object: 'hello.txt', /* Path of the text file to be moderated in the bucket */
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
      Key: '/text/auditing', /** Fixed value (required) */
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
| :----------------- | :----- | :------------- | :-------- | :--- |
| Request | None | Text moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :--------------- | :-------- | :--- |
| Input              | Request | Content to be moderated.                   | Container | Yes       |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Object | Request.Input | Name of the text file stored in the current COS bucket; for example, if the file is `img.jpg` in the `test` directory, then the filename is `test/img.jpg`. Only text files in UTF-8 and GBK encodings are supported, and the file size cannot exceed 1 MB. | String | No |
| Content | Request.Input | When the input content is plain text, it needs to be Base64-encoded first. The length of the original text before encoding cannot exceed 10,000 UTF-8 characters. If the length limit is exceeded, the API will report an error. | String | No |

>!
> - `Object` and `Content` cannot be entered at the same time.
> - If `Object` is selected, the moderation result will be returned asynchronously, which can be obtained through the API for [Querying Text Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48189).
> - If `Content` is selected, the moderation result will be returned synchronously, which can be viewed in the `TextAuditingResponse` response body.
>- Currently, only Chinese, English, and Arabic numerals can be detected and moderated.
> 

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :--- |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography), `Ads` (advertising), `Illegal` (illegal), and `Abuse` (abusive). You can pass in multiple types and separate them by commas, such as `Porn,Ads`. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |
| BizType            | Request.Conf | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console. For more information, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). | String | No |

#### Response description

For more information, see [Submitting Text Moderation Job](https://intl.cloud.tencent.com/document/product/436/48188#.E5.93.8D.E5.BA.94).


## Querying Text Moderation Job

#### Feature description
This API is used to query the status and result of a text moderation job.

#### Sample request

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket. Required */
  Region: 'COS_REGION',     /* Bucket region. Required */
};
function getTextAuditingResult() {
  var jobId = 'st8d88c664aff511ecb23352540078cxxx'; // `jobId`, which is returned after a text moderation job is submitted (with `Object` passed in to `Input`).
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com';
  var url = 'https://' + host + '/text/auditing/' + jobId;
  cos.request({
      Bucket: config.Bucket,
      Region: config.Region,
      Method: 'GET',
      Key: '/text/auditing/' + jobId,
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

For more information, see [Querying Text Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48189#.E5.93.8D.E5.BA.94).
