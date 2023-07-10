## Overview

This document provides an overview of APIs and SDK code samples related to the access control lists (ACLs) for buckets and objects.

**Bucket ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting a bucket ACL | Sets an ACL for a bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying a bucket ACL | Queries the ACL of a bucket |

**Object ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for an object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

## Bucket ACL
### Setting a bucket ACL

#### API description

This API (PUT Bucket acl) is used to set an ACL for a bucket. This operation will overwrite existing permission configurations. ACL includes predefined permission policies (CannedAccessControlList) or custom permission policies (AccessControlList). If both types of policies are set, predefined policies are ignored and custom policies will be used.

#### Method prototype

```cpp
CosResult PutBucketACL(const PutBucketACLReq& request, PutBucketACLResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

// bucket_name needs to be passed to the constructor of PutBucketACLReq.
qcloud_cos::PutBucketACLReq req(bucket_name);
qcloud_cos::PutBucketACLResp resp;

// Set the ACL through either the body or the header. Using both will cause a conflict.
// 1. Set the ACL through the header.
req.SetXCosAcl("public-read-write");

// 2. Set the ACL through the body.
qcloud_cos::Owner owner = {"qcs::cam::uin/00000000001:uin/00000000001", "qcs::cam::uin/00000000001:uin/00000000001" };
qcloud_cos::Grant grant;
req.SetOwner(owner);
grant.m_grantee.m_type = "Group";
grant.m_grantee.m_uri = "http://cam.qcloud.com/groups/global/AllUsers";
grant.m_perm = "READ";
req.AddAccessControlList(grant);

qcloud_cos::PutBucketACLResp resp;
qcloud_cos::CosResult result = cos.PutBucketACL(req, &resp);

if (result.IsSucc()) {
    // Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------| ----------------| ------|
| req  | Request of the `PutBucketACL` operation | PutBucketACLReq | Yes |
| resp | Response of the `PutBucketACL` operation | PutBucketACLResp | Yes |

`PutBucketACLReq` contains the following member function:

```
// Define the ACL attribute of the bucket. Valid values: private, public-read-write, public-read
// Default: private
void SetXCosAcl(const std::string& str);

// Grant read permission in the format of x-cos-grant-read: id=" ",id=" ".
// To authorize a sub-account, use id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// To authorize the root account, use id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantRead(const std::string& str);

// Grant write permission in the format of x-cos-grant-write: id=" ",id=" "./
// To authorize a sub-account, use id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// To authorize the root account, use id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantWrite(const std::string& str);

// Grant read-write permission in the format of x-cos-grant-full-control: id=" ",id=" ".
// To authorize a sub-account, use id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// To authorize the root account, use id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantFullControl(const std::string& str);

// ID of the bucket owner
void SetOwner(const Owner& owner);

// Set the grantee and permission to grant.
void SetAccessControlList(const std::vector<Grant>& grants);

// Add authorization for a single bucket.
void AddAccessControlList(const Grant& grant);

```

> !APIs such as `SetXCosAcl`, `SetXCosGrantRead`, `SetXCosGrantWrite`, and `SetXCosGrantFullControl` cannot be used together with `SetAccessControlList` or `AddAccessControlList`. This is because the former type is implemented with HTTP headers, while the latter is implemented by adding XML content to the body. The former type is preferred in the SDK.

Classes involved in this request are defined as follows:

```
struct Owner {
    // Information about the bucket owner
    std::string m_id; // Complete ID of the owner, formatted as qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name;  // Name of the owner
};

struct Grantee {
    // "type" can be RootAccount or SubAccount.
    // If the type is “RootAccount”, enter the account ID in the “uin” field or enter "anyone" (representing all types of user) to replace “uin/<OwnerUin>” and “uin/<SubUin>”.
    // When “type” is “RootAccount”, “uin” represents the root account and “Subaccount” the sub-account.
    std::string m_type; 
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; // Optional
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; // Information about the grantee
    std::string m_perm; // Permission granted. Valid values: "READ", "WRITE", "FULL_CONTROL"
};

