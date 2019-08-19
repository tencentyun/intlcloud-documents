## Overview
This document provides an overview of APIs related to cross-origin access, lifecycle, versioning, and cross-region replication and corresponding SDK sample code.

**Cross-origin access**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning feature of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation Name | Operation Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rule of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rule of a bucket |


## Cross-origin Access
### Setting Cross-origin Access Configuration

#### Feature Description

This API (PUT Bucket cors) is used to set the cross-origin access configuration information of the specified bucket.

#### Method Prototype
```go
func (s *BucketService) PutCORS(ctx context.Context, opt *BucketPutCORSOptions) (*Response, error)
```

#### Sample Request
```go
opt := &cos.BucketPutCORSOptions{
    Rules: []cos.BucketCORSRule{
        {
            AllowedOrigins: []string{"http://www.qq.com"},
            AllowedMethods: []string{"PUT", "GET"},
            AllowedHeaders: []string{"x-cos-meta-test", "x-cos-xx"},
            MaxAgeSeconds:  500,
            ExposeHeaders:  []string{"x-cos-meta-test1"},
        },
        {
            ID:             "1234",
            AllowedOrigins: []string{"http://www.baidu.com", "twitter.com"},
            AllowedMethods: []string{"PUT", "GET"},
            MaxAgeSeconds:  500,
        },
    },
}
resp, err := client.Bucket.PutCORS(context.Background(), opt)
```

#### Parameter Descriptions

```go
type BucketCORSRule struct {
	ID             string   
	AllowedMethods []string 
	AllowedOrigins []string 
	AllowedHeaders []string 
	MaxAgeSeconds  int      
	ExposeHeaders  []string 
}
```

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | Sets the corresponding cross-origin access rule, including MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | struct | Yes |
| ID | Sets the rule ID | String | No |
| AllowedMethods | Sets the allowed method such as GET, PUT, HEAD, POST, and DELETE | []string | Yes |
| AllowedOrigins | Sets the allowed origin such as `"http://intl.cloud.tencent.com"`. Wildcard * is supported | []string | Yes |
| AllowedHeaders | Sets the custom HTTP request headers that can be used for the request. Wildcard * is supported | []string | No |
| MaxAgeSeconds | Sets the validity period of the result of the OPTIONS request | int | No |
| ExposeHeaders  | Sets custom header information from the server that the browser can receive | []string | No |


### Querying Cross-origin Access Configuration

#### Feature Description

This API (GET Bucket cors) is used to query the cross-origin access configuration information of a bucket.

#### Method Prototype
```go
func (s *BucketService) GetCORS(ctx context.Context) (*BucketGetCORSResult, *Response, error)
```

#### Sample Request
```go
v, resp, err := client.Bucket.GetCORS(context.Background())
```

#### Return Result Descriptions
The result of the request is returned through GetBucketCORSResult.

```go
type BucketCORSRule struct {
	ID             string   
	AllowedMethods []string 
	AllowedOrigins []string 
	AllowedHeaders []string 
	MaxAgeSeconds  int      
	ExposeHeaders  []string 
}
```

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | Sets the corresponding cross-origin access rule, including MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | struct | Yes |
| ID | Sets the rule ID | String | No |
| AllowedMethods | Sets the allowed method such as GET, PUT, HEAD, POST, and DELETE | []string | Yes |
| AllowedOrigins | Sets the allowed origin such as `"http://intl.cloud.tencent.com"`. Wildcard * is supported | []string | Yes |
| AllowedHeaders | Sets the custom HTTP request headers that can be used for the request. Wildcard * is supported | []string | No |
| MaxAgeSeconds | Sets the validity period of the result of the OPTIONS request | int | No |
| ExposeHeaders  | Sets custom header information from the server that the browser can receive | []string | No | |

### Deleting Cross-origin Access Configuration

#### Feature Description

This API (DELETE Bucket cors) is used to delete the cross-origin access configuration of the specified bucket.

#### Method Prototype

```go
func (s *BucketService) DeleteCORS(ctx context.Context) (*Response, error)
```

#### Sample Request
```go
resp, err := client.Bucket.DeleteCORS(context.Background())
```

## Lifecycle
### Setting Lifecycle

#### Feature Description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration information of the specified bucket.

#### Method Prototype
```go
func (s *BucketService) PutLifecycle(ctx context.Context, opt *BucketPutLifecycleOptions) (*Response, error)
```

#### Sample Request
```go
lc := &cos.BucketPutLifecycleOptions{
    Rules: []cos.BucketLifecycleRule{
        {
            ID:     "1234",
            Filter: &cos.BucketLifecycleFilter{Prefix: "test"},
            Status: "Enabled",
            Transition: &cos.BucketLifecycleTransition{
                Days:         10,
                StorageClass: "Standard",
            },
        },
        {
            ID:     "123422",
            Filter: &cos.BucketLifecycleFilter{Prefix: "gg"},
            Status: "Disabled",
            Expiration: &cos.BucketLifecycleExpiration{
                Days: 10,
            },
        },
    },
}
resp, err := client.Bucket.PutLifecycle(context.Background(), lc)
```

