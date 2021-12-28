## Overview

This document provides an overview of the API and sample code for quickly checking whether an object exists in a bucket. 

The sample code actually calls the [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) COS API and is a simplified version of the API.

In addition to checking whether an object exists, `HeadObject` returns object metadata. To view the SDK API that contains the full functionality of `HeadObject`, please see [Querying Object Metadata](https://intl.cloud.tencent.com/document/product/436/37688).


## Querying Object Metadata

#### Description

You can check whether an object exists by using the shortcut API provided by the SDK.

#### Method prototype
```go
func (s *ObjectService) IsExist(ctx context.Context, key string, id ...string) (isExist bool, err error)
```
#### Sample code

```go
key := "exampleobject"
ok, err := c.Object.IsExist(context.Background(), name)
if err == nil && ok {
	fmt.Printf("object exists\n")
} else if err != nil {
	fmt.Printf("head object failed: %v\n", err)
} else {
	fmt.Printf("object does not exist\n")
}
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`. | String | Yes |
| id  | `VersionId` of the object | string | No |

#### Response description

| Parameter | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| isExist | Whether the object exists                    | bool |
| err | Whether the request is successful | struct |