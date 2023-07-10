

## Overview

This document provides an overview of APIs and SDK code samples for image QR codes.

| API | Description |
| :----------------------------------------------------------- | :--------- |
| [QR code recognition](https://intl.cloud.tencent.com/document/product/1045/47945) | Recognizes the location and content of valid QR codes in an image, outputs the text information (URL or text) contained in the QR codes, and pixelates the recognized QR codes. |
| [QR code generation](https://intl.cloud.tencent.com/document/product/1045/47946) | Generates QR codes or barcodes based on the specified text information (URL or text). |


## QR Code Recognition

#### Feature description

CI's QR code recognition feature recognizes the location and content of valid QR codes in an image, outputs the text information (URL or text) contained in the QR codes, and pixelates the recognized QR codes.

#### Method prototype

```
func (s *CIService) GetQRcode(ctx context.Context, name string, cover int, opt *ObjectGetOptions, id ...string) (*GetQRcodeResult, *Response, error)
```

#### Sample 1: Recognizing during upload
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
			Rule:   "QRcode/cover/1",
		},
	},
}
opt.XOptionHeader.Add("Pic-Operations", cos.EncodePicOperations(pic))
name := "test.jpg"
filepath := "./QRcode.jpg"
res, _, err := c.CI.PutFromFile(context.Background(), name, filepath, opt)
```

#### Sample 2: Recognizing during download

```go
name := "test.jpg"
res, _, err := c.CI.GetQRcode(context.Background(), name, 1, nil)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ---- | ---- |
| cover    | Pixelates the recognized QR code. Valid values: 0 (no), 1 (yes). Default value: 0. | int  | Yes   |

#### Response description

The returned result of recognition during download is as follows:
```
type GetQRcodeResult struct {
    CodeStatus  int        
    QRcodeInfo  *QRcodeInfo
    ResultImage string
}
type QRcodeInfo struct {
    CodeUrl      string    
    CodeLocation *CodeLocation
}
type CodeLocation struct {
    Point []string
}
```
| Parameter | Description | Type |
| ------------ | ------------------------------------------------------ | ------ |
| CodeStatus   | Whether QR codes are recognized. 0: no; 1: yes.  | int    |
| QRcodeInfo   | Recognized QR code. There may be multiple ones.                             | Struct |
| ResultImage  | Base64-encoded image data, which is returned if the request parameter `cover` is 1.      | string |
| CodeUrl      | QR code content. Content may not be recognized.                         | string |
| CodeLocation | Location coordinates of the QR code recognized in the image.                             | Struct |
| Point        | QR code coordinates (X,Y).                            | Array  |

## QR Code Generation

#### Feature description

CI's QR code generation feature generates QR codes or barcodes based on the specified text information (URL or text).

#### Method prototype

```go
func (s *CIService) GenerateQRcode(ctx context.Context, opt *GenerateQRcodeOptions) (*GenerateQRcodeResult, *Response, error)

func (s *CIService) GenerateQRcodeToFile(ctx context.Context, filePath string, opt *GenerateQRcodeOptions) (*GenerateQRcodeResult, *Response, error)
```

#### Sample request
```go
opt := &cos.GenerateQRcodeOptions{
	QRcodeContent: "<https://www.example.com>"
	Mode:          0,
	Width:         200,
}
// Case 1. Generate a QR code
res, _, err := c.CI.GenerateQRcode(context.Background(), opt)

// Case 2. Generate a QR code and save it as a file
filepath := "example.jpg"
res, _, err := c.CI.GenerateQRcodeToFile(context.Background(), filepath, opt)
```

#### Parameter description

```go
type GenerateQRcodeOptions struct {
    QRcodeContent string
    Mode          int 
    Width         int
}
```

| Parameter | Description | Type |
| ------------- | ------------------------------------------------------------ | ------ |
| QRcodeContent | Recognizable QR code text information                                       | string |
| Mode          | Type of the QR code to be generated. Valid values: 0 (QR code), 1 (barcode). Default value: 0. | int    |
| Width         | Width of the QR code or barcode to be generated. The height will be compressed proportionally.            | int    |

#### Response description

```go
type GenerateQRcodeResult struct {
    ResultImage string
}
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------- | ------ |
| ResultImage  | Base64-encoded QR code image data                           | string|

