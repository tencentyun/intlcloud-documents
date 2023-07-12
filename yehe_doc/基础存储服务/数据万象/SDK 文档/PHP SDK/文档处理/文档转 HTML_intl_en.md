## Overview

This document provides an overview of APIs and SDK code samples for file preview.

| API | Operation |  Description |
| :--------------- | :------------------ | :--------------------- |
| [File-to-HTML conversion](https://intl.cloud.tencent.com/document/product/436/49414) |  Getting the request URL for file-to-HTML conversion |   Gets the request URL for file-to-HTML conversion.   |

## File-to-HTML Conversion

#### Feature description

This API is used to get the request URL for file-to-HTML conversion.

#### Sample code

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // 2. Convert the file to HTML. For more information, visit https://cloud.tencent.com/document/product/460/52518.
    $bucket = 'examplebucket-1250000000';
    $key = 'exampleobject';
    $url = $cosClient->getObjectUrl($bucket, $key, "+30 minutes");
    $params = array(
        'ci-process' => 'doc-preview',
//        'srcType' => '',
        'dstType' => 'html',
//        'sign' => '',
//        'copyable' => '',
//        'htmlParams' => '',
//        'htmlwaterword' => '',
//        'htmlfillstyle' => '',
//        'htmlfront' => '',
//        'htmlrotate' => '',
//        'htmlhorizontal' => '',
//        'htmlvertical' => '',
    );
    $query = http_build_query($params);
    echo $url . $query; // The generated accessible URL
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Name | Description | Type | Required |
| :------------- | :----------------------------------------------------------- | :----- | :------- |
| Key        | Object filename, such as `folder/document.pdf`. | String  | Yes |
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
>   - Presentation files: PPTX, PPT, POT, POTX, PPS, PPSX, DPS, DPT, PPTM, POTM, PPSM.
>   - Text files: DOC, DOT, WPS, WPT, DOCX, DOTX, DOCM, DOTM.
>   - Spreadsheet files: XLS, XLT, ET, ETT, XLSX, XLTX, CSV, XLSB, XLSM, XLTM, ETS.
>   - Other files: PDF, LRC, C, CPP, H, ASM, S, JAVA, ASP, BAT, BAS, PRG, CMD, RTF, TXT, LOG, XML, HTM, HTML.
>- The input file size cannot exceed 200 MB.
>- The number of pages in the input file cannot exceed 5,000.
> 

#### Sample response

```php
Sync request URL
https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/example.ppt?sign=q-sign-algorithmxxxxxxxxxxxxx&ci-process=doc-preview&dstType=html
```

