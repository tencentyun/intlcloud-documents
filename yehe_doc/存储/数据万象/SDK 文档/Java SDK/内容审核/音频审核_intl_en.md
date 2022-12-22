## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for audio moderation.

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
|[Submitting audio moderation job](https://intl.cloud.tencent.com/document/product/436/48262) | Submits audio moderation job.   |
|[Querying audio moderation job result](https://intl.cloud.tencent.com/document/product/436/48263)  | Queries the result of specified audio moderation job. |


## Submitting Audio Moderation Job

#### Feature description

This API is used to submit an audio moderation job.

#### Method prototype

```java
AudioAuditingResponse createAudioAuditingJob(AudioAuditingRequest request);
```

#### Sample request

```java
//1. Create a job request object
AudioAuditingRequest request = new AudioAuditingRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.getInput().setObject("pron.mp3");
request.getConf().setDetectType("Porn,Ads");
request.getConf().setCallback("http://cloud.tencent.com/");
//3. Call the API to get the job response object
AudioAuditingResponse response = client.createAudioAuditingJobs(request);
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
| BizType            | Request.Conf | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console. | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |
| CallbackVersion | Request.Conf | Structure of the callback content. Valid values: Simple (the callback content contains basic information), Detail (the callback content contains detailed information). Default value: Simple. | string | No |

#### Response description

- Success: The `AudioAuditingResponse` audio moderation job result object is returned upon success.
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).



## Querying Audio Moderation Job

#### Feature description
This API is used to query the status and result of an audio moderation job.

#### Method prototype

```java
AudioAuditingResponse describeAuditingJob(AudioAuditingRequest request);
```

#### Sample request

```java
//1. Create a job request object
AudioAuditingRequest request = new AudioAuditingRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.setJobId("sacbf7269cbd2e11eba5325254009*****");
//3. Call the API to get the job response object
AudioAuditingResponse response = client.describeAudioAuditingJob(request);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |-----|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| jobId | ID of the job to be queried. | String | Yes |

#### Response description

- Success: The `AudioAuditingResponse` moderation job result object is returned. For field descriptions, see [Querying Audio Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48263).
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

