## Overview

The file preview feature allows generating images from multiple types of files for preview and performing basic processing operations on the output images synchronously. It addresses the display problems of file content on webpages and enables easy online file preview on PC, app, and other terminals. It is widely suitable for diverse business scenarios, such as online education, enterprise OA, and website transcoding.

> ?
> - To use this feature, you need to click **File Processing** on the management page of a bucket in the [CI console](https://console.cloud.tencent.com/ci), find the **File Preview** configuration item, and toggle it on. Then, you can call a specific file preview API to preview files in the bucket synchronously or asynchronously.
> - File preview is a paid feature. For billing details, see [File Processing Fees](https://intl.cloud.tencent.com/document/product/1045/49490).
> - The conversion logic of file transcoding is the same as that of local printing. If you need to change the conversion orientation (such as outputting an Excel file with many columns horizontally to one page), you need to change the source file print settings.
> 

## Request

#### Sample request

```plaintext
GET /<ObjectKey>?ci-process=doc-preview&page=<page>&srcType=<srcType>&ImageParams=<ImageParams> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>?
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> - For private buckets, the request needs to carry the signature for file download. 
>

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Common request parameters

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ | -------- |
| ObjectKey | Object name, such as `folder/document.pdf`. | String  | Yes |
| ci-process | CI's processing capability, which is fixed at `doc-preview` for file preview. | String | Yes |
| srcType    | Source data type. Currently, the file conversion feature determines the source data type according to the file extension of the COS object. If the object has no extension, you can set this value. | String | No       |
| page | Number of the page to be converted, which is counted from 1 by default. For spreadsheets, `page` indicates to convert the xth image in the xth sheet. | Int | No |
| dstType | Type of the output target file. Valid values: <br><li>png <br><li>jpg <br><li>pdf (the page number cannot be selected, and the `page` parameter does not take effect) <br/>If the input file format cannot be recognized, the `jpg` format will be used by default. | String | No |
| password | Password to open the Office file. If you need to convert a password-protected file, set this field. | String | No |
| comment    | Whether to hide comments and apply track changes. 0: hide comments and apply track changes; 1: show comments and track changes. Default value: 0. | Int    | No       |


#### Parameters for spreadsheet files (Excel)

| Header | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ---- | -------- |
| sheet | Sheet parameter, indicating to convert the xth sheet. Default value: 1. | Int | No |
| excelPaperDirection | Paper orientation of the spreadsheet. 0: vertical; other values: horizontal. Default value: 0.                | Int  | No       |
| excelPaperSize | Paper (canvas) size. Valid values: 0 (A4), 1 (A2), 2 (A0). Default value: 0. This parameter should be used together with `excelRow` or `excelCol`. | Int | No |


#### Parameters for transcoding to .png/.jpg images

| Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ------ | -------- |
| ImageParams | Processing parameters for the output image. All parameters of [basic image processing](https://www.tencentcloud.com/document/product/1045/33694) are supported. To specify multiple parameters, separate them with [pipeline operators](https://intl.cloud.tencent.com/document/product/1045/33727). In this way, the image can be processed by multiple parameters in sequence in the same request.  | String | No       |
| quality | Quality of the generated preview image. Value range: [1, 100]. Default value: 100. For example, if the value is 100, the quality of the generated image will be 100%. | Int | No |
| scale       | Scaling parameter of the preview image. Value range: [10, 200]. Default value: 100. For example, if the value is 200, the image will be scaled up (enlarged) by 200%.                | Int  | No       |
| imageDpi    | Renders the image based on the specified DPI. This parameter works together with `scale`. Value range: 96–600. Default value: 96. The width of the output image must be less than 65500 px. | Int | No |


>!
>- Currently supported input file types include:
>  - Presentation files: PPTX, PPT, POT, POTX, PPS, PPSX, DPS, DPT, PPTM, POTM, PPSM.
>  - Text files: DOC, DOT, WPS, WPT, DOCX, DOTX, DOCM, DOTM.
>  - Spreadsheet files: XLS, XLT, ET, ETT, XLSX, XLTX, CSV, XLSB, XLSM, XLTM, ETS.
   A spreadsheet file may be split into multiple pages, with multiple images generated.
>  - Other files: PDF, LRC, C, CPP, H, ASM, S, JAVA, ASP, BAT, BAS, PRG, CMD, RTF, TXT, LOG, XML, HTM, HTML.
>- The input file size cannot exceed 200 MB.
>- The number of pages in the input file cannot exceed 5,000.


#### Request body

The request body of this request is empty.


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).


#### Response parameter description

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ----- |
| X-Total-Page | Total number of pages in the file (or images converted from sheets in the spreadsheet file) returned in the HTTP header. This value will be empty in case of an exception.                  | Int   |
| Content-Type | Different values will be returned based on the actual image format, such as `image/jpeg` and `image/webp`. | String |
| X-ErrNo      | The error code returned in case of an exception, which can be viewed in the HTTP header.                  | String |
| X-Total-Sheet | Total number of sheets in the spreadsheet file returned in the HTTP header. | Int |
| X-Sheet-Name      | Name of the current sheet in the spreadsheet file returned in the HTTP header. | String |

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).


## Examples

**Sample 1: Previewing a general file**

#### Request

```plaintext
GET /sample.pdf?ci-process=doc-preview&page=1 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
```


#### Response 1: Preview succeeds

```plaintext
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
X-Total-Page: 100
 
[Image data after transcoding]
```

#### Response 2: The file does not exist

```plaintext
HTTP/1.1 404 OK
Connection: close
Content-Length: 455
Content-Type: application/xml
Date: Thu, 09 Apr 2020 13:44:52 GMT
X-ErrNo: -3004
```

#### Response 3: The specified page does not exist

```plaintext
HTTP/1.1 404 OK
Connection: close
Content-Length: 455
Content-Type: application/xml
Date: Thu, 09 Apr 2020 13:44:52 GMT
X-ErrNo: -3013
```


**Sample 2: Previewing a file and processing the image by scaling it and adding a text watermark**

#### Request

```plaintext
GET /sample.pdf?ci-process=doc-preview&page=1&ImageParams=imageMogr2/thumbnail/!50p|watermark/2/text/5pWw5o2u5LiH6LGh/fill/I0ZGRkZGRg==/fontsize/30/dx/20/dy/20 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
```

#### Response 1: Preview succeeds

```plaintext
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 645
Date: Tue, 03 Apr 2018 09:06:16 GMT
X-Total-Page: 100
 
[Image data after transcoding]
```

#### Response 2: The file does not exist

```plaintext
HTTP/1.1 404 OK
Connection: close
Content-Length: 455
Content-Type: application/xml
Date: Thu, 09 Apr 2020 13:44:52 GMT
X-ErrNo: -3004
```

#### Response 3: The specified page does not exist

```plaintext
HTTP/1.1 404 OK
Connection: close
Content-Length: 455
Content-Type: application/xml
Date: Thu, 09 Apr 2020 13:44:52 GMT
X-ErrNo: -3013
```
