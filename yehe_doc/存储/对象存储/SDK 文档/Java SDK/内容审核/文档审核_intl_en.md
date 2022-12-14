## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for file moderation.

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
| [Submitting file moderation job](https://www.tencentcloud.com/document/product/1045/52121) | Submits file moderation job.   |
| [Querying file moderation job result](https://intl.cloud.tencent.com/document/product/1045/52122)  | Queries the result of specified file moderation job. |


## Submitting File Moderation Job

#### Feature description

This API is used to submit a file moderation job.

#### Method prototype

```java
DocumentAuditingResponse createAuditingDocumentJobs(DocumentAuditingRequest request);
```

#### Sample request

```java
//1. Create a job request object
DocumentAuditingRequest request = new DocumentAuditingRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
//2.1.1 Set the object address
// request.getInput().setObject("1.txt");
//2.1.2 Or, directly set the file address
request.getInput().setUrl("https://markjrzhang-1251704708.cos.ap-chongqing.myqcloud.com/%E9%97%AE%E9%A2%98%E6%B1%87%E6%80%BB.pptx");
//2.2 Set the moderation type parameter
request.getConf().setDetectType("all");
//3. Call the API to get the job response object
DocumentAuditingResponse response = client.createAuditingDocumentJobs(request);
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
| BizType            | Request.Conf | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console. For more information, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |


#### Response description

- Success: The `DocumentAuditingResponse` file moderation job result object is returned upon success.
- Failure: An error (such as the bucket does not exist) occurs, reporting the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).



## Querying File Moderation Job

#### Feature description
This API is used to query the status and result of a file moderation job.

#### Method prototype

```java
DocumentAuditingResponse describeAuditingJob(DocumentAuditingRequest request);
```

#### Sample request

```java
//1. Create a job request object
DocumentAuditingRequest request = new DocumentAuditingRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.setJobId("sdd5d1cc630fdc11ecb3fa5254009******");
//3. Call the API to get the job response object
DocumentAuditingResponse response = client.describeAuditingDocumentJob(request);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |-----|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| jobId | ID of the job to be queried. | String | Yes |

#### Response description

- Success: The `DocumentAuditingResponse` moderation job result object is returned.
- Failure: If an error (such as authentication failure) occurs, the `CosClientException` or `CosServiceException` exception will be reported. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
