
## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for audio moderation.

| API | Description |
| :--------------- | :------------------ |
| [Submitting audio moderation job](https://intl.cloud.tencent.com/document/product/436/48262) | Submits audio moderation job.   |
| [Querying audio moderation job result](https://intl.cloud.tencent.com/document/product/436/48263)  | Queries the result of specified audio moderation job. |

## Creating Job

This API (`PutAudioAuditingJob`) is used to submit an audio moderation job. You can receive the moderation result by setting the callback address or querying by `JobId`.

#### Method prototype

```go
func (s *CIService) PutAudioAuditingJob(ctx context.Context, opt *PutAudioAuditingJobOptions) (*PutAudioAuditingJobResult, *Response, error)
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
opt := &cos.PutAudioAuditingJobOptions{
	InputObject: "test.mp3",
	Conf: &cos.AudioAuditingJobConf{
		DetectType: "Porn,Ads",
	},
}
res, _, err := c.CI.PutAudioAuditingJob(context.Background(), opt)
```

#### Parameter description

```go
type PutAudioAuditingJobOptions struct {
    InputObject   string
    InputUrl      string
    InputDataId   string
    InputUserInfo *UserExtraInfo
    Conf          *AudioAuditingJobConf
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
type AudioAuditingJobConf struct {
    DetectType      string
    Callback        string
	CallbackVersion string
	BizType         string
}
```

| Parameter | Description | Type |
| ----------- | ------------------------------------------------------------ | ------ |
| InputObject | Name of the audio file stored in the COS bucket; for example, if the file is `audio.mp3` in the `test` directory, then the filename is `test/audio.mp3`. Either `Object` or `Url` can be selected at a time. | String |
| InputUrl    | Full URL of the audio file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/audio.mp3`. Either `Object` or `Url` can be selected at a time. | String |
| InputDataId | Audio ID. This field will return the original content in the result, which can contain up to 512 bytes. | String |
| InputUserInfo | Business field. | Object |
| Conf        | Moderation rule configuration.                                                 | Struct |
| BizType     | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console as instructed in [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). | String |
| DetectType  | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String |
| Callback    | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String |
| CallbackVersion | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | String |

#### Response description

Calling the `PutAudioAuditingJob` function will parse the XML content returned by the API into the `PutAudioAuditingJobResult` structure. For specific response parameters, see [Submitting Audio Moderation Job](https://intl.cloud.tencent.com/document/product/436/48262).

## Querying Job

This API (`GetAudioAuditingJob`) is used to query the result of the specified audio moderation job by `JobId`.

#### Method prototype

```go
func (s *CIService) GetAudioAuditingJob(ctx context.Context, jobid string) (*GetAudioAuditingJobResult, *Response, error)
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
jobId := "sace25f391a72e11eb99f********"
res, _, err := c.CI.GetAudioAuditingJob(context.Background(), jobId)
```

#### Parameter description

| Parameter | Description | Type |
| -------- | -------- | ------ |
| jobId    | Job ID.   | String |

#### Response description

Calling the `GetAudioAuditingJob` function will parse the XML content returned by the API into the `GetAudioAuditingJobResult` structure. For specific response parameters, see [Querying Audio Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48263).
