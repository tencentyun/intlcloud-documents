## 简介

本文档提供关于媒体信息接口的 API 概览和 SDK 示例代码。

| API                        |             操作名                     | 操作描述                                               |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|  [GetMediaInfo](https://intl.cloud.tencent.com/document/product/436/46915)    |   查询文件信息 |用于查询媒体文件的信息      |


## 查询文件信息

#### 功能说明

用于获取媒体文件的信息。

#### 方法原型

```cpp
CosResult GetMediaInfo(const GetMediaInfoReq& request, GetMediaInfoResp* response);
```

#### 示例代码

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
GetMediaInfoReq req(bucket_name, object_name);
GetMediaInfoResp resp;
CosResult result = cos.GetMediaInfo(req, &resp);
if (result.IsSucc()) {
   // 调用成功，调用 resp 的成员函数获取返回内容
   std::cout << "Result: " << resp.GetResult().to_string() << std::endl;
} else {
   // 调用失败，调用 result 的成员函数获取错误信息
} 
```

#### 参数说明

| 参数名称 | 参数描述   | 类型             | 是否必填 |
| -------- | ---------- | ---------------- | -------- |
| request  | 操作的请求 | GetMediaInfoReq  | 是       |
| response | 操作的响应 | GetMediaInfoResp | 是       |