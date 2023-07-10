## Overview

This document provides an overview of APIs and SDK code samples related to CORS.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS | Sets the CORS permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |

## Setting CORS

#### API description

This API (PUT Bucket cors) is used to configure CORS for a bucket.

#### Method prototype

```cpp
CosResult PutBucketCORS(const PutBucketCORSReq& request, PutBucketCORSResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::PutBucketCORSReq req(bucket_name);
qcloud_cos::PutBucketCORSResp resp;

// Set the CORS configuration.
qcloud_cos::CORSRule rule;
rule.m_id = "123";  // Set the ID of the CORS rule.
rule.m_allowed_headers.push_back("x-cos-meta-test");  // Set the allowed HTTP request headers for CORS.
rule.m_allowed_origins.push_back("http://www.qq.com");  // Set the allowed origins for CORS.
rule.m_allowed_methods.push_back("PUT");  // Set the allowed HTTP methods for CORS.
rule.m_allowed_methods.push_back("GET");
rule.m_max_age_secs = "600";  // Set the validity period of the configuration.
rule.m_expose_headers.push_back("x-cos-expose");  // Allow the browser to obtain the headers of the CORS request response.
req.AddRule(rule);

qcloud_cos::CosResult result = cos.PutBucketCORS(req, &resp);
if (result.IsSucc()) {
    // Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
}

```


#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------| -----------------| ------|
| req  | Request of the `PutBucketCORS` operation | PutBucketCORSReq | Yes |
| resp | Response of the `PutBucketCORS` operation | PutBucketCORSResp| Yes |


`PutBucketCORSReq` provides the following member functions:

```
// Add a CORS rule.
void AddRule(const CORSRule& rule);
// Set a CORS rule.
void SetRules(const std::vector<CORSRule>& rules)
```

Classes for the request are defined as follows:

```

struct CORSRule {
    std::string m_id;
    std::string m_max_age_secs;
    std::vector<std::string> m_allowed_headers;
    std::vector<std::string> m_allowed_methods;
    std::vector<std::string> m_allowed_origins;
    std::vector<std::string> m_expose_headers;
};

```

## Querying CORS Configuration

#### Feature description

This API (GET Bucket cors) is used to query the CORS configuration of a bucket.

#### Method prototype

```cpp
CosResult CosAPI::GetBucketCORS(const GetBucketCORSReq& request, GetBucketCORSResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::GetBucketCORSReq req(bucket_name);
qcloud_cos::GetBucketCORSResp resp;

qcloud_cos::CosResult result = cos.GetBucketCORS(req, &resp);
if (result.IsSucc()) {
    // Request successful. You can call the `resp` method to query the CORS rules.
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
}
```


#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------| -----------------| ------|
| req  | Request of the `GetBucketCORS` operation | GetBucketCORSReq | Yes |
| resp | Response of the `GetBucketCORS` operation | GetBucketCORSResp | Yes |


`GetBucketCORSReq` provides the following member function:

```
// Obtain the CORS rules from the response.
std::vector<CORSRule> GetCORSRules() const;
```

## Deleting CORS Configuration

#### Feature description

This API (DELETE Bucket cors) is used to delete the CORS configuration of a bucket.

#### Method prototype

```cpp
CosResult BucketOp::DeleteBucketCORS(const DeleteBucketCORSReq& req, DeleteBucketCORSResp* resp);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::DeleteBucketCORSReq req(bucket_name);
qcloud_cos::DeleteBucketCORSResp resp;

qcloud_cos::CosResult result = cos.DeleteBucketCORS(req, &resp);
if (result.IsSucc()) {
    // Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ---------------------------| --------------------| ------|
| req  | Request of the `DeleteBucketCORS` operation | DeleteBucketCORSReq | Yes |
| resp | Response of the `DeleteBucketCORS` operation | DeleteBucketCORSResp | Yes |
