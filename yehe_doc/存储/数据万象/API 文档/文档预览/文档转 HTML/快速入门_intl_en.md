## Overview

The file-to-HTML conversion feature allows you to generate HTML pages for preview from multiple types of files. It enables easy online file preview on PC, app, and other terminals. It is widely suitable for diverse business scenarios, such as online education, enterprise OA, online knowledge base, and online file preview.

>? 
> - CI encapsulates the preview JS-SDK, so you can connect to the HTML preview service with only one URL.
> - If you want to use it in mini programs, see [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430).
>- To connect to a CDN domain name, you need to enable **Advanced Cache Expiration Settings** in CDN as instructed in [Node Caching Rule Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317).
>

## Request

#### Sample request

```plaintext
GET /<ObjectKey>?ci-process=doc-preview&dstType=html HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
```

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request parameters

| Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ------ | -------- |
| ObjectKey | Object name, such as `folder/document.pdf`. | String  | Yes |
| ci-process | CI's processing capability, which is fixed at `doc-preview` for file preview in HTML. | String | Yes |
| dstType   | Output target file type, which is fixed at `html` for HTML preview.  | String  | Yes       |
| srcType | Source file type as listed below.  | String | No |
| sign          | Object download signature, which must be URL-encoded. If the previewed object is privately readable, the signature needs to be passed in. </br>For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/1045/33452). | String | No      |
| copyable          | Whether the file content is copyable. Valid values: `1` (yes), `0` (no).     | String   | No      |
| htmlParams          | Custom configuration parameters in JSON structure, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430). Default configuration: { commonOptions: { isShowTopArea: true, isShowHeader: true } }. For supported configurations, see [Custom Configuration Overview](https://intl.cloud.tencent.com/document/product/436/49416).    | String   | No   |
| htmlwaterword          | Watermark text, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is empty by default.     | String  | No      |
| htmlfillstyle          | Watermark RGBA (color and transparency), which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is `rgba(192,192,192,0.6)` by default.  | String   | No      |
| htmlfront          | Watermark text style, which must be URL-safe Base64-encoded as described in [FAQs](https://intl.cloud.tencent.com/document/product/1045/33430) and is `bold 20px Serif` by default.    | String   | No      |
| htmlrotate          | Rotation angle of the watermark text in degrees. Value range: 0–360. Default value: `315`. | String   | No      |
| htmlhorizontal          | Horizontal spacing of the watermark text in px. Default value: `50`. | String | No |
| htmlvertical          | Vertical spacing of the watermark text in px. Default value: `100`. | String | No |

>!
>- Currently supported input file types include:
>  - Presentation files: PPTX, PPT, POT, POTX, PPS, PPSX, DPS, DPT, PPTM, POTM, PPSM.
>  - Text files: DOC, DOT, WPS, WPT, DOCX, DOTX, DOCM, DOTM.
>  - Spreadsheet files: XLS, XLT, ET, ETT, XLSX, XLTX, CSV, XLSB, XLSM, XLTM, ETS.
>  - Other files: PDF, LRC, C, CPP, H, ASM, S, JAVA, ASP, BAT, BAS, PRG, CMD, RTF, TXT, LOG, XML, HTM, HTML.
>- The input file size cannot exceed 200 MB.
>- The number of pages in the input file cannot exceed 5,000.
> 


#### Request body

The request body of this request is empty.


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).


#### Response body

The response body of this API request is the HTML preview content.


#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).


## Examples

#### Sample 1: Simple preview
To preview the PPT file with the `test.pptx` ObjectKey in the `examples-1258125638` bucket online, the final URL is as follows:

```plaintext
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/test.pptx?ci-process=doc-preview&dstType=html
```

>?You can also implement more custom features through JS-SDK. For more information, see [Custom Configuration Overview](https://www.tencentcloud.com/document/product/1045/47939).

Open the link directly in a browser to view the generated preview page. For slides, you can also perform full-screen slideshow, which supports **animation**, **trigger**, and other effects and provides **virtual laser pointer**, **speaker mode**, and other features.




#### Sample 2: Watermark + preview with custom configurations

Preview the PPT file with the `test.pptx` ObjectKey in the `examples-1258125638` bucket online.
1. Make it **uncopyable** by setting `copyable` to `0`.
2. Set the **test** watermark, which is URL-safe Based64-encoded into `htmlwaterword=dGVzdAog`.
2. Set **custom configuration parameters**. `htmlParams` is {"mode":"normal","commonOptions":{"isShowHeader":false,"isShowTopArea":true},"pptOptions":{"isSlidesStatusPlay": true}}, which is URL-safe Base64-encoded into `htmlParams=eyJtb2RlIjoibm9ybWFsIiwiY29tbW9uT3B0aW9ucyI6eyJpc1Nob3dIZWFkZXIiOmZhbHNlLCJpc1Nob3dUb3BBcmVhIjp0cnVlfSwicHB0T3B0aW9ucyI6eyJpc1NsaWRlc1N0YXR1c1BsYXkiOiB0cnVlfX0=`.

The final URL is as follows:

```plaintext
https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/test.pptx?ci-process=doc-preview&dstType=html&copyable=0&htmlwaterword=dGVzdAog&htmlParams=eyJtb2RlIjoibm9ybWFsIiwiY29tbW9uT3B0aW9ucyI6eyJpc1Nob3dIZWFkZXIiOmZhbHNlLCJpc1Nob3dUb3BBcmVhIjp0cnVlfSwicHB0T3B0aW9ucyI6eyJpc1NsaWRlc1N0YXR1c1BsYXkiOiB0cnVlfX0=
```

Open the link directly in a browser to view the generated preview page. For slides, you can also perform full-screen slideshow, which supports **animation**, **trigger**, and other effects and provides **virtual laser pointer**, **speaker mode**, and other features.




The preview link can also be embedded in a business webpage as an iframe as follows:

```plaintext
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <meta name="viewport"
        content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0,user-scalable=no">
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
    <meta name="keywords" content="COS, file preview">
    <meta name="description" content="">
    <title>Tencent Cloud - COS - file preview</title>
    <style>
        html,
        body {
            padding: 0;
            margin: 0;
            height: 100%;
            touch-action: manipulation;
        }
    </style>
</head>
<body>
    <iframe src="https://examples-1258125638.cos.ap-guangzhou.myqcloud.com/test.pptx?ci-process=doc-preview&dstType=html&copyable=0&htmlwaterword=dGVzdAog&htmlParams=eyJtb2RlIjoibm9ybWFsIiwiY29tbW9uT3B0aW9ucyI6eyJpc1Nob3dIZWFkZXIiOmZhbHNlLCJpc1Nob3dUb3BBcmVhIjp0cnVlfSwicHB0T3B0aW9ucyI6eyJpc1NsaWRlc1N0YXR1c1BsYXkiOiB0cnVlfX0=" width="100%" height="100%" allowFullScreen="true"></iframe>
</body>
</html>
```
