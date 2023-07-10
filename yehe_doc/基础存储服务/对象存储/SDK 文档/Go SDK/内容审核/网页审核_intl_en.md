
## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for webpage moderation.

| API | Description |
| :--------------- | :------------------ |
|[Submitting webpage moderation job](https://intl.cloud.tencent.com/document/product/436/48282)  | Submits a webpage moderation job.   |
|[Querying webpage moderation job result](https://intl.cloud.tencent.com/document/product/436/48283)  | Queries the result of a specified webpage moderation job. |

## Creating a Job

This API (`PutWebpageAuditingJob`) is used to submit a webpage moderation job. You can receive the moderation result by setting the callback address or querying by `JobId`.

#### Method prototype

```go
func (s *CIService) PutWebpageAuditingJob(ctx context.Context, opt *PutWebpageAuditingJobOptions) (*PutWebpageAuditingJobResult, *Response, error)
```

#### Sample request

```go
// Replace `examplebucket-1250000000` and `COS_REGION` with the actual information
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
opt := &cos.PutWebpageAuditingJobOptions{
	InputUrl: "http://www.test.com",
	Conf: &cos.WebpageAuditingJobConf{
		DetectType: "Porn,Ads",
	},
}
res, _, err := c.CI.PutWebpageAuditingJob(context.Background(), opt)
```

#### Parameter description

```go
type PutWebpageAuditingJobOptions struct {
	InputUrl      string
	InputDataId   string
	InputUserInfo *UserExtraInfo
	Conf          *WebpageAuditingJobConf
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
type WebpageAuditingJobConf struct {
	DetectType          string
	Callback            string
	ReturnHighlightHtml bool
}

```

| Parameter | Description | Type |
| ----------- | ------------------------------------------------------------ | ------ |
| InputUrl    | Full URL of the webpage, such as `http://www.test.com`.             | String |
| InputDataId | Webpage ID. This field will return the original content in the result, which can contain up to 512 bytes. | String |
| InputUserInfo | Business field. | Object |
| Conf        | Moderation rule configuration.                                                 | Struct |
| DetectType  | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String |
| Callback    | Callback address, which must start with `http://` or `https://`.              | String    |
| ReturnHighlightHtml | This parameter specifies whether to highlight the non-compliant text on the webpage and return the highlighted HTML link. Valid values: `true`, `false`. Default value: `false`. | Bool |

#### Response description

Calling the `PutWebpageAuditingJob` function will parse the XML content returned by the API into a `PutWebpageAuditingJobResult` structure. For specific response parameters, see [Submitting Webpage Moderation Job](https://intl.cloud.tencent.com/document/product/436/48282).

## Querying a Job

This API (`GetWebpageAuditingJob`) is used to query the result of the specified webpage moderation job by `JobId`.

#### Method prototype

```go
func (s *CIService) GetWebpageAuditingJob(ctx context.Context, jobid string) (*GetWebpageAuditingJobResult, *Response, error)
```

#### Sample request

```go
// Replace `examplebucket-1250000000` and `COS_REGION` with the actual information
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
jobId := "shce25f391a72e11eb99f********"
res, _, err := c.CI.GetWebpageAuditingJob(context.Background(), jobId)
```

#### Parameter description

| Parameter | Description | Type |
| -------- | -------- | ------ |
| jobId    | Job ID.   | String |

#### Response description

Calling the `GetWebpageAuditingJob` function will parse the XML content returned by the API into a `GetWebpageAuditingJobResult` structure. For specific response parameters, see [Querying Webpage Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48283).
