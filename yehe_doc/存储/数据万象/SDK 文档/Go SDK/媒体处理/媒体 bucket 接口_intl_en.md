## Overview

This document provides an overview of APIs and SDK code samples for media buckets.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
| [DescribeMediaBuckets](https://intl.cloud.tencent.com/document/product/436/46909) | Querying media processing activation status | Queries buckets with media processing enabled   |

## Querying Media Processing Activation Status

#### Feature description

This API is used to query buckets with media processing enabled.

>! The COS Go SDK version must be at least v0.7.32.

#### Method prototype

```go
func (s *CIService) DescribeMediaProcessBuckets(ctx context.Context, opt *DescribeMediaProcessBucketsOptions) (*DescribeMediaProcessBucketsResult, *Response, error)
```

#### Sample request
```go
// Set the request URL to `ci.<Region>.myqcloud.com`
cu, _ := url.Parse("https://ci.ap-guangzhou.myqcloud.com")
b := &cos.BaseURL{CIURL: cu}
c := cos.NewClient(b, &http.Client{
    Transport: &cos.AuthorizationTransport{
        SecretID:  "SECRETID",
        SecretKey: "SECRETKEY",
    })

opt := &cos.DescribeMediaProcessBucketsOptions{
    Regions: "ap-guangzhou",
}
res, _, err := c.CI.DescribeMediaProcessBuckets(context.Background(), opt)
if err != nil {
    // ERROR       
}
fmt.Printf("res: %+v\n", res)
```

#### Parameter description

```go
type DescribeMediaProcessBucketsOptions struct {
        Regions     string
        BucketNames string
        BucketName  string
        PageNumber  int
        PageSize    int
}
```

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :----- | :------- |
| Regions     |  Region information, such as `ap-shanghai` and `ap-beijing`. To specify multiple regions, separate them with commas. For more information, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). | string |  No    |
| BucketNames | Bucket name. To specify multiple bucket names, separate them with commas. Exact search is supported. | string | No |
| BucketName  | Bucket name prefix for prefix search.        | string |  No       |
| PageNumber  | Page number.                  |  string | No       |
| PageSize    | Number of entries per page.                | string | No       |

#### Response description

```go
type DescribeMediaProcessBucketsResult struct {
        RequestId       string
        TotalCount      int
        PageNumber      int
        PageSize        int
        MediaBucketList []MediaProcessBucket
}
type MediaProcessBucket struct {
        BucketId   string
        Region     string
        CreateTime string
}
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------------------ | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| TotalCount         | Response | Total number of media buckets.                | Int       |
| PageNumber         | Response | Current page number, which is the same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page, which is the same as `pageSize` in the request.   | Int       |
| MediaBucketList    | Response | Media bucket list.                | Container |

`MediaBucketList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------- | :---------------------- | :----- |
| BucketId           | Response.MediaBucketList | Bucket ID.               | String |
| Name               | Response.MediaBucketList | Bucket name, which is the same as `BucketId`. | String |
| Region             | Response.MediaBucketList | Bucket region.              | String |
| CreateTime         | Response.MediaBucketList | Creation time.                | String |


