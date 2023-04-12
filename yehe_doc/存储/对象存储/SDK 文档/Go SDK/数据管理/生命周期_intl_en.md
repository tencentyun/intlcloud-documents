## Overview

This document provides an overview of APIs and SDK code samples related to lifecycles.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://www.tencentcloud.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management configuration for a bucket |
| [GET Bucket lifecycle](https://www.tencentcloud.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://www.tencentcloud.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

## Setting a Lifecycle Configuration

#### Feature description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration for a bucket.

#### Method prototype
```go
func (s *BucketService) PutLifecycle(ctx context.Context, opt *BucketPutLifecycleOptions) (*Response, error)
```

#### Sample request
[//]: # (.cssg-snippet-put-bucket-lifecycle)
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
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://www.tencentcloud.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
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
    lc := &cos.BucketPutLifecycleOptions{
        Rules: []cos.BucketLifecycleRule{
            {
                ID:     "1234",
                Filter: &cos.BucketLifecycleFilter{Prefix: "test"},
                Status: "Enabled",
                Transition: []cos.BucketLifecycleTransition{
                    {
                        Days:         10,
                        StorageClass: "Standard",
                    },
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
    if err != nil{
        panic(err)
    }
}
```

#### Parameter description
```go
type BucketPutLifecycleOptions struct {
    XMLName                xml.Name
    Rules   []BucketLifecycleRule
}
type BucketLifecycleRule struct {
    ID                             string
    Status                         string
    Filter                         *BucketLifecycleFilter
    Transition                     []BucketLifecycleTransition
    Expiration                     *BucketLifecycleExpiration
    AbortIncompleteMultipartUpload *BucketLifecycleAbortIncompleteMultipartUpload
    NoncurrentVersionTransition    []BucketLifecycleNoncurrentVersion
    NoncurrentVersionExpiration    *BucketLifecycleNoncurrentVersion
}
type BucketLifecycleFilter struct {
    Prefix     string
    Tag    *BucketTaggingTag
    And    *BucketLifecycleAndOperator
}
type BucketLifecycleTransition struct {
	Date         string 
	Days         int    
	StorageClass   string
}
type BucketLifecycleExpiration struct {
    Date                      string
    Days                      int
    ExpiredObjectDeleteMarker bool
}
type BucketLifecycleNoncurrentVersion struct {
    NoncurrentDays int
    StorageClass   string
}
type BucketLifecycleAbortIncompleteMultipartUpload struct {
	DaysAfterInitiation int 
}
```

| Parameter | Parent Node | Description | Type | Required |
| :----------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------- | :------- |
| LifecycleConfiguration | None | Lifecycle configuration | Container | Yes |
| Rule | LifecycleConfiguration | Rule description | Container | Yes |
| ID | LifecycleConfiguration.Rule | A unique identifier for the rule. It can be up to 255 characters. | String | No |
| Filter | LifecycleConfiguration.Rule | Identifies objects that a lifecycle rule applies to. | Container | Yes |
| And                            | LifecycleConfiguration.Rule .Filter                          | A subset of the object filter. This element is only required when there are more than one filter criteria (for example, filtering with `Prefix` and `Tag` at the same time, or with more than one `Tag`). | Container | No       |
| Prefix                         | LifecycleConfiguration.Rule .Filter.And                      | Matching prefix for the rule. It specifies objects that the lifecycle rule applies to. There can be one `Prefix` at most. | String    | No       |
| Tag                            | LifecycleConfiguration.Rule .Filter.And                      | A set of tags. Up to 10 tags are supported.                                   | Container | No       |
| Key                            | LifecycleConfiguration.Rule .Filter.And.Tag                  | Key of the tag. It can be up to 128 bytes. Letters, digits, spaces, plus signs (+), minus signs (-), underscores (_), equal signs (=), dots (.), colons (:), and slashes (/) are supported. | String    | No       |
| Value                          | LifecycleConfiguration.Rule .Filter.And.Tag                  | Value of the tag. It can be up to 256 bytes. Letters, digits, spaces, plus signs (+), minus signs (-), underscores (_), equal signs (=), dots (.), colons (:), and slashes (/) are supported. | String    | No       |
| Status | LifecycleConfiguration.Rule | Indicates whether the rule is enabled. Enumerated values: `Enabled`, `Disabled` | String | Yes |
| Expiration | LifecycleConfiguration.Rule | Expiration attributes of the rule | Container | No |
| Transition | LifecycleConfiguration.Rule    | Specifies when to transition the object and the target storage class. | Container | No  |
| Days                           | LifecycleConfiguration.Rule .Transition or Expiration        | Specifies the number of days between the date an object was last modified and the date when the operation corresponding to the rule is performed. If it is a `Transition` operation, this value should be a non-negative integer. If it is an `Expiration` operation, this value should be a positive integer. The maximum value is 3650 (days). | Integer   | No       |
| Date                           | LifecycleConfiguration.Rule .Transition or Expiration        | Specifies when the operation corresponding to the rule is performed. Supported formats are `2007-12-01T12:00:00.000Z` and `2007-12-01T00:00:00+08:00`. | String    | No       |
| ExpiredObjectDeleteMarker      | LifecycleConfiguration.Rule .Expiration                      |  Indicates whether the delete marker of an expired object will be removed. Enumerated values: `true`, `false`                     | String    | No       |
| AbortIncompleteMultipartUpload | LifecycleConfiguration.Rule | Specifies the time to abort the multipart upload. | Container | No |
| DaysAfterInitiation | LifecycleConfiguration.Rule.AbortIncompleteMultipartUpload | Specifies the number of days within which the multipart upload must be completed after it starts. | Integer | Yes |
| NoncurrentVersionExpiration | LifecycleConfiguration.Rule | Specifies when noncurrent object versions shall expire. | Container | No |
| NoncurrentVersionTransition | LifecycleConfiguration.Rule | Specifies when to transition objects of noncurrent versions and the target storage class. | Container | No |
| NoncurrentDays                 | LifecycleConfiguration.Rule .NoncurrentVersionExpiration or NoncurrentVersionTransition | Specifies the number of days between the date when an object becomes noncurrent and the date when the operation corresponding to a rule is performed. If it is a `Transition` operation, this value should be a non-negative integer. If it is an `Expiration` operation, this value should be a positive integer. The maximum value is 3650 (days). | Integer   | No       |
| StorageClass | LifecycleConfiguration.Rule .Transition or NoncurrentVersionTransition | Specifies the storage class of the transitioned object. Enumerated values: `STANDARD_IA`, `MAZ_STANDARD_IA`, `INTELLIGENT_TIERING`, `MAZ_INTELLIGENT_TIERING`, `ARCHIVE`, `DEEP_ARCHIVE`. For more information about storage classes, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | Yes |



## Querying a Lifecycle Configuration

#### Feature description

This API (GET Bucket lifecycle) is used to query the lifecycle configuration of a bucket.

#### Method prototype
```go
func (s *BucketService) GetLifecycle(ctx context.Context) (*BucketGetLifecycleResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-lifecycle)
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
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://www.tencentcloud.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
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
    _, _, err := client.Bucket.GetLifecycle(context.Background())
    if err != nil{
        panic(err)
    }
}
```

#### Response description

The result of the request is returned through `GetBucketLifecycleResult`.

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
	StorageClass   string
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
| ID                             | Unique ID of the rule                                         | String | No  |
| Status | Whether a rule is enabled. Valid values: `Enabled`, `Disabled` | String | Yes |
| Filter | Filters objects that the rule applies to. If you want the rule to apply to all objects in the bucket, leave `Prefix` empty. | Struct | Yes |
| Transition | A rule to transition objects between storage classes. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. `StorageClass` can be set to `Standard_IA` or `Archive`. You can set more than one rule. | Struct | No |
| Expiration | Specifies when the objects should expire. You can specify a certain number of days (Days) or a specified date (Date). The date must be in GMT ISO 8601 format. | Struct | No |
| AbortIncompleteMultipartUpload | The number of days within which a multipart upload must be completed | Struct | No |


## Deleting a Lifecycle Configuration

#### Feature description

This API (DELETE Bucket lifecycle) is used to delete the lifecycle configuration from a bucket.

#### Method prototype

```go
func (s *BucketService) DeleteLifecycle(ctx context.Context) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
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
    // Replace it with your region, which can be viewed in the COS console at https://console.cloud.tencent.com/. For more information about regions, visit https://www.tencentcloud.com/document/product/436/6224.
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
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
    _, err := client.Bucket.DeleteLifecycle(context.Background())
    if err != nil{
        panic(err)
    }
}
```
