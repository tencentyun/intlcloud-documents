## Overview

This document provides an overview of APIs and SDK code samples related to object tagging.

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Tagging an object | Tags an uploaded object. |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all tags of an object. |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes all tags of an object. |


## Tagging an Object

#### Description

This API (PUT Object tagging) is used to tag an existing object by adding tag key-value pairs. This can help you group and manage your existing objects. For more information, please see [Object Tagging Overview](https://intl.cloud.tencent.com/document/product/436/35665).

#### Method prototype

```go
func (s *ObjectService) PutTagging(ctx context.Context, name string, opt *ObjectPutTaggingOptions, id ...string) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-object-tagging)
```go
// Sample 1. Use PutTagging to tag in-cloud objects
opt := &cos.ObjectPutTaggingOptions{
    TagSet: []cos.ObjectTaggingTag{
        {
            Key:   "test_k2",
            Value: "test_v2",
        },
        {
            Key:   "test_k3",
            Value: "test_v3",
        },
    },
}
name := "example"
_, err := c.Object.PutTagging(context.Background(), name, opt)
if err != nil {
    //ERROR
}

// Sample 2. Tag an object when it is uploaded
name = "test/example"
f := strings.NewReader("test")
popt := &cos.ObjectPutOptions{
    ObjectPutHeaderOptions: &cos.ObjectPutHeaderOptions{
        XOptionHeader: &http.Header{},
    },
}
popt.XOptionHeader.Add("x-cos-tagging", "Key1=Value1&Key2=Value2")
_, err = c.Object.Put(context.Background(), name, f, popt)
```

#### Parameter description

```go
type ObjectPutTaggingOptions struct {
    TagSet  []ObjectTaggingTag
}
type BucketTaggingTag struct {
    Key   string
    Value string
}
```
| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | ---- |
| name  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| TagSet   | A set of up to 10 tags | Array  | Yes |
| Key | Tag key. A tag key must not exceed 128 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String | Yes |
| Value | Tag value. A tag value must not exceed 256 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String | Yes |

## Querying Object Tags

#### Description

This API (GET Object tagging) is used to query the existing tags of an object.

#### Method prototype

```go
func (s *ObjectService) GetTagging(ctx context.Context, name string, id ...string) (*ObjectGetTaggingResult, *Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-get-object-tagging)
```go
name := "example"
res, _, err := c.Object.GetTagging(context.Background(), name)
if err != nil {
    //ERROR
}
```

#### Response
```go
type ObjectGetTaggingResult struct {
    TagSet  []ObjectTaggingTag
}
type BucketTaggingTag struct {
    Key   string
    Value string
}
```

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| TagSet   | A set of up to 10 tags    | Array  |
| Key | Tag key. A tag key must not exceed 128 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |
| Value | Tag value. A tag value must not exceed 256 characters and can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes. | String |

## Deleting Object Tags

#### Description

This API (DELETE Object tagging) is used to delete the existing tags of an object.

#### Method prototype

```go
func (s *ObjectService) DeleteTagging(ctx context.Context, name string, id ...string) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-delete-object-tagging)
```go
name := "example"
_, err = c.Object.DeleteTagging(context.Background(), name)
if err != nil {
    //ERROR
}
```
