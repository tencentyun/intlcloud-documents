## Overview

This document provides an overview of APIs and SDK code samples for file preview.

| API | Operation |  Description |
| :--------------- | :------------------ | :--------------------- |
| [File transcoding](https://intl.cloud.tencent.com/document/product/436/49404) |  Getting the request URL for file transcoding |   Gets the request URL for file transcoding   |


## Sync File Transcoding

#### Feature description

This API is used to get the request URL for file transcoding.
>! 
> - Before using this API, make sure that the file processing feature has been enabled in the data processing section in the console; otherwise, the error `doc bucket unbinded, bucket's host is unavailable` will be reported.
> - To use the file to HTML conversion feature, directly put the request parameters after the URL. The SDK is only responsible for calculating the signature.
>

#### Sample code
```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your actual `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$secretKey = "SECRETKEY"; // Replace it with your actual `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi.
$region = "ap-beijing"; // Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // 1. For more information on file transcoding, visit https://cloud.tencent.com/document/product/460/47074.
    $bucket = 'examplebucket-1250000000';
    $key = 'exampleobject';
    $url = $cosClient->getObjectUrl($bucket, $key);
    $params = array(
        'ci-process' => 'doc-preview',
//        'srcType' => '',
        'page' => 3,
        'dstType' => 'png',
//        'password' => '',
//        'comment' => '',
//        'sheet' => '',
//        'excelPaperDirection' => '',
//        'excelRow' => '',
//        'excelCol' => '',
//        'excelPaperSize' => '',
//        'txtPagination' => '',
        'ImageParams' => 'imageMogr2/thumbnail/!50p',
//        'quality' => '',
//        'scale' => '',
//        'imageDpi' => '',
    );
    $query = http_build_query($params);
    echo $url . $query; // The generated accessible URL
} catch (\Exception $e) {
    // The request failed.
    echo($e);
}
```

#### Parameter description

Common request parameters

| Parameter | Description | Type | Required |
| :--------- | :----------------------------------------------------------- | :----- | :------- |
| Key        | Object name, such as `folder/document.pdf`. | String  | Yes |
| ci-process | CI's processing capability, which is fixed at `doc-preview` for file preview. | String | Yes |
| srcType    | Source data type. Currently, the file conversion feature determines the source data type according to the file extension of the COS object. If the object has no extension, you can set this value. | String | No       |
| page | Number of the page to be converted, which is counted from 1 by default. For spreadsheets, `page` indicates to convert the xth image in the xth sheet. | Int | No |
| dstType | Type of the output target file. Valid values: `png`, `jpg`, `pdf` (the page number cannot be selected, and the `page` parameter does not take effect), `txt`. If the input file format cannot be recognized, the `jpg` format will be used by default. | String | No |
| password | Password to open the Office file. If you need to convert a password-protected file, set this field. | String | No |
| comment    | Whether to hide comments and apply track changes. `0`: Hide comments and apply track changes. `1`: Show comments and track changes. Default value: `0`.                | Int  | No       |

Parameters for spreadsheet files (Excel)

| Parameter | Description | Type | Required |
| :------------------ | :----------------------------------------------------------- | :--- | :------- |
| sheet | Sheet parameter, indicating to convert the xth sheet. Default value: `1`. | Int | No |
| excelPaperDirection | Paper orientation of the spreadsheet. 0: Vertical; other values: Horizontal. Default value: `0`.                | Int  | No       |
| excelRow | The value `1` indicates that all rows will be formatted on one page. Default value: `0`. | Int | No |
| excelCol            | The value `1` indicates that all columns will be formatted on one page. Default value: `0`. | Int | No |
| excelPaperSize | Paper (canvas) size. Valid values: `0` (A4), `1` (A2), `2` (A0). Default value: `0`. This parameter should be used together with `excelRow` or `excelCol`. | Int | No |

Parameters for transcoding into .txt files

| Parameter | Description | Type | Required |
| :------------ | :----------------------------------------------------------- | :--- | :------- |
| txtPagination | Whether to convert to long text. When this parameter is set to `true`, the text in the pages to be exported can be combined before export, and the pagination range can be controlled by `Ranges`. The default value is `false`, indicating to generate .txt files by page. This parameter takes effect only if `ExportType` is `txt`. | Bool | No |

Parameters for transcoding to .png/.jpg images

| Name | Description | Type | Required |
| :---------- | :----------------------------------------------------------- | :----- | :------- |
| ImageParams | Processing parameters for the output image. All parameters of [basic image processing](https://www.tencentcloud.com/document/product/1045/33694) are supported. To specify multiple parameters, separate them by [pipeline operator](https://intl.cloud.tencent.com/document/product/1045/33727). In this way, the image can be processed by multiple parameters in sequence in the same request.  | String | No       |
| quality | Quality of the generated preview image. Value range: [1, 100]. Default value: `100`. For example, if the value is 100, the quality of the generated image will be 100%. | Int | No |
| scale       | Scaling parameter of the preview image. Value range: [10, 200]. Default value: `100`. For example, if the value is 200, the image will be scaled up (enlarged) by 200%.                | Int  | No       |
| imageDpi    | Renders the image based on the specified DPI. This parameter works together with `scale`. Value range: 96–600. Default value: `96`. The width of the output image must be less than 65500 px. | Int | No |

>!
>- Currently supported input file types include:
>   - Presentation files: PPTX, PPT, POT, POTX, PPS, PPSX, DPS, DPT, PPTM, POTM, PPSM.
>   - Text files: DOC, DOT, WPS, WPT, DOCX, DOTX, DOCM, DOTM.
>   - Spreadsheet files: XLS, XLT, ET, ETT, XLSX, XLTX, CSV, XLSB, XLSM, XLTM, ETS.
>     A spreadsheet file may be split into multiple pages, with multiple images generated.
>   - Other files: PDF, LRC, C, CPP, H, ASM, S, JAVA, ASP, BAT, BAS, PRG, CMD, RTF, TXT, LOG, XML, HTM, HTML.
>- The input file size cannot exceed 200 MB.
>- The number of pages in the input file cannot exceed 5,000.
> 

#### Sample response

```php
Sync request URL
https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/example.ppt?sign=q-sign-algorithmxxxxxxxxxxxxx&ci-process=doc-preview&page=1&dstType=png
```

