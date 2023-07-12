## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/zh/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

## Setting Versioning

#### Feature description

This API (PUT Bucket versioning) is used to set the versioning configuration for a bucket.

#### Method prototype
```cpp
CosResult BucketOp::PutBucketVersioning(const PutBucketVersioningReq& req, PutBucketVersioningResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::PutBucketVersioningReq req(bucket_name);
qcloud_cos::PutBucketVersioningResp resp;

// Enable versioning
req.SetStatus(true);

qcloud_cos::CosResult result = cos.PutBucketVersioning(req, &resp);

if (result.IsSucc()) {
    // Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------------|------------------------| ------|
| req  | Request of the `PutBucketVersioning` operation | PutBucketVersioningReq | Yes |
| resp | Response of the `PutBucketVersioning` operation  | PutBucketVersioningResp| Yes |


`PutBucketVersioningReq` provides the following method to enable/suspend versioning:

```cpp
void SetStatus(bool is_enable);
```


## Querying Versioning

#### Feature description

This API is used to query the versioning configuration of a bucket.

#### Method prototype
```cpp
CosResult CosAPI::GetBucketVersioning(const GetBucketVersioningReq& request, GetBucketVersioningResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::GetBucketVersioningReq req(bucket_name);
qcloud_cos::GetBucketVersioningResp resp;

qcloud_cos::CosResult result = cos.GetBucketVersioning(req, &resp);

if (result.IsSucc()) {
    // Request successful. You can obtain the versioning status via the resp method.
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------------|------------------------| ------|
| req  | Request of the `GetBucketVersioning` operation | GetBucketVersioningReq | Yes |
| resp | Response of the `GetBucketVersioning` operation | GetBucketVersioningResp | Yes |


`GetBucketVersioningResp` provides the following method to obtain the status of versioning:

```cpp
int GetStatus() const;
```
