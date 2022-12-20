## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).


This document provides an overview of APIs and SDK code samples for image moderation.

| API | Description |
| ------------- |  ---------------------- |
| [Moderating single image](https://intl.cloud.tencent.com/document/product/436/48537) |  Scans existing data stored in COS for porn, illegal, and advertising images. |
| [Batch moderating images](https://intl.cloud.tencent.com/document/product/436/48538) |  Moderates multiple images in batches. |
| [Querying image moderation job result](https://intl.cloud.tencent.com/document/product/436/48539)  | Queries the result of specified image moderation job. |


## Single Image Moderation

#### Feature description

The existing data scan feature of image moderation leverages CI's persistent processing API to scan existing data stored in COS for porn, illegal, and advertising images.

#### Method prototype

```cpp
CosResult GetImageAuditing(const GetImageAuditingReq& req, GetImageAuditingResp* resp);
```


#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test.jpg";

GetImageAuditingReq req(bucket_name);
GetImageAuditingResp resp;

// Add request parameters as detailed in the API documentation
req.SetObjectKey(object_name);
req.SetBizType("b81d45f94b91a683255e9a9506f45a11");
// req.SetDetectType("Porn,Ads");

// Call the API to get the job response object
CosResult result = cos.GetImageAuditing(req, &resp);
if (result.IsSucc()) {
	// If the moderation job is created successfully, you can call the member functions of `GetImageAuditingResp`.
} else {
	// If the moderation job failed to be created, you can call the member functions of `CosResult` to output the error message.
}
```


#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ----------------- | -------- |
| req  | `GetImageAuditing` operation request | GetImageAuditingReq | Yes       |
| resp | `GetImageAuditing` operation response | GetImageAuditingResp | Yes       |

`GetImageAuditingReq` provides the following member functions:

```cpp
// Set the bucket for performing the operation
void SetBucketName(const std::string& bucket_name);
// Name of the image file to be moderated in the COS bucket
void SetObjectKey(const std::string& object_name);
// Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as porn, adverting, and illegal information. For configuration guides, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095).
// You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy.
void SetBizType(const std::string& biz_type);
// The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter.
void SetDetectType(const std::string& detect_type);
// URL of the image to be moderated, which can be a URL of any image accessible over the public network.
// If `detect-url` is set, moderation will be conducted by `detect-url` by default, and there will be no need to enter `ObjectKey`.
// If `detect-url` is not set, moderation will be conducted by `ObjectKey` by default.
void SetDetectUrl(const std::string& detect_url);
// For GIF image moderation, you can use this parameter to configure the frame capturing interval. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included).
void SetInterval(int interval);
// Maximum number of frames to be captured for animated image moderation. Default value: `5`.
void SetMaxFrames(int max_frames);
// Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`.
void SetLargeImageDetect(int large_image_detect);
// Image ID. This field will return the original content, which can contain up to 512 bytes.
void SetDataId(const std::string& data_id);
```

`GetImageAuditingResp` provides the following member functions:

```cpp
// Get the job details returned by the API request
ImageAuditingJobsDetail GetJobsDetail();
// Get the `RequestId` returned by the API
std::string GetRequestId();
```

#### Response description

- Success: The moderation job result in the XML content returned by the API will be parsed into the `ImageAuditingJobsDetail` structure. For specific response parameters, see [Single Image Moderation](https://intl.cloud.tencent.com/document/product/436/48537).
- Failure: If an error (for example, the bucket does not exist) occurs, the error message will be parsed into the `CosResult` structure. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31525).

## Batch Image Moderation

#### Feature description

The batch image moderation API adopts a sync POST request method. You can use this API to perform content moderation on multiple image files.

#### Method prototype

```cpp
CosResult CosAPI::BatchImageAuditing(const BatchImageAuditingReq& req, BatchImageAuditingResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
std::string object_name_a = "test1.jpg";
std::string object_name_b = "test2.jpg";

BatchImageAuditingReq req(bucket_name);
BatchImageAuditingResp resp;

// input 1
AuditingInput input_a = AuditingInput();
input_a.SetObject(object_name_a);
req.AddInput(input_a);

// input2
AuditingInput input_b = AuditingInput();
input_a.SetObject(object_name_b);
req.AddInput(input_b);

// Moderation configuration
req.SetBizType("b81d45f94b91a683255e9a9506f45a11");
// req.SetDetectType("Porn,Ads");

// Call the API to get the job response object
CosResult result = cos.BatchImageAuditing(req, &resp);
if (result.IsSucc()) {
	// If the moderation job is created successfully, you can call the member functions of `BatchImageAuditingResp`.
} else {
	// If the moderation job failed to be created, you can call the member functions of `CosResult` to output the error message.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ----------------- | -------- |
| req  | `BatchImageAuditing` operation request | BatchImageAuditingReq | Yes       |
| resp | `BatchImageAuditing` operation response | BatchImageAuditingResp | Yes       |
| input | Input parameter of the `BatchImageAuditing` operation request | AuditingInput | Yes |

`BatchImageAuditingReq` provides the following member functions:

```cpp
// Set the bucket for performing the operation
void SetBucketName(const std::string& bucket_name);
// Set the moderation configuration
void SetConf(const Conf& conf);
// Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as porn, adverting, and illegal information. For configuration guides, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095).
// You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy.
void SetBizType(const std::string& biz_type);
// The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter.
void SetDetectType(const std::string& detect_type);
// Add the input for single image moderation
void AddInput(const AuditingInput& input);
// Set the input array for batch moderation
void SetInputs(const std::vector<AuditingInput>& inputs);
```

`AuditingInput` provides the following member functions:

```cpp
// Name of the image file to be moderated in the COS bucket
void SetObject(const std::string& object);
// Full URL of the image file, such as `http://a-1250000.cos.ap-shanghai.myqcloud.com/image.jpg`. Either `Object` or `Url` can be selected at a time.
void SetUrl(const std::string& url);
// Frame capturing frequency, which takes effect for GIF images only. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included).
void SetInterval(const int interval);
// The maximum number of frames to be captured, which takes effect for GIF images only. The default value is `5`, indicating to capture only five frames of the GIF image for moderation. The parameter value must be greater than 0.
void SetMaxFrames(const int max_frames);
// Image ID. This field will return the original content in the result, which can contain up to 512 bytes.
void SetDataId(const std::string& data_id);
// Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`.
void SetLargeImageDetect(const int large_image_detect);
// Business field.
void SetUserInfo(const UserInfo& user_info);
```

`BatchImageAuditingResp` provides the following member functions:

```cpp
// Get the job details returned by the API request
std::vector<ImageAuditingJobsDetail>  GetJobsDetails();
// Get the `RequestId` returned by the API
std::string GetRequestId();
```

#### Response description

- Success: The moderation job result in the XML content returned by the API will be parsed into the `ImageAuditingJobsDetail` structure array. For specific response parameters, see [Batch Image Moderation](https://intl.cloud.tencent.com/document/product/436/48538).
- Failure: If an error (for example, the bucket does not exist) occurs, the error message will be parsed into the `CosResult` structure. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31525).


## Querying Image Moderation Job Result

#### Feature description

This API is used to submit an image moderation job.

#### Method prototype

```cpp
CosResult DescribeImageAuditingJob(const DescribeImageAuditingJobReq &req, DescribeImageAuditingJobResp *resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

DescribeImageAuditingJobReq req(bucket_name);
DescribeImageAuditingJobResp resp;

// Add request parameters as detailed in the API documentation
req.SetJobId("vab1ca9fc8a3ed11ea834c525400863904");

// Call the API to get the job response object
CosResult result = cos.DescribeImageAuditingJob(req, &resp);
if (result.IsSucc()) {
	// If the moderation job is created successfully, you can call the member functions of `DescribeImageAuditingJobResp`.
} else {
	// If the moderation job failed to be created, you can call the member functions of `CosResult` to output the error message.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ----------------- | -------- |
| req  | `DescribeImageAuditingJob` operation request | DescribeImageAuditingJobReq | Yes       |
| resp | `DescribeImageAuditingJob` operation response | DescribeImageAuditingJobResp | Yes       |

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
ImageAuditingJobsDetail GetJobsDetail();
// Get the `RequestId` returned by the API
std::string GetRequestId();

```

#### Response description

- Success: The moderation job result in the XML content returned by the API will be parsed into the `ImageAuditingJobsDetail` structure. For specific response parameters, see [Querying Image Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48539).
- Failure: If an error (for example, the bucket does not exist) occurs, the error message will be parsed into the `CosResult` structure. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

