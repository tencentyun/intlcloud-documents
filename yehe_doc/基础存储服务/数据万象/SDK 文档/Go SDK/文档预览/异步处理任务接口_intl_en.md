
## Overview

This document provides an overview of APIs and SDK code samples for file preview jobs.

| API | Operation | Description |
| ------------------- | -------------- | --------------------- |
|  CreateDocProcessJobs   | Submitting file preview job | Submits file preview job. |
|DescribeDocProcessJob  | Querying file preview job | Queries specified file preview job. |
| DescribeDocProcessJobs| Pulling file preview jobs | Pulls eligible file preview jobs. |


## Submitting File Preview Job

#### Feature description

This API (`CreateDocProcessJobs`) is used to submit a file preview job.

#### Method prototype
```go
func (s *CIService) CreateDocProcessJobs(ctx context.Context, opt *CreateDocProcessJobsOptions) (*CreateDocProcessJobsResult, *Response, error)
```

#### Sample request
```go
createJobOpt := &cos.CreateDocProcessJobsOptions{
	Tag: "DocProcess",
	Input: &cos.DocProcessJobInput{
		Object: "form.pdf",
	},
	Operation: &cos.DocProcessJobOperation{
		Output: &cos.DocProcessJobOutput{
			Region: "ap-guangzhou",
			Object: "test-doc${Number}",
			Bucket: "examplebucket-1250000000",
		},
		DocProcess: &cos.DocProcessJobDocProcess{
			TgtType:     "png",
			StartPage:   1,
			EndPage:     -1,
			ImageParams: "watermark/1/image/aHR0cDovL3Rlc3QwMDUtMTI1MTcwNDcwOC5jb3MuYXAtY2hvbmdxaW5nLm15cWNsb3VkLmNvbS8xLmpwZw==/gravity/southeast",
		},
	},
	QueueId: "p111a8dd208104ce3b11c78398f658ca8",
}
res, _, err := c.CI.CreateDocProcessJobs(context.Background(), createJobOpt)
```

#### Parameter description

```go
type CreateDocProcessJobsOptions struct {
    XMLName   xml.Name
    Tag       string
    Input     *DocProcessJobInput
    Operation *DocProcessJobOperation
    QueueId   string
}
type DocProcessJobInput struct {
    Object string
}
type DocProcessJobOperation struct {
    Output           *DocProcessJobOutput
    DocProcess       *DocProcessJobDocProcess
    DocProcessResult *DocProcessJobDocProcessResult
}
type DocProcessJobOutput struct {
    Region string
    Bucket string
    Object string
}
type DocProcessJobDocProcess struct {
    SrcType        string
    TgtType        string
    SheetId        int
    StartPage      int
    EndPage        int
    ImageParams    string
    DocPassword    string
    Comments       int
    PaperDirection int
    Quality        int
    Zoom           int
}
```

