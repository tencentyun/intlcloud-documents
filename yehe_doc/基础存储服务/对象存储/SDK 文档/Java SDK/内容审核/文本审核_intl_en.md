## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for text moderation.

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
| [Submitting text moderation job](https://intl.cloud.tencent.com/document/product/1045/48477)  | Submits text moderation job.   |
| [Querying text moderation job result](https://intl.cloud.tencent.com/document/product/1045/48478)  | Queries the result of specified text moderation job. |


## Submitting Text Moderation Job

#### Feature description

This API is used to submit a text moderation job.

#### Method prototype

```java
TextAuditingResponse createAuditingTextJobs(TextAuditingRequest request);
```

#### Sample request

```java
//1. Create a job request object
TextAuditingRequest request = new TextAuditingRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-12500000008");
//2.1.1 Set the object address
//request.getInput().setObject("1.txt");
//2.1.2 Or, directly set the request content, i.e., Base64-encoded text content
request.getInput().setContent("Base64Str");
//2.2 Set the moderation type parameter
request.getConf().setDetectType("all");
//2.3 Set the moderation template (optional)
//request.getConf().setBizType("aa3e9d84a6a079556b0109a935c*****");
//3. Call the API to get the job response object
TextAuditingResponse response = client.createAuditingTextJobs(request);
```


#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------- | :-------- | :--- |
| Request | None | Text moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :--------------- | :-------- | :--- |
| Input | Request | Content to be moderated. | Container | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Object | Request.Input | Name of the text file stored in the current COS bucket; for example, if the file is `test.txt` in the `test` directory, then the filename is `test/test.txt`. Only text files in UTF-8 and GBK encodings are supported, and the file size cannot exceed 1 MB. | String | No |
| Content | Request.Input | When the input content is plain text, it needs to be Base64-encoded first. The length of the original text before encoding cannot exceed 10,000 UTF-8 characters. If the length limit is exceeded, the API will report an error. | String | No |

>!
> - `Object` and `Content` cannot be entered at the same time.
> - If `Object` is selected, the moderation result will be returned asynchronously, which can be obtained through the API for [querying text moderation job result](https://intl.cloud.tencent.com/document/product/1045/48478).
> - If `Content` is selected, the moderation result will be returned synchronously, which can be viewed in the [response body](#1).
>- Currently, only Chinese, English, and Arabic numerals can be detected and moderated.
> 

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :--- |
| BizType            | Request.Conf | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console. For more information, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/1045/52107). | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography), `Ads` (advertising), `Illegal` (illegal), and `Abuse` (abusive). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |

#### Response description

- Success: The `TextAuditingResponse` text moderation job result object is returned upon success.
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).



## Querying Text Moderation Job

#### Feature description
This API is used to query the status and result of a text moderation job.

#### Method prototype

```java
TextAuditingResponse describeAuditingTextJob(TextAuditingRequest request);
```

#### Sample request

```java
//1. Create a job request object
TextAuditingRequest request = new TextAuditingRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.setJobId("st68d08596f35011eb9324525400*****");
//3. Call the API to get the job response object
TextAuditingResponse response = client.describeAuditingTextJob(request);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |-----|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| jobId | ID of the job to be queried. | String | Yes |

#### Response description

- Success: The `TextAuditingResponse` moderation job result object is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
