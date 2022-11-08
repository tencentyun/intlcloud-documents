
## Overview

This document provides an overview of APIs and SDK code samples for file preview jobs.

| API | Operation | Description |
| ------------------- | -------------- | --------------------- |
| [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49407) | Submitting file preview job | Submits file preview job. |
|  [DescribeDocProcessJob](https://intl.cloud.tencent.com/document/product/436/49408)  | Querying file preview job | Queries specified file preview job. |
|  [DescribeDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49409) | Pulling file preview jobs | Pulls eligible file preview jobs. |


## Submitting File Preview Job

#### Feature description

This API (`ci_create_doc_job`) is used to submit a file preview job.

#### Method prototype
```py
def ci_create_doc_job(self, Bucket, QueueId, InputObject, OutputBucket, OutputRegion, OutputObject, SrcType=None, TgtType=None,
                          StartPage=None, EndPage=-1, SheetId=0, PaperDirection=0, PaperSize=0, DocPassword=None, Comments=None, PageRanges=None, ImageParams=None, Quality=100, Zoom=100, ImageDpi=96, PicPagination=0, **kwargs)
```

#### Sample request
```py
def ci_create_doc_jobs():
    # Create an async file preview job
    response = client.ci_create_doc_job(
        Bucket=bucket_name,
        QueueId='p4bdf22xxxxxxxxxxxxxxxxxxxxxxxxxf1',
        InputObject='normal.pptx',
        OutputBucket=bucket_name,
        OutputRegion='ap-chongqing',
        OutputObject='/test_doc/normal/abc_${Number}.jpg',
        # DocPassword='123',
        Quality=109,
        PageRanges='1,3',
    )
    print(response)
    return response
```

#### Parameter description

| Parameter | Description | Type |
| --------- | -------------------------------------- | --------- |
| Bucket    | Bucket of the object                      | String    |
| QueueId   | ID of the queue which the job is in                      | String    |
| InputObject    | The object to be processed                       | Container |
| OutputRegion   | Bucket region                                                 | String |
| OutputBucket   | Result storage bucket                                             | String |
| OutputObject   | Output file path. **For non-spreadsheet files, the output file name must include the `${Number}` or `${Page}` parameter.** If there are multiple output files, `${Number}` indicates that serial numbers start from 1, and `${Page}` indicates that serial numbers are the same as preview page numbers. `${Number}` indicates that serial numbers start from 1 for multiple output files; for example, if the input parameter is `abc_${Number}.jpg` to preview pages 5–6 in the file, then output file names will be `abc_1.jpg` and `abc_2.jpg`. `${Page}` indicates that serial numbers are the same as preview page numbers for multiple output files; for example, if the input parameter is `abc_${Page}.jpg` to preview pages 5–6 in the file, then the output file names will be `abc_5.jpg` and `abc_6.jpg`. **For spreadsheet files, the output file path must include the `${SheetID}` placeholder, and the output file name must include the `${Number}` parameter.** For example, if the input parameter is `/${SheetID}/abc_${Number}.jpg`, then the corresponding number of folders will be generated first based on the number of Excel sheets to be converted, and then the corresponding number of image files will be generated in these folders. | String  |
| SrcType | Source data type. Currently, the file conversion feature determines the source data type based on the file extension of the COS object. If the object has no extension, you can set this value. | String |
| TgtType | Type of the output target image file. Valid values: `png`, `jpg`, `pdf`. If the input file format cannot be recognized, the `jpg` format will be used by default. | String |
| StartPage | Starts conversion from page X. A spreadsheet file may be split into multiple pages, with multiple images generated, and `StartPage` indicates to start the conversion from page X of the specified `SheetId`. Default value: `1`. | Int |
| EndPage | Ends conversion on page X. A spreadsheet file may be split into multiple pages, with multiple images generated, and `EndPage` indicates to end the conversion on page X of the specified `SheetId`. Default value: `-1` (converting all pages). | Int |
| SheetId |  Sheet parameter, indicating to convert the xth sheet. Default value: `1`. If this value is set to `0`, all sheets will be converted.                | Int  |
| PaperDirection | Paper orientation of the spreadsheet. 0: Vertical; other values: Horizontal. Default value: `0`.                | Int  |
| PaperSize      | Page (canvas) size. Valid values: `0` (A4), `1` (A2), `2` (A0). Default value: `0`. | Int  |
| DocPassword | Password to open the Office file. If you need to convert a password-protected file, set this field. | String |
| Comments | Whether to hide comments and apply track changes. 0: Hide comments and apply track changes; 1: Show comments and track changes. Default value: `0`. | Int |
| PageRanges     | Range of pages to be converted; for example, "1,2-4,7" means to convert pages 1, 2, 3, 4, and 7 in the file. | String |
| ImageParams | Processing parameters for the output image. All parameters of [basic image processing](https://www.tencentcloud.com/document/product/436/36365) are supported. To specify multiple parameters, separate them by [pipeline operator](https://intl.cloud.tencent.com/document/product/436/36380). In this way, the image can be processed by multiple parameters in sequence in the same request. | String |
| Quality | Quality of the generated preview image. Value range: [1-100]. Default value: `100`. For example, if the value is 100, the quality of the generated image will be 100%. | Int |
| Zoom                | Zooming parameter of the preview image. Value range: [10-200]. Default value: `100`. For example, if the value is 200, the image will be zoomed in (enlarged) by 200%. | Int |
| ImageDpi       | Renders the image according to the specified DPI. This parameter works together with `Zoom`. Value range: 96–600. Default value: `96`. The width of the output image must be less than 65500 px. | Int |
| PicPagination  | Whether to convert to a single long image. When this parameter is set to 1, up to 20 standard pages can be converted to a single long image, and more pages will cause an error. The page range can be controlled by `StartPage` and `EndPage`. The default value is 0, indicating to output images by page. This parameter will take effect only if `TgtType` is `png` or `jpg`. | Int |

#### Response description

```py
{
    'JobsDetail': {
        'Code': 'Success', 
        'CreationTime': '2022-09-14T00:00:00+0800', 
        'EndTime': '-', 
        'Input': {
            'BucketId': 'test-125xxxxxxxxxxx', 
            'Object': '1.txt', 
            'Region': 'ap-chongqing'
        }, 
        'JobId': 'dcf48xxxxxxxxxxxxxxxxxxxxxxxxxc523', 
        'Message': None, 
        'Operation': {
            'DocProcess': {
                'Comments': '1', 
                'DocPassword': None, 
                'EndPage': '-1', 
                'ImageDpi': '96', 
                'ImageParams': None, 
                'PageRanges': '1,3', 
                'PaperDirection': '0', 
                'PaperSize': '0', 
                'PicPagination': '0', 
                'Quality': '109', 
                'SheetId': '0', 
                'SrcType': None, 
                'StartPage': '0', 
                'TgtType': None, 
                'Zoom': '100'
            }, 
            'JobLevel': '0', 
            'Output': {
                'Bucket': 'test-125xxxxxxxxxxx', 
                'Object': '/test_doc/normal/abc_${Number}.jpg', 
                'Region': 'ap-chongqing'
            }
        }, 
        'QueueId': 'p4bxxxxxxxxxxxxxxxxxxxxxxxxxxxxx57f1', 
        'StartTime': '-', 
        'State': 'Submitted', 
        'Tag': 'DocProcess'
    }
}
```

| Parameter | Description | Type |
| ---------- | -------------- | --------- |
| JobsDetail | Job details |  Container |
| Code               | Error code, which will be returned only if `State` is `Failed`.      | String    |
| Message            | Error message, which will be returned only if `State` is `Failed`.   | String    |
| JobId        | Job ID                                              | String |
| Tag          | Job tag: DocProcess                                 | String |
| State        | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime | Job creation time |  String |
| QueueId      | ID of the queue which the job is in                                            | String |
| Input        | Input file path of the job                   | Container |
| Operation    | Operation rule | Container |



## Querying Specified File Preview Job

#### Feature description

This API (`ci_get_doc_job`) is used to query a specified file preview job.

#### Method prototype
```py
def ci_get_doc_job(self, Bucket, JobID, **kwargs):
```

#### Sample request

```py
def ci_get_doc_jobs():
    # Get the information of the specified async file preview job
    response = client.ci_get_doc_job(
        Bucket=bucket_name,
        JobID='d18a9xxxxxxxxxxxxxxxxxxxxff1aa',
    )
    print(response)
    return response
```

#### Parameter description
| Parameter | Description | Type |
| -------- | -------------- | ------ |
| Bucket    | Bucket of the object | String    |
| JobID    | File preview job ID | String |

#### Response description

```py
{
    'JobsDetail': 
    [{
        'Code': 'Success', 
        'CreationTime': '2022-09-14T17:15:43+0800', 
        'EndTime': '2022-09-14T17:15:45+0800', 
        'Input': {'BucketId': 'testpic-1253960454', 'Object': '1.txt', 'Region': 'ap-chongqing'}, 
        'JobId': 'dcf488492340d11edb2a0e3aa2e38c523', 
        'Message': None, 
        'Operation': {
            'DocProcess': {'Comments': '1', 
                'DocPassword': None, 
                'EndPage': '-1', 
                'ImageDpi': '96', 
                'ImageParams': None, 
                'PageRanges': '1,3', 
                'PaperDirection': '0', 
                'PaperSize': '0', 
                'PicPagination': '0',
                'Quality': '109', 
                'SheetId': '0', 
                'SrcType': None, 
                'StartPage': '0', 
                'TgtType': None, 
                'Zoom': '100'
            }, 
            'DocProcessResult': {
                'FailPageCount': '0', 
                'PageInfo': [{'PageNo': '1', 'TgtUri': '/test_doc/normal/abc_1.jpg'}, {'PageNo': '3', 'TgtUri': '/test_doc/normal/abc_3.jpg'}], 
                'SuccPageCount': '2', 
                'TaskId': None, 
                'TgtType': None, 
                'TotalPageCount': '7'
            }, 
            'JobLevel': '0', 
            'Output': {'Bucket': 'testpic-1253960454', 'Object': '/test_doc/normal/abc_${Number}.jpg', 'Region': 'ap-chongqing'}
        }, 
        'QueueId': 'p4bdf22746b014a22a5a097b1f1d057f1', 
        'StartTime': '2022-09-14T17:15:44+0800', 
        'State': 'Success', 
        'Tag': 'DocProcess'
    }]
}

```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | --------- |
| JobsDetail     | Job details, which is the same as `Response.JobsDetail` in the [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49407#.E5.93.8D.E5.BA.94) API. | Container |
| NonExistJobIds | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |


## Pulling Eligible File Preview Jobs 

#### Feature description

The API (`ci_list_doc_jobs`) is used to pull file preview jobs that meet specified conditions.

#### Method prototype
```py
def ci_list_doc_jobs(self, Bucket, QueueId, StartCreationTime=None, EndCreationTime=None, OrderByTime='Desc', States='All', Size=10, NextToken='', **kwargs):

```

#### Sample request
```py
def ci_list_doc_jobs():
    # Get the list of async file preview jobs
    response = client.ci_list_doc_jobs(
        Bucket=bucket_name,
        QueueId='p4bdxxxxxxxxxxxxxxxxxxxx57f1',
        Size=10,
    )
    print(response)
    return response
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| Bucket    | Bucket of the job | String    |
| QueueId           | ID of the queue from which jobs are pulled                                     | String |
| OrderByTime       | `Desc` (default) or `Asc`                                 | String |
| NextToken         | Context token for pagination                       | String |
| Size              | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100.                      | Int    |
| States            | Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. Valid values: `All` (default value), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. | String |
| StartCreationTime | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | String |
| EndCreationTime   | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | String |


#### Response description

```py
{
    'JobsDetail': [{
        'Code': 'Success', 
        'CreationTime': '2022-09-14T17:15:43+0800', 
        'EndTime': '2022-09-14T17:15:45+0800', 
        'Input': {'BucketId': 'testpic-1253960454', 'Object': '1.txt', 'Region': 'ap-chongqing'}, 
        'JobId': 'dcf488492340d11edb2a0e3aa2e38c523', 
        'Message': None, 
        'Operation': {
            'DocProcess': {
                'Comments': '1', 
                'DocPassword': None, 
                'EndPage': '-1', 
                'ImageDpi': '96', 
                'ImageParams': None, 
                'PageRanges': '1,3',
                'PaperDirection': '0', 
                'PaperSize': '0', 
                'PicPagination': '0', 
                'Quality': '109', 
                'SheetId': '0', 
                'SrcType': None, 
                'StartPage': '0', 
                'TgtType': None, 
                'Zoom': '100'
            }, 
            'DocProcessResult': {
                'FailPageCount': '0', 
                'PageInfo': [{'PageNo': '1', 'TgtUri': '/test_doc/normal/abc_1.jpg'}, {'PageNo': '3', 'TgtUri': '/test_doc/normal/abc_3.jpg'}], 
                'SuccPageCount': '2', 
                'TaskId': None, 
                'TgtType': None, 
                'TotalPageCount': '7'
            }, 
            'JobLevel': '0', 
            'Output': {'Bucket': 'testpic-1253960454', 'Object': '/test_doc/normal/abc_${Number}.jpg', 'Region': 'ap-chongqing'}
        }, 
        'QueueId': 'p4bdf22746b014a22a5a097b1f1d057f1', 
        'StartTime': '2022-09-14T17:15:44+0800', 
        'State': 'Success', 
        'Tag': 'DocProcess'
    }], 
    'NextToken': '75789'
}
```

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | --------- |
| JobsDetail     | Job details, which is the same as `Response.JobsDetail` in the [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49407#.E5.93.8D.E5.BA.94) API. | Container |
| NextToken             | Context token for pagination | String    |
