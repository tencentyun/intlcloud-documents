## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for webpage moderation.

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
| [Submitting webpage moderation job](https://intl.cloud.tencent.com/document/product/436/48282)  | Submits webpage moderation job.   |
| [Querying webpage moderation job result](https://intl.cloud.tencent.com/document/product/436/48283)  | Queries the result of specified webpage moderation job. |


## Submitting Webpage Moderation Job

#### Feature description

This API is used to submit a webpage moderation job.

#### Method prototype

```cpp
CosResult CosAPI::CreateWebPageAuditingJob(const CreateWebPageAuditingJobReq& req, CreateWebPageAuditingJobResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
std::string url = "http://test.com";

CreateWebPageAuditingJobReq req(bucket_name);
CreateWebPageAuditingJobResp resp;

// Add request parameters as detailed in the API documentation
req.SetUrl(url);
req.SetDetectType("Porn,Ads");

// Call the API to get the job response object
CosResult result = cos.CreateWebPageAuditingJob(req, &resp);
if (result.IsSucc()) {
	// If the moderation job is created successfully, you can call the member functions of `CreateWebPageAuditingJobResp`.
} else {
	// If the moderation job failed to be created, you can call the member functions of `CosResult` to output the error message.
}
```


#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ----------------- | -------- |
| req  | `CreateWebPageAuditing` operation request | CreateWebPageAuditingJobReq | Yes       |
| resp | `CreateWebPageAuditing` operation response | CreateWebPageAuditingJobResp | Yes       |

`CreateWebPageAuditingJobReq` provides the following member functions:

```cpp
// Set the bucket for performing the operation
void SetBucketName(const std::string& bucket_name);
// Set the input video to be moderated
void SetInput(const AuditingInput& input);
// Set moderation configuration rules
void SetConf(const Conf& conf);

// conf
// The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`.
void SetDetectType(const std::string& detect_type);
// Callback address, which must start with `http://` or `https://`.
void SetCallBack(const std::string& callback);
// Specify whether to highlight the non-compliant text on the webpage. When the result is queried or called back, this parameter decides whether to return the highlighted HTML content. Valid values: `true`, `false`. Default value: `false`.
void SetReturnHighligthHtml(const bool return_highlight_html);


// input
// Full URL of the webpage, such as `http://www.test.com`.
void SetUrl(const std::string& url);
// This field will return the original content in the moderation result, which can contain up to 512 bytes. You can use this field to uniquely identify the data to be moderated in your business.
void SetDataId(const std::string& data_id);
// Business field.
void SetUserInfo(const UserInfo& user_info);
```

`CreateWebPageAuditingJobResp` provides the following member functions:

```cpp
// Get the job details returned by the API request
WebPageAuditingJobsDetail GetJobsDetail();
// Get the `RequestId` returned by the API
std::string GetRequestId();

```

#### Response description

- Success: The moderation job result in the XML content returned by the API will be parsed into the `WebPageAuditingJobsDetail` structure. For specific response parameters, see [Submitting Webpage Moderation Job](https://intl.cloud.tencent.com/document/product/436/48282).
- Failure: If an error (for example, the bucket does not exist) occurs, the error message will be parsed into the `CosResult` structure. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31525).


## Querying Webpage Moderation Job Result

#### Feature description

This API is used to query the status and result of a webpage moderation job.

#### Method prototype

```cpp
CosResult DescribeWebPageAuditingJob(const DescribeWebPageAuditingJobReq& req, DescribeWebPageAuditingJobResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

DescribeWebPageAuditingJobReq req(bucket_name);
DescribeWebPageAuditingJobResp resp;

// Add request parameters as detailed in the API documentation
req.SetJobId("aab1ca9fc8a3ed11ea834c525400863904");

// Call the API to get the job response object
CosResult result = cos.DescribeWebPageAuditingJob(req, &resp);
if (result.IsSucc()) {
	// If the moderation job is queried successfully, you can call the member functions of `DescribeWebPageAuditingJobResp`.
} else {
	// If the moderation job failed to be queried, you can call the member functions of `CosResult` to output the error message.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ----------------- | -------- |
| req  | `DescribeWebPageAuditingJob` operation request | DescribeWebPageAuditingJobReq | Yes       |
| resp | `DescribeWebPageAuditingJob` operation response | DescribeWebPageAuditingJobResp | Yes       |

`DescribeWebPageAuditingJobReq` provides the following member functions:

```cpp
// Set the bucket for performing the operation
void SetBucketName(const std::string& bucket_name);
// Set the ID of the moderation job to be queried
void SetJobId(const std::string& job_id);
```

`DescribeWebPageAuditingJobResp` provides the following member functions:

```cpp
// Get the job details returned by the API request
WebPageAuditingJobsDetail GetJobsDetail();
// Get the `RequestId` returned by the API
std::string GetRequestId();

```

#### Response description

- Success: The moderation job result in the XML content returned by the API will be parsed into the `WebPageAuditingJobsDetail` structure. For specific response parameters, see [Querying Webpage Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48283).
- Failure: If an error (for example, the bucket does not exist) occurs, the error message will be parsed into the `CosResult` structure. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
