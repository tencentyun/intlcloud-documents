## Overview
This document provides an overview of APIs and SDK code samples related to lifecycle.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting a lifecycle | Sets a lifecycle for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting a lifecycle configuration | Deletes the lifecycle configuration of a bucket |

## Setting a Lifecycle

#### API description

This API (PUT Bucket lifecycle) is used to set a lifecycle for a bucket.

#### Method prototype

```cpp
CosResult CosAPI::PutBucketLifecycle(const PutBucketLifecycleReq& request, PutBucketLifecycleResp* response)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::PutBucketLifecycleReq req(bucket_name);
qcloud_cos::PutBucketLifecycleResp resp;

qcloud_cos::LifecycleRule rule;
rule.SetIsEnable(true);  // Specify whether to enable the rule. Enumerated values: Enabled, Disabled.	
rule.SetId("lifecycle_rule00");  // Set the unique ID for the rule. It can be up to 255 characters.

qcloud_cos::LifecycleFilter filter;
filter.SetPrefix("test");
rule.SetFilter(filter);  // Set a maximum of one prefix for the rule. It specifies the objects the rule applies to.

qcloud_cos::LifecycleTransition transition;  // Lifecycle transition attributes
transition.SetDays(30);
transition.SetStorageClass("Standard_IA");
rule.AddTransition(transition);
req.AddRule(rule);

qcloud_cos::CosResult result = cos.GetBucketWebsite(req, &resp);

if (result.IsSucc()) {
	// Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -----------------------------|-----------------------| ------|
| req  | Request of the `PutBucketLifecycle` operation | PutBucketLifecycleReq | Yes |
| resp | Response of the `PutBucketLifecycle` operation | PutBucketLifecycleResp | Yes |


`PutBucketLifecycleReq` provides the following methods to set the lifecycle rule:
```cpp
void AddRule(const LifecycleRule& rule);
void SetRule(const std::vector<LifecycleRule>& rules);
```

>?For the definition of the classes `LifecycleRule`, `LifecycleFilter`, `LifecycleTransition`, `LifecycleExpiration`, `LifecycleNonCurrTransition`, `LifecycleNonCurrExpiration`, and `AbortIncompleteMultipartUpload`, please refer to the SDK header file `include/cos_defines.h`.


## Querying a Lifecycle Configuration

#### API description

This API (GET Bucket lifecycle) is used to query the lifecycle configuration of a bucket.

#### Method prototype

```cpp
CosResult CosAPI::GetBucketLifecycle(const GetBucketLifecycleReq& request, GetBucketLifecycleResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::GetBucketLifecycleReq req(bucket_name);
qcloud_cos::GetBucketLifecycleResp resp;

qcloud_cos::CosResult result = cos.GetBucketLifecycle(req, &resp);

if (result.IsSucc()) {
	// Request successful. You can obtain the lifecycle configuration via `resp`.
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```


#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -----------------------------|-----------------------| ------|
| req  | Request of the `GetBucketLifecycle` operation | GetBucketLifecycleReq | Yes |
| resp | Response of the `GetBucketLifecycle` operation | GetBucketLifecycleResp | Yes |


`GetBucketLifecycleResp` provides the following method to obtain the lifecycle rule:
```cpp
std::vector<LifecycleRule> GetRules() const;
```

## Deleting a Lifecycle Configuration

#### API description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle configuration of a bucket.

#### Method prototype

```cpp
CosResult CosAPI::DeleteBucketLifecycle(const DeleteBucketLifecycleReq& request, DeleteBucketLifecycleResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::DeleteBucketLifecycleReq req(bucket_name);
qcloud_cos::DeleteBucketLifecycleResp resp;

qcloud_cos::CosResult result = cos.DeleteBucketLifecycle(req, &resp);

if (result.IsSucc()) {
	// Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -------------------------------|--------------------------| ------|
| req  | Request of the `DeletBucketLifecycle` operation | DelettBucketLifecycleReq | Yes  |
| resp | Response of the `DeletBucketLifecycle` operation | DeletBucketLifecycleResp | Yes |

