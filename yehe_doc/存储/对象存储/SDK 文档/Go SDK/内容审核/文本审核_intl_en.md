
## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for text moderation.

| API | Description |
| :--------------- | :------------------ |
| [Submitting text moderation job](https://intl.cloud.tencent.com/document/product/436/48188)  | Submits text moderation job.   |
| [Querying text moderation job result](https://intl.cloud.tencent.com/document/product/436/48189)  | Queries the result of specified text moderation job. |

## Creating Job

This API (`PutTextAuditingJob`) is used to submit a text moderation job. If the text content is moderated, the response body will directly return the moderation result. If the text object is moderated, the job summary will be returned. You can receive the moderation result by setting the callback address or querying by `JobId`.

#### Method prototype

```go
func (s *CIService) PutTextAuditingJob(ctx context.Context, opt *PutTextAuditingJobOptions) (*PutTextAuditingJobResult, *Response, error)
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
opt := &cos.PutTextAuditingJobOptions{
    InputObject: "test.txt",
    Conf: &cos.TextAuditingJobConf{
        DetectType: "Porn,Ads",
    },
}
res, _, err := c.CI.PutTextAuditingJob(context.Background(), opt)
```

#### Parameter description

```go
type PutTextAuditingJobOptions struct {
    InputObject   string
    InputUrl      string
    InputContent  string
    InputDataId   string
    InputUserInfo *UserExtraInfo
    Conf          *TextAuditingJobConf
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
type TextAuditingJobConf struct {
    DetectType      string
    Callback        string
    CallbackVersion string
    BizType         string
}
```

| Parameter | Description | Type |
| ----------- | ------------------------------------------------------------ | ------ |
| InputObject  | Name of the text file stored in the current COS bucket; for example, if the file is `test.txt` in the `test` directory, then the filename is `test/test.txt`. Only text files in UTF-8 and GBK encodings are supported, and the file size cannot exceed 1 MB. Only one parameter among `Object`, `Url`, and `Content` can be selected at a time. | String |
| InputContent | When the input content is plain text, it needs to be Base64-encoded first. The length of the original text before encoding cannot exceed 10,000 UTF-8 characters. If the length limit is exceeded, the API will report an error. Only one parameter among `Object`, `Url`, and `Content` can be selected at a time. | String |
| InputUrl    | Full URL of the text file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/test.txt`. Only one parameter among `Object`, `Url`, and `Content` can be selected at a time. | String |
| InputDataId | Text ID. This field will return the original content in the result, which can contain up to 512 bytes. | String |
| InputUserInfo | Business field. | Object |
| Conf        | Moderation rule configuration.                                                 | Struct |
| BizType     | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console as instructed in [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). | String |
| DetectType  | The scene to be moderated. Valid values: `Porn` (pornography), `Ads` (advertising), `Illegal` (law violation), and `Abuse` (abuse). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String |
| Callback     | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`. If `Input` is `Content`, this parameter will not take effect, and the result will be returned directly. | String |
| CallbackVersion | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | String |

#### Response description

Calling the `PutTextAuditingJob` function will parse the XML content returned by the API into the `PutTextAuditingJobResult` structure. For specific response parameters, see [Submitting Text Moderation Job](https://intl.cloud.tencent.com/document/product/436/48188).


## Querying Job

This API (`GetTextAuditingJob`) is used to query the result of the specified text moderation job by `JobId`.

#### Method prototype

```go
func (s *CIService) GetTextAuditingJob(ctx context.Context, jobid string) (*GetTextAuditingJobResult, *Response, error)
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
jobId := "stce25f391a72e11eb99f********"
res, _, err := c.CI.GetTextAuditingJob(context.Background(), jobId)
```

#### Parameter description

| Parameter | Description | Type |
| -------- | -------- | ------ |
| jobId    | Job ID.   | String |

#### Response description

Calling the `GetTextAuditingJob` function will parse the XML content returned by the API into the `GetTextAuditingJobResult` structure. For specific response parameters, see [Querying Text Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48189).
