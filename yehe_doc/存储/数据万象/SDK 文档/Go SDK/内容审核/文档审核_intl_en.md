
## Overview

This document provides an overview of APIs and SDK code samples for file moderation.

| API | Description |
| :--------------- | :------------------ |
|[Submitting file moderation job](https://intl.cloud.tencent.com/document/product/436/48258) | Submits file moderation job.   |
|[Querying file moderation job result](https://intl.cloud.tencent.com/document/product/436/48259)  | Queries the result of specified file moderation job. |

## Creating Job

This API (`PutDocumentAuditingJob`) is used to submit a file moderation job. You can receive the moderation result by setting the callback address or querying by `JobId`.

#### Method prototype

```go
func (s *CIService) PutDocumentAuditingJob(ctx context.Context, opt *PutDocumentAuditingJobOptions) (*PutDocumentAuditingJobResult, *Response, error)
```

#### Sample request

```go
// Replace `examplebucket-1250000000` and `COS_REGION` with your actual information
// For CI jobs, you need to provide the CIURL.
bu, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
cu, _ := url.Parse("https://examplebucket-1250000000.ci.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: bu, CIURL: cu}
c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			SecretID:  os.Getenv("SECRETID"),
			SecretKey: os.Getenv("SECRETKEY"),
        }
})
opt := &cos.PutDocumentAuditingJobOptions{
	InputUrl: "http://www.example.com/doctest.docx",
	InputType: "docx",
	Conf: &cos.DocumentAuditingJobConf{
		DetectType: "Porn,Ads",
	},
}
res, _, err := c.CI.PutDocumentAuditingJob(context.Background(), opt)
```

#### Parameter description

```go
type PutDocumentAuditingJobOptions struct {
    InputObject   string
    InputUrl      string
    InputType     string
    InputDataId   string
    InputUserInfo *UserExtraInfo
    Conf          *DocumentAuditingJobConf
}
type UserExtraInfo struct {
	TokenId  string
	Nickname string
	DeviceId string
	AppId    string
	Room     string
	IP       string
	Type     string
}
type DocumentAuditingJobConf struct {
    DetectType      string
    Callback        string
	BizType         string
}
```

| Parameter | Description | Type |
| ----------- | ------------------------------------------------------------ | ------ |
| InputObject | Name of the file stored in the COS bucket; for example, if the file is `test.doc` in the `test` directory, then the filename is `test/test.doc`. Either `Object` or `Url` can be selected at a time. | String |
| InputUrl    | Full URL of the file, such as `http://www.example.com/doctest.doc`. Either `Object` or `Url` can be selected at a time. | String |
| InputType   | File type. If this parameter is not specified, the file extension will be used as the type by default, such as DOC, DOCX, PPT, and PPTX. If the file has no extension, this field must be specified; otherwise, moderation will fail. | String |
| InputDataId | File ID. This field will return the original content in the result, which can contain up to 512 bytes. | String |
| InputUserInfo | Business field. | Object |
| Conf        | Moderation rule configuration.                                                 | Struct |
| BizType     | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console as instructed in Setting Moderation Policy. | String |
| DetectType  | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String |
| Callback    | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String |

#### Response description

Calling the `PutDocumentAuditingJob` function will parse the XML content returned by the API into a `PutDocumentAuditingJobResult` structure. For specific response parameters, see [Submitting File Moderation Job](https://intl.cloud.tencent.com/document/product/436/48258).


## Querying Job

This API (`GetDocumentAuditingJob`) is used to query the result of the specified file moderation job by `JobId`.

#### Method prototype

```go
func (s *CIService) GetDocumentAuditingJob(ctx context.Context, jobid string) (*GetDocumentAuditingJobResult, *Response, error)
```

#### Sample request

```go
// Replace `examplebucket-1250000000` and `COS_REGION` with your actual information
// For CI jobs, you need to provide the CIURL.
bu, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
cu, _ := url.Parse("https://examplebucket-1250000000.ci.COS_REGION.myqcloud.com")
b := &cos.BaseURL{BucketURL: bu, CIURL: cu}
c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			SecretID:  os.Getenv("SECRETID"),
			SecretKey: os.Getenv("SECRETKEY"),
        }
})
jobId := "sdce25f391a72e11eb99f********"
res, _, err := c.CI.GetDocumentAuditingJob(context.Background(), jobId)
```

#### Parameter description

| Parameter | Description | Type |
| -------- | -------- | ------ |
| jobId    | Job ID.   | String |

#### Response description

Calling the `GetDocumentAuditingJob` function will parse the XML content returned by the API into a `GetDocumentAuditingJobResult` structure. For specific response parameters, see [Querying File Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48259).
