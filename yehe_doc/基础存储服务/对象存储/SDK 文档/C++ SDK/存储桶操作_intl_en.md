## Overview

This document provides an overview of APIs and SDK code samples for basic bucket operations.


| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://www.tencentcloud.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://www.tencentcloud.com/document/product/436/7738) | Creating a bucket | Creates bucket under a specified account |
| [HEAD Bucket](https://www.tencentcloud.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://www.tencentcloud.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |


## Querying a Bucket List

#### Feature description

This API is used to query the list of all buckets under a specified account.

#### Method prototype

```cpp
CosResult GetService(const GetServiceReq& request, GetServiceResp* response)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Replace it with your bucket name, which is in the format of BucketName-APPID (APPID is required). It can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.

qcloud_cos::GetServiceReq req;
qcloud_cos::GetServiceResp resp;
qcloud_cos::CosResult result = cos.GetService(req, &resp);

// The call is successful. You can call the resp member functions to get the return content.
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
    // You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ---------------------|---------------| ------|
| req  | Request of the `GetService` operation | GetServiceReq | Yes |
| resp | Response of the `GetService` operation | GetServiceResp | Yes |


`GetServiceResp` provides the following member functions to obtain the specific content (in XML format) returned by `Get Service`. 

```C++
// Get bucket owner information
Owner GetOwner() const;
// Get list information for all buckets
std::vector<Bucket> GetBuckets() const
```

Owner is defined as follows:

```cpp
struct Owner {
    std::string m_id;    // ID of the bucket owner
    std::string m_display_name; // Bucket owner name
}; 
```

Bucket is defined as follows:

```cpp
// Describe the information of a single bucket                                                                                                                                                                    
struct Bucket {
    std::string m_name; // Bucket name
    std::string m_location; // Bucket region
    std::string m_create_date; // Bucket creation time in ISO 8601 format, such as 2016-11-09T08:46:32.000Z
};
```



## Creating a Bucket

#### Feature description

This API (PUT Bucket) is used to create a bucket.

#### Method prototype

```cpp
CosResult PutBucket(const PutBucketReq& req, PutBucketResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Replace it with your bucket name, which is in the format of BucketName-APPID (APPID is required). It can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.

qcloud_cos::PutBucketReq req(bucket_name);
// Set an MAZ bucket as follows
//req.SetMAZBucket();
qcloud_cos::PutBucketResp resp;
qcloud_cos::CosResult result = cos.PutBucket(req, &resp);

// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | --------------------|--------------| ------|
| req  | Request of the `PutBucket` operation | PutBucketReq | Yes |
| resp | Response of the `PutBucket` operation | PutBucketResp | Yes |


`PutBucketReq` provides the following member functions:

```C++
// Define the ACL attribute of the bucket. Valid values: private, public-read-write, public-read
// Default: private
void SetXCosAcl(const std::string& str);

// Grant read permission in the format of x-cos-grant-read: id=" ",id=" ".
// To authorize a sub-account, use id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>".
// To authorize the root account, use id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>".
void SetXCosGrantRead(const std::string& str);

// Grant write permission in the format: x-cos-grant-write: id=" ",id=" "./
// To authorize a sub-account, use id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// To authorize the root account, use id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>".
void SetXCosGrantWrite(const std::string& str);
    
// Grant read-write permission in the format: x-cos-grant-full-control: id=" ",id=" ".
// To authorize a sub-account, use id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>".
// To authorize the root account, use id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>".
void SetXCosGrantFullControl(const std::string& str);
```

## Checking a Bucket and Its Permissions

#### Feature description

This API is used to check whether a bucket exists and whether you have permission to access it.

#### Method prototype

```C++
CosResult HeadBucket(const HeadBucketReq& req, HeadBucketResp* resp)
```

#### Sample request

```C++
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Replace it with your bucket name, which is in the format of BucketName-APPID (APPID is required). It can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.

qcloud_cos::HeadBucketReq req(bucket_name);
qcloud_cos::HeadBucketResp resp;
qcloud_cos::CosResult result = cos.HeadBucket(req, &resp);

// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ---------------------| --------------| ------|
| req  | Request of the `HeadBucket` operation | HeadBucketReq | Yes |
| resp | Response of the `HeadBucket` operation | HeadBucketResp | Yes |


## Deleting a Bucket

#### Feature description

This API is used to delete an empty bucket under a specified account.

#### Method prototype

```cpp
CosResult DeleteBucket(const DeleteBucketReq& req, DeleteBucketResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.

// The bucket_name is required in the constructor of DeleteBucketReq
qcloud_cos::DeleteBucketReq req(bucket_name);
qcloud_cos::DeleteBucketResp resp;
qcloud_cos::CosResult result = cos.DeleteBucket(req, &resp);

// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | -----------------------| ----------------| ------|
| req  | Request of the `DeleteBucket` operation | DeleteBucketReq | Yes |
| resp | Response of the `DeleteBucket` operation | DeleteBucketResp | Yes |
