## Overview

This document provides an overview of APIs and SDK code samples for blind watermarking.

| API | Description |
| ------------------------------------------ | -------------------------- |
| [Blind watermarking](https://intl.cloud.tencent.com/document/product/1045/43029) | Adds a blind watermark to or extracts a blind watermark from a local image and uploads the image to a bucket. |


## Adding Blind Watermark

#### Feature description

You can add a blind watermark when uploading or downloading an object.

#### Sample 1: Adding a blind watermark during upload

```go
opt := &cos.ObjectPutOptions{
	nil,
	&cos.ObjectPutHeaderOptions{
		XOptionHeader: &http.Header{},
	},
}
pic := &cos.PicOperations{
	IsPicInfo: 1,
	Rules: []cos.PicOperationsRules{
		{
			FileId: ".jpg",
			Rule:   "watermark/3/type/3/text/" + base64.StdEncoding.EncodeToString([]byte("testwatermark")),
		},
	},
}
opt.XOptionHeader.Add("Pic-Operations", cos.EncodePicOperations(pic))
name := "test.jpg"
filepath := "./test.jpg"
res, _, err := c.CI.PutFromFile(context.Background(), name, filepath, opt)
```

#### Sample 2: Adding a blind watermark during download

```go
name = "test.jpg"
filepath := "watermark.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "watermark/3/type/3/text/"+base64.StdEncoding.EncodeToString([]byte("testwatermark")), nil)
```

## Extracting Blind Watermark

The request for extracting a blind watermark is the same as that used to simply upload a file to COS, except that you need to add the image processing parameter `Pic-Operations` to the request header and use the blind watermark extraction parameter `watermark/4`.

#### Sample request

```go
opt := &cos.ObjectPutOptions{
	nil,
	&cos.ObjectPutHeaderOptions{
		XOptionHeader: &http.Header{},
	},
}
pic := &cos.PicOperations{
	IsPicInfo: 1,
	Rules: []cos.PicOperationsRules{
		{
			FileId: "format2.jpg",
			Rule:   "watermark/4/type/3/text/" + base64.StdEncoding.EncodeToString([]byte("testwatermark")),
		},
	},
}
opt.XOptionHeader.Add("Pic-Operations", cos.EncodePicOperations(pic))
name := "test2.jpg"
_, err := c.Object.PutFromFile(context.Background(), name, filepath, opt)
```