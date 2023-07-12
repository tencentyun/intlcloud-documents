

## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for video moderation.

| API | Description |
| :--------------- | :------------------ |
| [Submitting video moderation job](https://intl.cloud.tencent.com/document/product/436/48249) | Submits a video moderation job.   |
| [Querying video moderation job result](https://intl.cloud.tencent.com/document/product/436/48250)  | Queries the result of a specified video moderation job. |


## Creating a Job

This API (`PutVideoAuditingJob`) is used to submit a video moderation job. You can receive the moderation result by setting the callback address or querying by `JobId`.

#### Method prototype

```go
func (s *CIService) PutVideoAuditingJob(ctx context.Context, opt *PutVideoAuditingJobOptions) (*PutVideoAuditingJobResult, *Response, error)
```

#### Sample request

```go
// Replace examplebucket-1250000000 and COS_REGION with the actual information.
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
opt := &cos.PutVideoAuditingJobOptions{
	InputObject: "demo.mp4",
	Conf: &cos.VideoAuditingJobConf{
		DetectType: "Porn,Ads",
		Snapshot: &cos.PutVideoAuditingJobSnapshot{
			Mode:         "Interval",
			TimeInterval: 50.5,
			Count:        100,
		},
	},
}
res, _, err := c.CI.PutVideoAuditingJob(context.Background(), opt)
```

#### Parameter description

```go
type PutVideoAuditingJobOptions struct {
    InputObject   string
    InputUrl      string
    InputDataId   string
    InputUserInfo *UserExtraInfo
    Conf          *VideoAuditingJobConf
    Type          string
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
type VideoAuditingJobConf struct {
    DetectType      string
    Snapshot        *PutVideoAuditingJobSnapshot
    Callback        string
	CallbackVersion string
    CallbackType    int
	BizType         string
	DetectContent   int
}
type PutVideoAuditingJobSnapshot struct {
    Mode         string
    Count        int
    TimeInterval float32
}
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| InputObject | Name of the video file in the COS bucket; for example, if the file is `video.mp4` in the `test` directory, then the filename is `test/video.mp4`. Either `Object` or `Url` can be selected at a time. | String |
| InputUrl    | Full URL of the video file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/test.mp4`. Either `Object` or `Url` can be selected at a time. | String |
| InputDataId | Video ID. This field will return the original content in the result, which can contain up to 512 bytes. | String |
| InputUserInfo | Business field. | Object |
| Type         | Moderation job type, which is fixed at `live_video` for live stream moderation. | String |
| Conf        | Moderation rule configuration.                                                 | Struct |
| BizType     | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console as instructed in [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). | String |
| DetectType  | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String |
| Snapshot     | Video image moderation is implemented by taking a certain number of screenshots based on the video frame capturing capability and then moderating the screenshots one by one. This parameter is used to specify the configuration of video frame capturing. | Struct |
| Callback    | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String |
| CallbackVersion | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | String |
| CallbackType | Callback segment type. Valid values: `1` (calls back all captured frames and audio segments); `2` (calls back only non-compliant captured frames and audio segments). Default value: `1`. | Integer |
| DetectContent | Whether to moderate video sound. Valid values: `0` (moderates the video image only), `1` (moderates both the video image and video sound). Default value: `0`. | Integer |
| Mode         | Frame capturing mode. Valid values: `Interval` (interval mode), `Average` (average mode), `Fps` (fixed frame rate mode). Default value: `Interval`. `Interval` mode: The `TimeInterval` and `Count` parameters take effect. If `Count` is set but `TimeInterval` is not, all frames will be captured to generate a total of `Count` images. `Average` mode: The `Count` parameter takes effect, indicating to capture a total of `Count` images at an average interval in the entire video. `Fps` mode: `TimeInterval` indicates how many frames to capture per second. If `TimeInterval` is not set, all frames will be captured to generate a total of `Count` images. | String |
| Count        | The number of captured frames. Value range: (0, 10000].                                | Integer |
| TimeInterval | Video frame capturing frequency. Value range: (0.000, 60.000] seconds. The value supports the float format, accurate to the millisecond. | Float  |

#### Response description

Calling the `PutVideoAuditingJob` function will parse the XML content returned by the API into the `PutVideoAuditingJobResult` structure. For specific response parameters, see [Submitting Video Moderation Job](https://intl.cloud.tencent.com/document/product/436/48249).


## Querying a Job

This API (`GetVideoAuditingJob`) is used to query the result of the specified video moderation job by `JobId`.

#### Method prototype

```go
func (s *CIService) GetVideoAuditingJob(ctx context.Context, jobid string) (*GetVideoAuditingJobResult, *Response, error)
```

#### Sample request

```go
// Replace examplebucket-1250000000 and COS_REGION with the actual information.
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
jobId := "avce25f391a72e11eb99f********"
res, _, err := c.CI.GetVideoAuditingJob(context.Background(), jobId)
```

#### Parameter description

| Parameter | Description | Type |
| -------- | -------- | ------ |
| jobId    | Job ID   | String |

#### Response description

Calling the `GetVideoAuditingJob` function will parse the XML content returned by the API into the `GetVideoAuditingJobResult` structure. For specific response parameters, see [Querying Video Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48250).
