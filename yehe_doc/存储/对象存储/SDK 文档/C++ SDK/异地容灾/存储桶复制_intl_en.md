## Overview

This document provides an overview of APIs and SDK code samples related to cross-bucket replication.

| API | Operation | Description |
| :----------------------------------------------------------- | :------------- | :----------------------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-bucket replication | Sets a cross-bucket replication rule for a versioning-enabled bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-bucket replication | Queries the cross-bucket replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting a cross-bucket replication rule | Deletes a cross-bucket replication rule of a bucket |

## Setting Cross-Bucket Replication

#### Feature description

This API (PUT Bucket replication) is used to set the cross-bucket replication rule for a bucket.

#### Method prototype

```
CosResult PutBucketReplication(const PutBucketReplicationReq& request, PutBucketReplicationResp* response);
```


#### Sample request

```
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::PutBucketReplicationReq req(bucket_name);
qcloud_cos::PutBucketReplicationResp resp;

req.SetRole("qcs::cam::uin/100000000001:uin/100000000001");  // Set the role of the request initiator.
qcloud_cos::ReplicationRule rule("", "qcs::cos:ap-guangzhou:uid/1250000000:destinationbucket-1250000000",
                                 "", "", true);  // Set the cross-bucket replication rule.
req.AddReplicationRule(rule);

qcloud_cos::CosResult result = cos.PutBucketReplication(req, &resp);

if (result.IsSucc()) {
    // Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```


#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------------|-------------------------| ------|
| req  | Request of the `PutBucketReplication` operation | PutBucketReplicationReq | Yes |
| resp | Response of the `PutBucketReplication` operation | PutBucketReplicationResp| Yes |


`PutBucketReplicationReq` provides the following methods to configure cross-bucket replication:

```cpp
void SetRole(const std::string& role)
void AddReplicationRule(const ReplicationRule& rule)
void SetReplicationRule(const std::vector<ReplicationRule>& rules)
```

`ReplicationRule` is defined as follows:

```cpp
struct ReplicationRule {
    bool m_is_enable;
    std::string m_id; // Name of the rule    
    std::string m_prefix;  // Prefix matching policy. It cannot overlap. Otherwise, an error will be returned.
    std::string m_dest_bucket;  // Destination bucket information    
    std::string m_dest_storage_class;  // Storage class. Enumerated values: `STANDARD`, `STANDARD_IA`.
```

## Querying Cross-Bucket Replication

#### Feature description

This API (GET Bucket replication) is used to query the cross-bucket replication rule of a bucket.

#### Method prototype

```
CosResult GetBucketReplication(const GetBucketReplicationReq& request, GetBucketReplicationResp* response);
```


#### Sample request

```
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::GetBucketReplicationReq req(bucket_name);
qcloud_cos::GetBucketReplicationResp resp;

qcloud_cos::CosResult result = cos.GetBucketReplication(req, &resp);

if (result.IsSucc()) {
    // Request successful. You can call the `resp` method to obtain the cross-bucket replication rule.
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------------|-------------------------| ------|
| req  | Request of the `GetBucketReplication` operation | GetBucketReplicationReq | Yes |
| resp | Response of the `GetBucketReplication` operation | GetBucketReplicationResp| Yes |

`GetBucketReplicationResp` provides the following methods to obtain the cross-bucket replication rules.



```
std::string GetRole() const;
std::vector<ReplicationRule> GetRules() const;
```



## Deleting Cross-Bucket Replication

#### Feature description

This API (DELETE Bucket replication) is used to delete the cross-bucket replication rule of a bucket.

#### Method prototype

```
CosResult DeleteBucketReplication(const DeleteBucketReplicationReq& request, DeleteBucketReplicationResp* response);
```


#### Sample request

```
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::DeleteBucketReplicationReq req(bucket_name);
qcloud_cos::DeleteBucketReplicationResp resp;

qcloud_cos::CosResult result = cos.DeleteBucketReplication(req, &resp);

if (result.IsSucc()) {
    // Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ---------------------------------|----------------------------| ------|
| req  | Request of the `DeleteBucketReplication` operation | DeleteBucketReplicationReq | Yes |
| resp | Response of the `DeleteBucketReplication` operation | DeleteBucketReplicationResp | Yes |
