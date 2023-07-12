
## Overview

This document provides an overview of APIs and SDK code samples for file compression in CI.

| API | Description  |
| ------------------- | ------------------- |
| [Submitting a multi-file zipping job](https://intl.cloud.tencent.com/document/product/436/53995)   | Submits a multi-file zipping job.        |
| [Querying the result of a multi-file zipping job](https://intl.cloud.tencent.com/document/product/436/53996)  | Queries the result of a specified multi-file zipping job. |



## Submitting a Multi-File Zipping Job

#### Feature description

The multi-file zipping feature uses a request to zip multiple files into a compressed file such as a ZIP file. You can submit a job to zip multiple files and asynchronously return the compressed file.

#### Method prototype
```go
func (s *CIService) CreateFileProcessJob(ctx context.Context, opt *FileProcessJobOptions) (*FileProcessJobResult, *Response, error)
```

#### Sample request
```go
createJobOpt := &cos.FileProcessJobOptions{
	Tag: "FileCompress",
	Operation: &cos.FileProcessJobOperation{
		FileCompressConfig: &cos.FileCompressConfig{
			Format:  "zip",
			Flatten: "0",
			Key:     []string{"1.mp3", "2.jpg"},
		},
		Output: &cos.FileProcessOutput{
			Region: "ap-shanghai",
			Bucket: "test-1250000000",
			Object: "vvvvxxxzz.zip",
		},
	},
	QueueId: "p111a8dd208104ce3b11c78398f658ca8",
}
res, _, err := c.CI.CreateFileProcessJob(context.Background(), createJobOpt)
```

#### Parameter description

```go
type FileProcessJobOptions struct {
	XMLName          xml.Name
	Tag              string
	Input            *FileProcessInput
	Operation        *FileProcessJobOperation
	QueueId          string
	CallBackFormat   string
	CallBackType     string
	CallBack         string
	CallBackMqConfig *NotifyConfigCallBackMqConfig
}
type FileProcessInput struct {
	Region     string
	Bucket     string
	Object           string
}
type FileProcessJobOperation struct {
	FileHashCodeConfig   *FileHashCodeConfig
	FileHashCodeResult   *FileHashCodeResult
	FileUncompressConfig *FileUncompressConfig
	FileUncompressResult *FileUncompressResult
	FileCompressConfig   *FileCompressConfig
	FileCompressResult   *FileCompressResult
	Output               *FileProcessOutput
	UserData             string
}
type FileHashCodeConfig struct {
	Type        string
	AddToHeader bool
}
type FileHashCodeResult struct {
	MD5          string
	SHA1         string
	SHA256       string
	FileSize     int
	LastModified string
	Etag         string
}
type FileUncompressConfig struct {
	Prefix         string
	PrefixReplaced string
}
type FileUncompressResult struct {
	Region    string
	Bucket    string
	FileCount string
}
type FileCompressConfig struct {
	Flatten string
	Format  string
	UrlList string
	Prefix  string
	Key     []string
}
type FileCompressResult struct {
	Region     string
	Bucket     string
	Object           string
}
type FileProcessOutput struct {
	Region     string
	Bucket     string
	Object           string
}
type NotifyConfigCallBackMqConfig struct {
	MqMode   string
	MqRegion string
	MqName   string
}
```

| Parameter | Description | Type | Required |
| --------- | -------------------------------------- | --------- | --------- |
| Tag       | Job tag, which currently can only be `FileCompress`. | String    | Yes |
| Input     | The object to be processed. For more information, see [Input](https://www.tencentcloud.com/document/product/436/53995). | Container | Yes         |
| Operation | Operation rule                               | Container | Yes         |
| Operation.FileCompressConfig | File zipping rule. For more information, see [Submitting Multi-File Zipping Job](https://intl.cloud.tencent.com/document/product/436/53995). | Container | Yes         |
| Operation.FileCompressResult | Multi-file zipping result, which will not be returned when the job is not completed. For more information, see [Submitting Multi-File Zipping Job](https://intl.cloud.tencent.com/document/product/436/53995). | Container | No         |
| Operation.Output | Address where the output file is stored. For more information, see [Submitting Multi-File Zipping Job](https://intl.cloud.tencent.com/document/product/436/53995). | Container | Yes         |
| Operation.UserData | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| QueueId   | ID of the queue where the job is in                      | String    | Yes         |
| CallBackFormat | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| CallBackType | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack   | Job callback address. It takes higher priority over that of the queue.                    | String    | No       |
| CallBackMqConfig | TDMQ configuration for job callback as described in [Structure](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

#### Response description

```go
type FileProcessJobResult struct {
    JobsDetail FileProcessJobResult
}
type FileProcessJobResult struct {
    Code         string
    Message      string
    JobId        string
    Tag          string
    State        string
    CreationTime string
	StartTime    string
	EndTime      string
    QueueId      string
    Input        *FileProcessInput
    Operation    *FileProcessJobOperation
}
```

| Parameter | Description | Type |
| ---------- | -------------- | --------- |
| JobsDetail | Job details |  Container |
| Code               | Error code, which will be returned only if `State` is `Failed`.      | String    |
| Message            | Error message, which will be returned only if `State` is `Failed`.   | String    |
| JobId        | Job ID                                              | String |
| Tag          | Job tag: FileCompress | String |
| State        | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime | Job creation time |  String |
| StartTime    | Job start time |  String |
| EndTime      | Job end time |  String |
| QueueId      | ID of the queue which the job is in                                            | String |
| Input | Path of the input file for this job. For more information, see `FileProcessJobOptions.Input`. | Container |
| Operation    | Operation rule. For more information, see `FileProcessJobOptions.Operation`. | Container |



## Querying Multi-File Zipping Result

#### Feature description

This API is used to query the details of a file processing job by job ID.

#### Method prototype
```go
func (s *CIService) DescribeFileProcessJob(ctx context.Context, jobid string) (*FileProcessJobResult, *Response, error)
```

#### Sample request

```go
jobid := "<jobid>"
res, _, err := c.CI.DescribeFileProcessJob(context.Background(), jobid)
```

#### Parameter description
| Parameter | Description | Type | Required |
| -------- | -------------- | ------ | -------- |
| jobid    | File processing job ID | String | Yes         |

#### Response description

```go
type FileProcessJobResult struct {
	JobsDetail *FileProcessJobsDetail
}
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | --------- |
| JobsDetail     | Job details, which is the same as `Response.JobsDetail` in the `CreateFileProcessJob` API. | Container |

