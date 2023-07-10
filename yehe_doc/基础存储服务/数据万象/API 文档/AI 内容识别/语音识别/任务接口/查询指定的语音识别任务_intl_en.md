## Feature Description

This API (`DescribeSpeechJob`) is used to query a specified speech recognition job.

## Request

#### Sample request

```shell
GET /asr_jobs/<jobId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request does not have a request body.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610). 

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <JobsDetail></JobsDetail>
  <NonExistJobIds></NonExistJobIds>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| JobsDetail | Response | Job details. Same as `Response.JobsDetail` in `CreateSpeechJobs`. |  Container |
| NonExistJobIds | Response | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |
| SpeechRecognitionResult     | Response | Returned speech recognition result details when the job type is `SpeechRecognition` and the status is `success`.            | Container    |

`SpeechRecognitionResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| Result         | Response.SpeechRecognitionResult | Recognition result | Container |
| ResultDetail     | Response.SpeechRecognition.ResultDetail | Recognition result details, including the time offsets of words in each sentence (generally used to generate subtitles). This field will not be empty if `ResTextFormat` in the recognition request is `1`.<br>Note: This field may return null, indicating that no valid values can be obtained. | Array of SentenceDetail |
| AudioTime     | Response.SpeechRecognition.audioTime | Speech duration            | double    |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

