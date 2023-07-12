## Overview

This document provides an overview of APIs and SDK code samples for CI.

| API | Description  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Binding CI](https://intl.cloud.tencent.com/document/product/1045/33701) | Activates the CI service, which needs to be bound to an existing COS bucket. |
| [Querying CI status](https://intl.cloud.tencent.com/document/product/1045/33702) | Queries whether the CI service has been activated for a bucket.  |
| [Unbinding CI](https://intl.cloud.tencent.com/document/product/1045/33703) | Unbinds the CI service from a bucket (the bucket and files in it will be retained in COS). |


## Binding CI

#### Feature description

This API is used to activate the CI service.

#### Method prototype

```go
func (s *CIService) OpenCIService(ctx context.Context) (*Response, error)
```

#### Sample request

```go
_, err := c.CI.OpenCIService(context.Background())
```

## Querying CI Status

#### Feature description

This API is used to query whether CI has been enabled for a bucket.

#### Method prototype

```go
func (s *CIService) GetCIService(ctx context.Context) (*CIServiceResult, *Response, error)
```

#### Sample request

```go
res, _, err := c.CI.GetCIService(context.Background())
```

#### Parameter description

| Parameter | Description |
| --------- | ------------------------------------------------------------ |
| CIServiceResult  | Whether the CI service is activated. |

## Unbinding CI

#### Feature description

This API is used to unbind the CI service from a bucket.

#### Method prototype

```go
func (s *CIService) CloseCIService(ctx context.Context) (*Response, error)
```

#### Sample request

```go
_, err := c.CI.CloseCIService(context.Background())
```
