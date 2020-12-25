## Overview
This document provides an overview of APIs and SDK code samples related to CORS, lifecycle, versioning, cross-bucket replication, and bucket policies.

**CORS**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting CORS configuration | Sets CORS permissions for a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying CORS configuration | Queries the CORS configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting CORS configuration | Deletes the CORS configuration of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle configuration | Sets lifecycle for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting a lifecycle configuration | Deletes the lifecycle configuration of a bucket |

**Versioning**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning configuration of a bucket |

**Cross-bucket replication**

| API | Operation | Description |
| ------------------- | ------------ | ------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting a bucket replication rule | Sets a cross-bucket replication rule for a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying a bucket replication rule | Queries the cross-bucket replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting a bucket replication rule | Deletes a cross-bucket replication rule of a bucket |

**Bucket policies**

| API | Operation | Description |
| ----------------------------------------------------------- | ----------- | ----------------------- |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for a bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying a bucket policy | Queries the permission policy of a bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting a bucket policy | Deletes the permission policy of a bucket |

## CORS
### Setting CORS

#### API description

This API (PUT Bucket cors) is used to set CORS for a bucket.

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

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | CORS rules, including `ID`, `MaxAgeSeconds`, `AllowedOrigin`, `AllowedMethod`, `AllowedHeader`, and `ExposeHeader` | struct | Yes |
| ID | Rule ID | string | No |
| AllowedMethods | Allowed methods, including GET, PUT, HEAD, POST, and DELETE | []string | Yes |
| AllowedOrigins | Allowed access sources, such as `"http://cloud.tencent.com"`. Asterisks (*) are supported. | []string | Yes |
| AllowedHeaders | Custom HTTP request headers that can be used by requests. Asterisks (*) are supported. | []string | No |
| MaxAgeSeconds | Validity period of the `OPTIONS` request result | int | No |
| ExposeHeaders | Custom header information that can be received by the browser from the server | []string | No |


### Querying a CORS configuration

#### API description

This API (GET Bucket cors) is used to query the CORS configuration of a bucket.

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
The result of the request is returned through `GetBucketCORSResult`.

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

| Parameter | Description | Type | Required |
| -------------- | ------------------------------------------------------------ | -------- | ---- |
| BucketCORSRule | CORS rules, including `ID`, `MaxAgeSeconds`, `AllowedOrigin`, `AllowedMethod`, `AllowedHeader`, and `ExposeHeader` | struct | Yes |
| ID | Rule ID | string | No |
| AllowedMethods | Allowed methods, including GET, PUT, HEAD, POST, and DELETE | []string | Yes |
| AllowedOrigins | Allowed access sources, such as `"http://cloud.tencent.com"`. Asterisks (*) are supported. | []string | Yes |
| AllowedHeaders | Allowed custom HTTP request headers that can be used by requests. Asterisks (*) are supported. | []string | No |
| MaxAgeSeconds | Validity period of the `OPTIONS` request result | int | No |
| ExposeHeaders | Custom header information that can be received by the browser from the server | []string | No |

### Deleting CORS configuration

#### API description

This API (DELETE Bucket cors) is used to delete the CORS configuration of a bucket.

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
### Setting lifecycle configuration

#### API description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration for a bucket.

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

