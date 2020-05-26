

## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting a bucket tag | Sets a tag for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting a bucket tag | Deletes a specified bucket tag |

## Setting Bucket Tag

#### Feature description

This API (PUT Bucket tagging) is used to set a tag for an existing bucket.

#### Method prototype

```go
func (s *BucketService) PutTagging(ctx context.Context, opt *BucketPutTaggingOptions) (*Response, error)
```

#### Sample request

```go
opt := &cos.BucketPutTaggingOptions{
	TagSet: []cos.BucketTaggingTag{
	{   
		Key:   "testk1",
		Value: "testv1",
    },  
    {   
    	Key:   "testk2",
        Value: "testv2",
    },  
    },  
}   
resp, err := client.Bucket.PutTagging(context.Background(), opt)
```

#### Parameter description

```go
type BucketTaggingTag struct {
    Key   string
    Value string
}
type BucketPutTaggingOptions struct {
    XMLName xml.Name           
    TagSet  []BucketTaggingTag 
}
```

| Parameter Name | Description | Type |
| ----------------------- | ------------------------------------------------------------ | ------ |
| BucketPutTaggingOptions | Bucket tag configuration parameter                                           | Struct |
| TagSet                  | Bucket tag configuration information                                           | Struct |
| key | Tag key, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 128 bytes | String |
| value | Tag value, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 256 bytes | String |

## Querying Bucket Tag

#### Feature description

This API (GET Bucket tagging) is used to query the existing tags of a specified bucket.

#### Method prototype

```go
func (s *BucketService) GetTagging(ctx context.Context) (*BucketGetTaggingResult, *Response, error)
```

#### Sample request

```go
v, resp, err := client.Bucket.GetTagging(context.Background())
```

#### Returned result description

```go
type BucketTaggingTag struct {
    Key   string
    Value string
}
type BucketGetTaggingResult struct {
    XMLName xml.Name           
    TagSet  []BucketTaggingTag 
}

```

| Parameter Name | Description | Type |
| ---------------------- | ------------------------------------------------------------ | ------ |
| BucketGetTaggingResult | Bucket tag configuration parameter                                           | Struct |
| TagSet                  | Bucket tag configuration information                                           | Struct |
| key | Tag key, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 128 bytes | String |
| value | Tag value, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 256 bytes | String |

## Deleting Bucket Tag

#### Feature description

This API (DELETE Bucket tagging) is used to delete an existing tag of a specified bucket.

#### Method prototype

```go
func (s *BucketService) DeleteTagging(ctx context.Context) (*Response, error)
```

#### Sample request

```go
resp, err := client.Bucket.DeleteTagging(context.Background())
```
