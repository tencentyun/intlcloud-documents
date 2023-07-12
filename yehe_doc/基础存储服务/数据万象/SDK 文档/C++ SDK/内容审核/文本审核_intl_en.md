## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for text moderation.

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
| [Submitting text moderation job](https://intl.cloud.tencent.com/document/product/436/48188)  | Submits text moderation job.   |
| [Querying text moderation job result](https://intl.cloud.tencent.com/document/product/436/48189)  | Queries the result of specified text moderation job. |


## Submitting Text Moderation Job

#### Feature description

This API is used to submit a text moderation job.

#### Method prototype

```cpp
CosResult CosAPI::CreateTextAuditingJob(const CreateTextAuditingJobReq& req, CreateTextAuditingJobResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test.txt";

CreateTextAuditingJobReq req(bucket_name);
CreateTextAuditingJobResp resp;

// Add request parameters as detailed in the API documentation
req.SetObject(object_name);
req.SetBizType("b81d45f94b91a683255e9a9506f45a11");
// req.SetDetectType("Porn,Ads");

// Call the API to get the job response object
CosResult result = cos.CreateTextAuditingJob(req, &resp);
if (result.IsSucc()) {
	// If the moderation job is created successfully, you can call the member functions of `CreateTextAuditingJobResp`.
} else {
	// If the moderation job failed to be created, you can call the member functions of `CosResult` to output the error message.
}
```


#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ----------------- | -------- |
| req  | `CreateTextAuditing` operation request | CreateTextAuditingJobReq | Yes       |
| resp | `CreateTextAuditing` operation response | CreateTextAuditingJobResp | Yes       |

`CreateTextAuditingJobReq` provides the following member functions:

```cpp
// Set the bucket for performing the operation
void SetBucketName(const std::string& bucket_name);
// Set the input video to be moderated
void SetInput(const AuditingInput& input);
// Set moderation configuration rules
void SetConf(const Conf& conf);

// conf
// Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as porn, adverting, and illegal information. For configuration guides, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095).
// You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy.
void SetBizType(const std::string& biz_type);
// The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter.
void SetDetectType(const std::string& detect_type);
// Callback address, which must start with `http://` or `https://`.
void SetCallBack(const std::string& callback);
// Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`.
void SetCallBackVersion(const std::string& callback_version);


// input
// Name of the text file stored in the current COS bucket; for example, if the file is `test.txt` in the `test` directory, then the filename is `test/test.txt`. Only text files in UTF-8 and GBK encodings are supported, and the file size cannot exceed 1 MB.
void SetObject(const std::string& object);
// Full URL of the text file, such as `https://www.test.com/test.txt`.
void SetUrl(const std::string& url);
// This field will return the original content in the moderation result, which can contain up to 512 bytes. You can use this field to uniquely identify the data to be moderated in your business.
void SetDataId(const std::string& data_id);
// Business field.
void SetUserInfo(const UserInfo& user_info);
// When the input content is plain text, it needs to be Base64-encoded first. The length of the original text before encoding cannot exceed 10,000 UTF-8 characters. If the length limit is exceeded, the API will report an error.
void SetContent(const std::string& content) { m_input.SetContent(content); }

```

`CreateTextAuditingJobResp` provides the following member functions:

```cpp
// Get the job details returned by the API request
TextAuditingJobsDetail GetJobsDetail();
// Get the `RequestId` returned by the API
std::string GetRequestId();

```

#### Response description

- Success: The moderation job result in the XML content returned by the API will be parsed into the `TextAuditingJobsDetail` structure. For specific response parameters, see [Submitting Text Moderation Job](https://intl.cloud.tencent.com/document/product/436/48188).
- Failure: If an error (for example, the bucket does not exist) occurs, the error message will be parsed into the `CosResult` structure. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31525).


## Querying Text Moderation Job Result

#### Feature description

This API is used to query the status and result of a text moderation job.

#### Method prototype

```cpp
CosResult DescribeTextAuditingJob(const DescribeTextAuditingJobReq& req, DescribeTextAuditingJobResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

DescribeTextAuditingJobReq req(bucket_name);
DescribeTextAuditingJobResp resp;

// Add request parameters as detailed in the API documentation
req.SetJobId("aab1ca9fc8a3ed11ea834c525400863904");

// Call the API to get the job response object
CosResult result = cos.DescribeTextAuditingJob(req, &resp);
if (result.IsSucc()) {
	// If the moderation job is queried successfully, you can call the member functions of `DescribeTextAuditingJobResp`.
} else {
	// If the moderation job failed to be queried, you can call the member functions of `CosResult` to output the error message.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ----------------- | -------- |
| req  | `DescribeTextAuditingJob` operation request | DescribeTextAuditingJobReq | Yes       |
| resp | `DescribeTextAuditingJob` operation response | DescribeTextAuditingJobResp | Yes       |

`DescribeTextAuditingJobReq` provides the following member functions:

```cpp
// Set the bucket for performing the operation
void SetBucketName(const std::string& bucket_name);
// Set the ID of the moderation job to be queried
void SetJobId(const std::string& job_id);
```

`DescribeTextAuditingJobResp` provides the following member functions:

```cpp
// Get the job details returned by the API request
TextAuditingJobsDetail GetJobsDetail();
// Get the `RequestId` returned by the API
std::string GetRequestId();

```

#### Response description

- Success: The moderation job result in the XML content returned by the API will be parsed into the `TextAuditingJobsDetail` structure. For specific response parameters, see [Querying Text Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48189).
- Failure: If an error (for example, the bucket does not exist) occurs, the error message will be parsed into the `CosResult` structure. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
