## Feature Overview

This document provides an overview of APIs and SDK code samples related to the access control lists (ACLs) for buckets and objects.


**Bucket ACL**

| API | Operation | Description |
| :----------------------------------------------------------- | :------------- | :-------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting a bucket ACL | Sets an ACL for a bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying a bucket ACL | Queries the ACL of a bucket |


**Object ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for an object (file) in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object (file) |


## Bucket ACL

### Setting a bucket ACL

#### Feature description

This API is used to set the access control list (ACL) of a specified bucket.

#### Method prototype

```go
func (s *BucketService) PutACL(ctx context.Context, opt *BucketPutACLOptions) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-acl)
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
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })
    // 1. Configure the bucket ACL through the request header
    opt := &cos.BucketPutACLOptions{
        Header: &cos.ACLHeaderOptions{
            // private, public-read, public-read-write
            XCosACL: "private",
        },
    }
    _, err := client.Bucket.PutACL(context.Background(), opt)
    if err != nil{
        panic(err)
    }
  	// 2. Configure the bucket ACL through the request body
    opt = &cos.BucketPutACLOptions{
        Body: &cos.ACLXml{
            Owner: &cos.Owner{
                ID: "qcs::cam::uin/100000000001:uin/100000000001",
            },
            AccessControlList: []cos.ACLGrant{
                {
                    Grantee: &cos.ACLGrantee{
                        'Type': 'CanonicalUser'|'Group',
                        Type: "RootAccount",
                        ID:   "qcs::cam::uin/100000760461:uin/100000760461",
                    },
                    'Permission': 'FULL_CONTROL'|'WRITE'|'READ'
                    Permission: "FULL_CONTROL",
                },
            },
        },
    }
    _, err = client.Bucket.PutACL(context.Background(), opt)
    if err != nil{
        panic(err)
    }
}
```

#### Field description

```go
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| XCosACL | Sets the bucket ACL, such as private, public-read, and public-read-write | String | No |
| XCosGrantFullControl | Grants a specified account read and write access to a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, use `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`. To authorize a root account, use `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. <br>Example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |
| XCosGrantRead | Grants a specified account read access to a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, use `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`. To authorize a root account, use `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. <br>Example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |
| XCosGrantWrite | Grants a specified account write access to a bucket. Format: `id=" ",id=" "`. To authorize a sub-account, use `id="qcs::cam::uin/{OwnerUin}:uin/{SubUin}"`. To authorize a root account, use `id="qcs::cam::uin/{OwnerUin}:uin/{OwnerUin}"`. <br>Example: `id="qcs::cam::uin/100000000001:uin/100000000011",id="qcs::cam::uin/100000000001:uin/100000000001"` | string | No |
| ACLXML | Grants a specified account access permission for a bucket. For more information on the format, see the response description of `Get Bucket acl`. | struct | No |

### Querying a bucket ACL

#### Feature description

This API is used to query the ACL of a specified bucket.

#### Method prototype

```go
func (s *BucketService) GetACL(ctx context.Context) (*BucketGetACLResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-acl)
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
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })
    _, _, err := client.Bucket.GetACL(context.Background())
    if err != nil{
        panic(err)
    }
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
    URI         string 
}
```

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner | Information on the bucket owner, including `DisplayName` and `ID` | struct |
| AccessControlList | Information on the authorized user granted with bucket permissions, including `Grantee` and `Permission` | struct |
| Grantee | Information on the grantees, including `DisplayName`, `Type`, `ID` and `URI` | struct |
| Type | Type of grantee. Valid values: `CanonicalUser` and `Group` | string |
| ID                | ID of the grantee when `Type` is `CanonicalUser`, in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, for example, `qcs::cam::uin/100000000001:uin/100000000001`. This parameter is required when `Type` is `CanonicalUser` | string |
| DisplayName       | Name of the grantee. This parameter can be left empty or be consistent with the value of `ID`       | string |
| URI               | URI of the preset user group when `Type` is `Group`, for example, `http://cam.qcloud.com/groups/global/AllUsers`. For more information, please see [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583) | string |
| Permission | Bucket permission granted. Valid values: `FULL_CONTROL` (read and write), `WRITE`, and `READ` | string |



