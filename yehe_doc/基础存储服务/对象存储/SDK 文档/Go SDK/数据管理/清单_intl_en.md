

## Feature Overview

This document provides an overview of APIs and SDK code samples for COS inventory.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | Creating an inventory job | Creates an inventory job for a bucket |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | Querying inventory jobs | Queries the inventory jobs of a bucket |
|  [List Bucket Inventory Configurations](https://intl.cloud.tencent.com/document/product/436/30627) | Querying the list of inventory configurations | Queries the list of inventory configurations for a bucket |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | Deleting an inventory job | Deletes an inventory job from a bucket |

## Creating an Inventory Job

#### Feature description

This API (PUT Bucket inventory) is used to create an inventory job for a bucket.

#### Method prototype

```go
func (s *BucketService) PutInventory(ctx context.Context, id string, opt *BucketPutInventoryOptions) (*Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-put-bucket-inventory"
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
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://www.tencentcloud.com/document/product/598/32675.
        },
    })
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
            Bucket: "dest_bucket-1250000000",
            Format: "CSV",
        },
    }
    _, err := client.Bucket.PutInventory(context.Background(), "test_id", opt)
    if err != nil{
        // ERROR
    }
}
```

#### Field description

```go
type BucketInventoryFilter struct {
    Prefix     string 
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

| Parameter | Description | Type |
| ------------------------- | ------------------------------------------------------------ | -------- |
| BucketPutInventoryOptions | Inventory configuration information of the bucket                                           | Struct   |
| ID                       | Inventory name, corresponding to the ID in the request parameter                           | String |
| IsEnabled             | Indicates whether inventory is enabled.<br><li>`true` indicates it is enabled<br><li>`false` indicates no inventory list will be generated.                                           | String      |
| IncludedObjectVersions | Indicates whether to include object versions in the inventory<br><li>If this is set to `All`, the inventory will include all object versions and the additional fields `VersionId`, `IsLatest`, and `DeleteMarker`.<br><li>If this is set to `Current`, no object versions will be included in the inventory.</li> | String |
| Filter                    | Filter                                                       | Struct   |
| Prefix | Prefix of the objects to be inventoried | String |
| OptionalFields                   | Sets the analysis items that should be included in the inventory result                               | Struct |
| BucketInventoryFields     | Optional analysis dimensions, including `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `IsMultipartUploaded`, and `ReplicationStatus` | []String |
| Schedule                  | Schedule for the inventory job                                                 | Struct   |
| Frequency             | Frequency of the inventory job. Enumerated values: `Daily`, `Weekly`                                           | String      |
| Destination              | Destination to store the inventory result                                       | Struct |
| Bucket             | Name of the bucket that stores the inventory results                                           | String      |
| AccountId             | ID of the bucket owner, e.g. 100000000001                                           | String      |
| Prefix | Prefix of the inventory result | String |
| Format             | Format of the inventory results. Option: `CSV`                                           | String      |
| Encryption                | Option of enabling server-side encryption for inventory results                               | Struct   |
| SSECOS                    | Encryption with SSE-COS                                            | String   |

#### Error codes

The following describes some common errors that may occur when you call this API:

| Error Code | Description | Status Code |
| --------------------- | -------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied          | Unauthorized access. You most likely do not have access permission for the bucket | HTTP 403 Forbidden   |

## Querying Inventory Jobs

#### Feature description

This API is used to query the inventory jobs of a bucket.

#### Method prototype

```go
func (s *BucketService) GetInventory(ctx context.Context, id string) (*BucketGetInventoryResult, *Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-get-bucket-inventory"
```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://www.tencentcloud.com/document/product/598/32675.
        },
    })
    v, _, err := client.Bucket.GetInventory(context.Background(), "test_id")
    if err != nil{
        // ERROR
    }
    fmt.Println(v)
}
```

#### Response description

```go
type BucketGetInventoryResult BucketPutInventoryOptions
```

| Parameter | Description | Type |
| ------------------------- | ------------------------------------------------------------ | -------- |
| BucketPutInventoryOptions | Inventory configuration information of the bucket                                           | Struct   |
| ID                       | Inventory name, corresponding to the ID in the request parameter                           | String |
| IsEnabled             | Indicates whether inventory is enabled.<br><li>`true` indicates it is enabled<br><li>`false` indicates no inventory list will be generated.                                           | String      |
| IncludedObjectVersions | Indicates whether to include object versions in the inventory<br><li>If this is set to `All`, the inventory will include all object versions and the additional fields `VersionId`, `IsLatest`, and `DeleteMarker`.<br><li>If this is set to `Current`, no object versions will be included in the inventory.</li> | String |
| Filter                    | Filter                                                       | Struct   |
| Prefix | Prefix of the objects to be inventoried | String |
| OptionalFields                   | Sets the analysis items that should be included in the inventory result                               | Struct |
| BucketInventoryFields     | Optional analysis dimensions, including `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `IsMultipartUploaded`, and `ReplicationStatus` | []String |
| Schedule                  | Schedule for the inventory job                                                 | Struct   |
| Frequency             | Frequency of the inventory job. Enumerated values: `Daily`, `Weekly`                                           | String      |
| Destination              | Destination to store the inventory result                                       | Struct |
| Bucket             | Name of the bucket that stores the inventory results                                           | String      |
| AccountId             | ID of the bucket owner, e.g. 100000000001                                           | String      |
| Prefix | Prefix of the inventory result | String |
| Format             | Format of the inventory results. Option: `CSV`                                           | String      |
| Encryption                | Option of enabling server-side encryption for inventory results                               | Struct   |
| SSECOS                    | Encryption with SSE-COS                                            | String   |

