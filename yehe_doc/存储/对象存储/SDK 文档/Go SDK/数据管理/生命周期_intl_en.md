## Overview

This document provides an overview of APIs and SDK code samples related to lifecycle.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle configuration | Sets lifecycle for a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying a lifecycle configuration | Queries the lifecycle configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting a lifecycle configuration | Deletes the lifecycle configuration of a bucket |

## Setting a Lifecycle Configuration

#### Feature description

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
	DaysAfterInitiation string 
}
```

| Parameter | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule | Lifecycle rules, including `ID`, `Filter`, `Status`, `Expiration`, `Transition`, and `AbortIncompleteMultipartUpload` | List | Yes |
| ID | Rule ID | String | No |
| Status | Sets whether a rule is enabled. Valid values: `Enabled`, `Disabled` | String | Yes |
| Filter | Specifies a set of objects that the rules apply to. To set the rules for all objects in the bucket, leave `Prefix` empty. | Struct | Yes |
| Transition | Sets the rule for changing the storage class of the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. Valid values for `StorageClass` are `Standard_IA` and `Archive`. Multiple rules can be set at a time. | Struct | No |
| Expiration | Sets the expiration rule for the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. | Struct | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which a multipart upload operation must be completed once it starts | Struct | No |

## Querying a Lifecycle Configuration

#### Feature description

This API (GET Bucket lifecycle) is used to query the lifecycle configuration of a bucket.

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
	DaysAfterInitiation string 
}
```

| Parameter | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------ | ---- |
| BucketLifecycleRule | Lifecycle rules, including `ID`, `Filter`, `Status`, `Expiration`, `Transition`, and `AbortIncompleteMultipartUpload` | List | Yes |
| ID | Rule ID | String | No |
| Status | Sets whether a rule is enabled. Valid values: `Enabled`, `Disabled` | String | Yes |
| Filter | Specifies a set of objects that the rules apply to. To set the rules for all objects in the bucket, leave `Prefix` empty. | Struct | Yes |
| Transition | Sets the rule for changing the storage class of the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. Valid values for `StorageClass` are `Standard_IA` and `Archive`. Multiple rules can be set at a time. | Struct | No |
| Expiration | Sets the expiration rule for the object. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. | Struct | No |
| AbortIncompleteMultipartUpload | Indicates the number of days within which a multipart upload operation must be completed once it starts | Struct | No |


## Deleting a Lifecycle Configuration

#### Feature description

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
