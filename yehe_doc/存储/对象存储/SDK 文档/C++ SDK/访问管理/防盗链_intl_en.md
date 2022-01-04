## Overview

This document provides an overview of APIs and SDK code samples related to bucket referer allowlist or blocklist.

>! v5.5.0 or later is required.
>

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting bucket referer configuration | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying bucket referer configuration | Queries a bucket referer allowlist or blocklist |

## Setting Bucket Referer Configuration

#### Description

This API (PUT Bucket referer) is used to set a referer allowlist/blocklist for a bucket.

#### Method prototype

```cpp
CosResult PutBucketReferer(const PutBucketRefererReq& request, PutBucketRefererResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000"; // Replaced with the bucket name

qcloud_cos::PutBucketRefererReq req(bucket_name);
qcloud_cos::PutBucketRefererResp resp;
// Construct the request as needed
req.SetStatus("Enabled");
req.SetRefererType("White-List");
req.AddDomain("test1.com");
req.AddDomain("test2.com");
qcloud_cos::CosResult result = cos.PutBucketReferer(req, &resp);
if (result.IsSucc()) {
    // Request succeeded
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -------------------------- | -------------------- | -------- |
| req | Request of the `PutBucketReferer` operation | PutBucketRefererReq  | Yes |
| resp | Response of the `PutBucketReferer` operation | PutBucketRefererResp | Yes |

#### Response description
No

## Querying Bucket Referer Configuration

#### Description

This API (GET Bucket referer) is used to query the referer allowlist/blocklist of a bucket.

#### Method prototype

```cpp
CosResult GetBucketReferer(const GetBucketRefererReq& request, GetBucketRefererResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000"; // Replaced with the bucket name

qcloud_cos::GetBucketRefererReq req(bucket_name);
qcloud_cos::GetBucketRefererResp resp;
qcloud_cos::CosResult result = cos.GetBucketReferer(req, &resp);
if (result.IsSucc()) {
    // Request succeeded. Obtain the referer configuration.
    std::cout << "Status:" << resp.GetStatus() << std::endl;
    std::cout << "RefererType:" << resp.GetRefererType() << std::endl;
    for (auto& domain : resp.GetDomainList()) {
        std::cout << "Domain:" << domain  << std::endl;
    }
    std::cout << "EmptyReferConfiguration:" << resp.GetEmptyReferConf() << std::endl;
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -------------------------- | -------------------- | -------- |
| req  | Request of the `GetBucketReferer` operation | GetBucketRefererReq | Yes |
| resp | Response of the `GetBucketReferer` operation | GetBucketRefererResp | Yes |

#### Response description
No
