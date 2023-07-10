## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for file moderation.

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
| [Submitting file moderation job](https://intl.cloud.tencent.com/document/product/436/48258) | Submits file moderation job.   |
| [Querying file moderation job result](https://intl.cloud.tencent.com/document/product/436/48259)  | Queries the result of specified file moderation job. |


## Submitting File Moderation Job

#### Feature description

This API is used to submit a file moderation job.

#### Method prototype

```cpp
CosResult CosAPI::CreateDocumentAuditingJob(const CreateDocumentAuditingJobReq& req, CreateDocumentAuditingJobResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test.docx";

CreateDocumentAuditingJobReq req(bucket_name);
CreateDocumentAuditingJobResp resp;

// Add request parameters as detailed in the API documentation
req.SetObject(object_name);
req.SetType("docx");
req.SetBizType("b81d45f94b91a683255e9a9506f45a11");
// req.SetDetectType("Porn,Ads");

// Call the API to get the job response object
CosResult result = cos.CreateDocumentAuditingJob(req, &resp);
if (result.IsSucc()) {
	// If the moderation job is created successfully, you can call the member functions of `CreateDocumentAuditingJobResp`.
} else {
	// If the moderation job failed to be created, you can call the member functions of `CosResult` to output the error message.
}
```


#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ----------------- | -------- |
| req  | `CreateDocumentAuditing` operation request | CreateDocumentAuditingJobReq | Yes       |
| resp | `CreateDocumentAuditing` operation response | CreateDocumentAuditingJobResp | Yes       |

`CreateDocumentAuditingJobReq` provides the following member functions:

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



// input
// Name of the file stored in the COS bucket; for example, if the file is `test.doc` in the `test` directory, then the filename is `test/test.doc`. Either `Object` or `Url` can be selected at a time.
void SetObject(const std::string& object);
// Full URL of the file, such as `http://www.example.com/doctest.doc`. Either `Object` or `Url` can be selected at a time.
void SetUrl(const std::string& url);
// This field will return the original content in the moderation result, which can contain up to 512 bytes. You can use this field to uniquely identify the data to be moderated in your business.
void SetDataId(const std::string& data_id);
// Business field.
void SetUserInfo(const UserInfo& user_info);
// File type. If this parameter is not specified, the file extension will be used as the type by default.
void SetType(const std::string& type);

```

`CreateDocumentAuditingJobResp` provides the following member functions:

```cpp
// Get the job details returned by the API request
DocumentAuditingJobsDetail GetJobsDetail();
// Get the `RequestId` returned by the API
std::string GetRequestId();

```

#### Response description

- Success: The moderation job result in the XML content returned by the API will be parsed into the `DocumentAuditingJobsDetail` structure. For specific response parameters, see [Submitting File Moderation Job](https://intl.cloud.tencent.com/document/product/436/48258).
- Failure: If an error (for example, the bucket does not exist) occurs, the error message will be parsed into the `CosResult` structure. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31525).


## Querying File Moderation Job Result

#### Feature description

This API is used to query the status and result of a file moderation job.

#### Method prototype

```cpp
CosResult DescribeDocumentAuditingJob(const DescribeDocumentAuditingJobReq& req, DescribeDocumentAuditingJobResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

DescribeDocumentAuditingJobReq req(bucket_name);
DescribeDocumentAuditingJobResp resp;

// Add request parameters as detailed in the API documentation
req.SetJobId("stb1ca9fc8a34c525400863904****");

// Call the API to get the job response object
CosResult result = cos.DescribeDocumentAuditingJob(req, &resp);
if (result.IsSucc()) {
	// If the moderation job is queried successfully, you can call the member functions of `DescribeDocumentAuditingJobResp`.
} else {
	// If the moderation job failed to be queried, you can call the member functions of `CosResult` to output the error message.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ----------------- | -------- |
| req  | `DescribeDocumentAuditingJob` operation request | DescribeDocumentAuditingJobReq | Yes       |
| resp | `DescribeDocumentAuditingJob` operation response | DescribeDocumentAuditingJobResp | Yes       |

`DescribeDocumentAuditingJobReq` provides the following member functions:

```cpp
// Set the bucket for performing the operation
void SetBucketName(const std::string& bucket_name);
// Set the ID of the moderation job to be queried
void SetJobId(const std::string& job_id);
```

`DescribeDocumentAuditingJobResp` provides the following member functions:

```cpp
// Get the job details returned by the API request
DocumentAuditingJobsDetail GetJobsDetail();
// Get the `RequestId` returned by the API
std::string GetRequestId();

```

#### Response description

- Success: The moderation job result in the XML content returned by the API will be parsed into the `DocumentAuditingJobsDetail` structure. For specific response parameters, see [Querying File Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48259).
- Failure: If an error (for example, the bucket does not exist) occurs, the error message will be parsed into the `CosResult` structure. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).