## Object ACL

### Setting an object ACL

#### Feature description

This API is used to set an ACL for an object.

#### Method prototype

```go
func (s *ObjectService) PutACL(ctx context.Context, key string, opt *ObjectPutACLOptions) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-object-acl)
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
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })
    // 1. Configure through the request header
    opt := &cos.ObjectPutACLOptions{
        Header: &cos.ACLHeaderOptions{
            XCosACL: "private",
        },
    }
    key := "exampleobject"
    _, err := client.Object.PutACL(context.Background(), key, opt)
    if err != nil{
        panic(err)
    }
    // 2. Configure through the request body
    opt = &cos.ObjectPutACLOptions{
        Body: &cos.ACLXml{
            Owner: &cos.Owner{
                ID: "qcs::cam::uin/100000000001:uin/100000000001",
            },
            AccessControlList: []cos.ACLGrant{
                {
                    Grantee: &cos.ACLGrantee{
                        Type: "RootAccount",
                        ID:   "qcs::cam::uin/100000760461:uin/100000760461",
                    },

                    Permission: "FULL_CONTROL",
                },
            },
        },
    }
    _, err = client.Object.PutACL(context.Background(), key, opt)
    if err != nil{
        panic(err)
    }
}
```

#### Field description

```go
type ACLHeaderOptions struct {
	XCosACL              string 
	XCosGrantRead        string 
	XCosGrantWrite       string 
	XCosGrantFullControl string 
}
```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| XCosACL | Sets the object ACL, such as private, public-read | string | No |
| XCosGrantFullControl | Grants full permission in the format: `id="[OwnerUin]"` | String | No |
| XCosGrantRead | Grants read permission in the format: id="[OwnerUin]" | String | No |
| ACLXML | Grants the specified account bucket access permission. For more information on the format, see the response to the "GET object acl" request. | struct | No |

### Querying an object ACL

#### Feature description

This API is used to query the ACL of an object.

#### Method prototype

```go
func (s *ObjectService) GetACL(ctx context.Context, key string) (*ObjectGetACLResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-object-acl)
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
            SecretID: os.Getenv("SECRETID"),  // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://cloud.tencent.com/document/product/598/37140.
            // Environment variable `SECRETKEY` refers to the user's `SecretKey`, which can be viewed in the CAM console at https://console.cloud.tencent.com/cam/capi.
            SecretKey: os.Getenv("SECRETKEY"),  // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit  https://cloud.tencent.com/document/product/598/37140.
        },
    })
    key := "exampleobject"
    _, _, err := client.Object.GetACL(context.Background(), key)
    if err != nil{
        panic(err)
    }
}
```

#### Field description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |

#### Response description

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
    URI         string 
}
```

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| Owner | Information on the bucket owner, including `DisplayName` and `ID` | struct |
| AccessControlList | Information on the authorized user granted with bucket permissions, including `Grantee` and `Permission` | struct |
| Grantee | Information on the grantees, including `DisplayName`, `Type`, `ID` and `URI` | struct |
| Type | Type of grantee. Valid values: `CanonicalUser` and `Group` | string |
| ID                | ID of the grantee when `Type` is `CanonicalUser`, in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, for example, `qcs::cam::uin/100000000001:uin/100000000001`. This parameter is required when `Type` is `CanonicalUser` | string |
| DisplayName       | Name of the grantee. This parameter can be left empty or be consistent with the value of `ID`       | string |
| URI               | URI of the preset user group when `Type` is `Group`, for example, `http://cam.qcloud.com/groups/global/AllUsers`. For more information, please see [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583) | string |
| Permission | Bucket permission granted. Valid values: `FULL_CONTROL` (read and write), `WRITE`, and `READ` | string |