| Parameter | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule | Lifecycle rules, including `ID`, `Filter`, `Status`, `Expiration`, ``Transition`, and `AbortIncompleteMultipartUpload` | List | Yes |
| ID | Rule ID | string | No |
| Status | Sets whether a rule is enabled. Valid values: `Enabled`, `Disabled` | string | Yes |
| Filter | Describes a collection of objects that are subject to the rules. To set rules for all objects in the bucket, leave `Prefix` empty. | struct | Yes |
| Transition | Sets the rule for changing the storage class of the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. Available values for StorageClass: Standard_IA and Archive. Multiple rules can be set at a time. | struct | No |
| Expiration | Sets the expiration rule for the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. | struct | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which a multipart upload operation must be completed once it starts | struct | No |

### Querying a lifecycle configuration

#### API description

This API (GET Bucket lifecycle) is used to query the lifecycle management configuration of a bucket.

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

The result of the request is returned through `GetBucketLifecycleResult`.

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

| Parameter | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule | Lifecycle rules, including `ID`, `Filter`, `Status`, `Expiration`, `Transition`, and `AbortIncompleteMultipartUpload` | List | Yes |
| ID | Rule ID | string | No |
| Status | Sets whether a rule is enabled. Valid values: `Enabled`, `Disabled` | string | Yes |
| Filter | Describes a collection of objects that are subject to the rules. To set rules for all objects in the bucket, leave `Prefix` empty. | struct | Yes |
| Transition | Sets the rule for changing the storage class of the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. Available values for StorageClass: Standard_IA and Archive. Multiple rules can be set at a time. | struct | No |
| Expiration | Sets the expiration rule for the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. | struct | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which a multipart upload operation must be completed once it starts | struct | No |


### Deleting a lifecycle configuration

#### API description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle configuration of a bucket.

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

#### API description

This API (PUT Bucket versioning) is used to set the versioning configuration for a bucket.

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
| Parameter | Description | Type |
| ----| ---- | ---- |
| BucketPutVersionOptions | Versioning policies | struct |
| Status | Indicates whether versioning is enabled. Enumerated values: `Suspended` (versioning is paused), `Enabled` (versioning is enabled) | string |

### Querying versioning

#### API description

This API (GET Bucket versioning) is used to query the versioning configuration of a bucket.

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
| Parameter | Description | Type |
| ----| ---- | ---- |
| BucketGetVersionResult | Versioning policies | struct |
| Status | Indicates whether versioning is enabled. Enumerated values: `Suspended` (versioning is paused), `Enabled` (versioning is enabled) | string |

## Cross-Bucket Replication
### Setting cross-bucket replication

#### API description

This API (PUT Bucket replication) is used to set the cross-bucket replication rule for a bucket.

#### Method prototype
```go
func (s *BucketService) PutBucketReplication(ctx context.Context, opt *PutBucketReplicationOptions) (*Response, error)
```

#### Sample request
[//]: # ".cssg-snippet-put-bucket-replication"
```go
opt := &cos.PutBucketReplicationOptions{
    // qcs::cam::uin/[UIN]:uin/[Subaccount]
    Role: "qcs::cam::uin/100000000001:uin/100000000001",
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
| Parameter | Description | Type |
| ----| ---- | ---- |
| PutBucketReplicationOptions | Cross-bucket replication rules | struct |
| Role | Request initiator identifier, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | string |
| Rule | Specific configuration. You can set a maximum of 1,000 rules, which should apply to the same destination bucket | NSArray *|
| ID | Indicates the name of a specific rule | String |
| Status | `Rule` status identifier. Enumerated values: `Enabled`, `Disabled` | string |
| Prefix | Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. To match the root directory, leave this parameter empty. | NSString* |
| Destination | Destination bucket information | struct |
| Bucket | Resource identifier, formatted as `qcs::cos:[region]::[bucketname-AppId]` | string |
| StorageClass | Storage class. Enumerated values: `STANDARD`, `STANDARD_IA`. Defaults to the storage class of the source bucket. | string |

### Querying cross-bucket replication

#### API description

This API (GET Bucket replication) is used to query the cross-bucket replication rule of a bucket.

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
| Parameter | Description | Type |
| ----| ---- | ---- |
| GetBucketReplicationResult | Cross-bucket replication rules | struct |
| Role | Request initiator identifier, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`  | string |
| Rule | Specific configuration. You can set a maximum of 1,000 rules, which should apply to the same destination bucket | NSArray *|
| id | Name of the `Rule` | String |
| Status | `Rule` status identifier. Enumerated values: `Enabled`, `Disabled` | string |
| Prefix | Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. To match the root directory, leave this parameter empty. | NSString* |
| Destination | Destination bucket information | struct |
| Bucket | Resource identifier, formatted as `qcs::cos:[region]::[bucketname-AppId]` | string |
| StorageClass | Storage class. Enumerated values: `STANDARD`, `STANDARD_IA`. Defaults to the storage class of the source bucket. | string |


### Deleting a cross-bucket replication rule

#### API description

This API (DELETE Bucket replication) is used to delete the cross-bucket replication rule from a bucket.

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

## Bucket Policies

### Setting bucket policies

#### API description

This API (PUT Bucket policy) is used to write a permission policy for a bucket. The policy passed in this API will overwrite the existing one (if any) in the bucket.

#### Method prototype
```go
func (s *BucketService) PutPolicy(ctx context.Context, opt *BucketPutPolicyOptions) (*Response, error)
```

#### Sample request
```go
opt := &cos.BucketPutPolicyOptions{
	Version: "2.0",
	Statement: []cos.BucketStatement{
	{
		Principal: map[string][]string{
			"qcs": []string{
				"qcs::cam::uin/100000000001:uin/100000000011", // Replace with the uin of the account to be granted the permission.
			},
		},
		Action: []string{
			"name/cos:GetObject",
		},
		Effect: "allow",
		Resource: []string{
			// Change it to the allowed path prefix (such as "a.jpg", "a/*", or "*"). You can determine the upload path based on your login status. (Keep in mind that using asterisks (*) could bring high risks.)
			"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/exampleobject",
		},
		Condition: map[string]map[string]interface{}{
			"ip_not_equal": map[string]interface{}{
				"qcs:ip": []string{
					"192.168.1.1",
				},
			},
		},
	},
	},
}
_, err := c.Bucket.PutPolicy(context.Background(), opt)
```

#### Parameter description

```go
type BucketStatement struct {
    Principal map[string][]string
    Action    []string
    Effect    string
    Resource  []string
    Condition map[string]map[string]interface{}
}

type BucketPutPolicyOptions struct {
    Statement []BucketStatement
    Version   string
    Principal map[string][]string
}
```
| Parameter | Description | Type |
| ----| ---- | ---- |
| Statement | Detailed information about one or more permissions | Struct |
| Version | Policy syntax version | Struct            |
| Principal | Entity to which the permission is granted. For more information, please see [Access Policy Language Overview](https://intl.cloud.tencent.com/document/product/436/18023) | String |
| action | COS API. You can specify one, several, or all (`*`) COS APIs as needed, e.g., set `action` to `name/cos:GetService`. **Note that this parameter is case-sensitive**. |
| Effect | Allow or explicitly deny | String |
| resource | Specific data authorized to be operated on. It can be any resource, a resource whose path prefix is specified, a resource with a specified absolute path, or a combination thereof. | Array |
| condition | Condition (optional). For more information, please see [Condition](https://intl.cloud.tencent.com/document/product/598/10603) | Struct |

### Querying bucket policies

#### API description

 This API (GET Bucket policy) is used to read the permission policy of a bucket.

#### Method prototype

```go
func (s *BucketService) GetPolicy(ctx context.Context) (*BucketGetPolicyResult, *Response, error)
```

#### Sample request
```go
res, resp, err := c.Bucket.GetPolicy(context.Background())
```

#### Response description

```go
type BucketGetPolicyResult BucketPutPolicyOptions
// For details, please see `BucketPutPolicyOptions`.
```

### Deleting bucket policies

#### API description

  This API (DELETE Bucket policy) is used to delete the permission policy of a bucket.

#### Method prototype

```go
func (s *BucketService) DeletePolicy(ctx context.Context) (*Response, error)
```

#### Sample request

```go
resp, err := c.Bucket.DeletePolicy(context.Background())
```
