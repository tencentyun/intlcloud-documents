## Overview

This document provides an overview of APIs and SDK code samples for file moderation.
>! The COS Mini Program SDK version must be at least v1.1.1.
>

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
|[Submitting file moderation job](https://intl.cloud.tencent.com/document/product/436/48258) | Submits file moderation job.   |
|[Querying file moderation job result](https://intl.cloud.tencent.com/document/product/436/48259)  | Queries the result of specified file moderation job. |


## Submitting File Moderation Job

#### Feature description

This API is used to submit a file moderation job.

#### Sample request

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket (required) */
  Region: 'COS_REGION', /* Bucket region (required) */
};
function postDocumentAuditing() {
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com';
  var url = 'https://' + host + '/document/auditing';
  var body = COS.util.json2xml({
    Request: {
      Input: {
        Object: 'test.xlsx', /* Path of the file to be moderated in the bucket */
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
      Key: '/document/auditing', /** Fixed value (required) */
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
| Url                | Request.Input | Full URL of the file, such as `http://www.example.com/doctest.doc`.             | String | Yes       |
| Type | Request.Input | File type. If this parameter is not specified, the file extension will be used as the type by default, such as DOC, DOCX, PPT, and PPTX. <br>If the file has no extension, this field must be specified; otherwise, moderation will fail. | String | No |

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :------- |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by commas, such as `Porn,Ads`. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |
| BizType            | Request.Conf | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console as instructed in Setting Moderation Policy. | String | No |


#### Response description

For more information, see [Submitting File Moderation Job](https://intl.cloud.tencent.com/document/product/436/48258).



## Querying File Moderation Job

#### Feature description
This API is used to query the status and result of a file moderation job.

#### Sample request

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket (required) */
  Region: 'COS_REGION', /* Bucket region (required) */
};
function getDocumentAuditingResult() {
  var jobId = 'sd7815c21caff611eca12f525400d88xxx'; // `jobId`, which is returned after a file moderation job is submitted.
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com';
  var url = 'https://' + host + '/document/auditing/' + jobId;
  cos.request({
      Bucket: config.Bucket,
      Region: config.Region,
      Method: 'GET',
      Key: '/document/auditing/' + jobId,
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

For more information, see [Querying File Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48259).
