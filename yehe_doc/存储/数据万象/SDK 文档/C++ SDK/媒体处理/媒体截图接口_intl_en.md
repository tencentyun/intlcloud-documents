## Overview

This document provides an overview of APIs and SDK code samples for media screenshot.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|   [GetSnapshot](https://intl.cloud.tencent.com/document/product/436/46912)     |  Querying screenshot |   Query the screenshot of media file at some time point     |


## Querying Screenshot

#### Feature description

This API is used to get a screenshot of a media file at some time point and put the screenshot information in a local file.

#### Method prototype

```cpp
CosResult GetSnapshot(const GetSnapshotReq& request, GetSnapshotResp* response);
```

#### Sample code

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
GetSnapshotReq req(bucket_name, object_name, local_file);
GetSnapshotResp resp;
req.SetTime(100);
// Set the screenshot width
// req.SetWitdh(xxx);
// Set the screenshot height
// req.SetHeight(xxx);
// Set the format
// req.SetFormat(xxx);
CosResult result = cos.GetSnapshot(req, &resp);
if (result.IsSucc()) {
   // The call is successful. You can call the `resp` member functions to get the return content.
} else {
   // The call failed. You can call the `result` member functions to get the error information.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ---------- | --------------- | -------- |
| request  | Operation request. | GetSnapshotReq  | Yes       |
| response | Operation response. | GetSnapshotResp | Yes       |
