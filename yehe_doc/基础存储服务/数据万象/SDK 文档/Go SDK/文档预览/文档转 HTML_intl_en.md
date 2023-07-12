## Overview

This document provides an overview of APIs and SDK code samples for sync requests for file preview.

| API  |	Description  |
|----|-----|
| [File-to-HTML conversion](https://intl.cloud.tencent.com/document/product/436/49414)  | The file-to-HTML conversion feature allows you to generate HTML pages for preview from multiple types of files. It enables easy online file preview on PC, app, and other terminals. It is widely suitable for diverse use cases, such as online education, enterprise OA, online knowledge base, and online file preview. | 


## File-to-HTML Conversion

#### Feature description

This API is used to convert files in various formats to HTML for preview.

#### Method prototype

```go
func (s *CIService) DocPreviewHTML(ctx context.Context, name string, opt *DocPreviewHTMLOptions) (*Response, error)
```

#### Sample request

```go
opt := &cos.DocPreviewHTMLOptions{
    DstType:  "html",
    SrcType:  "ppt",
    Copyable: "1",
    HtmlParams: &cos.HtmlParams{
        CommonOptions: &cos.HtmlCommonParams{
            IsShowTopArea: false,
        },
        PptOptions: &cos.HtmlPptParams{
            IsShowBottomStatusBar: true,
        },
    },
    Htmlwaterword:  "5pWw5o2u5LiH6LGhLeaWh+aho+mihOiniA==",
    Htmlfillstyle:  "cmdiYSgxMDIsMjA0LDI1NSwwLjMp", // rgba(102,204,255,0.3)
    Htmlfront:      "Ym9sZCAyNXB4IFNlcmlm",         // bold 25px Serif
    Htmlrotate:     "315",
    Htmlhorizontal: "50",
    Htmlvertical:   "100",
}
resp, err := c.CI.DocPreviewHTML(context.Background(), "form.pdf", opt)
```

#### Parameter description

```go
type DocPreviewHTMLOptions struct {
	DstType        string      `url:"dstType,omitempty"`
	SrcType        string      `url:"srcType,omitempty"`
	Sign           string      `url:"sign,omitempty"`
	Copyable       string      `url:"copyable,omitempty"`
	HtmlParams     *HtmlParams `url:"htmlParams,omitempty"`
	Htmlwaterword  string      `url:"htmlwaterword,omitempty"`
	Htmlfillstyle  string      `url:"htmlfillstyle,omitempty"`
	Htmlfront      string      `url:"htmlfront,omitempty"`
	Htmlrotate     string      `url:"htmlrotate,omitempty"`
	Htmlhorizontal string      `url:"htmlhorizontal,omitempty"`
	Htmlvertical   string      `url:"htmlvertical,omitempty"`
}

type HtmlParams struct {
	CommonOptions *HtmlCommonParams `json:"commonOptions,omitempty"`
	WordOptions   *HtmlWordParams   `json:"wordOptions,omitempty"`
	PdfOptions    *HtmlPdfParams    `json:"pdfOptions,omitempty"`
	PptOptions    *HtmlPptParams    `json:"pptOptions,omitempty"`
}

type HtmlCommonParams struct {
	IsShowTopArea           bool `json:"isShowTopArea"`
	IsShowHeader            bool `json:"isShowHeader"`
	IsBrowserViewFullscreen bool `json:"isBrowserViewFullscreen"`
	IsIframeViewFullscreen  bool `json:"isIframeViewFullscreen"`
}

type HtmlWordParams struct {
	IsShowDocMap          bool `json:"isShowDocMap"`
	IsBestScale           bool `json:"isBestScale"`
	IsShowBottomStatusBar bool `json:"isShowBottomStatusBar"`
}

type HtmlPdfParams struct {
	IsShowComment         bool `json:"isShowComment"`
	IsInSafeMode          bool `json:"isInSafeMode"`
	IsShowBottomStatusBar bool `json:"isShowBottomStatusBar"`
}

type HtmlPptParams struct {
	IsShowBottomStatusBar bool `json:"isShowBottomStatusBar"`
}

```


| Parameter        | Description                                                         | Type   | Required |
| ----------- | ------------------------------------------------------------ | ------ | -------- |
| DstType   | Output target file type, which is fixed at `html` for HTML preview.  | String  | Yes       |  
| SrcType | Source file type as listed in [Getting Started](https://intl.cloud.tencent.com/document/product/436/49414).  | String | No |
| Sign          | Object download signature, which must be URL-encoded. If the previewed object is privately readable, the signature needs to be passed in. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/1045/33452). | String | No      | 
| Copyable          | Whether the file content is copyable. Valid values: `1` (yes), `0` (no).     | String   | No      | 
| HtmlParams          | Custom configuration parameters in JSON structure, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430). Default configuration: { commonOptions: { isShowTopArea: true, isShowHeader: true } }. For supported configurations, see [Custom Configuration Overview](https://intl.cloud.tencent.com/document/product/436/49416).    | String   | No   |
| Htmlwaterword          | Watermark text, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is empty by default.     | String  | No      | 
| Htmlfillstyle          | Watermark RGBA (color and transparency), which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is `rgba(192,192,192,0.6)` by default.  | String   | No      | 
| Htmlfront          | Watermark text style, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is `bold 20px Serif` by default.    | String   | No      | 
| Htmlrotate          | Rotation angle of the watermark text in degrees. Value range: 0–360. Default value: `315`. | String   | No      | 
| Htmlhorizontal          | Horizontal spacing of the watermark text in px. Default value: `50`. | String | No | 
| Htmlvertical          | Vertical spacing of the watermark text in px. Default value: `100`. | String | No | 

