## Overview

This document provides an overview of APIs and SDK code samples for original image protection.

| API | Description |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Enabling original image protection](https://intl.cloud.tencent.com/document/product/1045/33711) | Enables the original image protection feature for a bucket.   |
| [Querying original image protection status](https://intl.cloud.tencent.com/document/product/1045/33710) | Queries whether the original image protection feature is enabled. |
| [Disabling original image protection](https://intl.cloud.tencent.com/document/product/1045/33712) | Disables the original image protection feature.   |


## Enabling Original Image Protection

#### Feature description

This API is used to enable the original image protection feature for a bucket.

#### Method prototype

```go
func (s *CIService) OpenOriginProtect(ctx context.Context) (*Response, error)
```

#### Sample request

```go
_, err := c.CI.OpenOriginProtect(context.Background())
```

## Querying Original Image Protection Status

#### Feature description

This API is used to query whether the original image protection feature is enabled.

#### Method prototype

```go
func (s *CIService) GetOriginProtect(ctx context.Context) (*OriginProtectResult, *Response, error)
```

#### Sample request

```go
res, _, err := c.CI.GetOriginProtect(context.Background())
```

#### Parameter description

| Parameter | Description |
| --------- | ------------------------------------------------------------ |
| OriginProtectResult  | Whether original image protection is enabled |

## Disabling Original Image Protection

#### Feature description

This API is used to disable the original image protection feature.

#### Method prototype

```go
func (s *CIService) CloseOriginProtect(ctx context.Context) (*Response, error)
```

#### Sample request

```go
_, err := c.CI.CloseOriginProtect(context.Background())
```