| Parameter | Description | Type |
| --------- | -------------------------------------- | --------- |
| Tag       | Job type, which currently can only be `DocProcess`. | String    |
| Input     | The object to be processed                       | Container |
| Operation | Operation rule                               | Container |
| QueueId   | ID of the queue which the job is in                      | String    |
| Object    | File URL in COS. `Bucket` is specified by `Host`. | String    |
| Output     | Result output address                                  | Container |
| DocProcess | Job type parameter, which takes effect only if `Tag` is `DocProcess`. | Container |
| Region   | Bucket region                                                 | String |
| Bucket   | Result storage bucket                                             | String |
| Object   | Output file path. **For non-spreadsheet files, the output file name must include the `${Number}` or `${Page}` parameter.** If there are multiple output files, `${Number}` indicates that serial numbers start from 1, and `${Page}` indicates that serial numbers are the same as preview page numbers. `${Number}` indicates that serial numbers start from 1 for multiple output files; for example, if the input parameter is `abc_${Number}.jpg` to preview pages 5–6 in the file, then output file names will be `abc_1.jpg` and `abc_2.jpg`. `${Page}` indicates that serial numbers are the same as preview page numbers for multiple output files; for example, if the input parameter is `abc_${Page}.jpg` to preview pages 5–6 in the file, then the output file names will be `abc_5.jpg` and `abc_6.jpg`. **For spreadsheet files, the output file path must include the `${SheetID}` placeholder, and the output file name must include the `${Number}` parameter.** For example, if the input parameter is `/${SheetID}/abc_${Number}.jpg`, then the corresponding number of folders will be generated first based on the number of Excel sheets to be converted, and then the corresponding number of image files will be generated in these folders. | String  |
| SrcType | Source data type. Currently, the file conversion feature determines the source data type based on the file extension of the COS object. If the object has no extension, you can set this value. | String |
| TgtType | Type of the output target image file. Valid values: `png`, `jpg`, `pdf`. If the input file format cannot be recognized, the `jpg` format will be used by default. | String |
| SheetId |  Sheet parameter, indicating to convert the xth sheet. Default value: `1`. If this value is set to `0`, all sheets will be converted.                | Int  |
| StartPage | Starts conversion from page X. A spreadsheet file may be split into multiple pages, with multiple images generated, and `StartPage` indicates to start the conversion from page X of the specified `SheetId`. Default value: 1. | Int |
| EndPage | Ends conversion on page X. A spreadsheet file may be split into multiple pages, with multiple images generated, and `EndPage` indicates to end the conversion on page X of the specified `SheetId`. Default value: -1 (converting all pages). | Int |
| ImageParams | Processing parameters for the output image. All parameters of [basic image processing](https://www.tencentcloud.com/document/product/436/36365) are supported. To specify multiple parameters, separate them by [pipeline operator](https://intl.cloud.tencent.com/document/product/436/36380). In this way, the image can be processed by multiple parameters in sequence in the same request. | String |
| DocPassword | Password to open the Office file. If you need to convert a password-protected file, set this field. | String |
| Comments | Whether to hide comments and apply track changes. 0: hide comments and apply track changes; 1: show comments and track changes. Default value: 0. | Int |
| PaperDirection | Paper orientation of the spreadsheet. 0: vertical; other values: horizontal. Default value: 0.                | Int  |
| Quality | Quality of the generated preview image. Value range: [1-100]. Default value: 100. For example, if the value is 100, the quality of the generated image will be 100%. | Int |
| Zoom                | Zooming parameter of the preview image. Value range: [10-200]. Default value: 100. For example, if the value is 200, the image will be zoomed in (enlarged) by 200%. | Int |

#### Response description

```go
type CreateDocProcessJobsResult struct {
    JobsDetail DocProcessJobDetail
}
type DocProcessJobDetail struct { 
    Code         string
    Message      string
    JobId        string
    Tag          string
    State        string
    CreationTime string
    QueueId      string
    Input        *DocProcessJobInput
    Operation    *DocProcessJobOperation
}
```

| Parameter | Description | Type |
| ---------- | -------------- | --------- |
| JobsDetail | Job details |  Container |
| Code               | Error code, which will be returned only if `State` is `Failed`.      | String    |
| Message            | Error message, which will be returned only if `State` is `Failed`.   | String    |
| JobId        | Job ID                                              | String |
| Tag          | Job type: DocProcess                                 | String |
| State        | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime | Job creation time |  String |
| QueueId      | ID of the queue which the job is in                                            | String |
| Input | Path of the input file for this job. For more information, see `CreateDocProcessJobsOptions.Input`. | Container |
| Operation    | Operation rule. For more information, see `CreateDocProcessJobsOptions.Operation`. | Container |



## Querying Specified File Preview Job

#### Feature description

This API (`DescribeDocProcessJob`) is used to query a specified file preview job.

#### Method prototype
```go
func (s *CIService) DescribeDocProcessJob(ctx context.Context, jobid string) (*DescribeDocProcessJobResult, *Response, error)
```

#### Sample request

```go
jobid := "<jobid>"
res, _, err := c.CI.DescribeDocProcessJob(context.Background(), jobid)
```

#### Parameter description
| Parameter | Description | Type |
| -------- | -------------- | ------ |
| jobid    | File preview job ID | String |

#### Response description

```go
type DescribeDocProcessJobResult struct {
    JobsDetail     *DocProcessJobDetail 
    NonExistJobIds string
}
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | --------- |
| JobsDetail     | Job details. Same as `Response.JobsDetail` in `CreateDocProcessJobs`. | Container |
| NonExistJobIds | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |


## Pulling Eligible File Preview Jobs 

#### Feature description

The API (`DescribeDocProcessJobs`) is used to pull file preview jobs that meet specified conditions.

#### Method prototype
```go
func (s *CIService) DescribeDocProcessJobs(ctx context.Context, opt *DescribeDocProcessJobsOptions) (*DescribeDocProcessJobsResult, *Response, error)
```

#### Sample request
```go
DescribeJobsOpt := &cos.DescribeDocProcessJobsOptions{
	QueueId: "p111a8dd208104ce3b11c78398f658ca8",
	Tag:     "DocProcess",
}
res, _, err := c.CI.DescribeDocProcessJobs(context.Background(), DescribeJobsOpt)
```

#### Parameter description

```go
type DescribeDocProcessJobsOptions struct {
    QueueId           string
    Tag               string
    OrderByTime       string
    NextToken         string
    Size              int
    States            string
    StartCreationTime string
    EndCreationTime   string
}
```

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| QueueId           | ID of the queue from which jobs are pulled                                     | String |
| Tag               | Job type: DocProcess                                     | String |
| OrderByTime       | `Desc` (default) or `Asc`                                 | String |
| NextToken         | Context token for pagination                       | String |
| Size              | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100.                      | Int    |
| States            | Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. Valid values: `All` (default value), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. | String |
| StartCreationTime | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | String |
| EndCreationTime   | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | String |


#### Response description

```go
type DescribeDocProcessJobsResult struct {
    JobsDetail []DocProcessJobDetail
    NextToken  string
}
```

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | --------- |
| JobsDetail     | Job details. Same as `Response.JobsDetail` in `CreateDocProcessJobs`. | Container |
| NextToken             | Context token for pagination | String    |
