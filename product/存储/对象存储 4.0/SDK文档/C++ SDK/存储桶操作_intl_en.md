## Overview

This document provides an overview of APIs related to basic bucket operations and access control list (ACL) and corresponding SDK sample code.

**Basic operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for the specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a bucket |

## Basic Operations

### Querying Bucket List

#### Feature Description

This API is used to query the list of all buckets under the specified account.

#### Method Prototype

```cpp
CosResult GetService(const GetServiceReq& request, GetServiceResp* response)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::GetServiceReq req;
qcloud_cos::GetServiceResp resp;
qcloud_cos::CosResult result = cos.GetService(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    const qcloud_cos::Owner& owner = resp.GetOwner();
    const std::vector<qcloud_cos::Bucket>& buckets = resp.GetBuckets();
    std::cout << "owner.m_id=" << owner.m_id << ", owner.display_name=" << owner.m_display_name << std::endl;               
     for (std::vector<qcloud_cos::Bucket>::const_iterator itr = buckets.begin(); itr != buckets.end(); ++itr) {
     	const qcloud_cos::Bucket& bucket = *itr;
     	std::cout << "Bucket name=" << bucket.m_name << ", location=" 
     	<< bucket.m_location << ", create_date=" << bucket.m_create_date << std::endl;                                  
     } 
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------- |
| req | GetServiceReq, which is the request for the GetServiceReq operation |
| resp | GetServiceResp, which is the return of the GetService operation |

GetServiceResp provides the following member functions for getting the specific content in XML format returned by Get Service. 

```C++
// Get bucket owner information
Owner GetOwner() const;
// Get list information of all buckets
std::vector<Bucket> GetBuckets() const
```

Owner is defined as follows:

```cpp
struct Owner {
	std::string m_id;	// Bucket owner ID
	std::string m_display_name; // Bucket owner name
}; 
```

Bucket is defined as follows:

```cpp
// Describe the information of a single bucket                                                                                                                                                                    
struct Bucket {
	std::string m_name; // Bucket name
	std::string m_location; // Bucket region
	std::string m_create_date; // Bucket creation time in ISO8601 format, such as 2016-11-09T08:46:32.000Z
};
```



### Creating a Bucket

#### Feature Description

This API (PUT Bucket) is used to created a bucket.

#### Method Prototype

```cpp
CosResult PutBucket(const PutBucketReq& req, PutBucketResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::PutBucketReq req(bucket_name);
qcloud_cos::PutBucketResp resp;
qcloud_cos::CosResult result = cos.PutBucket(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ----------------------------------- |
| req  | PutBucketReq, which is the request for the PutBucket operation  |
| resp | PutBucketResp, which is the return of the PutBucket operation |

PutBucketReq provides the following member functions:

```C++
// Define the ACL attribute of the bucket. Value range: private, public-read-write, public-read
// Default value: private
void SetXCosAcl(const std::string& str);

// Grant the grantee read permission in the format of x-cos-grant-read: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantRead(const std::string& str);

// Grant the grantee write permission in the format of x-cos-grant-write: id=" ",id=" "./
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantWrite(const std::string& str);
    
// Grant the grantee read-write permission in the format of x-cos-grant-full-control: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantFullControl(const std::string& str);
```

### Checking a Bucket and Its Permission

#### Feature Description

This API is used to check whether a bucket exists and you have permission to access it.

#### Method Prototype

```C++
CosResult HeadBucket(const HeadBucketReq& req, HeadBucketResp* resp)
```

#### Sample Request

```C++
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::HeadBucketReq req(bucket_name);
qcloud_cos::HeadBucketResp resp;
qcloud_cos::CosResult result = cos.HeadBucket(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------- |
| req  | HeadBucketReq, which is the request for the HeadBucket operation  |
| resp | HeadBucketResp, which is the return of the HeadBucket operation |

### Deleting a Bucket

#### Feature Description

This API is used to delete an empty bucket under the specified account.

#### Method Prototype

```cpp
CosResult DeleteBucket(const DeleteBucketReq& req, DeleteBucketResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of DeleteBucketReq requires bucket_name to be passed in
qcloud_cos::DeleteBucketReq req(bucket_name);
qcloud_cos::DeleteBucketResp resp;
qcloud_cos::CosResult result = cos.DeleteBucket(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ---------------------------------------- |
| req  | DeleteBucketReq, which is the request for the DeleteBucket operation |
| resp | DeletBucketResp, which is the return of the DeletBucket operation |

## ACL

### Setting Bucket ACL

#### Feature Description

This API is used to set the access control list (ACL) for the specified bucket.

#### Method Prototype

```cpp
CosResult PutBucketACL(const DPutBucketACLReq& req, PutBucketACLResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of PutBucketACLReq requires bucket_name to be passed in
qcloud_cos::PutBucketACLReq req(bucket_name);
qcloud_cos::ACLRule rule;
rule.m_id = "123";
rule.m_allowed_headers.push_back("x-cos-meta-test");
rule.m_allowed_origins.push_back("http://www.qq.com");
rule.m_allowed_origins.push_back("http://intl.cloud.tentent.com");
rule.m_allowed_methods.push_back("PUT");
rule.m_allowed_methods.push_back("GET");
rule.m_max_age_secs = "600";
rule.m_expose_headers.push_back("x-cos-expose");
req.AddRule(rule);

qcloud_cos::PutBucketACLResp resp;
qcloud_cos::CosResult result = cos.PutBucketACL(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // Set the ACL. You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ----------------------------------------- |
| req  | PutBucketACLReq, which is the request for the PutBucketACL operation |
| resp | PutBucketACLResp, which is the return of the PutBucketACL operation |

PutBucketACLReq provides the following member functions:

```
// Define the ACL attribute of the bucket. Value range: private, public-read-write, public-read
// Default value: private
void SetXCosAcl(const std::string& str);

// Grant the grantee read permission in the format of x-cos-grant-read: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantRead(const std::string& str);

// Grant the grantee write permission in the format of x-cos-grant-write: id=" ",id=" "./
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantWrite(const std::string& str);

// Grant the grantee read-write permission in the format of x-cos-grant-full-control: id=" ",id=" ".
// When you need to authorize a sub-account, id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// When you need to authorize a root account, id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantFullControl(const std::string& str);

// Bucket owner ID
void SetOwner(const Owner& owner);

// Set the information of grantee and permission
void SetAccessControlList(const std::vector<Grant>& grants);

// Add the permission information of a single bucket
void AddAccessControlList(const Grant& grant);
        

```

> APIs such as SetXCosAcl, SetXCosGrantRead, SetXCosGrantWrite, and SetXCosGrantFullControl cannot be used together with SetAccessControlList or AddAccessControlList at the same time, because the former type is actually implemented by setting the HTTP header, while the latter type is to add content in XML format to the body. You can choose only one type of them. The former type is preferred within the SDK.

ACLRule is defined as follows:

```
struct Grantee {
    // The type can be RootAccount or SubAccount
    // If the type is RootAccount, you can enter an account ID in the uin field in the ID or enter anyone (representing all types of users) in place of uin/<OwnerUin> and uin/<SubUin>
    // If the type is RootAccount, uin represents the root account, while Subaccount represents the sub-account
    std::string m_type; 
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; // Optional
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; // Resource information of the grantee
    std::string m_perm; // Specify the permission granted to the grantee. Enumerated values: READ, WRITE, FULL_CONTROL
};
```

### Querying Bucket ACL

#### Feature Description

This API is used to query the access control list (ACL) of a bucket.

#### Method Prototype

```cpp
CosResult GetBucketACL(const DGetBucketACLReq& req, GetBucketACLResp* resp)
```

#### Sample Request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";

// The constructor of GetBucketACLReq requires bucket_name to be passed in
qcloud_cos::GetBucketACLReq req(bucket_name);
qcloud_cos::GetBucketACLResp resp;
qcloud_cos::CosResult result = cos.GetBucketACL(req, &resp);

// The call is successful. You can call the member function of resp to get the return content
if (result.IsSucc()) {
    // ...
} else {
    // Failed to get the ACL. You can call the member function of CosResult to output the error information such as requestID
} 
```

#### Parameter Descriptions

| Parameter | Description |
| ---- | ----------------------------------------- |
| req  | GetBucketACLReq, which is the request for the GetBucketACL operation |
| resp | GetBucketACLResp, which is the return of the GetBucketACL operation |

GetBucketACLResp provides the following member functions:

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();
```
