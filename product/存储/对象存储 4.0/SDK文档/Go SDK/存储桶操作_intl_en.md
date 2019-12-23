
## Overview

This document provides an overview of APIs related to basic bucket operations and access control list (ACL) and corresponding SDK sample code.

**Basic operations**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | --------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL configuration of a bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL configuration of a bucket |

## Basic Operations

### Querying Bucket List

#### Feature Description

This API is used to query the list of all buckets under the specified account.

#### Method Prototype

```go
func (s *ServiceService) Get(ctx context.Context) (*ServiceGetResult, *Response, error)
```

#### Sample Request

```go
s, resp, err := c.Service.Get(context.Background()) 
```

#### Return Result Descriptions
The result of the request is returned through GetServiceResult.
```go
type ServiceGetResult struct {
    Owner   *Owner  
    Buckets []Bucket 
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
| ID | Bucket owner ID | string |
| DisplayName | Bucket owner name | string |
| Name | Bucket name | string |
| Region | Bucket region | string |
| CreationDate | Bucket creation time in ISO8601 format, such as 2016-11-09T08:46:32.000Z | string |

### Creating a Bucket

#### Feature Description

This API is used to create a bucket under the specified account.

#### Method Prototype

```go
func (s *BucketService) Put(ctx context.Context, opt *BucketPutOptions) (*Response, error)
```

#### Sample Request

```go
opt := &cos.BucketPutOptions{
	XCosACL: "public-read",
}
resp, err := client.Bucket.Put(context.Background(), opt)
```

#### Parameter Descriptions
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
| XCosACL | Sets the ACL for the bucket, such as private, public-read, and public-read-write | string | No |
| XCosGrantFullControl | Grants the specified account read-write permission of the bucket in the format of `id=" ",id=" "`. When you need to authorize a sub-account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; when you need to authorize a master account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`, such as `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |
| XCosGrantRead | Grants the specified account read permission of the bucket in the format of `id=" ",id=" "`. When you need to authorize a sub-account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; when you need to authorize a master account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`, such as `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |
| XCosGrantWrite | Grants the specified account write permission of the bucket in the format of `id=" ",id=" "`. When you need to authorize a sub-account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; when you need to authorize a master account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`, such as `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |

### Checking a Bucket and Its Permission

#### Feature Description

This API is used to check whether a bucket exists and you have permission to access it.

#### Method Prototype

```go
func (s *BucketService) Head(ctx context.Context) (*Response, error)
```

#### Sample Request

```go
resp, err := client.Bucket.Head(context.Background())
```


### Deleting a Bucket

#### Feature Description

This API is used to delete an empty bucket under the specified account.

#### Method Prototype

```go
func (s *BucketService) Delete(ctx context.Context) (*Response, error)
```

#### Sample Request

```go
resp, err := client.Bucket.Delete(context.Background())
```

## ACL

### Setting Bucket ACL

#### Feature Description

This API (PUT Bucket acl) is used to set the access control list (ACL) for the specified bucket.

#### Method Prototype

```go
func (s *BucketService) PutACL(ctx context.Context, opt *BucketPutACLOptions) (*Response, error)
```

#### Sample Request

```go
// 1. Set Bucket ACL by header.
opt := &cos.BucketPutACLOptions{
	Header: &cos.ACLHeaderOptions{
		//private，public-read，public-read-write
		XCosACL: "private",
	},
}
resp, err := client.Bucket.PutACL(context.Background(), opt)

// 2. Set Bucket ACL by body.
opt = &cos.BucketPutACLOptions{
    Body: &cos.ACLXml{
        Owner: &cos.Owner{
            ID: "qcs::cam::uin/100000760461:uin/100000760461",
        },
        AccessControlList: []cos.ACLGrant{
            {
                Grantee: &cos.ACLGrantee{
		// Type can also chose the "Group", "CanonicalUser"
                    Type: "RootAccount",
                    ID:"qcs::cam::uin/100000760461:uin/100000760461",
                },
		// Permission can also chose the "WRITE"，"FULL_CONTROL" 
                Permission: "FULL_CONTROL",
            },
        },
    },
}
resp, err := client.Bucket.PutACL(context.Background(), opt)
```

#### Parameter Descriptions

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
| XCosACL | Sets the ACL for the bucket, such as private, public-read, and public-read-write | string | No |
| XCosGrantFullControl | Grants the specified account read-write permission of the bucket in the format of `id=" ",id=" "`. When you need to authorize a sub-account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; when you need to authorize a master account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`, such as `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |
| XCosGrantRead | Grants the specified account read permission of the bucket in the format of `id=" ",id=" "`. When you need to authorize a sub-account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; when you need to authorize a master account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`, such as `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |
| XCosGrantWrite | Grants the specified account write permission of the bucket in the format of `id=" ",id=" "`. When you need to authorize a sub-account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`; when you need to authorize a master account, the format is `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`, such as `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |
| ACLXML | Grants the specified account access to the bucket. For detailed format, see the return result descriptions of GET Bucket acl | struct | No |

### Querying Bucket ACL

#### Feature Description

This API (GET Bucket acl) is used to query the access control list (ACL) for the specified bucket.

#### Method Prototype

```go
func (s *BucketService) GetACL(ctx context.Context) (*BucketGetACLResult, *Response, error)
```

#### Sample Request

```go
v, resp, err := client.Bucket.GetACL(context.Background())
```

#### Return Result Descriptions

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
| Owner | Bucket owner information, including DisplayName and ID | struct |
| AccessControlList | Bucket permission grantee information, including Grantee and Permission           | struct |
| Grantee           | Permission grantee information, including DisplayName, Type, ID, and UIN          | struct |
| Type              | Permission grantee type; CanonicalUser or Group            | string |
| ID | If Type is CanonicalUser, this parameter corresponds to the ID of the permission grantee | string |
| DisplayName | Permission grantee name | string |
| UIN | If Type is Group, this parameter corresponds to the UIN of the permission grantee | string |
| Permission | Permission to the bucket owned by the grantee. Value range: FULL_CONTROL (for read/write permission), WRITE (for write permission), READ (for read permission) | string |
