## Overview

This document provides an overview of APIs and SDK code samples related to bucket referer allowlist or blocklist.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting a bucket referer | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying a bucket referer | Queries a bucket referer allowlist or blocklist |

## Setting a Bucket Referer

#### API description

This API (PUT Bucket referer) is used to set the referer allowlist/blocklist for a bucket.

#### Method prototype

```go
func (s *BucketService) PutReferer(ctx context.Context, opt *BucketPutRefererOptions) (*Response, error)
```

#### Sample request

```go
opt := &cos.BucketPutRefererOptions{
	Status:      "Enabled",
	RefererType: "White-List",
	DomainList: []string{
		"*.qq.com",
		"*.qcloud.com",
	},
	EmptyReferConfiguration: "Allow",
}
  
_, err := c.Bucket.PutReferer(context.Background(), opt)
```

#### Parameter description

```go
type BucketPutRefererOptions struct {
    Status                  string 
    RefererType             string 
    DomainList              []string 
    EmptyReferConfiguration string
}
```

| Parameter  | Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| Status   | Whether to enable hotlink protection. Enumerated values: `Enabled, `Disabled` | String |
| RefererType    | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String |
| DomainList | A list of domains, which can include ports, IPs, or asterisks (\*). You can set multiple domains. | Array |
| EmptyReferConfiguration |  Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` | String |

## Querying a Bucket Referer

#### API description

This API (GET Bucket referer) is used to query the referer allowlist/blocklist of a bucket.

#### Method prototype

```go
func (s *BucketService) GetReferer(ctx context.Context) (*BucketGetRefererResult, *Response, error)
```

#### Sample request

```go
res, _, err := c.Bucket.GetReferer(context.Background())
```

#### Response description

```go
type BucketGetRefererResult struct {
    Status                  string 
    RefererType             string 
    DomainList              []string 
    EmptyReferConfiguration string
}
```

| Parameter  | Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| Status   | Whether hotlink protection is enabled. Enumerated values: `Enabled, `Disabled` | String                                   |
| RefererType    | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String |
| DomainList | A list of domains, which can include ports, IPs, or asterisks (\*). You can set multiple domains. | Array |
| EmptyReferConfiguration |  Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` | String |
