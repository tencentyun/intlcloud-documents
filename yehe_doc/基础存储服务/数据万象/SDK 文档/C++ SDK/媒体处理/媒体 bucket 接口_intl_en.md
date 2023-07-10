## Overview

This document provides an overview of APIs and SDK code samples for media buckets.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
| [DescribeMediaBuckets](https://intl.cloud.tencent.com/document/product/436/46909) | Querying media processing activation status | Queries buckets with media processing enabled   |


## Querying Media Processing Activation Status

#### Feature description

This API is used to query buckets with media processing enabled.

#### Method prototype

```cpp
CosResult DescribeMediaBuckets(const DescribeMediaBucketsReq& request, DescribeMediaBucketsResp* response);
```

#### Sample code

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
DescribeMediaBucketsReq req;
DescribeMediaBucketsResp resp;
req.SetRegions("ap-guangzhou");
// Set the bucket name. To specify multiple bucket names, separate them with commas. Exact search is supported.
// req.SetBucketNames("xxx");
// Set the bucket name prefix for prefix search
// req.SetBucketName("xxx");
// Set the page number
// req.SetPageNumber();
// Set the number of entries per page
// req.SetPageSize();
CosResult result = cos.DescribeMediaBuckets(req, &resp);
qcloud_cos::CosResult result = cos.GetObject(req, &resp);
if (result.IsSucc()) {
   // The call is successful. You can call the `resp` member functions to get the return content.
   std::cout << "Result: " << resp.GetResult().to_string() << std::endl;
} else {
   // The call failed. You can call the `result` member functions to get the error information.
} 
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------- | ------------------ |
| request     | Operation request.                                              | DescribeMediaBucketsReq | Yes |
| response | Operation response.                                    | DescribeMediaBucketsResp | Yes |

