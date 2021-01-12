## Overview

This document provides an overview of APIs and SDK code samples related to cross-bucket replication.[](id:API)

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-bucket replication | Sets a cross-bucket replication rule for a versioning-enabled bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying a cross-bucket replication rule | Queries the cross-bucket replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting a cross-bucket replication rule | Deletes a cross-bucket replication rule of a bucket |

## Setting Cross-Bucket Replication

#### Feature description

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
| Rule | Specific configuration. You can set a maximum of 1,000 rules, which should apply to the same destination bucket | struct |
| ID | Indicates the name of a specific rule | String |
| Status | `Rule` status identifier. Enumerated values: `Enabled`, `Disabled` | string |
| Prefix | Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. To match the root directory, leave this parameter empty. | string |
| Destination | Destination bucket information | struct |
| Bucket | Resource identifier, formatted as `qcs::cos:[region]::[bucketname-AppId]` | string |
| StorageClass | Storage class. Enumerated values: `STANDARD`, `STANDARD_IA`. Defaults to the storage class of the source bucket. For more information, please see [API](#API) overview. | string |

## Querying Cross-Bucket Replication

#### Feature description

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
| Rule | Specific configuration. You can set a maximum of 1,000 rules, which should apply to the same destination bucket | struct |
| id | Name of the `Rule` | string |
| Status | `Rule` status identifier. Enumerated values: `Enabled`, `Disabled` | string |
| Prefix | Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. To match the root directory, leave this parameter empty. | string |
| Destination | Destination bucket information | struct |
| Bucket | Resource identifier, formatted as `qcs::cos:[region]::[bucketname-AppId]` | string |
| StorageClass | Storage class. Enumerated values: `STANDARD`, `STANDARD_IA`. Defaults to the storage class of the source bucket. For more information, please see [API](#API) overview. | string |


## Deleting Cross-Bucket Replication

#### Feature description

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

