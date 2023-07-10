## Overview

This document provides an overview of APIs and SDK code samples related to basic bucket operations.


| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and whether you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket from a specified account |




## Querying a Bucket List

#### Feature description

This API is used to query the list of all buckets under a specified account.

#### Method prototype

```go
func (s *ServiceService) Get(ctx context.Context) (*ServiceGetResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-service)
```go
s, _, err := c.Service.Get(context.Background())
if err != nil {
    panic(err)
}
```


#### Response description

The result of the request is returned through GetServiceResult.

```go
type ServiceGetResult struct {
    Owner   *Owner  
    'Bucket' => $bucket 
}
type Owner struct {
    ID          string 
    DisplayName string                                              
}
type Bucket struct {
	Name       string
    Region     string
    CreationDate string                                               
} 
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| ID | ID of the bucket owner | String |
| DisplayName | Name of the bucket owner | String |
| Name | Bucket name | String |
| Region | Bucket region | String |
| CreationDate | Time when the bucket was created, in ISO 8601 format, such as 2016-11-09T08:46:32.000Z | String |

## Creating a Bucket

#### Feature description

This API is used to create a bucket under a specified account.

#### Method prototype

```go
func (s *BucketService) Put(ctx context.Context, opt *BucketPutOptions) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket)
```go
opt := &cos.BucketGetOptions{
    XCosACL: "private",
}
_, err := client.Bucket.Put(context.Background(), opt)
if err != nil {
    panic(err)
}


// Create a multi-AZ bucket
opt.CreateBucketConfiguration = &cos.CreateBucketConfiguration{
    BucketAZConfig: "MAZ",
}
_, err := client.Bucket.Put(context.Background(), opt)
if err != nil {
    panic(err)
}

```

#### Parameter description
```go
type BucketPutOptions struct {
	XCosACL              string 
	XCosGrantRead        string  
	XCosGrantWrite       string  
	XCosGrantFullControl string 
    CreateBucketConfiguration *CreateBucketConfiguration
}
type CreateBucketConfiguration struct {
    BucketAZConfig string
}
```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL | Sets the bucket ACL, such as private, public-read, and public-read-write | String | No |
| XCosGrantFullControl | Grants a specified account permission to read and write a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, use `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, use `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. <br>Example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |
| XCosGrantRead | Grants a specified account permission to read a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, use `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, use `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. <br>Example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |
| XCosGrantWrite | Grants a specified account permission to write to a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, use `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, use `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. <br>Example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |
| BucketAZConfig | Bucket AZ configuration. Set the parameter to `MAZ` to create MAZ buckets. MAZ buckets are currently supported only in the Beijing and Guangzhou regions. | Struct | No   |

## Checking a Bucket and Its Permissions

#### Feature description

This API is used to verify whether a bucket exists and you have the permission to access it.

#### Method prototype

```go
func (s *BucketService) Head(ctx context.Context) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-head-bucket)
```go
_, err := client.Bucket.Head(context.Background())
if err != nil {
    panic(err)
}
```


## Deleting a Bucket

#### Feature description

This API (DELETE Bucket) is used to delete an empty bucket under a specified account.

#### Method prototype

```go
func (s *BucketService) Delete(ctx context.Context) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket)
```go
_, err := client.Bucket.Delete(context.Background())
if err != nil {
    panic(err)
}
```
