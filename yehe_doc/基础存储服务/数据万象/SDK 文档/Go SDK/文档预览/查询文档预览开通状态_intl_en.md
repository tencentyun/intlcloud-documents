## Overview

This document provides an overview of APIs and SDK code samples for querying the file preview feature status.

| API  |	Description  |
|----|-----|
|  [Querying file preview feature status](https://intl.cloud.tencent.com/document/product/1045/47928)  | Queries whether the file preview feature is enabled for a bucket.  |


## Querying File Preview Feature Status

#### Feature description

This API (`DescribeDocProcessBuckets`) is used to query whether the file preview feature is enabled for a bucket.

#### Method prototype

```go
func (s *CIService) DescribeDocProcessBuckets(ctx context.Context, opt *DescribeDocProcessBucketsOptions) (*DescribeDocProcessBucketsResult, *Response, error)
```

#### Sample request

```go
BucketsOpt := &cos.DescribeDocProcessBucketsOptions{
	Regions: "ap-shanghai",
}
res, _, err := c.CI.DescribeDocProcessBuckets(context.Background(), BucketsOpt)
```

#### Parameter description

```go
type DescribeDocProcessBucketsOptions struct {
    Regions     string
    BucketNames string 
    BucketName  string
    PageNumber  int
    PageSize    int
}
```

| Parameter | Description | Type |
| ----------- | ------------------------------------------------------------ | ------ |
| Regions     | Region information, such as `ap-shanghai` and `ap-beijing`. To specify multiple regions, separate them with commas. For more information, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423).  | string |
| BucketNames | Bucket name. To specify multiple bucket names, separate them with commas. Exact search is supported. | string |
| BucketName  | Bucket name prefix for prefix search.                                     | string |
| PageNumber  | Page number.                                                       | int |
| pageSize    | Number of entries per page.                                                     | int |

#### Response description

```go
type DescribeDocProcessBucketsResult struct {
    RequestId     string
    TotalCount    int
    PageNumber    int
    PageSize      int
    DocBucketList []DocProcessBucket
}
type DocProcessBucket struct {
    BucketId      string
    Name          string
    Region        string
    CreateTime    string
    AliasBucketId string
}
```

| Parameter | Description | Type |
| ------------- | ------------------------------- | --------- |
| RequestId     | Unique ID of the request.                   | string    |
| TotalCount    | Total number of buckets with file preview enabled.            | int       |
| PageNumber    | Current page number, which is the same as `pageNumber` in the request. | int       |
| PageSize      | Number of entries per page, which is the same as `pageSize` in the request.   | int       |
| DocBucketList | List of buckets with file preview enabled.            | Container |
| BucketId      | Bucket ID.               | string |
| Name          | Bucket name, which is the same as `BucketId`. | string |
| Region        | Region.              | string |
| CreateTime    | Creation time.                | string |
| AliasBucketId | Bucket alias.              | string |
