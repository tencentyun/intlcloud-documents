

## Overview

This document provides an overview of APIs and SDK code samples related to inventory.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Setting an inventory job | Sets an inventory job in a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries inventory jobs for a bucket |
| [List Bucket Inventory Configurations](https://intl.cloud.tencent.com/document/product/436/30672) | Querying all inventories | Queries all inventory jobs of a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job of a bucket |

## Setting Inventory Job

#### Feature description

This API (PUT Bucket inventory) is used to create an inventory job in a bucket.

#### Method prototype

```go
func (s *BucketService) PutInventory(ctx context.Context, id string, opt *BucketPutInventoryOptions) (*Response, error)
```

#### Sample request

```go
opt := &cos.BucketPutInventoryOptions{
    ID: "test_id",
	// True or False
	IsEnabled:              "True",
	IncludedObjectVersions: "All",
	Filter: &cos.BucketInventoryFilter{
		Prefix: "test",
    },
	OptionalFields: &cos.BucketInventoryOptionalFields{
		BucketInventoryFields: []string{
			"Size", "LastModifiedDate",
		},
	},
	Schedule: &cos.BucketInventorySchedule{
		// Weekly or Daily
		Frequency: "Daily",
	},
	Destination: &cos.BucketInventoryDestination{
		Bucket: dBucket,
		Format: "CSV",
	},
}
resp, err := client.Bucket.PutInventory(context.Background(), id, opt)
```

#### Parameter description

```go
type BucketInventoryFilter struct {
    Prefix string 
}
type BucketInventoryOptionalFields struct {
    BucketInventoryFields []string 
}
type BucketInventorySchedule struct {
    Frequency string 
}
type BucketInventoryEncryption struct {
    SSECOS string 
}
type BucketInventoryDestination struct {
    Bucket     string                     
    AccountId  string                     
    Prefix     string                    
    Format     string
    Encryption *BucketInventoryEncryption 
}
// BucketPutInventoryOptions ...
type BucketPutInventoryOptions struct {
    XMLName                xml.Name                     
    ID                     string                         
    IsEnabled              string                       
    IncludedObjectVersions string                      
    Filter                 *BucketInventoryFilter        
    OptionalFields         *BucketInventoryOptionalFields 
    Schedule               *BucketInventorySchedule      
    Destination            *BucketInventoryDestination
}
```

| Parameter Name | Description | Type |
| ------------------------- | ------------------------------------------------------------ | -------- |
| BucketPutInventoryOptions | Inventory configuration information of bucket                                           | Struct   |
| ID                        | Inventory name, corresponding to the ID in the request parameter                           | String   |
| IsEnabled              | Inventory status flag: <br><li>If this is set to `true`, the inventory is enabled; <br><li>if `false`, no inventories will be generated | String        |
| IncludedObjectVersions | Whether to include object versions in the inventory <br><li>If this is set to `All`, the inventory will include all object versions and add `VersionId`, `IsLatest`, and `DeleteMarker` fields <br><li>If `Current`, no object version information will be included in the inventory | String |
| Filter                    | Filter                                                       | Struct   |
| Prefix | Prefix of the objects to be analyzed | String |
| OptionalFields            | Sets the analysis items that should be included in the inventory result                               | Struct   |
| BucketInventoryFields     | Name of the analysis items that can be optionally included in the inventory result. Valid values: Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, ReplicationStatus | []String |
| Schedule                  | Inventory job frequency                                                 | Struct   |
| Frequency | Inventory job frequency. Enumerated values: Daily, Weekly | String |
| Destination            | Describes the information of the inventory result storage                                       | Struct   |
| Bucket | Name of the bucket where the inventory result is stored | String |
| AccountId                 | Bucket owner ID, such as 100000000001                          | String   |
| Prefix | Prefix of the inventory result | String |
| Format | File format of the inventory result. CSV is available | String |
| Encryption             | Option to provide server-side encryption for the inventory result                               | Struct         |
| SSECOS                    | Uses SSE-COS encryption                                            | String   |

#### Error code description

Some frequent special errors that may occur with this request are listed below:

| Error code | Description | Status code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You probably do not have access to the bucket. | HTTP 403 Forbidden |

## Querying Inventory Job

#### Feature description

This API (GET Bucket inventory) is used to query the inventory job information in a bucket.

#### Method prototype

```go
func (s *BucketService) GetInventory(ctx context.Context, id string) (*BucketGetInventoryResult, *Response, error)
```

#### Sample request

```go
v, response, err := client.Bucket.GetInventory(context.Background(), id)
```

#### Returned result description

```go
type BucketGetInventoryResult BucketPutInventoryOptions
```

| Parameter Name | Description | Type |
| ------------------------- | ------------------------------------------------------------ | -------- |
| BucketPutInventoryOptions | Inventory configuration information of bucket                                           | Struct   |
| ID                        | Inventory name, corresponding to the ID in the request parameter                           | String   |
| IsEnabled              | Inventory status flag: <br><li>If this is set to `true`, the inventory is enabled; <br><li>if `false`, no inventories will be generated | String        |
| IncludedObjectVersions | Whether to include object versions in the inventory <br><li>If this is set to `All`, the inventory will include all object versions and add `VersionId`, `IsLatest`, and `DeleteMarker` fields <br><li>If `Current`, no object version information will be included in the inventory | String |
| Filter                    | Filter                                                       | Struct   |
| Prefix | Prefix of the objects to be analyzed | String |
| OptionalFields            | Sets the analysis items that should be included in the inventory result                               | Struct   |
| BucketInventoryFields     | Name of the analysis items that can be optionally included in the inventory result. Valid values: Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, ReplicationStatus | []String |
| Schedule                  | Inventory job frequency                                                 | Struct   |
| Frequency | Inventory job frequency. Enumerated values: Daily, Weekly | String |
| Destination            | Describes the information of the inventory result storage                                       | Struct   |
| Bucket | Name of the bucket where the inventory result is stored | String |
| AccountId                 | Bucket owner ID, such as 100000000001                          | String   |
| Prefix | Prefix of the inventory result | String |
| Format | File format of the inventory result. CSV is available | String |
| Encryption             | Option to provide server-side encryption for the inventory result                               | Struct         |
| SSECOS                    | Uses SSE-COS encryption                                            | String   |

## Querying All Inventories

#### Feature description

This API (List Bucket Inventory Configurations) is used to request that all inventory jobs in a bucket be returned. Up to 1,000 inventory jobs can be configured in one bucket.

#### Method prototype

```go
func (s *BucketService) ListInventoryConfigurations(ctx context.Context, token string) (*ListBucketInventoryConfigResult, *Response, error)
```

#### Sample request

```go
v, resp, err := client.Bucket.ListInventoryConfigurations(context.Background(), "")
```

#### Returned result description

```go
type BucketListInventoryConfiguartion BucketPutInventoryOptions

type ListBucketInventoryConfigResult struct {
    XMLName                 xml.Name          
    InventoryConfigurations []BucketListInventoryConfiguartion 
    IsTruncated             bool   
    ContinuationToken       string    
    NextContinuationToken   string
}
```

| Parameter Name | Description | Type |
| ------------------------------- | ------------------------------------------------------------ | ------ |
| ListBucketInventoryConfigResult | All inventory configuration information of bucket                                       | Struct |
| InventoryConfigurations         | Inventory configuration information                                                 | Struct |
| IsTruncated            | Flag about whether all inventory jobs have been listed. If yes, it is `false`; otherwise, it is `true` | Bool   |
| ContinuationToken               | Flag of the inventory list on the current page, which can be understood as the page number. It corresponds to the `continuation-token` parameter in the request | String |
| NextContinuationToken | Flag of the next page of inventory list. If there is a value in this parameter, the value can be used as the `continuation-token` parameter to initiate a GET request to get the inventory job information of the next page | String |

## Deleting Inventory Job

#### Feature description

This API (DELETE Bucket inventory) is used to delete a specified inventory job of a bucket.

#### Method prototype

```go
func (s *BucketService) DeleteInventory(ctx context.Context, id string) (*Response, error)

```

#### Sample request

```go
resp, err = client.Bucket.DeleteInventory(context.Background(), "test_id")

```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ---------- | ------ |
| id       | Inventory name | String |
