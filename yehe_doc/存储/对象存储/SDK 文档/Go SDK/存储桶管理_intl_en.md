### Introduction
This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycles, versioning, and cross-region replication.

**Cross-origin access**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting a cross-origin access configuration | Sets the cross-origin access permissions of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying a cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting a cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting a lifecycle configuration | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting a lifecycle configuration | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning configuration of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication rules | Sets the cross-region replication rules of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication rules | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication rules| Deletes the cross-region replication rules of a bucket |


## Cross-origin access
### Setting a cross-origin access configuration

#### Feature description

This API is used to set the cross-origin access configuration of a bucket.

#### Method prototype
```go
func (s *BucketService) PutCORS(ctx context.Context, opt *BucketPutCORSOptions) (*Response, error)
```

#### Sample request 
[//]: # ".cssg-snippet-put-bucket-cors"
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
_, err := client.Bucket.PutCORS(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### Parameter description

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
| BucketCORSRule | Sets the appropriate cross-origin rules, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | struct | Yes |
| ID | Sets the rule ID. | string | No |
| AllowedMethods | Sets allowed methods, including GET, PUT, HEAD, POST and DELETE | []string | Yes |
| AllowedOrigins | Sets allowed access sources, such as `"http://cloud.tencent.com"`. The wildcard "*" is supported. | []string | Yes |
| AllowedHeaders | Sets the custom HTTP request headers that can be used by requests. The wildcard "*" is supported. | []string | No |
| MaxAgeSeconds | Sets the validity period of the `OPTIONS` request result | int | No |
| ExposeHeaders | Sets the custom header information that can be received by the browser from the server end | []string | No |


### Querying a cross-origin access configuration

#### Feature description

This API is used to query the cross-origin access configuration of a bucket.

#### Method prototype
```go
func (s *BucketService) GetCORS(ctx context.Context) (*BucketGetCORSResult, *Response, error)
```

#### Sample request 
[//]: # ".cssg-snippet-get-bucket-cors"
```go
_, _, err := client.Bucket.GetCORS(context.Background())
if err != nil {
    panic(err)
}
```

#### Response description
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
| BucketCORSRule | Sets the appropriate cross-origin rules, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | struct | Yes |
| ID | Sets the rule ID. | string | No |
| AllowedMethods | Sets allowed methods, including GET, PUT, HEAD, POST and DELETE | []string | Yes |
| AllowedOrigins | Sets allowed access sources, such as `"http://cloud.tencent.com"`. The wildcard "*" is supported. | []string | Yes |
| AllowedHeaders | Sets the custom HTTP request headers that can be used by requests. The wildcard "*" is supported. | []string | No |
| MaxAgeSeconds | Sets the validity period of the `OPTIONS` request result | int | No |
| ExposeHeaders | Sets the custom header information that can be received by the browser from the server end | []string | No |

### Deleting a cross-origin configuration

#### Feature description

This API is used to delete the cross-origin access configuration of a bucket.

#### Method prototype

```go
func (s *BucketService) DeleteCORS(ctx context.Context) (*Response, error)
```

#### Sample request 
[//]: # ".cssg-snippet-delete-bucket-cors"
```go
_, err := client.Bucket.DeleteCORS(context.Background())
if err != nil {
    panic(err)
}
```

## Lifecycle
### Setting a lifecycle configuration

#### Feature description

This API is used to set the lifecycle configuration of a bucket.

#### Method prototype
```go
func (s *BucketService) PutLifecycle(ctx context.Context, opt *BucketPutLifecycleOptions) (*Response, error)
```

#### Sample request 
[//]: # ".cssg-snippet-put-bucket-lifecycle"
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
_, err := client.Bucket.PutLifecycle(context.Background(), lc)
if err != nil {
    panic(err)
}
```

#### Parameter description
```go
type BucketLifecycleRule struct {
	ID                             string
	Status                         string
	Filter                            *BucketLifecycleFilter
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
	"DaysAfterInitiation": "30" 
}
```

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule | Sets the appropriate lifecycle rules, including ID, Filter, Status, Expiration, Transition, and AbortIncompleteMultipartUpload | List | Yes |
| ID | Sets the rule ID. | string | No |
| Status | Sets whether a rule is enabled. Available values: Enabled or Disabled | string | Yes |
| Filter | Describes a collection of objects that are subject to the rules. To set rules for all objects in the bucket, leave Prefix empty. | struct | Yes |
| Transition | Sets the rule for changing the storage class of the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. Available values for StorageClass: Standard_IA and Archive. Multiple rules can be set at a time. | struct | No |
| Expiration | Sets the expiration rule for the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. | struct | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which a multipart upload operation must be completed once it starts | struct | No |

### Querying a lifestyle configuration

#### Feature description

This API is used to query the lifecycle management configuration of a bucket.

#### Method prototype
```go
func (s *BucketService) GetLifecycle(ctx context.Context) (*BucketGetLifecycleResult, *Response, error)
```

#### Sample request 

[//]: # ".cssg-snippet-get-bucket-lifecycle"
```go
_, _, err := client.Bucket.GetLifecycle(context.Background())
if err != nil {
    panic(err)
}
```

#### Response description

The result of the request is returned through GetBucketLifecycleResult.

```go
type BucketLifecycleRule struct {
	ID                             string
	Status                         string
	Filter                            *BucketLifecycleFilter
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
	"DaysAfterInitiation": "30" 
}
```

| Parameter Name | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule | Sets the appropriate lifecycle rules, including ID, Filter, Status, Expiration, Transition, and AbortIncompleteMultipartUpload | List | Yes |
| ID | Sets the rule ID. | string | No |
| Status | Sets whether a rule is enabled. Available values: Enabled or Disabled | string | Yes |
| Filter | Describes a collection of objects that are subject to the rules. To set rules for all objects in the bucket, leave Prefix empty. | struct | Yes |
| Transition | Sets the rule for changing the storage class of the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. Available values for StorageClass: Standard_IA and Archive. Multiple rules can be set at a time. | struct | No |
| Expiration | Sets the expiration rule for the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. | struct | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which a multipart upload operation must be completed once it starts | struct | No |


### Deleting a lifecycle configuration

#### Feature description

This API is used to delete the lifecycle configuration of a Bucket.

#### Method prototype

```go
func (s *BucketService) DeleteLifecycle(ctx context.Context) (*Response, error)
```

#### Sample request 

[//]: # ".cssg-snippet-delete-bucket-lifecycle"
```go
_, err := client.Bucket.DeleteLifecycle(context.Background())
if err != nil {
    panic(err)
}
```

## Versioning
### Setting versioning

#### Feature description

This API is used to set the versioning configuration of a bucket.

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
| Status | Indicates whether versioning is enabled. Valid values: Suspended (versioning is paused), Enabled (versioning is enabled) | string |

### Querying versioning

#### Feature description

This API is used to query the versioning configuration of a bucket.

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
| Status | Indicates whether versioning is enabled. Valid values: Suspended (versioning is paused), Enabled (versioning is enabled) | string |

## Cross-region replication
### Setting cross-region replication rules

#### Feature description

This API is used to set the cross-region replication rules of a bucket

#### Method prototype
```go
func (s *BucketService) PutBucketReplication(ctx context.Context, opt *PutBucketReplicationOptions) (*Response, error)
```

#### Sample request 
[//]: # ".cssg-snippet-put-bucket-replication"
```go
opt := &cos.PutBucketReplicationOptions{
    qcs::cam::uin/[UIN]:uin/[Subaccount]
    Role: "qcs::cam::uin/100000760461:uin/100000760461",
    Rule: []cos.BucketReplicationRule{
        {
            ID: "1",
            Enabled, Disabled
            Status: "Enabled",
            Destination: &cos.ReplicationDestination{
                // qcs::cos:[Region]::[Bucketname-Appid]
                Bucket: "qcs::cos:ap-beijing::destinationbucket-1250000000",
            },
        },
    },
}
_, err := client.Bucket.PutBucketReplication(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### Parameter description
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
| PutBucketReplicationOptions  | Cross-region replication rules | struct |
| Role | Identifies the replication initiator：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>`  | string |
| Rule | Specific configuration information. Up to 1000 rules are supported. All rules must be directed to a single destination bucket | NSArray *|
| ID | Indicates the name of a specific rule | String |
| Status | Indicates whether a rule is enabled. Valid values: Enabled, Disabled | string |
| Prefix | Prefix matching policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned | NSString* |
| Destination |  Describes information on the destination bucket | struct |
| Bucket | Source bucket name：`qcs::cos:[region]::[bucketname-AppId]`  | string |
| StorageClass | Sets the object storage class. Valid values：STANDARD，TANDARD_IA. Default value: STANDARD | string |

### Querying cross-region replication rules

#### Feature description

This API is used to query the cross-region replication rules of a bucket.

#### Method prototype
```go
func (s *BucketService) GetBucketReplication(ctx context.Context) (*GetBucketReplicationResult, *Response, error)
```

#### Sample request 
[//]: # ".cssg-snippet-get-bucket-replication"
```go
_, _, err := client.Bucket.GetBucketReplication(context.Background())
if err != nil {
    panic(err)
}
```

#### Response description
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
| GetBucketReplicationResult  | Cross-region replication rules | struct |
| Role | Identifies the replication initiator：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>`  | string |
| Rule | Specific configuration information. Up to 1000 rules are supported. All rules must be directed to a single destination bucket | NSArray *|
| id | Indicates the name of a specific Rule | String |
| Status | Indicates whether a rule is enabled. Enumerated values: Enabled, Disabled | String |
| prefix | Prefix matching policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned | NSString* |
| Destination |  Describes information on the destination bucket | struct |
| Bucket | Source bucket name：`qcs::cos:[region]::[bucketname-AppId]`  | string |
| StorageClass | Sets the object storage class. Valid values: Standard, Standard_IA. Default value: Standard | String | No |


## Deleting cross-region replication rules

#### Feature description

This API is used to delete the cross-region replication rules of a bucket.

#### Method prototype
```go
func (s *BucketService) DeleteBucketReplication(ctx context.Context) (*Response, error)
```

#### Sample request 
[//]: # ".cssg-snippet-delete-bucket-replication"
```go
_, err := client.Bucket.DeleteBucketReplication(context.Background())
if err != nil {
    panic(err)
}
```

