
## Overview

This document provides an overview of APIs and SDK code samples related to global acceleration.

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :------------------------------- |
| [PUT Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33411)| Setting global acceleration | Enables/Suspends global acceleration for a bucket |
| [GET Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33412)| Querying global acceleration | Queries the global acceleration configuration of a bucket |


## Setting Global Acceleration

#### API description

This API is used to enable or suspend global acceleration.

#### Method prototype

```go
func (s *BucketService) PutAccelerate(ctx context.Context, opt *BucketPutAccelerateOptions) (*Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-put-accelerate"
```go
opt := &cos.BucketPutAccelerateOptions{
    Status: "Enabled",
    Type:   "COS",
}
_, err = c.Bucket.PutAccelerate(context.Background(), opt)
if err != nil {
    // ERROR
}
```
#### Parameter description

```go
type BucketPutAccelerateOptions struct {
    Status  string
}
```
| Parameter | Description | Type | Required |
| -------- | ---------------------------------------------------- | ------ | ---- |
| Status   | Whether to enable global acceleration. Valid values: `Suspended`, `Enabled` | string | Yes   |

### Querying global acceleration

#### API description

This API is used to query the global acceleration configuration of a bucket.

#### Method prototype

```go
func (s *BucketService) GetAccelerate(ctx context.Context) (*BucketGetAccelerateResult, *Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-get-accelerate"
```go
res, _, err = c.Bucket.GetAccelerate(context.Background())
if err != nil {
    // ERROR
}
```
#### Response description

```go
type BucketGetAccelerateResult struct {
    Status  string
}
```
| Parameter | Description | Type | Required |
| -------- | ---------------------------------------------------- | ------ | ---- |
| Status   | Whether global acceleration is enabled. Valid values: `Suspended`, `Enabled` | string | Yes   |
