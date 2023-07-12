## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for webpage moderation.
>! The COS Mini Program SDK version should be or later than v1.1.1.
>

| API | Description    |
| :----------------------------------------------------------- | :------------------------- |
|[Submitting webpage moderation job](https://intl.cloud.tencent.com/document/product/436/48282)  | Submits a webpage moderation job.   |
|[Querying webpage moderation job result](https://intl.cloud.tencent.com/document/product/436/48283)  | Queries the result of a specified webpage moderation job. |


## Submitting a Webpage Moderation Job

#### Feature description

This API is used to submit a webpage moderation job.

#### Sample request

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket. Required */
  Region: 'COS_REGION',     /* Bucket region. Required */
};
function postWebpageAuditing() {
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com';
  var url = 'https://' + host + '/webpage/auditing';
  var body = COS.util.json2xml({
    Request: {
      Input: {
        Url: 'https://cloud.tencent.com/', // The resource stored in COS. The moderation result is returned asynchronously, which can be viewed by calling the API for querying webpage moderation result.
      },
      Conf: {
        BizType: '',
        DetectType: 'Porn,Ads',
      }
    }
  });
  cos.request({
      Bucket: config.Bucket,
      Region: config.Region,
      Method: 'POST',
      Url: url,
      Key: '/webpage/auditing', /** Fixed value (required) */
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
| :----------------- | :----- | :--------------------- | :-------- | :------- |
| Request | None | Webpage moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :------------------- | :-------- | :------- |
| Input              | Request | Webpage to be moderated.                   | Container | Yes       |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Url                | Request.Input | Full URL of the webpage, such as `http://www.test.com`.             | String | Yes       |
| DataId | Request.Input | This field will return the original content in the moderation result, which can contain up to 512 bytes. You can use this field to uniquely identify the data to be moderated in your business. | String | No |
| UserInfo | Request.Input | Business field. | Container | No |

`UserInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :---------------- | :--------------------- | :------------------------------------------------------ | :----- | :------- |
| TokenId           | Request.Input.UserInfo | Business `TokenId`, which can contain up to 128 bytes.                      | String | No       |
| Nickname          | Request.Input.UserInfo | Business `Nickname`, which can contain up to 128 bytes.                     | String | No       |
| DeviceId          | Request.Input.UserInfo | Business `DeviceId`, which can contain up to 128 bytes.                     | String | No       |
| AppId             | Request.Input.UserInfo | Business `AppId`, which can contain up to 128 bytes.                         | String | No       |
| Room              | Request.Input.UserInfo | Business `Room`, which can contain up to 128 bytes.                          | String | No       |
| IP                | Request.Input.UserInfo | Business `IP`, which can contain up to 128 bytes.                            | String | No       |
| Type              | Request.Input.UserInfo | Business `Type`, which can contain up to 128 bytes.                          | String | No       |


`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :------------------ | :----------- | :----------------------------------------------------------- | :------ | :------- |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. | String | Yes |
| Callback           | Request.Conf | Callback address, which must start with `http://` or `https://`.              | String    | No       |
| ReturnHighlightHtml | Request.Conf | This parameter specifies whether to highlight the non-compliant text on the webpage. When the result is queried or called back, this parameter decides whether to return the highlighted HTML content. Valid values: `true`, `false`. Default value: `false`. | Boolean | No |


#### Response description

For more information, see [Submitting Webpage Moderation Job](https://intl.cloud.tencent.com/document/product/436/48282#.E5.93.8D.E5.BA.94).



## Querying Webpage Moderation Job Result

#### Feature description
This API is used to query the status and result of a webpage moderation job.

#### Sample request

```js
var config = {
  // Replace with your own bucket information
  Bucket: 'examplebucket-1250000000', /* Bucket. Required */
  Region: 'COS_REGION',     /* Bucket region. Required */
};
function getWebpageAuditingResult() {
  var jobId = 'shce868019aff611ecb1155254009a4xxx'; // `jobId`, which is returned after a webpage moderation job is submitted.
  var host = config.Bucket + '.ci.' + config.Region + '.myqcloud.com';
  var url = 'https://' + host + '/webpage/auditing/' + jobId;
  cos.request({
      Bucket: config.Bucket,
      Region: config.Region,
      Method: 'GET',
      Key: '/webpage/auditing/' + jobId,
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

For more information, see [Querying Webpage Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48283#.E5.93.8D.E5.BA.94).
