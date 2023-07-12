## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for video moderation.

| API | Description |
| :----------------------------------------------------------- | :------------------------- |
| [Submitting video moderation job](https://intl.cloud.tencent.com/document/product/436/48249) | Submits video moderation job.   |
| [Querying video moderation job result](https://intl.cloud.tencent.com/document/product/436/48250)  | Queries the result of specified video moderation job. |


## Submitting Video Moderation Job

#### Feature description

This API is used to submit a video moderation job.

#### Method prototype

```cpp
CosResult CreateVideoAuditingJob(const CreateVideoAuditingJobReq& req, CreateVideoAuditingJobResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test.mp4";

CreateVideoAuditingJobReq req(bucket_name);
CreateVideoAuditingJobResp resp;

// Add request parameters as detailed in the API documentation
req.SetObject(object_name);
req.SetBizType("b81d45f94b91a683255e9a9506f45a11");
// req.SetDetectType("Porn,Ads");
SnapShotConf snap_shot = SnapShotConf();
snap_shot.SetCount(100);
snap_shot.SetMode("Interval");
snap_shot.SetTimeInterval(10);
req.SetSnapShot(snap_shot);

// Call the API to get the job response object
CosResult result = cos.CreateVideoAuditingJob(req, &resp);
if (result.IsSucc()) {
	// If the moderation job is created successfully, you can call the member functions of `CreateVideoAuditingJobResp`.
} else {
	// If the moderation job failed to be created, you can call the member functions of `CosResult` to output the error message.
}
```


#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ----------------- | -------- |
| req  | `CreateVideoAuditing` operation request | CreateVideoAuditingReq | Yes       |
| resp | `CreateVideoAuditing` operation response | CreateVideoAuditingResp | Yes       |

`CreateVideoAuditingReq` provides the following member functions:

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
// Video image moderation is implemented by taking a certain number of screenshots based on the video frame capturing capability and then moderating the screenshots one by one. This parameter is used to specify the configuration of video frame capturing.
void SetSnapShot(const SnapShotConf& snap_shot);
// Callback address, which must start with `http://` or `https://`.
void SetCallBack(const std::string& callback);
// Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`.
void SetCallBackVersion(const std::string& callback_version);
// Specify whether to moderate video sound. Valid values: `0` (moderates the video image only), `1` (moderates both the video image and video sound). Default value: `0`.
void SetDetectContent(const int detect_content);

// input
// Name of the video file stored in the COS bucket; for example, if the file is `video.mp4` in the `test` directory, then the filename is `test/video.mp4`.
void SetObject(const std::string& object);
// Full URL of the video file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/test.mp4`. Either `Object` or `Url` can be selected at a time.
void SetUrl(const std::string& url);
// This field will return the original content in the moderation result, which can contain up to 512 bytes. You can use this field to uniquely identify the data to be moderated in your business.
void SetDataId(const std::string& data_id);
// Business field.
void SetUserInfo(const UserInfo& user_info);
```

`CreateVideoAuditingResp` provides the following member functions:

```cpp
// Get the job details returned by the API request
VideoAuditingJobsDetail GetJobsDetail();
// Get the `RequestId` returned by the API
std::string GetRequestId();

```

#### Response description

- Success: The moderation job result in the XML content returned by the API will be parsed into the `VideoAuditingJobsDetail` structure. For specific response parameters, see [Submitting Video Moderation Job](https://intl.cloud.tencent.com/document/product/436/48249).
- Failure: If an error (for example, the bucket does not exist) occurs, the error message will be parsed into the `CosResult` structure. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31525).


## Querying Video Moderation Job Result

#### Feature description

This API is used to query the status and result of a video moderation job.

#### Method prototype

```cpp
CosResult DescribeVideoAuditingJob(const DescribeVideoAuditingJobReq& req, DescribeVideoAuditingJobResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

DescribeVideoAuditingJobReq req(bucket_name);
DescribeVideoAuditingJobResp resp;

// Add request parameters as detailed in the API documentation
req.SetJobId("vab1ca9fc8a3ed11ea834c525400863904");

// Call the API to get the job response object
CosResult result = cos.DescribeVideoAuditingJob(req, &resp);
if (result.IsSucc()) {
	// If the moderation job is queried successfully, you can call the member functions of `DescribeVideoAuditingJobResp`.
} else {
	// If the moderation job failed to be queried, you can call the member functions of `CosResult` to output the error message.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ----------------- | -------- |
| req  | `DescribeVideoAuditingJob` operation request | DescribeVideoAuditingJobReq | Yes       |
| resp | `DescribeVideoAuditingJob` operation response | DescribeVideoAuditingJobResp | Yes       |

`DescribeVideoAuditingJobReq` provides the following member functions:

```cpp
// Set the bucket for performing the operation
void SetBucketName(const std::string& bucket_name);
// Set the ID of the moderation job to be queried
void SetJobId(const std::string& job_id);
```

`DescribeVideoAuditingJobResp` provides the following member functions:

```cpp
// Get the job details returned by the API request
VideoAuditingJobsDetail GetJobsDetail();
// Get the `RequestId` returned by the API
std::string GetRequestId();

```

#### Response description

- Success: The moderation job result in the XML content returned by the API will be parsed into the `VideoAuditingJobsDetail` structure. For specific response parameters, see [Submitting Video Moderation Job](https://intl.cloud.tencent.com/document/product/436/48249).
- Failure: If an error (for example, the bucket does not exist) occurs, the error message will be parsed into the `CosResult` structure. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31525).

