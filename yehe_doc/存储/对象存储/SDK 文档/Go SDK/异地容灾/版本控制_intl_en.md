## Overview

This document provides an overview of APIs and SDK code samples related to versioning.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning configuration of a bucket |

## Setting Versioning

#### Feature description

This API (PUT Bucket versioning) is used to set the versioning configuration for a bucket.

#### Method prototype
```go
func (s *BucketService) PutVersioning(ctx context.Context, opt *BucketPutVersionOptions) (*Response, error)
```

#### Sample request
[//]: # ".cssg-snippet-put-bucket-versioning"
```go
opt := &cos.BucketPutVersionOptions{
    // Enabled or Suspended; once enabled, versioning can only be paused but not deleted.
    Status: "Enabled",
}
_, err := client.Bucket.PutVersioning(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### Parameter description
```go
type BucketPutVersionOptions struct {
	Status  string
}
```
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| BucketPutVersionOptions | Versioning policies | struct |
| Status | Indicates whether versioning is enabled. Enumerated values: `Suspended` (versioning is paused), `Enabled` (versioning is enabled) | string |

## Querying Versioning

#### Feature description

This API (GET Bucket versioning) is used to query the versioning configuration of a bucket.

#### Method prototype
```go
func (s *BucketService) GetVersioning(ctx context.Context) (*BucketGetVersionResult, *Response, error)
```

#### Sample request
[//]: # ".cssg-snippet-get-bucket-versioning"
```go
_, _, err := client.Bucket.GetVersioning(context.Background())
if err != nil {
    panic(err)
}
```

#### Response description
```go
type BucketGetVersionResult struct {
	Status  string
}
```
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| BucketGetVersionResult | Versioning policies | struct |
| Status | Indicates whether versioning is enabled. Enumerated values: `Suspended` (versioning is paused), `Enabled` (versioning is enabled) | string |

