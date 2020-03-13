## Introduction

This document provides an overview of APIs and SDK code samples related to basic operations on buckets and bucket access control list (ACL).

**Basic Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://cloud.tencent.com/document/product/436/7735) | Retrieving information on a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under a specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a specified bucket |

## Basic Operations

### Querying the Bucket List

#### Feature Description

This API is used to query the list of all buckets under a specified account.

#### Method Prototype

```go
func (s *ServiceService) Get(ctx context.Context) (*ServiceGetResult, *Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-get-service)
```go
s, _, err := c.Service.Get(context.Background())
if err != nil {
    panic(err)
}
```

#### Returned Result
Request result is returned through GetServiceResult.
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

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| ID | ID of the bucket owner | string |
| DisplayName | Name of the bucket owner | string |
| Name | Bucket name | string |
| Region | Bucket region | string |
| CreationDate | Time when the bucket was created, in ISO8601 format, such as 2016-11-09T08:46:32.000Z | string |

### Creating a Bucket

#### Feature Description

This API (PUT Bucket) is used to create a bucket under a specified account.

#### Method Prototype

```go
func (s *BucketService) Put(ctx context.Context, opt *BucketPutOptions) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-put-bucket)
```go
opt := &cos.BucketGetOptions{
    XCosACL: "private",
}
_, err := c.Bucket.Put(context.Background(), nil)
if err != nil {
    panic(err)
}
```

#### Parameter Description
```go
type BucketPutOptions struct {
	XCosACL              string 
	XCosGrantRead        string  
	XCosGrantWrite       string  
	XCosGrantFullControl string 
}
```
| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL | Sets the bucket ACL, such as private, public-read, and public-read-write. | string | No |
| XCosGrantFullControl | Grants the specified account the permission to read and write buckets. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantRead | Grants the specified account the permission to read buckets. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantWrite | Grants the specified account the permission to write buckets. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |

### Retrieving information on a bucket and its permission

#### Feature Description

This API is used to verify whether a bucket exists and whether you have the permission to access it.

#### Method Prototype

```go
func (s *BucketService) Head(ctx context.Context) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-head-bucket)
```go
_, err := client.Bucket.Head(context.Background())
if err != nil {
    panic(err)
}
```


### Deleting a bucket

#### Feature Description

This API is used to delete an empty bucket under a specified account.

#### Method Prototype

```go
func (s *BucketService) Delete(ctx context.Context) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-delete-bucket)
```go
_, err := client.Bucket.Delete(context.Background())
if err != nil {
    panic(err)
}
```

## ACL

### Configuring bucket ACL

#### Feature Description

This API (Put Bucket ACL) is used to set an ACL for the specified bucket.

#### Method Prototype

```go
func (s *BucketService) PutACL(ctx context.Context, opt *BucketPutACLOptions) (*Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-put-bucket-acl)
```go
// 1. Configure bucket ACL through request header
opt := &cos.BucketGetOptions{
    Header: &cos.ACLHeaderOptions{
        //private，public-read，public-read-write
        XCosACL: "private",
    },
}
_, err := c.Bucket.Put(context.Background(), nil)
if err != nil {
    panic(err)
}

// 2. Configure bucket ACL through request body
opt := &cos.BucketGetOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            "ID": "qcs::cam::uin/100000000001:uin/100000000001",
        },
        AccessControlList: []cos.ACLGrant{
            {
                Grantee: &cos.ACLGrantee{
                    'Type': 'CanonicalUser'|'Group',
                    Type: "RootAccount",
                    "ID": "qcs::cam::uin/100000000001:uin/100000000001",
                },
                'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
                Permission: "FULL_CONTROL",
            },
        },
    },
}
_, err := c.Bucket.Put(context.Background(), nil)
if err != nil {
    panic(err)
}
```

#### Parameter Description

```go
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
```

| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL | Sets the bucket ACL, such as private, public-read, and public-read-write. | string | No |
| XCosGrantFullControl | Grants the specified account the permission to read and write buckets. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantRead | Grants the specified account the permission to read buckets. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantWrite | Grants the specified account the permission to write buckets. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| ACLXML | Grants the specified account the access to buckets. For more information on the format, see the returned results of "Get Bucket acl". | struct | No |

### Querying bucket ACL

#### Feature Description

This API (Get Bucket ACL) is used to get the ACL of the specified bucket.

#### Method Prototype

```go
func (s *BucketService) GetACL(ctx context.Context) (*BucketGetACLResult, *Response, error)
```

#### Request Samples

[//]: # (.cssg-snippet-get-bucket-acl)
```go
_, _, err := client.Bucket.GetACL(context.Background())
if err != nil {
    panic(err)
}
```

#### Returned Result

Request result is returned through GetBucketACLResult.

```go
type ACLXml struct {
	Owner             *Owner
	AccessControlList []ACLGrant 
}
type Owner struct { 
	ID          string 
	DisplayName string
}
type ACLGrant struct {
	Grantee    *ACLGrantee
	Permission string
}
type ACLGrantee struct {
	Type        string 
	ID          string 
	DisplayName string
    UIN         string 
}
```

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner | Information of the bucket owner, including DisplayName and ID | struct |
| AccessControlList | Information of the user granted with bucket permissions, including Grantee and Permission | struct |
| Grantee | Information of grantee, including DisplayName, Type, ID and UIN | struct |
| Type | Type of grantee: CanonicalUser or Group | string |
| ID | ID of grantee when Type is CanonicalUser | string |
| DisplayName | Name of grantee | string |
| UIN | UIN of grantee when Type is Group | string |
| Permission | Bucket permissions of grantee. Available values: FULL_CONTROL (read and write permissions), WRITE (write permission), and READ (read permission) | string |
