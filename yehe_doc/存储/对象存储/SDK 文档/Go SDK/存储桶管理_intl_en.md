## Introduction
This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycle, version control, and cross-region replication.

**Cross-origin Access**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets cross-origin access permissions for a bucket |
| [GET Bucket cors](https://cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management for a bucket |
| [GET Bucket lifecycle](https://cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Versioning**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning configuration for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region Replication**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets cross-region replication rules for a bucket |
| [GET Bucket replication](https://cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |


## Cross-Origin Access
### Set cross-origin configuration

#### Feature

This API (Put Bucket CORS) is used to set the configurations on cross-origin access (CORS) of a bucket.

#### Method Prototype
```go
func (s *BucketService) PutCORS(ctx context.Context, opt *BucketPutCORSOptions) (*Response, error)
```

#### Request Samples
[//]: # (.cssg-snippet-put-bucket-cors)
```go
opt := &cos.BucketPutCORSOptions{
    Rules: []cos.BucketCORSRule{
        {
            AllowedOrigins: []string{"http://www.qq.com"},
            AllowedMethods: []string{"PUT", "GET"},
            AllowedHeaders: []string{"x-cos-meta-test", "x-cos-xx"},
            'MaxAgeSeconds' => 1,
            ExposeHeaders:  []string{"x-cos-meta-test1"},
        },
        {
            ID:             "1234",
            AllowedOrigins: []string{"http://www.baidu.com", "twitter.com"},
            AllowedMethods: []string{"PUT", "GET"},
            'MaxAgeSeconds' => 1,
        },
    },
}
_, err := client.Bucket.PutCORS(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### Parameter Description

```go
type BucketCORSRule struct {
	ID             string   
	AllowedMethods []string 
	AllowedOrigins []string 
	AllowedHeaders []string 
	'MaxAgeSeconds' => 1,      
	ExposeHeaders  []string 
}
```

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | Sets the appropriate cross-origin rules, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | struct | Yes |
| ID | Sets rule ID. | string | No |
| AllowedMethods | Sets allowed methods, including GET, PUT, HEAD, POST and DELETE | []string | Yes |
| AllowedOrigins | Sets allowed access sources, such as `"http://cloud.tencent.com"`. The wildcard "*" is supported. | []string | Yes |
| AllowedHeaders | Sets the custom HTTP request headers that can be used by requests. The wildcard "*" is supported. | []string | No |
| MaxAgeSeconds | Sets the validity period of the results obtained by OPTIONS | int | No |
| ExposeHeaders | Sets the custom header information that can be received by the browser from the server end | []string | No |


### Query cross-origin configuration

#### Feature

This API (Get Bucket CORS) is used to query the cross-origin access configuration of a bucket.

#### Method Prototype
```go
func (s *BucketService) GetCORS(ctx context.Context) (*BucketGetCORSResult, *Response, error)
```

#### Request Samples
[//]: # (.cssg-snippet-get-bucket-cors)
```go
_, _, err := client.Bucket.GetCORS(context.Background())
if err != nil {
    panic(err)
}
```

#### Returned Result
Request result is returned through GetBucketCORSResult.

```go
type BucketCORSRule struct {
	ID             string   
	AllowedMethods []string 
	AllowedOrigins []string 
	AllowedHeaders []string 
	'MaxAgeSeconds' => 1,      
	ExposeHeaders  []string 
}
```

| Parameter Name | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | Sets the appropriate cross-origin rules, including ID, MaxAgeSeconds, AllowedOrigin, AllowedMethod, AllowedHeader, and ExposeHeader | struct | Yes |
| ID | Sets rule ID. | string | No |
| AllowedMethods | Sets allowed methods, including GET, PUT, HEAD, POST and DELETE | []string | Yes |
| AllowedOrigins | Sets allowed access sources, such as `"http://cloud.tencent.com"`. The wildcard "*" is supported. | []string | Yes |
| AllowedHeaders | Sets the custom HTTP request headers that can be used by requests. The wildcard "*" is supported. | []string | No |
| MaxAgeSeconds | Sets the validity period of the results obtained by OPTIONS | int | No |
| ExposeHeaders | Sets the custom header information that can be received by the browser from the server end | []string | No |

### Delete cross-origin configuration

#### Feature

This API (Delete Bucket CORS) is used to delete the cross-origin access configuration of a bucket.

#### Method Prototype

```go
func (s *BucketService) DeleteCORS(ctx context.Context) (*Response, error)
```

#### Request Samples
[//]: # (.cssg-snippet-delete-bucket-cors)
```go
_, err := client.Bucket.DeleteCORS(context.Background())
if err != nil {
    panic(err)
}
```

## Lifecycle
### Set the lifestyle

#### Feature

This API (Put Bucket LifeCycle) is used to set the lifecycle configuration of a bucket.

#### Method Prototype
```go
func (s *BucketService) PutLifecycle(ctx context.Context, opt *BucketPutLifecycleOptions) (*Response, error)
```

#### Request Samples
[//]: # (.cssg-snippet-put-bucket-lifecycle)
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

#### Parameter Description
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
	'StorageClass' => 'string'
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
| Rule | Sets the appropriate rules, including ID, Filter, Status, Expiration, Transition, and AbortIncompleteMultipartUpload | List | Yes |
| ID | Sets rule ID. | string | No |
| Status | Sets whether Rule is enabled. Available values: Enabled or Disabled | string | Yes |
| Filter | Describes a collection of objects that are subject to the rules. To set rules for all objects in the bucket, leave Prefix empty. | struct | Yes |
| Transition | Sets the rule for changing the storage type of the object. You can specify the number of days (Days) or a specified date (Date). The format of Date must be GMT ISO 8601. Available values for StorageClass: Standard_IA and Archive. Multiple rules can be set at a time. | struct | No |
| Expiration | Sets the expiration rule for the object. You can specify the number of days (Days) or a specified date (Date). The format of Date must be GMT ISO 8601. | struct | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which multipart uploads must be completed once they start | struct | No |

### Query the lifestyle

#### Feature

This API (GET Bucket lifecycle) is used to query the lifecycle management configuration of a bucket.

#### Method Prototype
```go
func (s *BucketService) GetLifecycle(ctx context.Context) (*BucketGetLifecycleResult, *Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```go
_, _, err := client.Bucket.GetLifecycle(context.Background())
if err != nil {
    panic(err)
}
```

#### Returned Result

Request result is returned through GetBucketLifecycleResult.

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
	'StorageClass' => 'string'
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
| Rule | Sets the appropriate rules, including ID, Filter, Status, Expiration, Transition, and AbortIncompleteMultipartUpload | List | Yes |
| ID | Sets rule ID. | string | No |
| Status | Sets whether Rule is enabled. Available values: Enabled or Disabled | string | Yes |
| Filter | Describes a collection of objects that are subject to the rules. To set rules for all objects in the bucket, leave Prefix empty. | struct | Yes |
| Transition | Sets the rule for changing the storage type of the object. You can specify the number of days (Days) or a specified date (Date). The format of Date must be GMT ISO 8601. Available values for StorageClass: Standard_IA and Archive. Multiple rules can be set at a time. | struct | No |
| Expiration | Sets the expiration rule for the object. You can specify the number of days (Days) or a specified date (Date). The format of Date must be GMT ISO 8601. | struct | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which multipart uploads must be completed once they start | struct | No |


### Delete the lifecycle

#### Feature

This API (Delete Bucket Lifecycle) is used to delete the lifecycle configuration of a Bucket.

#### Method Prototype

```go
func (s *BucketService) DeleteLifecycle(ctx context.Context) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```go
_, err := client.Bucket.DeleteLifecycle(context.Background())
if err != nil {
    panic(err)
}
```

## Versioning
### Set Versioning

#### Feature

This API (Put Bucket versioning) is used to set the versioning information of a bucket.

#### Method Prototype
```go
func (s *BucketService) PutVersioning(ctx context.Context, opt *BucketPutVersionOptions) (*Response, error)
```

#### Request Samples
[//]: # (.cssg-snippet-put-bucket-versioning)
```go
opt := &cos.BucketPutVersionOptions{
    // Enabled or Suspended, configuration for versioning can only be paused but not deleted once it starts
    Status: "Enabled",
}
_, err := client.Bucket.PutVersioning(context.Background(), opt)
if err != nil {
    panic(err)
}
```

#### Parameter Description
```go
type BucketPutVersionOptions struct {
	Status  string
}
```
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| BucketPutVersionOptions | Versioning Rules | struct |
| Status | Indicates whether the version is enabled. Valid values: Suspended (pause version control), Enabled (enable version control) | string |

### Query Versioning

#### Feature

This API (Get Bucket versioning) is used to get the versioning information of a bucket.

#### Method Prototype
```go
func (s *BucketService) GetVersioning(ctx context.Context) (*BucketGetVersionResult, *Response, error)
```

#### Request Samples
[//]: # (.cssg-snippet-get-bucket-versioning)
```go
_, _, err := client.Bucket.GetVersioning(context.Background())
if err != nil {
    panic(err)
}
```

#### Returned Result
```go
type BucketGetVersionResult struct {
	Status  string
}
```
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| BucketGetVersionResult | Versioning Rules | struct |
| Status | Indicates whether the version is enabled. Valid values: Suspended (pause version control), Enabled (enable version control) | string |

## Cross-region Replication
### Set cross-region replication

#### Feature

This API (Put Bucket rereplication) is used to set cross-region replication rules of a bucket.

#### Method Prototype
```go
func (s *BucketService) PutBucketReplication(ctx context.Context, opt *PutBucketReplicationOptions) (*Response, error)
```

#### Request Samples
[//]: # (.cssg-snippet-put-bucket-replication)
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

#### Parameter Description
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
	'StorageClass' => 'string'
}
```
| Parameter Name | Description | Type |
| ----| ---- | ---- |
| PutBucketReplicationOptions  | Cross-region replication rules | struct                         |
| Role | Identifies the replication initiator：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>`  | string |
| Rule | Specific configuration information. Up to 1000 rules are supported. All rules must be directed to one destination bucket | NSArray *|
| ID | Indicates the name of a specific Rule | String |
| Status | Sets whether the rule is enabled. Valid values: Enabled, Disabled | string |
| Prefix | Prefix match policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned | NSString* |
| Destination |  Describes information on destination bucket | struct |
| Bucket | Source bucket name：`qcs::cos:[region]::[bucketname-AppId]`  | string | 
| StorageClass | Sets the object storage class. Valid values：STANDARD，TANDARD_IA. Default value: STANDARD | string |

### Querying cross-region replication

#### Feature

This API (Get Bucket rereplication) is used to get cross-region replication rules of a bucket.

#### Method Prototype
```go
func (s *BucketService) GetBucketReplication(ctx context.Context) (*GetBucketReplicationResult, *Response, error)
```

#### Request Samples
[//]: # (.cssg-snippet-get-bucket-replication)
```go
_, _, err := client.Bucket.GetBucketReplication(context.Background())
if err != nil {
    panic(err)
}
```

#### Returned Result
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
| GetBucketReplicationResult  | Cross-region replication rules | struct                         |
| Role | Identifies the replication initiator：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>`  | string |
| rule | Specific configuration information. Up to 1000 rules are supported. All rules must be directed to one destination bucket | NSArray *|
| id | Indicates the name of a specific Rule | String |
| status | Indicates whether the rule is enabled. Enumerated values: Enabled, Disabled | String |
| prefix | Prefix match policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned | NSString* |
| Destination |  Describes information on destination bucket | struct |
| Bucket | Source bucket name：`qcs::cos:[region]::[bucketname-AppId]`  | string | 
| StorageClass |Sets the storage class. Valid values: Standard, Standard_IA. Default value: Standard | String | No |


## Deleting cross-region replication

#### Feature

This API (Delete Bucket replication) is used to delete cross-region replication of a bucket.

#### Method Prototype
```go
func (s *BucketService) DeleteBucketReplication(ctx context.Context) (*Response, error)
```

#### Request Samples
[//]: # (.cssg-snippet-delete-bucket-replication)
```go
_, err := client.Bucket.DeleteBucketReplication(context.Background())
if err != nil {
    panic(err)
}
```

