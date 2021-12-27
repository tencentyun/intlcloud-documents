## Overview
This document provides an overview of APIs and SDK code samples related to restoring an archived object.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | Restoring an archived object | Restores an archived object for access. |

## Restoring an Archived Object 

#### Description

This API (`POST Object restore`) is used to restore an archived object for access.

#### Method prototype

```go
func (s *ObjectService) PostRestore(ctx context.Context, key string, opt *ObjectRestoreOptions) (*Response, error) 
```

#### Sample request

[//]: # (.cssg-snippet-restore-object)
```go
key := "example_restore"
f, err := os.Open("../test")
if err != nil {
    panic(err)
}
opt := &cos.ObjectPutOptions{
    ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
        ContentType:      "text/html",
        XCosStorageClass: "ARCHIVE", //ARCHIVE storage class
    },
    ACLHeaderOptions: &cos.ACLHeaderOptions{
        // Considering the ACL limit, we recommend not setting an object ACL when uploading an object unless required. The object will then inherit the bucket ACL by default.
        XCosACL: "private",
    },
}
// Upload an object directly to ARCHIVE storage class
_, err = client.Object.Put(context.Background(), key, f, opt)
if err != nil {
    panic(err)
}

opts := &cos.ObjectRestoreOptions{
    Days: 2,
    Tier: &cos.CASJobParameters{
        // Standard, Expedited, and Bulk
        Tier: "Expedited",
    },
}
// Restore an archived object.
_, err = client.Object.PostRestore(context.Background(), key, opts)
if err != nil {
    panic(err)
}
```

#### Parameter description

```go
type ObjectRestoreOptions struct {        
    Days    int               
    Tier    *CASJobParameters 
}
type CASJobParameters struct {
    Tier    string 
}
```

| Parameter | Description | Type | Required |
| -------------------- | ------------------------------------------------------------ | ------ | ---- |
| key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| ObjectRestoreOptions | Describes rules for retrieved temporary files | Struct | Yes |
| Days | Specifies the number of days before a temporary object expires | Int | Yes |
| CASJobParameters | Specifies the restoration configuration | Struct | No |
| Tier | Object restoration mode. For ARCHIVE, valid values are `Expedited`, `Standard`, and `Bulk`. For DEEP ARCHIVE, valid values are `Standard` and `Bulk` | String | No |

