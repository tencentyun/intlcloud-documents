### Introduction

This document provides an overview of APIs and SDK sample codes related to basic bucket operations and access control lists (ACL).

**Basic Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deletes a bucket | Deletes an empty bucket under a specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting a bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying a bucket ACL | Queries the ACL of a specified bucket |

## Basic operations

### Querying a bucket list

#### Feature description

This API is used to query the list of all buckets under a specified account.

#### Method prototype

```go
func (s *ServiceService) Get(ctx context.Context) (*ServiceGetResult, *Response, error)
```

#### Sample request 

[//]: # ".cssg-snippet-get-service"
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

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| ID | ID of the bucket owner | string |
| DisplayName | Name of the bucket owner | string |
| Name | Bucket name | string |
| Region | Bucket region | string |
| CreationDate | Time when the bucket was created, in ISO8601 format, such as 2016-11-09T08:46:32.000Z | string |

### Creating a bucket

#### Feature description

This API is used to create a bucket under a specified account.

#### Method prototype

```go
func (s *BucketService) Put(ctx context.Context, opt *BucketPutOptions) (*Response, error)
```

#### Sample request 

[//]: # ".cssg-snippet-put-bucket"
```go
opt := &cos.BucketGetOptions{
    XCosACL: "private",
}
_, err := c.Bucket.Put(context.Background(), nil)
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
}
```
| Parameter Name | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL | Sets the bucket ACL, such as private, public-read, and public-read-write. | string | No |
| XCosGrantFullControl | Grants a specified account read and write permission for a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantRead | Grants a specified account read permission for a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantWrite | Grants a specified account write permission for a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |

### Checking a bucket and its permissions

#### Feature description

This API is used to verify whether a bucket exists and you have the permission to access it.

#### Method prototype

```go
func (s *BucketService) Head(ctx context.Context) (*Response, error)
```

#### Sample request 

[//]: # ".cssg-snippet-head-bucket"
```go
_, err := client.Bucket.Head(context.Background())
if err != nil {
    panic(err)
}
```


### Deleting a bucket

#### Feature description

This API is used to delete an empty bucket under a specified account. 

#### Method prototype

```go
func (s *BucketService) Delete(ctx context.Context) (*Response, error)
```

#### Sample request 

[//]: # ".cssg-snippet-delete-bucket"
```go
_, err := client.Bucket.Delete(context.Background())
if err != nil {
    panic(err)
}
```

## ACL

### Setting a bucket ACL

#### Feature description

This API is used to set the access control list (ACL) of a specified bucket.

#### Method prototype

```go
func (s *BucketService) PutACL(ctx context.Context, opt *BucketPutACLOptions) (*Response, error)
```

#### Sample request 

[//]: # ".cssg-snippet-put-bucket-acl"
```go
// 1. Configure the bucket ACL through the request header
opt := &cos.BucketGetOptions{
    Header: &cos.ACLHeaderOptions{
        // private，public-read，public-read-write
        XCosACL: "private",
    },
}
_, err := c.Bucket.Put(context.Background(), nil)
if err != nil {
    panic(err)
}

// 2. Configure the bucket ACL through the request body
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

#### Parameter description

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
| XCosGrantFullControl | Grants a specified account read and write permission for a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantRead | Grants a specified account read permission for a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| XCosGrantWrite | Grants a specified account write permission for a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; To authorize a root account, `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. For example: `id="qcs::cam::uin/123:uin/456",id="qcs::cam::uin/123:uin/123"` | string | No |
| ACLXML | Grants a specified account access permission for a bucket. For more information on the format, see the response description of `Get Bucket acl`. | struct | No |

### Querying a bucket ACL

#### Feature description

This API is used to query the ACL of a specified bucket.

#### Method prototype

```go
func (s *BucketService) GetACL(ctx context.Context) (*BucketGetACLResult, *Response, error)
```

#### Sample request 

[//]: # ".cssg-snippet-get-bucket-acl"
```go
_, _, err := client.Bucket.GetACL(context.Background())
if err != nil {
    panic(err)
}
```

#### Response description

The result of the request is returned through GetBucketACLResult.

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
| Owner | Information on the bucket owner, including DisplayName and ID | struct |
| AccessControlList | Information on the authorized user granted with bucket permissions, including Grantee and Permission | struct |
| Grantee | Information on the authorized user, including DisplayName, Type, ID and UIN | struct |
| Type | Type of authorized user: CanonicalUser or Group | string |
| ID | ID of the authorized user when the type is CanonicalUser | string |
| DisplayName | Name of the authorized user | string |
| UIN | UIN of the authorized user when the type is group | string |
| Permission | Bucket permission granted to the authorized user. Available values: FULL_CONTROL (read and write permission), WRITE (write permission), and READ (read permission) | string |
