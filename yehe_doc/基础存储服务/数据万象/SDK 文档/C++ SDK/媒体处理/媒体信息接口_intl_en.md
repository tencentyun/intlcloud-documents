## Overview

This document provides an overview of APIs and SDK code samples for media information.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|  [GetMediaInfo](https://intl.cloud.tencent.com/document/product/436/46915)    |   Querying file information | Queries media file information      |


## Querying File Information

#### Feature description

This API is used to get media file information.

#### Method prototype

```cpp
CosResult GetMediaInfo(const GetMediaInfoReq& request, GetMediaInfoResp* response);
```

#### Sample code

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
GetMediaInfoReq req(bucket_name, object_name);
GetMediaInfoResp resp;
CosResult result = cos.GetMediaInfo(req, &resp);
if (result.IsSucc()) {
   // The call is successful. You can call the `resp` member functions to get the return content.
   std::cout << "Result: " << resp.GetResult().to_string() << std::endl;
} else {
   // The call failed. You can call the `result` member functions to get the error information.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ---------- | ---------------- | -------- |
| request  | Operation request.  | GetMediaInfoReq  | Yes       |
| response | Operation response. | GetMediaInfoResp | Yes       |