
## Overview

This document provides an overview of APIs and SDK code samples for sync requests for file preview.

| API  |	Description  |
|----|-----|
| [Sync request API](https://intl.cloud.tencent.com/document/product/436/49404)  |       Synchronously requests for file preview.   |



## Sync Request API

#### Feature description

This API is used to synchronously request for file preview.

#### Method prototype

```py
    def ci_doc_preview_process(self, Bucket, Key, SrcType=None, Page=None, DstType=None, PassWord=None, Comment=0, Sheet=1,
                               ExcelPaperDirection=0, ExcelRow=0, ExcelCol=0, ExcelPaperSize=None, TxtPagination=False,
                               ImageParams=None, Quality=100, Scale=100, ImageDpi=96, **kwargs)
```

#### Sample request

```py
    def ci_doc_preview_process():
        # Sync file preview API
        response = client.ci_doc_preview_process(
            Bucket=bucket_name,
            Key='1.txt',
        )
        print(response)
        response['Body'].get_stream_to_file('result.png')
```

#### Parameter description


| Parameter | Description | Type |
| ------------------- | ------------------------------------------------------------ | ------ |
| Bucket    | Bucket of the object | String    |
| Key        | Object name, such as `folder/document.pdf`. | String  |
| SrcType | Source data type. Currently, the file conversion feature determines the source data type according to the file extension of the COS object. If the object has no extension, you can set this value. | String |
| Page | Number of the page to be converted, which is counted from 1 by default. For spreadsheets, `page` indicates to convert the xth image in the xth sheet. | int |
| DstType | Type of the output target image file. Valid values: `png`, `jpg`, `pdf`. If the input file format cannot be recognized, the `jpg` format will be used by default. | String |
| Password | Password to open the Office file. If you need to convert a password-protected file, set this field. | String |
| Comment | Whether to hide comments and apply track changes. 0: hide comments and apply track changes; 1: show comments and track changes. Default value: `0`. | int |
| Sheet | Sheet parameter, indicating to convert the xth sheet. Default value: `1`. | int |
| ExcelPaperDirection | Paper orientation of the spreadsheet. `0`: vertical; other values: horizontal. Default value: `0`. | int |
| ExcelRow | The value `1` indicates that all rows will be formatted on one page. Default value: `0`. | int |
| ExcelCol | The value `1` indicates that all columns will be formatted on one page. Default value: `0`. | int |
| ExcelPaperSize      | Page (canvas) size. Valid values: `0` (A4), `1` (A2), `2` (A0). Default value: `0`. This parameter needs to be used together with `excelRow` or `excelCol`.   | int  |
| TxtPagination       | Whether to convert to long text. When this parameter is set to `true`, the text in the pages to be exported can be combined before export, and the pagination range can be controlled by `Ranges`. The default value is `false`, indicating to generate .txt files by page. This parameter takes effect only if `ExportType` is `txt`. | bool |
| ImageParams | Processing parameters for the output image. All parameters of [basic image processing](https://www.tencentcloud.com/document/product/436/36365) are supported. To specify multiple parameters, separate them with [pipeline operators](https://intl.cloud.tencent.com/document/product/436/36380). In this way, the image can be processed by multiple parameters in sequence in the same request. | String |
| Quality | Quality of the generated preview image. Value range: [1-100]. Default value: `100`. For example, if the value is `100`, the quality of the generated image will be 100%. | int |
| Scale       | Scaling parameter of the preview image. Value range: [10, 200]. Default value: `100`. For example, if the value is `200`, the image will be scaled up (enlarged) by 200%.                | int  |
| ImageDpi       | Renders the image according to the specified DPI. This parameter works together with `scale`. Value range: 96–600. Default value: `96`. The width of the output image must be less than 65500 px. | int |
