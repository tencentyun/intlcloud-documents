## 简介

本文档提供关于盲水印的相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作描述                         |
| ------------------------------------------ | -------------------------- |
| 盲水印 | 对本地图片添加或提取盲水印并上传至存储桶 |


## 上传时添加盲水印

#### 功能说明

在上传图片时添加盲水印。

#### 方法原型

```cpp
CosResult PutImage(const PutImageByFileReq& request, PutImageByFileResp* response);
```

#### 请求示例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

PutImageByFileReq req(bucket_name, object_name, local_file);
PutImageByFileResp resp;

PicOperation pic_operation;
PicRules rule;
// 存储文件路径
rule.fileid = "/" + object_name + "_watermark";
// 盲水印图片地址，需要经过 URL 安全的 Base64 编码
std::string image = "http://" + bucket_name + ".cos.ap-guangzhou.myqcloud.com/" + object_name + "_watermark";
// 盲水印处理参数
rule.rule = "watermark/3/type/1/image/" + CodecUtil::Base64Encode(image);
pic_operation.AddRule(rule);

CosResult result = cos.PutImage(req, &resp);
if (result.IsSucc()) {
   // 调用成功，调用 resp 的成员函数获取返回内容
} else {
   // 调用失败，调用 result 的成员函数获取错误信息
} 
```

#### 参数说明

| 参数 | 参数描述           | 类型               | 是否必填 |
| ---- | ------------------ | ------------------ | -------- |
| req  | PutImage操作的请求 | PutImageByFileReq  | 是       |
| resp | PutImage操作的响应 | PutImageByFileResp | 是       |



## 下载时添加盲水印

#### 功能说明

在图片下载时添加盲水印。

#### 方法原型

```cpp
CosResult GetObject(const GetObjectByFileReq& request, GetObjectByFileResp* response);
```

#### 请求示例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

GetObjectByFileReq req(bucket_name, object_name, local_file);
GetObjectByFileResp resp;

// 盲水印文本
std::string watermark_text = "test";
// 盲水印参数，需要经过 URL 安全的 Base64 编码
std::string watermark_param = "watermark/3/type/3/text/" + CodecUtil::Base64Encode(watermark_text);
req.AddParam(watermark_param, "");

CosResult result = cos.GetObject(req, &resp);
if (result.IsSucc()) {
   // 调用成功，调用 resp 的成员函数获取返回内容
} else {
   // 调用失败，调用 result 的成员函数获取错误信息
} 
```

#### 参数说明

| 参数 | 参数描述           | 类型               | 是否必填 |
| ---- | ------------------ | ------------------ | -------- |
| req  | PutImage操作的请求 | PutImageByFileReq  | 是       |
| resp | PutImage操作的响应 | PutImageByFileResp | 是       |
