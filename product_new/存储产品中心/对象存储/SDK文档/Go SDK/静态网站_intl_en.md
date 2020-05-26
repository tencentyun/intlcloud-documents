

## Overview

This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Sets static website configuration for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying static website configuration | Queries the static website configuration information of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting static website configuration | Deletes the static website configuration of a bucket |

## Setting Static Website

#### Feature description

This API (PUT Bucket website) is used to configure a static website for a bucket.

#### Method prototype

```go
func (s *BucketService) PutWebsite(ctx context.Context, opt *BucketPutWebsiteOptions) (*Response, error)
```

#### Sample request

```go
opt := &cos.BucketPutWebsiteOptions{
	Index: "index.html",
	Error: &cos.ErrorDocument{"index_backup.html"},
	RoutingRules: &cos.WebsiteRoutingRules{
        []cos.WebsiteRoutingRule{
        {   
            ConditionErrorCode: "404",
            RedirectProtocol:   "https",
            RedirectReplaceKey: "404.html",
        },  
        {   
            ConditionPrefix:          "docs/",
            RedirectProtocol:         "https",
            RedirectReplaceKeyPrefix: "documents/",
        },  
        },  
	},  
}   
resp, err := client.Bucket.PutWebsite(context.Background(), opt)
```

#### Parameter description

```go
type WebsiteRoutingRule struct {
    ConditionErrorCode string 
    ConditionPrefix    string 

    RedirectProtocol         string 
    RedirectReplaceKey       string 
    RedirectReplaceKeyPrefix string 
}

type WebsiteRoutingRules struct {
    Rules []WebsiteRoutingRule
}

type ErrorDocument struct {
    Key string 
}

type RedirectRequestsProtocol struct {
    Protocol string 
}

type BucketPutWebsiteOptions struct {
    XMLName          xml.Name                  
    Index            string                    
    RedirectProtocol *RedirectRequestsProtocol
    Error            *ErrorDocument            
    RoutingRules     *WebsiteRoutingRules
}
```

| Parameter Name | Description | Type |
| ------------------------ | ------------------------------------------------------------ | ------ |
| BucketPutWebsiteOptions  | Static website configuration parameter                                             | Struct |
| Index                       | Specifies index document                                                 | String |
| RedirectProtocol         | Protocol for global redirect                                             | Struct |
| Protocol                    | Specifies the protocol for global redirect, which can only be `https`                       | String   |
| Error                    | Error document                                                     | Struct |
| Key                         | Specifies the common return for errors                                             | String   |
| RoutingRules                | Sets redirect rules. Up to 100 `RoutingRule` can be set                    | Struct |
| ConditionErrorCode       | Specifies the error code triggering redirect, which can only be 4XX and has a higher priority than `Error.Key`   | String |
| ConditionPrefix          | Specifies the path for prefix-triggered redirect, which replaces the specified `folder/`                     | String |
| RedirectProtocol         | Specifies the protocol for redirect, which can only be `https`                       | String |
| RedirectReplaceKey       | Replaces the entire `Key` with the specified content                                    | String |
| RedirectReplaceKeyPrefix | Replaces the matched prefix with the specified content, which can be set only if `Condition` is `KeyPrefixEquals` | String |

## Querying Static Website Configuration

#### Feature description

This API (GET Bucket website) is used to query the configuration information of a static website associated with a bucket.

#### Method prototype

```go
func (s *BucketService) GetWebsite(ctx context.Context) (*BucketGetWebsiteResult, *Response, error)
```

#### Sample request

```go
res, rsp, err := client.Bucket.GetWebsite(context.Background())
```

#### Returned result description

```go
type BucketGetWebsiteResult BucketPutWebsiteOptions
```

| Parameter Name | Description | Type |
| ------------------------ | ------------------------------------------------------------ | ------ |
| BucketGetWebsiteResult   | Static website configuration parameter                                             | Struct |
| Index                       | Specifies index document                                                 | String |
| RedirectProtocol         | Protocol for global redirect                                             | Struct |
| Protocol                    | Specifies the protocol for global redirect, which can only be `https`                       | String   |
| Error                    | Common return for errors                                                 | Struct |
| Key                         | Specifies the common return for errors                                             | String   |
| RoutingRules                | Sets redirect rules. Up to 100 `RoutingRule` can be set                    | Struct |
| ConditionErrorCode       | Specifies the error code triggering redirect, which can only be 4XX and has a higher priority than `Error.Key`   | String |
| ConditionPrefix          | Specifies the path for prefix-triggered redirect, which replaces the specified `folder/`                     | String |
| RedirectProtocol         | Specifies the protocol for redirect, which can only be `https`                       | String |
| RedirectReplaceKey       | Replaces the entire `Key` with the specified content                                    | String |
| RedirectReplaceKeyPrefix | Replaces the matched prefix with the specified content, which can be set only if `Condition` is `KeyPrefixEquals` | String |

## Deleting Static Website Configuration

#### Feature description

This API (DELETE Bucket website) is used to delete the static website configuration of a bucket.

#### Method prototype

```go
func (s *BucketService) DeleteWebsite(ctx context.Context) (*Response, error)
```

#### Sample request

```go
resp, err = s.Client.Bucket.DeleteWebsite(context.Background())
```
