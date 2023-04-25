## Overview

This document provides an overview of APIs and SDK code samples related to bucket policies.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://www.tencentcloud.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for the specified bucket |
| [GET Bucket policy](https://www.tencentcloud.com/document/product/436/8276) | Querying bucket policy | Queries the permission policy of the specified bucket |
| [DELETE Bucket policy](https://www.tencentcloud.com/document/product/436/8285) | Deleting a bucket policy | Deletes the permission policy of a specified bucket |

## Setting a bucket policy

#### Feature description

This API (PUT Bucket policy) is used to write a permission policy for a bucket. The policy passed in this API will overwrite the existing one (if any) in the bucket.

#### Method prototype
```cpp
CosResult PutBucketPolicy(const PutBucketPolicyReq& req, PutBucketPolicyResp* resp)
```

#### Sample request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Replace it with your bucket name, which is in the format of BucketName-APPID (APPID is required). It can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.

qcloud_cos::PutBucketPolicyReq req(bucket_name);
qcloud_cos::PutBucketPolicyResp resp;
std::string bucket_policy = 
"  {"
"    \"Statement\": ["
"      {"
"        \"Principal\": {"
"          \"qcs\": ["
"            \"qcs::cam::uin/100000000001:uin/100000000011\"" // Replace with the UIN of the account to be granted the permission.
"          ]\n"
"        },\n"
"        \"Effect\": \"allow\","
"        \"Action\": ["
"          \"cos:PutObject\""
"        ],\n"
"        \"Resource\": [" // Change it to the allowed path prefix (such as "a.jpg", "a/*", or "*"). You can determine the upload path based on your login status. (Keep in mind that using asterisks (*) could bring high risks.)
"          \"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/exampleobject\""
"        ],\n"
"        \"Condition\": {"
"          \"string_equal\": {"
"            \"cos:x-cos-mime-limit\": \"image/jpeg\""
"          }"
"        }"
"      }"
"    ],"
"    \"Version\": \"2.0\""
"  }";

req.SetBody(bucket_policy);
qcloud_cos::CosResult result = cos.PutBucketPolicy(req, &resp);

if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Parameter description

| Parameter | Description | Required |
| ----| ---- | ---- |
| Statement | Specifies one or more permissions | Yes |
| Version | The policy syntax version. Default value: 2.0 | Yes |
| Principal | Entity to which the permission is granted. For more information, see [Access Policy Language Overview](https://www.tencentcloud.com/document/product/436/18023) | Yes |
| Action | COS API. You can specify one, several, or all (`*`) COS APIs as needed. An example value is `name/cos:GetService`. **Note that this parameter is case-sensitive**. | Yes |
| Effect | `allow` or `deny` | Yes |
| Resource | Specific data authorized to be operated on. It can be any resource, a resource in a path with a specified prefix, a resource in a specified absolute path, or a combination thereof. | Yes |
| Condition | Condition (this value is optional). For more information, see [Condition](https://www.tencentcloud.com/document/product/598/10603) | No |

## Querying a bucket policy

#### Feature description

This API (GET Bucket policy) is used to read the permission policy of a bucket.

#### Method prototype

```cpp
CosResult GetBucketPolicy(const GetBucketPolicyReq& req, GetBucketPolicyResp* resp)
```

#### Sample request
```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Replace it with your bucket name, which is in the format of BucketName-APPID (APPID is required). It can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.

qcloud_cos::GetBucketPolicyReq req(bucket_name);
qcloud_cos::GetBucketPolicyResp resp;
qcloud_cos::CosResult result = cos.GetBucketPolicy(req, &resp);

// The call is successful. You can call the resp member functions to get the return content.
if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 
```

#### Response description
`GetBucketPolicyResp` provides the following member functions to obtain the `Policy` content returned by `Get Bucket Policy`.
```cpp
std::string resp.GetPolicy()
```

## Deleting a bucket policy

#### Feature description

This API (DELETE Bucket policy) is used to delete the permission policy of a bucket.

#### Method prototype

```cpp
CosResult DeleteBucketPolicy(const DeleteBucketPolicyReq& req, DeleteBucketPolicyResp* resp)
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Replace it with your bucket name, which is in the format of BucketName-APPID (APPID is required). It can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.

qcloud_cos::DeleteBucketPolicyReq req(bucket_name);
qcloud_cos::DeleteBucketPolicyResp resp;
qcloud_cos::CosResult result = cos.DeleteBucketPolicy(req, &resp);

if (result.IsSucc()) {
    // ...
} else {
    // You can call the CosResult member functions to output the error information, such as requestID
} 

```
