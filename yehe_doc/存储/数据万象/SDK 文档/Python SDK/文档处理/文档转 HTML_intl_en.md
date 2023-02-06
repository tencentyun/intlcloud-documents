## Overview

This document provides an overview of APIs and SDK code samples for sync requests for file preview.

| API  |	Description  |
|----|-----|
| [File-to-HTML conversion](https://intl.cloud.tencent.com/document/product/436/49414)  | The file-to-HTML conversion feature allows you to generate HTML pages for preview from multiple types of files. It enables easy online file preview on PC, app, and other terminals. It is widely suitable for diverse business scenarios, such as online education, enterprise OA, online knowledge base, and online file preview. | 


## File-to-HTML Conversion

#### Feature description

This API is used to covert files in various formats to HTML for preview.

#### Method prototype

```py
def ci_doc_preview_html_process(self, Bucket, Key, SrcType=None, Copyable='1', DstType='html', HtmlParams=None, HtmlWaterword=None, HtmlFillStyle=None,
                                    HtmlFront=None, HtmlRotate=None, HtmlHorizontal=None, HtmlVertical=None, **kwargs):
```

#### Sample request

```py
def ci_doc_preview_to_html_process():
    # Sync file preview API (generating HTML)
    response = client.ci_doc_preview_html_process(
        Bucket=bucket_name,
        Key='1.txt',
    )
    print(response)
    response['Body'].get_stream_to_file('result.html')
```

#### Parameter description

| Parameter        | Description                                                         | Type   | Required |
| ----------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket    | Bucket of the object | String    | Yes |  
| Key      | Object name  | String  | Yes       |  
| SrcType | Source file type as listed in [Getting Started](https://intl.cloud.tencent.com/document/product/436/49414).  | String | No |
| Copyable          | Whether the file content is copyable. Valid values: `1` (yes), `0` (no).     | String   | No      | 
| DstType   | Output target file type, which is fixed at `html` for HTML preview.  | String  | Yes       |  
| HtmlParams          | Custom configuration parameters in JSON structure, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430). Default configuration: { commonOptions: { isShowTopArea: true, isShowHeader: true } }. For supported configurations, see [Custom Configuration Overview](https://intl.cloud.tencent.com/document/product/436/49416).    | String   | No   |
| HtmlWaterword          | Watermark text, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is empty by default.     | String  | No      | 
| HtmlFillStyle          | Watermark RGBA (color and transparency), which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is `rgba(192,192,192,0.6)` by default.  | String   | No      | 
| HtmlFront          | Watermark text style, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is `bold 20px Serif` by default.    | String   | No      | 
| HtmlRotate          | Rotation angle of the watermark text in degrees. Value range: 0–360. Default value: `315`. | String   | No      | 
| HtmlHorizontal          | Horizontal spacing of the watermark text in px. Default value: `50`. | String | No | 
| HtmlVertical          | Vertical spacing of the watermark text in px. Default value: `100`. | String | No | 









