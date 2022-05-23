## Overview

This document provides an overview of APIs and SDK code samples for blind watermarking.

| API | Description |
| ------------------------------------------ | -------------------------- |
| Blind watermarking | Adds blind watermark to or extracts blind watermark from local image and uploads it to bucket |


## Adding Blind Watermark During Upload

#### Feature description

This API is used to add a blind watermark when uploading images.

#### Method prototype

```cpp
CosResult PutImage(const PutImageByFileReq& request, PutImageByFileResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

PutImageByFileReq req(bucket_name, object_name, local_file);
PutImageByFileResp resp;

PicOperation pic_operation;
PicRules rule;
// File storage path
rule.fileid = "/" + object_name + "_watermark";
// URL-safe Base64-encoded URL of the blind watermark image
std::string image = "http://" + bucket_name + ".cos.ap-guangzhou.myqcloud.com/" + object_name + "_watermark";
// Blind watermark processing parameter
rule.rule = "watermark/3/type/1/image/" + CodecUtil::Base64Encode(image);
pic_operation.AddRule(rule);

CosResult result = cos.PutImage(req, &resp);
if (result.IsSucc()) {
   // The call is successful. You can call the `resp` member functions to get the return content.
} else {
   // The call failed. You can call the `result` member functions to get the error information.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ------------------ | -------- |
| req  | `PutImage` operation request. | PutImageByFileReq  | Yes       |
| resp | `PutImage` operation response. | PutImageByFileResp | Yes       |



## Adding Blind Watermark During Download

#### Feature description

This API is used to add a blind watermark when downloading images.

#### Method prototype

```cpp
CosResult GetObject(const GetObjectByFileReq& request, GetObjectByFileResp* response);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

GetObjectByFileReq req(bucket_name, object_name, local_file);
GetObjectByFileResp resp;

// Blind watermark text
std::string watermark_text = "test";
// URL-safe Base64-encoded blind watermark parameter
std::string watermark_param = "watermark/3/type/3/text/" + CodecUtil::Base64Encode(watermark_text);
req.AddParam(watermark_param, "");

CosResult result = cos.GetObject(req, &resp);
if (result.IsSucc()) {
   // The call is successful. You can call the `resp` member functions to get the return content.
} else {
   // The call failed. You can call the `result` member functions to get the error information.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---- | ------------------ | ------------------ | -------- |
| req  | `PutImage` operation request. | PutImageByFileReq  | Yes       |
| resp | `PutImage` operation response. | PutImageByFileResp | Yes       |