#### Parameter Descriptions
```go
type BucketLifecycleRule struct {
	ID                             string
	Status                         string
	Filter                         *BucketLifecycleFilter
	Transition                     *BucketLifecycleTransition
	Expiration                     *BucketLifecycleExpiration
	AbortIncompleteMultipartUpload  *BucketLifecycleAbortIncompleteMultipartUpload 
}
type BucketLifecycleFilter struct {
	Prefix       string 
}
type BucketLifecycleTransition struct {
	Date         string 
	Days         int    
	StorageClass string
}
type BucketLifecycleExpiration struct {
	Date string 
	Days int    
}
type BucketLifecycleAbortIncompleteMultipartUpload struct {
	DaysAfterInitiation string 
}
```

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule | Sets the corresponding rule, including ID, Filter, Status, Expiration, Transition, and AbortIncompleteMultipartUpload | List | Yes |
| ID | Sets the rule ID | String | No |
| Status | Sets whether a rule is enabled; value range: Enabled, Disabled | string | Yes |
| Filter | Describes the set of objects subject to the rule. If you want to set for all objects in the bucket, leave Prefix blank | Yes |
| Transition | Sets the object transition rule (either a number of days (Days) or a date (Date) in GMT ISO 8601 format can be specified). StorageClass value range: Standard_IA, Archive. Multiple rules can be set at the same time | struct | No |
| Expiration | Sets the object expiration rule (either a number of days (Days) or a date (Date) in GMT ISO 8601 format can be specified) | struct | No |
| AbortIncompleteMultipartUpload | Indicates in how many days a multipart upload has to be completed once started | struct | No |

### Querying Lifecycle

#### Feature Description

This API (GET Bucket lifecycle) is used to query the lifecycle management configuration for a bucket.

#### Method Prototype
```go
func (s *BucketService) GetLifecycle(ctx context.Context) (*BucketGetLifecycleResult, *Response, error)
```

#### Sample Request

```go
v, resp, err := client.Bucket.GetLifecycle(context.Background()) 
```

#### Return Result Descriptions

The result of the request is returned through GetBucketLifecycleResult.

```go
type BucketLifecycleRule struct {
	ID                             string
	Status                         string
	Filter                         *BucketLifecycleFilter
	Transition                     *BucketLifecycleTransition
	Expiration                     *BucketLifecycleExpiration
	AbortIncompleteMultipartUpload  *BucketLifecycleAbortIncompleteMultipartUpload 
}
type BucketLifecycleFilter struct {
	Prefix       string 
}
type BucketLifecycleTransition struct {
	Date         string 
	Days         int    
	StorageClass string
}
type BucketLifecycleExpiration struct {
	Date string 
	Days int    
}
type BucketLifecycleAbortIncompleteMultipartUpload struct {
	DaysAfterInitiation string 
}
```

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule | Sets the corresponding rule, including ID, Filter, Status, Expiration, Transition, and AbortIncompleteMultipartUpload | List | Yes |
| ID | Sets the rule ID | String | No |
| Status | Sets whether a rule is enabled; value range: Enabled, Disabled | string | Yes |
| Filter | Describes the set of objects subject to the rule. If you want to set for all objects in the bucket, leave Prefix blank | Yes |
| Transition | Sets the object transition rule (either a number of days (Days) or a date (Date) in GMT ISO 8601 format can be specified). StorageClass value range: Standard_IA, Archive. Multiple rules can be set at the same time | struct | No |
| Expiration | Sets the object expiration rule (either a number of days (Days) or a date (Date) in GMT ISO 8601 format can be specified) | struct | No |
| AbortIncompleteMultipartUpload | Indicates in how many days a multipart upload has to be completed once started | struct | No |


### Deleting Lifecycle

#### Feature Description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle management configuration of a bucket.

#### Method Prototype

```go
func (s *BucketService) DeleteLifecycle(ctx context.Context) (*Response, error)
```

#### Sample Request

```go
resp, err := client.Bucket.DeleteLifecycle(context.Background())
```

## Versioning
### Setting Versioning

#### Feature Description

This API (PUT Bucket versioning) is used to set the versioning feature of the specified bucket.

#### Method Prototype
```go
func (s *BucketService) PutVersioning(ctx context.Context, opt *BucketPutVersionOptions) (*Response, error)
```

#### Sample Request
```go
opt := &cos.BucketPutVersionOptions{
	// Enabled or Suspended, the versioning once opened can not close.
	Status: "Enabled",
}
resp, err := c.Bucket.PutVersioning(context.Background(), opt)
```

