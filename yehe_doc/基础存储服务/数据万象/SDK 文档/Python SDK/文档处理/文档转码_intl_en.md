
## Overview

This document provides an overview of APIs and SDK code samples for file preview.

| API | Operation |  Description |
| :--------------- | :------------------ | :--------------------- |
| [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49407)|   Submitting file preview job | Submits file preview job. |
| [DescribeDocProcessJob](https://intl.cloud.tencent.com/document/product/436/49408) |   Querying file preview job | Queries specified file preview job. |
| [DescribeDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49409)  |  Pulling file preview jobs | Pulls eligible file preview jobs. |



## Submitting File Preview Job

#### Feature description

This API (`ci_create_doc_job`) is used to submit a file preview job.

#### Sample code

```python
   response = client.ci_create_doc_job(
                    Bucket="examplebucket-1250000000",
                    QueueId='pbbbcc56b344e422da78c984be45*****',
                    InputObject='normal.pptx',
                    OutputBucket="examplebucket-1250000000",
                    OutputRegion='ap-chongqing',
                    OutputObject='/test_doc/normal/abc_${Number}.jpg',
                )
    print(response)
    return response 
```


#### Parameter description

To call the `ci_create_doc_job` function, the specific request parameters are as follows:

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket name.                                 | String  | Yes       |
| QueueId| Queue ID of the job.                | String  | Yes       |
| InputObject| File URL in COS.                | String  | Yes       |
| OutputBucket| Result storage bucket.                | String  | Yes       |
| OutputRegion| Result storage bucket region.                | String  | Yes       |
| OutputObject| Output file path. <br/>**For non-spreadsheet files, the output file name must include the `${Number}` or `${Page}` parameter.** If there are multiple output files, `${Number}` indicates that serial numbers start from 1, and `${Page}` indicates that serial numbers are the same as preview page numbers. <ul style="margin-bottom:0px"><li>`${Number}` indicates that serial numbers start from 1 for multiple output files; for example, if the input parameter is `abc_${Number}.jpg` to preview pages 5–6 in the file, then output file names will be `abc_1.jpg` and `abc_2.jpg`.</li><li>`${Page}` indicates that serial numbers are the same as preview page numbers for multiple output files; for example, if the input parameter is `abc_${Page}.jpg` to preview pages 5–6 in the file, then the output file names will be `abc_5.jpg` and `abc_6.jpg`. <br/>**For spreadsheet files, the output file path must include the `${SheetID}` placeholder, and the output file name must include the `${Number}` parameter.** <br>For example, if the input parameter is `/${SheetID}/abc_${Number}.jpg`, then the corresponding number of folders will be generated first according to the number of Excel sheets to be converted, and then the corresponding number of image files will be generated in these folders.</li>   </ul> | String  | Yes |
| SrcType|  Source data type. Currently, the file conversion feature determines the source data type according to the file extension of the COS object. If the object has no extension, you can set this value.                | String  | No       |
| TgtType| Type of the output target file. Valid values: png, jpg, pdf. If the input file format cannot be recognized, the `jpg` format will be used by default. You cannot specify pages for the `pdf` format. | String | No |
| StartPage| Starts conversion from page X. A spreadsheet file may be split into multiple pages, with multiple images generated, and `StartPage` indicates to start the conversion from page X of the specified `SheetId`. Default value: 1. | Int | No |
| EndPage| Ends conversion on page X. A spreadsheet file may be split into multiple pages, with multiple images generated, and `EndPage` indicates to end the conversion on page X of the specified `SheetId`. Default value: -1 (converting all pages). | Int | No |
| SheetId|  Sheet parameter, indicating to convert the xth sheet. Default value: 0 (converting all sheets).                | Int  | No       |
| PaperDirection| Paper orientation of the spreadsheet. 0: vertical; other values: horizontal. Default value: 0.                | Int  | No       |
| PaperSize|  Page (canvas) size. Valid values: 0 (A4), 1 (A2), 2 (A0). Default value: 0.            | Int  | No       |
| DocPassword|  Password to open the Office file. If you need to convert a password-protected file, set this field.	                | String  | No       |
| Comments|  Whether to hide comments and apply track changes. 0: hide comments and apply track changes; 1: show comments and track changes. Default value: 0.                | Int  | No       |
| ImageParams|   Processing parameters for the output image. All parameters of basic image processing are supported. To specify multiple parameters, separate them by pipeline operator. In this way, the image can be processed by multiple parameters in sequence in the same request.                | String  | No       |
| Quality|  Quality of the generated preview image. Value range: [1-100]. Default value: 100. For example, if the value is 100, the quality of the generated image will be 100%.                | Int  | No       |
| Zoom|   Scaling parameter of the preview image. Value range: [10-200]. Default value: 100. For example, if the value is 200, the image will be scaled up (enlarged) by 200%.                | Int  | No       |
| ImageDpi|  Renders the image according to the specified DPI. This parameter works together with `Zoom`. Value range: 96–600. Default value: 96. The width of the output image must be less than 65500 px. | Int | No |
| PicPagination| Whether to convert to a single long image. When this parameter is set to 1, up to 20 standard pages can be converted to a single long image, and more pages will cause an error. The page range can be controlled by `StartPage` and `EndPage`. The default value is 0, indicating to output images by page. This parameter will take effect only if `TgtType` is `png` or `jpg`. | Int | No |

#### Response parameter description

Calling the `ci_create_doc_jobs` function will convert the XML returned in the API into a `dict` value. For specific response parameters, see [Submitting File Preview Job](https://intl.cloud.tencent.com/document/product/436/49407).

## Querying Specified File Preview Job

#### Feature description


This API (`ci_get_doc_job`) is used to query a specified file preview job.

#### Sample code

```python
    response = client.ci_get_doc_job(
                    Bucket="examplebucket-1250000000",
                    JobID='d31d414c8c07811ec894cd30d17*****',
                )
    print(response)
    return response 
```

#### Parameter description

To call the `ci_get_doc_job` function, the specific request parameters are as follows:

| Parameter | Description | Type | Required |
| --------- | --------------------- | ------ | -------- |
| Bucket | Bucket name.          | String  | Yes       |
| JobID| Job ID.                | String  | Yes       |

#### Response parameter description

Calling the `ci_get_doc_job` function will convert the XML returned in the API into a `dict` value. For specific response parameters, see [Querying File Preview Job](https://intl.cloud.tencent.com/document/product/436/49408).



## Querying All File Preview Jobs

#### Feature description

This API (`ci_list_doc_jobs`) is used to query a specified file preview job.

#### Sample code

```python
    response = client.ci_list_doc_jobs(
                    Bucket="examplebucket-1250000000",
                    QueueId='pbbbcc56b344e422da78c984be45*****',
                )
    print(response)
    return response 
```

#### Parameter description

To call the `ci_list_doc_jobs` function, the specific request parameters are as follows:

| Parameter | Description | Type | Required |
| --------- | ----------------- | ------ | -------- |
| Bucket | Bucket name.          | String  | Yes       |
| QueueId| Queue ID of the job.         | String  | Yes       |
| StartCreationTime| Start time.      | String  | No       |
| EndCreationTime| End time.       | String  | No       |
| OrderByTime| Sorting order. Valid values: Desc, Asc. Default value: Desc.  | String  | No    |
| States| Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. Valid values: All (default), Submitted, Running, Success, Failed, Pause, Cancel.  | String  | No       |
| Size| 	Maximum number of jobs that can be pulled. Default value: 10. Maximum value: 100.   | String  | No       |
| NextToken| Context token for pagination.   | String  | No       |

#### Response parameter description

Calling the `ci_list_doc_jobs` function will convert the XML returned in the API into a `dict` value. For specific response parameters, see [Pulling File Preview Job](https://intl.cloud.tencent.com/document/product/436/49409).