```

### Querying a bucket ACL

#### API description

This API is used to query the ACL of a bucket.

#### Method prototype

```cpp
CosResult GetBucketACL(const GetBucketACLReq& req, GetBucketACLResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::GetBucketACLReq req(bucket_name);
qcloud_cos::GetBucketACLResp resp;
qcloud_cos::CosResult result = cos.GetBucketACL(req, &resp);

if (result.IsSucc()) {
    // Request successful. You can call the resp member functions to get the content returned.
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 

```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------| ----------------| ------|
| req  | Request of the `GetBucketACL` operation  | GetBucketACLReq | Yes |
| resp | Response of the `GetBucketACL` operation | GetBucketACLResp | Yes |


`GetBucketACLResp` contains the following member functions:

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();
```

## Object ACL


### Setting an object ACL

#### API description

This API is used to set an ACL for a specified object in a bucket.

> !You can configure up to 1,000 bucket ACLs. Do not set object ACL control unless absolutely necessary. The object inherits bucket permissions by default.

There are two types of ACL policies: predefined ACLs (CannedAccessControlList) and custom ACLs (AccessControlList). If both of them are set, the custom ACL prevails over the predefined ACL.

#### Method prototype

```cpp
CosResult PutObjectACL(const PutObjectACLReq& req, PutObjectACLResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test";

// 1. Set the ACL configuration (through the body. You can set the ACL through either the body or header, but you may only use one of these two methods; otherwise, a conflict will occur)
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);
    qcloud_cos::Owner owner = {"qcs::cam::uin/xxxxx:uin/xxx", "qcs::cam::uin/xxxxxx:uin/xxxxx" };
    qcloud_cos::Grant grant;
    req.SetOwner(owner);
    grant.m_grantee.m_type = "Group";
    grant.m_grantee.m_uri = "http://cam.qcloud.com/groups/global/AllUsers";
    grant.m_perm = "READ";
    req.AddAccessControlList(grant);

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    if (result.IsSucc()) {
        // Request successful
    } else {
        // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
    } 
}   

// 2. Set the ACL configuration (through the header. You can set the ACL through either the body or header, but you may only use one of these two methods; otherwise, a conflict will occur)
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);                                                                                                                    
    req.SetXCosAcl("public-read-write");

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    if (result.IsSucc()) {
        // Request successful
    } else {
        // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
    } 
}   
```


#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------| -----------------| ------|
| req  | Request of the `PutObjectACL` operation | PuttObjectACLReq | Yes |
| resp | Response of the `PutObjectACL` operation | PutObjectACLResp | Yes |


`PutObjectACLReq` contains the following member functions:

```
// Define the ACL attribute of the object. Valid values: private, public-read
// Default: private
void SetXCosAcl(const std::string& str);

// Grant read permission in the format: id="[OwnerUin]" 
void SetXCosGrantRead(const std::string& str);

// Grant full permission in the format: id="[OwnerUin]"
void SetXCosGrantFullControl(const std::string& str);

// ID of the object owner
void SetOwner(const Owner& owner);

// Set the grantee and permission to grant.
void SetAccessControlList(const std::vector<Grant>& grants);

// Add authorization for a single object.
void AddAccessControlList(const Grant& grant);

```

> !APIs such as `SetXCosAcl`, `SetXCosGrantRead/SetXCosGrantWrite`, and `SetXCosGrantFullControl` cannot be used together with `SetAccessControlList` or `AddAccessControlList`. This is because the former type is implemented with HTTP headers, while the latter is implemented by adding XML content to the body. The former type is preferred in the SDK.

`ACLRule` is defined as follows:

```
struct Grantee {
    // "type" can be RootAccount or SubAccount.
    // If the type is “RootAccount”, enter the account ID in the “uin” field or enter "anyone" (representing all types of user) to replace “uin/<OwnerUin>” and “uin/<SubUin>”.
    // When “type” is “RootAccount”, “uin” represents the root account and “Subaccount” the sub-account.
    std::string m_type; 
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; // Optional
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; // Information about the grantee
    std::string m_perm; // Permission granted. Valid values: "READ", "WRITE", "FULL_CONTROL"
};

```

### Querying an object ACL

#### API description

This API (GET Object acl) is used to query the ACL of an object.

#### Method prototype

```cpp
CosResult GetObjectACL(const GetObjectACLReq& req, GetObjectACLResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";

// Object_name needs to be passed to the constructor of GetObjectACLReq.
qcloud_cos::GetObjectACLReq req(bucket_name, object_name);
qcloud_cos::GetObjectACLResp resp;
qcloud_cos::CosResult result = cos.GetObjectACL(req, &resp);

if (result.IsSucc()) {
    // Request successful. You can call the resp member functions to get the content returned.
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------| ----------------| ------|
| req  | Request of the `GetObjectACL` operation | GetObjectACLReq | Yes |
| resp | Response of the `GetObjectACL` operation | GetObjectACLResp | Yes |


`GetObjectACLResp` contains the following member functions:

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();
```
