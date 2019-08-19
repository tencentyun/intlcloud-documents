## Overview
This document provides an overview of APIs related to cross-origin access, lifecycle, versioning, and cross-region replication and corresponding SDK sample code.

**Cross-origin access**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration 	| Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration 	| Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) 	| Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) |	 Setting lifecycle 	| Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle 	| Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle 	| Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning feature of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rule of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rule of a bucket |

## Cross-origin Access
### Setting Cross-origin Access Configuration

#### Feature Description

This API is used to set the cross-origin access permission to a bucket.

#### Method Prototype
```cpp
CosResult PutBucketCORS(const PutBucketCORSReq& req, PutBucketCORSResp* resp)
```

#### Sample Request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of PutBucketCORSReq requires bucket_name to be passed in
qcloud_cos::PutBucketCORSReq req(bucket_name);
qcloud_cos::CORSRule rule;
rule.m_id = "123";
rule.m_allowed_headers.push_back("x-cos-meta-test");
rule.m_allowed_origins.push_back("http://www.qq.com");
rule.m_allowed_origins.push_back("http://intl.cloud.tentent.com");
rule.m_allowed_methods.push_back("PUT");
rule.m_allowed_methods.push_back("GET");
rule.m_max_age_secs = "600";
rule.m_expose_headers.push_back("x-cos-expose");
req.AddRule(rule);

