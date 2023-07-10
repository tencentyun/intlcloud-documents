
## Overview

This document provides an overview of APIs and SDK code samples for sync requests for file preview.

| API  |	Description  |
|----|-----|
| [Sync request API](https://intl.cloud.tencent.com/document/product/1045/47929)  |       Synchronously requests for file preview.   |



## Sync Request API

#### Feature description

This API is used to synchronously request for file preview.

#### Method prototype

```go
func (s *CIService) DocPreview(ctx context.Context, name string, opt *DocPreviewOptions) (*Response, error)
```

#### Sample request

```go
opt := &cos.DocPreviewOptions{
	Page: 1,
}
resp, err := c.CI.DocPreview(context.Background(), "form.pdf", opt)
```

#### Parameter description

```go
type DocPreviewOptions struct {
    SrcType             string
    Page                int
    ImageParams         string
    Sheet               int
    DstType             string
    Password            string
    Comment             int
    ExcelPaperDirection int
    Quality             int
    Zoom                int
}
```

| Parameter | Description | Type |
| ------------------- | ------------------------------------------------------------ | ------ |
| name                | Object name, such as `folder/document.pdf`.                         | String |
| SrcType | Source data type. Currently, the file conversion feature determines the source data type according to the file extension of the COS object. If the object has no extension, you can set this value. | String |
| page | Number of the page to be converted, which is counted from 1 by default. For spreadsheets, `page` indicates to convert the xth image in the xth sheet. | int |
| ImageParams | Processing parameters for the output image. All parameters of [basic image processing](https://intl.cloud.tencent.com/document/product/1045/33694) are supported. To specify multiple parameters, separate them with [pipeline operators](https://intl.cloud.tencent.com/document/product/436/36380). In this way, the image can be processed by multiple parameters in sequence in the same request. | String |
| Sheet | Sheet parameter, indicating to convert the xth sheet. Default value: 1. | int |
| DstType | Type of the output target image file. Valid values: png, jpg, pdf. If the input file format cannot be recognized, the `jpg` format will be used by default. | String |
| Password | Password to open the Office file. If you need to convert a password-protected file, set this field. | String |
| Comment | Whether to hide comments and apply track changes. 0: hide comments and apply track changes; 1: show comments and track changes. Default value: 0. | int |
| ExcelPaperDirection | Paper orientation of the spreadsheet. 0: vertical; other values: horizontal. Default value: 0. | int |
| Quality | Quality of the generated preview image. Value range: [1-100]. Default value: 100. For example, if the value is 100, the quality of the generated image will be 100%. | int |
| Zoom                | Zooming parameter of the preview image. Value range: [10-200]. Default value: 100. For example, if the value is 200, the image will be zoomed in (enlarged) by 200%. | int |
