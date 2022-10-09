
## Overview

This document provides an overview of APIs and SDK code samples for persistent image processing.

| API | Description |
| :----------------------------------------------------------- | :----------------------------------- |
| [Persistent image processing](https://intl.cloud.tencent.com/document/product/436/40592) | Processes images persistently. |


## Processing During Upload

COS allows you to process images during upload. To enable this, add `Pic-Operations` to the request header and set relevant parameters. You can also save the input images and processing results to COS. Currently, images within 20 MB can be processed.

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
			FileId: "format.jpg",
			Rule:   "imageView2/format/png",
		},
	},
}
opt.XOptionHeader.Add("Pic-Operations", cos.EncodePicOperations(pic))
name := "test.jpg"
local_filename := "./test.jpg"
res, _, err := c.CI.PutFromFile(context.Background(), name, local_filename, opt)
```

#### Parameter description

```go
type PicOperations struct {
    IsPicInfo int                  
    Rules     []PicOperationsRules
}
type PicOperationsRules struct {
    Bucket string
    FileId string
    Rule   string
}
```

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| IsPicInfo | Whether to return the input image information. Valid values: 0 (no), 1 (yes). Default value: 0. | int    | No   |
| Rules     | Processing rules (up to five rules are supported). Each rule corresponds to one processing result. If this parameter is not specified, images will not be processed. | Array | No       |
| Bucket    | Name of the destination bucket to store the results in the format of `BucketName-APPID`. If this parameter is not specified, the results will be stored in the current bucket by default. | String | No       |
| FileId    | Path of the processing result file. If the path starts with `/`, the result file will be stored in the specified folder; otherwise, it will be stored in the same directory as the input image file. | string | Yes |
| Rule      | Processing parameters. For more information, see the persistent image processing API. To process an image with a specified style, the value must start with `style/` with the style name followed. For example, if the style name is `test`, the value of `rule` should be `style/test`. | string | No   |

## Processing In-Cloud Data

This API is used to process an image stored in COS and save the processing result to COS.

#### Sample request
```go
opt := &cos.ImageProcessOptions{
	IsPicInfo: 1,
	Rules: []cos.PicOperationsRules{
		{
			FileId: "format.jpg",
			Rule:   "imageView2/format/png",
		},
	},
}
name := "test.jpg"
res, _, err := c.CI.ImageProcess(context.Background(), name, opt)
```