qcloud_cos::PutBucketCORSResp resp;
qcloud_cos::CosResult result = cos.PutBucketCORS(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | --------------------------------------------- |
| req  | PutBucketCORSReq, which is the request for the PutBucketCORS operation |
| resp | PutBucketCORSResp, which is the return of the PutBucketCORS operation |

PutBucketCORSReq provides the following member functions:
```
// Add a CORSRule
void AddRule(const CORSRule& rule);

// Set a CORSRule
void SetRules(const std::vector<CORSRule>& rules)
```

CORSRule is defined as follows:
```
struct CORSRule {
    std::string m_id; // Configured rule ID; optional
    std::string m_max_age_secs; // Set the validity period of the result of the OPTIONS request
    std::vector<std::string> m_allowed_headers; // Tell the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard * is supported
    std::vector<std::string> m_allowed_methods; // Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE
    std::vector<std::string> m_allowed_origins; // Allowed origin in the format of protocol://domain name[:port number], such as http://www.qq.com. Wildcard * is supported
    std::vector<std::string> m_expose_headers;  // Set custom header information from the server that the browser can receive
};
```

### Querying Cross-origin Access Configuration

#### Feature Description

This API is used to query the cross-origin access configuration information of a bucket.

#### Method Prototype
```cpp
CosResult GetBucketCORS(const GetBucketCORSReq& req, GetBucketCORSResp* resp)
```

#### Sample Request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of GetBucketCORSReq requires bucket_name to be passed in
qcloud_cos::GetBucketCORSReq req(bucket_name);
qcloud_cos::GetBucketCORSResp resp;
qcloud_cos::CosResult result = cos.GetBucketCORS(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | --------------------------------------------- |
| req  | GetBucketCORSReq, which is the request for the GetBucketCORS operation |
| resp | GetBucketCORSResp, which is the return of the GetBucketCORS operation |

GetBucketCORSResp provides the following member functions:
```
// Get CORSRules. For the definition of CORSRule, see Put Bucket CORS
std::vector<CORSRule> GetCORSRules();
```

### Deleting Cross-origin Access Configuration

#### Feature Description

This API is used to delete the cross-origin access configuration of the specified bucket.

#### Method Prototype

```cpp
CosResult DeleteBucketCORS(const DeleteBucketCORSReq& req, DeleteBucketCORSResp* resp)
```

#### Sample Request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of DeleteBucketCORSReq requires bucket_name to be passed in
qcloud_cos::DeleteBucketCORSReq req(bucket_name);
qcloud_cos::DeleteBucketCORSResp resp;
qcloud_cos::CosResult result = cos.DeleteBucketCORS(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | --------------------------------------------------- |
| req  | DeleteBucketCORSReq, which is the request for the DeleteBucketCORS operation |
| resp | DeleteBucketCORSResp, which is the return of the DeleteBucketCORS operation |

## Lifecycle
### Setting Lifecycle

#### Feature Description

This API is used to set the lifecycle configuration information of the specified bucket.

#### Method Prototype

```cpp
CosResult PutBucketLifecycle(const PutBucketLifecycleReq& req, PutBucketLifecycleResp* resp)
```

#### Sample Request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of PutBucketLifecycleReq requires bucket_name to be passed in
qcloud_cos::PutBucketLifecycleReq req(bucket_name);
// Set rule 1
{
    qcloud_cos::LifecycleRule rule;
    rule.SetIsEnable(true);
    rule.SetId("lifecycle_rule00");
    qcloud_cos::LifecycleFilter filter;
    filter.SetPrefix("sevenyou_e1");
    rule.SetFilter(filter);
    qcloud_cos::LifecycleExpiration expiration;
    expiration.SetDays(1);
    rule.SetExpiration(expiration);
    req.AddRule(rule);
}

// Set rule 2
{
    qcloud_cos::LifecycleRule rule;
    rule.SetIsEnable(true);
    rule.SetId("lifecycle_rule01");
    qcloud_cos::LifecycleFilter filter;
    filter.SetPrefix("sevenyou_e2");
    rule.SetFilter(filter);
    qcloud_cos::LifecycleExpiration expiration;
    expiration.SetDays(3);
    rule.SetExpiration(expiration);
    req.AddRule(rule);
}

qcloud_cos::PutBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.PutBucketLifecycle(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // Failed to set the lifecycle. You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------------------------- |
| req  | PutBucketLifecycleReq, which is the request for the PutBucketLifecycle operation |
| resp | PutBucketLifecycleResp, which is the return of the PutBucketLifecycle operation |

PutBucketLifecycleReq provides the following member functions:
```
// Add a LifecycleRule
void AddRule(const LifecycleRule& rule)

// Set a LifecycleRule
void SetRule(const std::vector<LifecycleRule>& rules)
```

The definition of LifecycleRule is quite complicated as follows:

```
struct LifecycleTag {
    std::string key;
    std::string value;
};

class LifecycleFilter {
public:
    LifecycleFilter();

    std::string GetPrefix();
    std::vector<LifecycleTag> GetTags();

    void SetPrefix(const std::string& prefix);
    void SetTags(const std::vector<LifecycleTag>& tags);
    void AddTag(const LifecycleTag& tag);

    bool HasPrefix();
    bool HasTags();

private:
    std::string m_prefix; // Specify the prefix to which the rule applies. Objects that match the prefix are subject to this rule. There can be at most one prefix
    std::vector<LifecycleTag> m_tags; // Tag. There can be zero, one, or multiple tags
};

class LifecycleTransition {
public:
    LifecycleTransition();

    uint64_t GetDays();
    std::string GetDate();
    std::string GetStorageClass();

    void SetDays(uint64_t days);
    void SetDate(const std::string& date);
    void SetStorageClass(const std::string& storage_class);

    bool HasDays();
    bool HasDate();
    bool HasStorageClass();
    
private:
    // Days and Date cannot be used in the same rule at the same time
    uint64_t m_days; // Specify the number of days after the last modified date of an object that should elapse before the action corresponding to a rule is performed. A valid value is a non-negative integer
    std::string m_date; // Specify when the action corresponding to a rule should be performed
    std::string m_storage_class; // Specify the transitioned storage class of an object. Enumerated values: Standard_IA
};

class LifecycleExpiration {
public:
    LifecycleExpiration();
    
    uint64_t GetDays();
    std::string GetDate();
    bool IsExpiredObjDelMarker();
    
    void SetDays(uint64_t days);
    void SetDate(const std::string& date);
    void SetExpiredObjDelMarker(bool marker);

    bool HasDays();
    bool HasDate();
    bool HasExpiredObjDelMarker();
    
private:
    // Days and Date cannot be used in the same rule at the same time
    uint64_t m_days; // Specify the number of days after the last modified date of an object that should elapse before the action corresponding to a rule is performed. A valid value is a positive integer
    std::string m_date; // Specify when the action corresponding to a rule should be performed
    ool m_expired_obj_del_marker; // Delete the expired object deletion tag; enumerated values: true, false
};

class LifecycleNonCurrTransition {
public:
    LifecycleNonCurrTransition();

    uint64_t GetDays();
    std::string GetStorageClass();

    void SetDays(uint64_t days);  
    void SetStorageClass(const std::string& storage_class);

    bool HasDays();
    bool HasStorageClass();

private:
    uint64_t m_days; // Specify the number of days after the last modified date of an object that should elapse before the action corresponding to a rule is performed. A valid value is a non-negative integer
    std::string m_storage_class; // Specify the transitioned storage class of an object. Enumerated values: Standard_IA
};

class LifecycleNonCurrExpiration {
public:
    LifecycleNonCurrExpiration();
    
    uint64_t GetDays();

    void SetDays(uint64_t days);

    bool HasDays();

private:
    uint64_t m_days; // Specify the number of days after the last modified date of an object that should elapse before the action corresponding to a rule is performed. A valid value is a positive integer
};

struct AbortIncompleteMultipartUpload {
    uint64_t m_days_after_init; // Indicate in how many days a multipart upload has to be completed once started
};

class LifecycleRule {
public:
    LifecycleRule();

    void SetIsEnable(bool is_enable);
    void SetId(const std::string& id);
    void SetFilter(const LifecycleFilter& filter);
    void AddTransition(const LifecycleTransition& rh);
    void SetExpiration(const LifecycleExpiration& rh);
    void SetNonCurrTransition(const LifecycleNonCurrTransition& rh);
    void SetNonCurrExpiration(const LifecycleNonCurrExpiration& rh);
    void SetAbortIncompleteMultiUpload(const AbortIncompleteMultipartUpload& rh);

    bool IsEnable();
    std::string GetId();
    LifecycleFilter GetFilter();
    std::vector<LifecycleTransition> GetTransitions();
    LifecycleExpiration GetExpiration();
    LifecycleNonCurrTransition GetNonCurrTransition();
    LifecycleNonCurrExpiration GetNonCurrExpiration();
    AbortIncompleteMultipartUpload GetAbortIncompleteMultiUpload();

    bool HasIsEnable();
    bool HasId();
    bool HasFilter();
    bool HasExpiration();
    bool HasNonCurrTransition();
    bool HasNonCurrExpiration();
    bool HasAbortIncomMultiUpload();

private:
    bool m_is_enable; // Whether the rule is effective
    std::string m_id; // Rule ID
    LifecycleFilter m_filter; // Filter used to specify the range of objects for which the rule takes effect
    std::vector<LifecycleTransition> m_transitions; // Transition operation
    LifecycleExpiration m_expiration; // Expiration operation
    LifecycleNonCurrTransition m_non_curr_transition; // Non-current version transition operation
    LifecycleNonCurrExpiration m_non_curr_expiration; // Non-current version expiration operation
    AbortIncompleteMultipartUpload m_abort_multi_upload; // Set the maximum amount of time allowed for a multipart upload to keep running
}
```

### Querying Lifecycle

#### Feature Description

This API is used to query the lifecycle configuration information of the specified bucket.

#### Method Prototype

```cpp
CosResult GetBucketLifecycle(const GetBucketLifecycleReq& req, GetBucketLifecycleResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of GetBucketLifecycleReq requires bucket_name to be passed in
qcloud_cos::GetBucketLifecycleReq req(bucket_name);
qcloud_cos::GetBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.GetBucketLifecycle(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // Failed to get the lifecycle configuration. You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------------------------- |
| req  | GetBucketLifecycleReq, which is the request for the GetBucketLifecycle operation |
| resp | GetBucketLifecycleResp, which is the return of the GetBucketLifecycle operation |

GetBucketLifecycleResp provides the following member functions:
```
// Get LifecycleRules
std::vector<LifecycleRule> GetRules()
```

For the definition of LifecycleRule, see [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280).


### Deleting Lifecycle

#### Feature Description

This API is used to delete the lifecycle configuration information of the specified bucket.

#### Method Prototype

```cpp
CosResult DeleteBucketLifecycle(const DeleteBucketLifecycleReq& req, DeleteBucketLifecycleResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of DeleteBucketLifecycleReq requires bucket_name to be passed in
qcloud_cos::DeleteBucketLifecycleReq req(bucket_name);
qcloud_cos::DeleteBucketLifecycleResp resp;
qcloud_cos::CosResult result = cos.DeleteBucketLifecycle(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // Failed to delete the lifecycle configuration. You can call the member function of CosResult to output the error information such as requestID
} 
```


#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------------------------------ |
| req  | DeleteBucketLifecycleReq, which is the request for the DeleteBucketLifecycle operation |
| resp | DeleteBucketLifecycleResp, which is the return of the DeleteBucketLifecycle operation |


## Versioning
### Setting Versioning

#### Feature Description

This API is used to set the versioning feature of the specified bucket.

#### Method Prototype
```cpp
CosResult PutBucketVersioning(const PutBucketVersioningReq& request, PutBucketVersioningResp* response)
```

#### Sample Request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of PutBucketVersioningReq requires bucket_name to be passed in
qcloud_cos::PutBucketVersioningReq req(bucket_name);
req.SetStatus(true);
qcloud_cos::PutBucketVersioningResp resp;
qcloud_cos::CosResult result = cos.PutBucketVersioning(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions
| Parameter | Description |
| ---- | ------------------------------------------- |
| req  | PutBucketVersioningReq, which is the request for the PutBucketVersioning operation |
| resp | PutBucketVersioningResp, which is the return of the PutBucketVersioning operation|

PutBucketVersioningReq provides the following member functions:

```cpp
// Whether versioning is enabled. Once enabled, it cannot be disabled; instead, it can only be suspended
void SetStatus(bool is_enable);
```

### Querying Versioning

#### Feature Description

This API is used to query the versioning information of the specified bucket.

#### Method Prototype
```cpp
CosResult GetBucketVersioning(const GetBucketVersioningReq& request, GetBucketVersioningResp* response) 
```

#### Sample Request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::GetBucketVersioningReq req(bucket_name);
qcloud_cos::GetBucketVersioningResp resp;
qcloud_cos::CosResult result = cos.GetBucketVersioning(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions
| Parameter | Description |
| ---- | ------------------------------------------- |
| req  | GetBucketVersioningReq, which is the request for the GetBucketVersioning operation |
| resp | GetBucketVersioningResp, which is the return of the GetBucketVersioning operation |

GetBucketVersioningResp provides the following member functions:

```cpp
// Return the versioning status of the bucket. 0: versioning never enabled; 1: versioning enabled; 2: versioning suspended
int GetStatus() const
```

## Cross-region Replication
### Setting Cross-region Replication

#### Feature Description

This API is used to set the cross-region replication rule of the specified bucket.

#### Method Prototype
```go
func (s *BucketService) PutBucketReplication(ctx context.Context, opt *PutBucketReplicationOptions) (*Response, error)
```

#### Sample Request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::PutBucketReplicationReq req(bucket_name);
req.SetRole("qcs::cam::uin/100000000001:uin/100000000001");
qcloud_cos::ReplicationRule rule("", "qcs::cos:ap-guangzhou::examplebucket-1250000000", "", "", true);

req.AddReplicationRule(rule);
qcloud_cos::PutBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.PutBucketReplication(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
}
```

#### Parameter Descriptions
| Parameter | Description |
| ---- | ------------------------------------------- |
| req  | PutBucketReplicationReq, which is the request for the PutBucketReplication operation |
| resp | PutBucketReplicationResp, which is the return of the PutBucketReplication operation |

PutBucketReplicationReq provides the following member functions:

```
// Initiator ID: qcs::cam::uin/<OwnerUin>:uin/<SubUin>
void SetRole(const std::string& role)；
// Add specific configuration information of up to 1,000 rules. All rules must point to the same destination bucket
void AddReplicationRule(const ReplicationRule& rule)；

// The structure of ReplicationRule is as follows:
struct ReplicationRule {
	bool m_is_enable;
	std::string m_id; // Optional
	std::string m_prefix;
	std::string m_dest_bucket;
	std::string m_dest_storage_class; // Optional 
}
```

### Querying Cross-region Replication

#### Feature Description

This API is used to query the cross-region replication rule of the specified bucket.

#### Method Prototype
```cpp
CosResult GetBucketReplication(const GetBucketReplicationReq& request, GetBucketReplicationResp* response)
```

#### Sample Request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::GetBucketReplicationReq req(bucket_name);
qcloud_cos::GetBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.GetBucketReplication(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions
| Parameter | Description |
| ---- | ------------------------------------------- |
| req  | GetBucketReplicationReq, which is the request for the GetBucketReplication operation |
| resp | GetBucketReplicationResp, which is the return of the GetBucketReplication operation |

GetBucketReplicationResp provides the following member functions:

```cpp
// Get the initiator ID: qcs::cam::uin/<OwnerUin>:uin/<SubUin>
std::string GetRole();
// Get specific configuration information of up to 1,000 rules. All rules must point to the same destination bucket
std::vector<ReplicationRule> GetRules();
// The structure of ReplicationRule is as described in PutBucketReplication
```


### Deleting Cross-region Replication

#### Feature Description

This API is used to delete the cross-region replication rule of the specified bucket.

#### Method Prototype
```cpp
CosResult DeleteBucketReplication(const DeleteBucketReplicationReq& request, DeleteBucketReplicationResp* response)
```

#### Sample Request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::DeleteBucketReplicationReq req(bucket_name);
qcloud_cos::DeleteBucketReplicationResp resp;
qcloud_cos::CosResult result = cos.DeleteBucketReplication(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions
| Parameter | Description |
| ---- | ------------------------------------------- |
| req  | DeleteBucketReplicationReq, which is the request for the DeleteBucketReplication operation |
| resp | DeleteBucketReplicationResp, which is the return of the DeleteBucketReplication operation |
