## Overview

This document provides an overview of APIs and SDK code samples related to logging.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | Setting logging | Enables logging for a source bucket |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | Querying logging configuration | Queries the logging configuration of a source bucket |

## Setting Logging

#### API description

This API (PUT Bucket logging) is used to enable logging for a source bucket and store the access logs in a specified destination bucket.

#### Method prototype

```cpp
CosResult CosAPI::PutBucketLogging(const PutBucketLoggingReq& request, PutBucketLoggingResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::PutBucketLoggingReq req(bucket_name);
qcloud_cos::PutBucketLoggingResp resp;

qcloud_cos::LoggingEnabled rules;
rules.SetTargetBucket(TargetBucketname);  // Set the destination bucket to store the logs.
rules.SetTargetPrefix(TargetPrefix);  // Set the path in the destination bucket to store the logs.    
req.SetLoggingEnabled(rules);

qcloud_cos::CosResult result = cos.PutBucketLogging(req, &resp);

if (result.IsSucc()) {
    // Request successful. You can obtain the static website configuration via `resp`.
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -----------------------------|---------------------| ------|
| req  | Request of the `PutBucketLogginge` operation | PutBucketLoggingReq | Yes |
| resp | Response of the `PutBucketLogging` operation | PutBucketLoggingResp | Yes |


`PutBucketLoggingReq` provides the following method to configure logging for the bucket:
```cpp
void SetLoggingEnabled(const LoggingEnabled& rules);
```

`LoggingEnabledt` provides the following methods for the configuration:
```cpp
class LoggingEnabled {
public:
    void SetTargetBucket(const std::string &targetbucket);
    void SetTargetPrefix(const std::string &targetprefix);
```


## Querying Logging

#### API description

This API (GET Bucket logging) is used to query the logging configuration of a bucket.

#### Method prototype

```cpp
CosResult CosAPI::GetBucketLogging(const GetBucketLoggingReq& request, GetBucketLoggingResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::GetBucketLoggingReq req(bucket_name);
qcloud_cos::GetBucketLoggingResp resp;

qcloud_cos::CosResult result = cos.GetBucketLogging(req, &resp);

if (result.IsSucc()) {
    // Request successful. You can obtain the bucket logging configuration via `resp`.
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -----------------------------|---------------------| ------|
| req  | Request of the `GetBucketLogginge` operation | GetBucketLoggingReq | Yes |
| resp | Response of the `GetBucketLogging` operation | GetBucketLoggingResp | Yes |

`GetBucketLoggingResp` provides the following method to obtain the logging configuration:

```cpp
LoggingEnabled GetLoggingEnabled() const;
```
