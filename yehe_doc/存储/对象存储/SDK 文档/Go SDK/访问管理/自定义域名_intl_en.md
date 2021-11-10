

## Overview

This document provides an overview of APIs and SDK code samples related to custom domains.

| API | Operation | Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting a custom domain | Sets a custom domain for a bucket |
| GET Bucket domain    | Querying a custom domain | Queries the custom domain of a bucket |
| DELETE Bucket domain | Deleting custom domains | Deletes custom domains from a bucket |

## Setting Custom Domains

#### API description 

This API (PUT Bucket domain) is used to set a custom domain for a bucket.

#### Method prototype

```go
func (s *BucketService) PutDomain(ctx context.Context, opt *BucketPutDomainOptions) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-domain)
```go
opt := &cos.BucketPutDomainOptions{
    Rules: []cos.BucketDomainRule{
    {
        Status:            "ENABLED",
        Name:              "www.example.com",
        Type:              "REST",
        ForcedReplacement: "CNAME",
    },
    },
}   
resp, err := c.Bucket.PutDomain(context.Background(), opt)
```

#### Parameter description

```go
type BucketDomainRule struct {
    Status            string
    Name              string
    Type              string
    ForcedReplacement string
}

type BucketPutDomainOptions struct {
    XMLName xml.Name
    Rules   []BucketDomainRule
}
```

| Parameter | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| BucketPutDomainOptions | Custom domain configurations                                   | Struct |
| Rules                  | Domain configuration rules                                     | Array  |
| Status                 | Domain status. Valid values: `ENABLED`, `DISABLED`             | String |
| Name                   | Custom domain. Letters, digits, and dots (.) are supported.          | String |
| Type                   | Type of the origin server to bind. Valid values: `REST`, `WEBSITE`                          | String |
| ForcedReplacement      | Replaces existing configurations. Valid values: `CNAME`, `TXT`. If this parameter is specified, configurations will only be delivered after the domain ownership is verified. | String |

#### Error codes

The following describes some common errors that may occur when you call this API:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict | The domain record already exists, and forced overwrite is not specified in the request; OR the domain record does not exist, and forced overwrite is specified in the request |
| HTTP 451 Unavailable For Legal Reasons | The domain does not have an ICP filing in the Chinese mainland                          |

## Querying a Custom Domain

#### API description 

This API (GET Bucket domain) is used to query the custom domain set for a bucket.

#### Method prototype

```go
func (s *BucketService) GetDomain(ctx context.Context) (*BucketGetDomainResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-domain)
```go
v, resp, err := c.Bucket.GetDomain(context.Background())
```

#### Response description

```go
type BucketGetDomainResult BucketPutDomainOptions
```

| Parameter | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| BucketGetDomainResult | Custom domain configurations                                          | Struct |
| Rules                 | Domain configuration rules                            | Array  |
| Status                | Domain status. Valid values: `ENABLED`, `DISABLED`                   | String |
| Name                  | Custom domain. Letters, digits, and dots (.) are supported. | String |
| Type                  | Type of the origin server bound. Valid values: `REST`, `WEBSITE`                          | String |
| ForcedReplacement      | Replaces existing configurations. Valid values: `CNAME`, `TXT`. If this parameter is specified, configurations will only be delivered after the domain ownership is verified. | String |

## Deleting Custom Domains

This API (DELETE  Bucket domain) is used to delete all custom domains bound to a bucket.

#### Method prototype

```go
func (s *BucketService) DeleteDomain(ctx context.Context) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-domain)
```go
_, err := c.Bucket.DeleteDomain(context.Background())
```
