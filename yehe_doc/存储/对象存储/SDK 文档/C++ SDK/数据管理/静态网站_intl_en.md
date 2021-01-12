

## Overview

This document provides an overview of APIs and SDK code samples related to static websites.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Configures a static website for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying a static website configuration | Queries the static website configuration of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting a static website configuration | Deletes the static website configuration of a bucket |

## Setting Static Website

#### API description

This API (PUT Bucket website) is used to configure a static website for a bucket.

#### Method prototype

```cpp
CosResult CosAPI::PutBucketWebsite(const PutBucketWebsiteReq& request,PutBucketWebsiteResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::PutBucketWebsiteReq req(bucket_name);
qcloud_cos::PutBucketWebsiteResp resp;

req.SetSuffix("index.xml"); // Required
req.SetProtocol("https");
req.SetKey("Error.html");

// Set a maximum of 100 redirection rules. 

// Set the first rule.
qcloud_cos::RoutingRule routerule1;
qcloud_cos::Condition temp_condtion1;
temp_condtion1.SetHttpErrorCodeReturnedEquals(404);// Required. Defaults to `404`.
routerule1.SetCondition(temp_condtion1);
qcloud_cos::Redirect temp_redirect1;
temp_redirect1.SetProtocol("https");
temp_redirect1.SetReplaceKeyWith("404.htmp");
routerule1.SetRedirect(temp_redirect1);

// Set the second rule.
qcloud_cos::RoutingRule routerule2;
qcloud_cos::Condition temp_condtion2;
temp_condtion2.SetHttpErrorCodeReturnedEquals(403);// Required. Defaults to `404`.
routerule2.SetCondition(temp_condtion2);
qcloud_cos::Redirect temp_redirect2;
temp_redirect2.SetProtocol("https");
temp_redirect2.SetReplaceKeyWith("403.htmp");
routerule2.SetRedirect(temp_redirect2);

// Set the third rule.
qcloud_cos::RoutingRule routerule3;
qcloud_cos::Condition temp_condtion3;
temp_condtion3.SetKeyPrefixEquals("img/");
temp_condtion3.SetHttpErrorCodeReturnedEquals(402);
routerule3.SetCondition(temp_condtion3);
qcloud_cos::Redirect temp_redirect3;
temp_redirect3.SetProtocol("https");
temp_redirect3.SetReplaceKeyWith("401.htmp");
routerule3.SetRedirect(temp_redirect3);

// Set the fourth rule.
qcloud_cos::RoutingRule routerule4;
qcloud_cos::Condition temp_condtion4;
temp_condtion4.SetKeyPrefixEquals("img1/");
routerule4.SetCondition(temp_condtion4);
qcloud_cos::Redirect temp_redirect4;
temp_redirect4.SetProtocol("https");
temp_redirect4.SetReplaceKeyPrefixWith("402.htmp");
routerule4.SetRedirect(temp_redirect4);

req.AddRoutingRule(routerule1);
req.AddRoutingRule(routerule2);
req.AddRoutingRule(routerule3);
req.AddRoutingRule(routerule4);

qcloud_cos::CosResult result = cos.PutBucketWebsite(req, &resp);

if (result.IsSucc()) {
	// Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | --------------------------| --------------------| ------|
| req  | Request of the `PutBucketWebsite` operation | PutBucketWebsiteReq | Yes |
| resp | Response of the `PutBucketWebsite` operation | PutBucketWebsiteResp | Yes |


## Querying Static Website Configuration

#### API description

This API (GET Bucket website) is used to query the static website configuration associated with a bucket.

#### Method prototype

```cpp
CosResult CosAPI::GetBucketWebsite(const GetBucketWebsiteReq& request, GetBucketWebsiteResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::GetBucketWebsiteReq req(bucket_name);
qcloud_cos::GetBucketWebsiteResp resp;

qcloud_cos::CosResult result = cos.GetBucketWebsite(req, &resp);

if (result.IsSucc()) {
	// Request successful. You can obtain the static website configuration via `resp`.
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | --------------------------| --------------------| ------|
| req  | Request of the `GetBucketWebsite` operation | GetBucketWebsiteReq | Yes |
| resp | Response of the `GetBucketWebsite` operation | GetBucketWebsiteResp | Yes |


`GetBucketWebsiteResp` provides the following method to obtain the static website configuration:
```cpp
std::vector<RoutingRule> GetRoutingRules() const;
```

For the definition of `RoutingRule`, please refer to the SDK header files.


## Deleting Static Website Configuration

#### API description

This API (DELETE Bucket website) is used to delete the static website configuration of a bucket.

#### Method prototype

```java
CosResult CosAPI::DeleteBucketWebsite(const DeleteBucketWebsiteReq& request, DeleteBucketWebsiteResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::DeleteBucketWebsiteReq req(bucket_name);
qcloud_cos::DeleteBucketWebsiteResp resp;

qcloud_cos::CosResult result = cos.DeleteBucketWebsite(req, &resp);

if (result.IsSucc()) {
	// Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -----------------------------| -----------------------| ------|
| req  | Request of the `DeleteBucketWebsite` operation | DeleteBucketWebsiteReq | Yes |
| resp | Response of the `DeleteBucketWebsite` operation | DeleteBucketWebsiteResp | Yes |

