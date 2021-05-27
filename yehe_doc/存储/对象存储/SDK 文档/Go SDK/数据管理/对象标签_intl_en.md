## Overview

This document provides an overview of APIs and SDK code samples related to object tagging.

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT   Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Setting object tags | Sets tags for an uploaded object |
| [GET   Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all tags of an object |
| [DELETE   Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes all tags of an object |


## Setting Object Tags

#### API description

This API (PUT Object tagging) is used to set tags on an existing object. It can help you group and manage existing object resources by adding key-value pairs as object tags. For more information, please see [Object Tagging Overview](https://intl.cloud.tencent.com/document/product/436/35665).

#### Method prototype

```go
func (s *ObjectService) PutTagging(ctx context.Context, name string, opt *ObjectPutTaggingOptions, id ...string) (*Response, error)
```

#### Sample request

[//]: # (.cssg-snippet-put-object-tagging)
```go
// Sample 1. Use PutTagging to set tags for in-cloud objects.
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

// Sample 2. Set object tags upon the upload.
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
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |
| TagSet   | A set of up to 10 tags | Array  | Yes |
| Key | Tag key, which can contain up to 128 characters. A tag key can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String | Yes |
| Value | Tag value, which can contain up to 256 characters. A tag value can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String | Yes |

## Querying Object Tags

#### API description

This API (GET Object tagging) is used to query existing tags set on an object.

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

#### Result description
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
| Key | Tag key, which can contain up to 128 characters. A tag key can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String |
| Value | Tag value, which can contain up to 256 characters. A tag value can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String |

## Deleting Object Tags

#### API description

This API (GET Object tagging) is used to query existing tags set on an object.

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
