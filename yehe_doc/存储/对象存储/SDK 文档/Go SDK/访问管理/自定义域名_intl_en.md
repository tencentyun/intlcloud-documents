## Overview

This document provides an overview of APIs and SDK code samples related to custom domain name.

| API | Operation Name | Operation Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting custom domain name | Sets custom domain name information for a bucket |
| GET Bucket domain | Querying custom domain name | Queries the custom domain name information of a bucket |

## Setting Custom Domain Name

#### Feature description

This API (PUT Bucket domain) is used to configure a custom domain name for a bucket.

#### Method prototype

```go
func (s *BucketService) PutDomain(ctx context.Context, opt *BucketPutDomainOptions) (*Response, error)
```

#### Sample request

```go
opt := &cos.BucketPutDomainOptions{
 Status:            "ENABLED",
 Name:              "www.example.com",
 Type:              "REST",
 ForcedReplacement: "CNAME",
}   
resp, err := c.Bucket.PutDomain(context.Background(), opt)
```

#### Parameter description

```go
type BucketPutDomainOptions struct {
    XMLName           xml.Name
    Status            string   
    Name              string   
    Type              string   
    ForcedReplacement string   
}
```

| Parameter Name | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| BucketPutDomainOptions | Custom domain name configuration                                               | Struct |
| Status                 | Domain name status. Valid values: ENABLED/DISABLED                   | String |
| Name                   | Custom domain name. Valid values: letter, digit, dot                     | String |
| Type                   | Type of bound origin server. Valid values: REST/WEBSITE                          | String |
| ForcedReplacement | Overwrites existing configuration. Valid values: CNAME/TXT. If this parameter is entered, the configuration will be distributed after the domain name ownership is forcibly verified | String |

#### Returned error code description

Some frequent special errors that may occur with this request are listed below:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict                      | The domain name record already exists, and no forced overwriting is set in the request. Or, the domain name record does not exist, but forced overwriting is set in the request. |
| HTTP 451 Unavailable For Legal Reasons | The domain name is served in Mainland China but has no ICP filing.                          |

## Querying Custom Domain Name

#### Feature description

This API (GET Bucket domain) is used to query the custom domain name information of a bucket.

#### Method prototype

```go
func (s *BucketService) GetDomain(ctx context.Context) (*BucketGetDomainResult, *Response, error)
```

#### Sample request

```go
v, resp, err := c.Bucket.GetDomain(context.Background())
```

#### Returned result description

```go
type BucketGetDomainResult BucketPutDomainOptions
```

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| BucketGetDomainResult | Custom domain name configuration                                               | Struct |
| Status                 | Domain name status. Valid values: ENABLED/DISABLED                   | String |
| Name                   | Custom domain name. Valid values: letter, digit, dot                     | String |
| Type                   | Type of bound origin server. Valid values: REST/WEBSITE                          | String |
| ForcedReplacement | Overwrites existing configuration. Valid values: CNAME/TXT. If this parameter is entered, the configuration will be distributed after the domain name ownership is forcibly verified | String |
