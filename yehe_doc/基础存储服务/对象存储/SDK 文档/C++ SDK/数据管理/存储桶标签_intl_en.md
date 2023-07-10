## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes a specified bucket tag |

## Setting a bucket tag

#### API description

This API (PUT Bucket tagging) is used to set tags for an existing bucket.

#### Method prototype

```cpp
CosResult PutBucketTagging(const PutBucketTaggingReq& request, PutBucketTaggingResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::PutBucketTaggingReq req(bucket_name);
qcloud_cos::PutBucketTaggingResp resp;

std::vector<Tag> tagset;
Tag tag1;
tag1.SetKey("age");
tag1.SetValue("19");

Tag tag2;
tag2.SetKey("name");
tag2.SetValue("xiaoming");
tagset.push_back(tag1);
tagset.push_back(tag2);
req.SetTagSet(tagset);

qcloud_cos::CosResult result = cos.PutBucketTagging(req, &resp);

if (result.IsSucc()) {
    // Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```


#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ---------------------------| --------------------| ------|
| req  | Request of the `PutBucketTagging` operation | PutBucketTaggingReq | Yes |
| resp | Response of the `PutBucketTagging` operation | PutBucketTaggingResp| Yes |



`PutBucketTaggingReq` provides the following method:

```
void SetTagSet(std::vector<Tag>& tagset)   // Set tagging.
```

`Tag` provides the following methods:

```cpp
class Tag {
    void SetKey(const std::string key);  // Set the key.
    void SetValue(const std::string value);  // Set the value.
```


## Querying Bucket Tags

#### API description

This API (GET Bucket tagging) is used to query the existing tags of a bucket.

#### Method prototype

```cpp
CosResult CosAPI::GetBucketTagging(const GetBucketTaggingReq& request, GetBucketTaggingResp* response);                                      
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::GetBucketTaggingReq req(bucket_name);
qcloud_cos::GetBucketTaggingResp resp;

qcloud_cos::CosResult result = cos.GetBucketTagging(req, &resp);

if (result.IsSucc()) {
    // Request successful. You can use the method of `resp` to obtain the bucket tags.
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

`GetBucketTaggingResp` provides the following method to obtain the bucket tags:

```
std::vector<Tag> GetTagSet() const;
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ---------------------------| --------------------| ------|
| req  | Request of the `GetBucketTagging` operation | GetBucketTaggingReq | Yes |
| resp | Response of the `GetBucketTagging` operation | GetBucketTaggingResp | Yes |



## Deleting Bucket Tags

#### API description 

This API (DELETE Bucket tagging) is used to delete the existing tags of a bucket.

#### Method prototype

```cpp
CosResult CosAPI::DeleteBucketTagging(const DeleteBucketTaggingReq& request, DeleteBucketTaggingResp* response);                              
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";
qcloud_cos::DeleteBucketTaggingReq req(bucket_name);
qcloud_cos::DeleteBucketTaggingResp resp;

qcloud_cos::CosResult result = cos.DeleteBucketTagging(req, &resp);

if (result.IsSucc()) {
    // Request successful
} else {
    // Request failed. You can call the CosResult member functions to output the error information, such as requestID.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------------------| -----------------------| ------|
| req  | Request of the `DeleteBucketTagging` operation | DeleteBucketTaggingReq | Yes |
| resp | Response of the `DeleteBucketTagging` operation | DeleteBucketTaggingResp | Yes |
