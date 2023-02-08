## Overview

This document provides an overview of APIs and SDK code samples related to bucket copying.[](id:API)

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-bucket replication | Sets a cross-bucket replication rule for a versioning-enabled bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-bucket replication | Queries the cross-bucket replication rule of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-bucket replication | Deletes a cross-bucket replication rule of a bucket |

## Setting Cross-Bucket Replication

#### Feature description

This API (PUT Bucket replication) is used to set the cross-bucket replication rule for a bucket.

#### Method prototype
```go
func (s *BucketService) PutBucketReplication(ctx context.Context, opt *PutBucketReplicationOptions) (*Response, error)
```

#### Sample request
[//]: # (.cssg-snippet-put-bucket-replication)
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-12500000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })
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
    if err != nil{
        panic(err)
    }
}
```

#### Field description
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
	StorageClass   string
}
```

| Parameter | Description | Type |
| ----| ---- | ---- |
| PutBucketReplicationOptions | Cross-bucket replication rules | struct |
| Role | Request initiator identifier, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | string |
| Rule | Specific configuration. You can set a maximum of 1,000 rules, which should apply to the same destination bucket | struct *|
| id | Name of the `Rule` | String |
| Status | `Rule` status identifier. Enumerated values: `Enabled`, `Disabled` | string |
| Prefix | Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. To match the root directory, leave this parameter empty. | string  |
| Destination | Destination bucket information | struct |
| Bucket | Resource identifier, formatted as `qcs::cos:[region]::[bucketname-AppId]` | string |
| StorageClass | Storage class. Enumerated values: `STANDARD`, `STANDARD_IA`. For more storage classes, please see the [API](#API) overview above. Defaults to the storage class of the source bucket.  | string |

## Querying Cross-Bucket Replication

#### Feature description

This API (GET Bucket replication) is used to query the cross-bucket replication rule of a bucket.

#### Method prototype
```go
func (s *BucketService) GetBucketReplication(ctx context.Context) (*GetBucketReplicationResult, *Response, error)
```

#### Sample request
[//]: # (.cssg-snippet-get-bucket-replication)
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-12500000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })
    _, _, err := client.Bucket.GetBucketReplication(context.Background())
    if err != nil{
        panic(err)
    }
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
	StorageClass   string
}
```

| Parameter | Description | Type |
| ----| ---- | ---- |
| GetBucketReplicationResult | Cross-bucket replication rules | struct |
| Role | Request initiator identifier, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | string |
| Rule | Specific configuration. You can set a maximum of 1,000 rules, which should apply to the same destination bucket | struct *|
| id | Name of the `Rule` | String |
| Status | `Rule` status identifier. Enumerated values: `Enabled`, `Disabled` | string |
| Prefix | Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. To match the root directory, leave this parameter empty. | string  |
| Destination | Destination bucket information | struct |
| Bucket | Resource identifier, formatted as `qcs::cos:[region]::[bucketname-AppId]` | string |
| StorageClass | Storage class. Enumerated values: `STANDARD`, `STANDARD_IA`. For more storage classes, please see the [API](#API) overview above. Defaults to the storage class of the source bucket.  | string |


## Deleting Cross-Bucket Replication

#### Feature description

This API (DELETE Bucket replication) is used to delete a cross-bucket replication rule from a bucket.

#### Method prototype
```go
func (s *BucketService) DeleteBucketReplication(ctx context.Context) (*Response, error)
```

#### Sample request
[//]: # (.cssg-snippet-delete-bucket-replication)
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-12500000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })
    _, err := client.Bucket.DeleteBucketReplication(context.Background())
    if err != nil{
        panic(err)
    }
}
```

