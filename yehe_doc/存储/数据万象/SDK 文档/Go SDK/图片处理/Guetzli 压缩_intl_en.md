
## Overview

This document provides an overview of APIs and SDK code samples for Guetzli compression.

| API | Description |
| :--------------- | :------------------ |
| [Enabling Guetzli compression](https://intl.cloud.tencent.com/document/product/1045/45583) | Enables the Guetzli compression feature for a bucket.   |
| [Querying Guetzli status](https://intl.cloud.tencent.com/document/product/1045/46329) | Queries whether the Guetzli compression feature is enabled. |
|[Disabling Guetzli compression](https://intl.cloud.tencent.com/document/product/1045/45584)  |   Disables the Guetzli compression feature.  |


## Enabling Guetzli Compression

#### Feature description

This API is used to enable the Guetzli compression feature for a bucket.

#### Method prototype

```go
func (s *CIService) PutGuetzli(ctx context.Context) (*Response, error)
```

#### Sample request

```go
// `CIURL` is required
u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
cu, _ := url.Parse("http://examplebucket-1250000000.pic.ap-guangzhou.myqcloud.com")
b := &cos.BaseURL{BucketURL: u, CIURL: cu}
c := cos.NewClient(b, &http.Client{
	Transport: &cos.AuthorizationTransport{
		SecretID:  os.Getenv("SECRETID"),
		SecretKey: os.Getenv("SECRETKEY"),
	},
})

_, err := c.CI.PutGuetzli(context.Background())
log_status(err)
```

## Querying Guetzli Status

#### Feature description

This API is used to query whether the Guetzli compression feature is enabled.

#### Method prototype

```go
func (s *CIService) GetGuetzli(ctx context.Context) (*GetGuetzliResult, *Response, error)
```

#### Sample request

```go
// `CIURL` is required
u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
cu, _ := url.Parse("http://examplebucket-1250000000.pic.ap-guangzhou.myqcloud.com")
b := &cos.BaseURL{BucketURL: u, CIURL: cu}
c := cos.NewClient(b, &http.Client{
	Transport: &cos.AuthorizationTransport{
		SecretID:  os.Getenv("SECRETID"),
		SecretKey: os.Getenv("SECRETKEY"),
	},
})

res, _, err := c.CI.GetGuetzli(context.Background())
if err == nil {
	fmt.Printf("%v\n", res.GuetzliStatus)
}
```

#### Response description

```go
type GetGuetzliResult struct {
    GuetzliStatus string
}
```

| Node Name            | Description                                                         | Type      |
| :------------ | :------------------------------------------------------ | :----- |
| GuetzliStatus | Whether to enable the Guetzli compression feature: `on` or `off` | String |

## Disabling Guetzli Compression

This API is used to disable the Guetzli compression feature.

#### Method prototype

```go
func (s *CIService) DeleteGuetzli(ctx context.Context) (*Response, error)
```

#### Sample request

```go
// `CIURL` is required
u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
cu, _ := url.Parse("http://examplebucket-1250000000.pic.ap-guangzhou.myqcloud.com")
b := &cos.BaseURL{BucketURL: u, CIURL: cu}
c := cos.NewClient(b, &http.Client{
	Transport: &cos.AuthorizationTransport{
		SecretID:  os.Getenv("SECRETID"),
		SecretKey: os.Getenv("SECRETKEY"),
	},
})

_, err := c.CI.DeleteGuetzli(context.Background())
```