## Querying All Inventories

#### Feature description

This API is used to query all inventory jobs configured for a bucket. You can configure up to 1,000 inventory jobs for a bucket.

#### Method prototype

```go
func (s *BucketService) ListInventoryConfigurations(ctx context.Context, token string) (*ListBucketInventoryConfigResult, *Response, error)
```

#### Sample request

[//]: # ".cssg-snippet-list-bucket-inventory"
```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main(){
    // Bucket name in the format of `BucketName-APPID` (`APPID` is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket.
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, see https://intl.cloud.tencent.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://www.tencentcloud.com/document/product/598/32675.
        },
    })
    v, _, err := client.Bucket.ListInventoryConfigurations(context.Background(), "")
    if err != nil{
        // ERROR
    }
    fmt.Println(v)
}
```

#### Response description

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

| Parameter | Description | Type |
| ------------------------------- | ------------------------------------------------------------ | ------ |
| ListBucketInventoryConfigResult | All inventory configuration information of the bucket                                       | Struct |
| InventoryConfigurations         | Inventory configuration information                                                 | Struct |
| IsTruncated            | Flag about whether all inventory jobs have been listed. If yes, it is `false`; otherwise, it is `true` | Bool |
| ContinuationToken      | Flag of the inventory list on the current page, which can be understood as the page number. It corresponds to the `continuation-token` parameter in the request | String |
| NextContinuationToken           | ListInventoryConfigurationResult | Identifier of the next response. You can pass the value of this parameter to `continuation-token` and initiate a GET request to obtain the inventory jobs from the next response | String |

## Deleting an Inventory Job

#### Feature description

This API is used to delete a specified inventory job from a bucket.

#### Method prototype

```go
func (s *BucketService) DeleteInventory(ctx context.Context, id string) (*Response, error)

```

#### Sample request

[//]: # ".cssg-snippet-delete-bucket-inventory"
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
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // Get the key from environment variables
            // Environment variable `SECRETID` refers to the user's `SecretId`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://www.tencentcloud.com/document/product/598/32675.
        },
    })
    _, err := client.Bucket.DeleteInventory(context.Background(), "test_id")
    if err != nil{
        // ERROR
    }
}
```

#### Field description

| Parameter | Description | Type |
| -------- | ---------- | ------ |
| id           | Inventory name                                                   | String |