#### Parameter Descriptions
```go
type BucketPutVersionOptions struct {
	Status  string
}
```
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| BucketPutVersionOptions | Versioning policy | struct |
| Status | Indicates whether versioning is enabled; enumerated values: Suspended (versioning suspended), Enabled (versioning enabled) | string |

### Querying Versioning

#### Feature Description

This API (GET Bucket versioning) is used to query the versioning information of the specified bucket.

#### Method Prototype
```go
func (s *BucketService) GetVersioning(ctx context.Context) (*BucketGetVersionResult, *Response, error)
```

#### Sample Request
```go
v, resp, err := c.Bucket.GetVersioning(context.Background())
```

#### Return Result Descriptions
```go
type BucketGetVersionResult struct {
	Status  string
}
```
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| BucketGetVersionResult | Versioning policy  | struct |
| Status | Indicates whether versioning is enabled; enumerated values: Suspended (versioning suspended), Enabled (versioning enabled) | string |

## Cross-region Replication
### Setting Cross-region Replication

#### Feature Description

This API (PUT Bucket replication) is used to set the cross-region replication rule for the specified bucket.

#### Method Prototype
```go
func (s *BucketService) PutBucketReplication(ctx context.Context, opt *PutBucketReplicationOptions) (*Response, error)
```

#### Sample Request
```go
opt := &cos.PutBucketReplicationOptions{
	// qcs::cam::uin/[UIN]:uin/[Subaccount]
	Role: "qcs::cam::uin/100000000001:uin/100000000001",
	Rule: []cos.BucketReplicationRule{
		{
			ID: "1",
			// Enabled or Disabled
			Status: "Enabled",
			Destination: &cos.ReplicationDestination{
				// qcs::cos:[Region]::[Bucketname-Appid]
				Bucket: "qcs::cos:ap-guangzhou::examplebucket-1250000000",
			},
		},
	},
}
resp, err := c.Bucket.PutBucketReplication(context.Background(), opt)
```

#### Parameter Descriptions
```go
type PutBucketReplicationOptions struct {
	Role    string
	Rule    []BucketReplicationRule
}
type BucketReplicationRule struct {
	ID          string
	Status      string
	Prefix      string
	Destination *ReplicationDestination
}
type ReplicationDestination struct {
	Bucket       string
	StorageClass string
}
```
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| PutBucketReplicationOptions  | Cross-region replication rule | struct                         |
| Role | Initiator ID: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | string |
| Rule | Specific configuration information of up to 1,000 rules. All rules must point to the same destination bucket  | struct |
| ID | 	Identifies the name of a specific rule  | string |
| Status | Indicates whether a rule is in effect; enumerated values: Enabled, Disabled | string |
| Prefix | 	Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. The prefix matching root directory is empty | string |
| Destination | Destination bucket information | struct |
| Bucket | Resource ID: `qcs::cos:[region]::[bucketname-AppId]`  | string |
| StorageClass | Storage class; enumerated values: STANDARD, STANDARD_IA; default value: class of the source bucket | string |

### Querying Cross-region Replication

#### Feature Description

This API (GET Bucket replication) is used to query the cross-region replication rule of the specified bucket.

#### Method Prototype
```go
func (s *BucketService) GetBucketReplication(ctx context.Context) (*GetBucketReplicationResult, *Response, error)
```

#### Sample Request
```go
v, resp, err := c.Bucket.GetBucketReplication(context.Background())
```

#### Return Result Descriptions
```go
type GetBucketReplicationResult struct {
	Role    string
	Rule    []BucketReplicationRule
}
type BucketReplicationRule struct {
	ID          string
	Status      string
	Prefix      string
	Destination *ReplicationDestination
}
type ReplicationDestination struct {
	Bucket       string
	StorageClass string
}
```
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| GetBucketReplicationResult  | Cross-region replication rule | struct                         |
| Role | Initiator ID: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | string |
| Rule | Specific configuration information of up to 1,000 rules. All rules must point to the same destination bucket  | struct |
| ID | 	Identifies the name of a specific rule  | string |
| Status | Indicates whether a rule is in effect; enumerated values: Enabled, Disabled | string |
| Prefix | 	Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. The prefix matching root directory is empty | string |
| Destination | Destination bucket information | struct |
| Bucket | Resource ID: `qcs::cos:[region]::[bucketname-AppId]`  | string |
| StorageClass | Storage class; enumerated values: STANDARD, STANDARD_IA; default value: class of the source bucket | string |


### Deleting Cross-region Replication

#### Feature Description

This API (DELETE Bucket replication) is used to delete the cross-region replication rule of the specified bucket.

#### Method Prototype
```go
func (s *BucketService) DeleteBucketReplication(ctx context.Context) (*Response, error)
```

#### Sample Request
```go
resp, err := c.Bucket.DeleteBucketReplication(context.Background())
```

