## Overview
This document describes how to use the content moderation feature provided by [Cloud Infinite (CI)](https://www.tencentcloud.com/document/product/1045). CI fully integrates the processing capabilities with the COS SDK.

>?To use the content moderation service, you need to have the permission to use CI:
- For root accounts, click [here](https://console.cloud.tencent.com/cam/role/grant?roleName=CI_QCSRole&policyName=QcloudCOSDataFullControl,QcloudAccessForCIRole,QcloudPartAccessForCIRole&principal=eyJzZXJ2aWNlIjoiY2kucWNsb3VkLmNvbSJ9&serviceType=%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fci) for role authorization.
- For sub-accounts, see [Authorizing Sub-Accounts to Access CI Services](https://intl.cloud.tencent.com/document/product/1045/33450).

This document provides an overview of APIs and SDK code samples for image moderation.

| API | Description |
| :--------------- | :------------------ |
| [Moderating single image](https://intl.cloud.tencent.com/document/product/436/48537) | Leverages CI's content moderation API to scan existing data stored in COS for porn, illegal, and advertising images. |
| [Batch moderating images](https://intl.cloud.tencent.com/document/product/436/48538) | Leverages CI's content moderation API to scan existing data stored in COS for porn, illegal, and advertising images. |
| [Querying image moderation job result](https://intl.cloud.tencent.com/document/product/436/48539) | Queries the details of a specified image moderation job. |

### Single image moderation

#### Feature description

The existing data scan feature of image moderation leverages CI's persistent processing API to scan existing data stored in COS for porn, illegal, and advertising images. Image moderation requests are `GET` requests.

#### Method prototype
```go
// Basic operations
func (s *CIService) ImageRecognition(ctx context.Context, name string, DetectType string) (*ImageRecognitionResult, *Response, error)
// You can specify more parameters.
func (s *CIService) ImageAuditing(ctx context.Context, name string, opt *ImageRecognitionOptions) (*ImageRecognitionResult, *Response, error)
```

#### Sample request

```go
DetectType := "porn,ads"
name := "test.jpg"
res, _, err := c.CI.ImageRecognition(context.Background(), name, DetectType)


opt := &cos.ImageRecognitionOptions{
	CIProcess: "sensitive-content-recognition",
    DetectType: "porn,ads",
    DetectUrl:   "http://www.example.com/test.jpg",
    BizType:     "ce25f391a72e11eb99f********",
}
res, _, err := c.CI.ImageAuditing(context.Background(), "", opt)
```

#### Parameter description
```go
type ImageRecognitionOptions struct {
	CIProcess        string
	DetectType       string
	DetectUrl        string
	Interval         int
	MaxFrames        int
	BizType          string
	LargeImageDetect int
	DataId           string
	Async            int
	Callback         string
}
```

| Parameter | Description | Type | Required |
| :---------- | ----- | ---- | ------------------------------------------------------------ |
| name       | Name of the image file in the COS bucket. The COS bucket is specified by `Host`. For example, if the file is `img.jpg` in the `test` directory in the `examplebucket-1250000000` bucket in Beijing, then `Host` is `examplebucket-1250000000.cos.ap-beijing.myqcloud.com`, and `ObjectKey` is `test/img.jpg`. If the `ImageAuditing` API is used to moderate an image URL, pass in an empty string. | String | Yes |
| CIProcess | This field identifies the data processing feature, which is `sensitive-content-recognition` for content moderation. | String | Yes |
| BizType    | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console. For more information, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). | String | No |
| DetectType  | Moderation type, such as `porn` (pornography) and `ads` (advertising). You can select multiple types; for example, `detect-type=porn,ads` indicates to moderate the image for porn and advertising information. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| DetectUrl  | You can enter a `detect-url` value to moderate an image accessible over the public network. If `detect-url` is not specified, the backend will moderate by `ObjectKey` by default. If `detect-url` is specified, the backend will moderate by `detect-url`, and there will be no need to enter `ObjectKey`. Sample `detect-url`: `http://www.example.com/abc.jpg`. | String | No       |
| Interval   | For GIF image moderation, you can use this parameter to configure the frame capturing interval. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included). | Integer | No |
| MaxFrames  | The maximum number of frames to be captured for GIF image moderation, which must be greater than 0. The default value is `5`, indicating to capture five frames at most. | Integer | No |
| LargeImageDetect | Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`. Note: Images up to 32 MB in size can be compressed, and image compression fees will be charged. For large animated images such as GIF, the compression time is long, which may cause the moderation to fail due to timeout. | Integer | No |
| DataId     | Image ID. This field will return the original content in the result, which can contain up to 512 bytes. | String | No |
| Async      | Whether to moderate asynchronously. Valid values: `0` (returns the result synchronously); `1` (moderates asynchronously). Default value: `0`.  | String    | No       |
| Callback | The moderation result (in `Detail` mode) can be sent to your callback address in the form of a callback. This parameter takes effect for async moderation. Addresses starting with `http://` or `https://` are supported, such as  `http://www.callback.com`.  | String | No |

#### Response description

Calling the `ImageRecognition` or `ImageAuditing` function will parse the XML content returned by the API into the `ImageRecognitionResult` structure. For specific response parameters, see [Single Image Moderation](https://intl.cloud.tencent.com/document/product/436/48537).

### Batch image moderation

#### Feature description

The batch image moderation API adopts a sync POST request method. You can use this API to perform content moderation on multiple image files.

#### Method prototype
```go
// Batch image moderation
func (s *CIService) BatchImageAuditing(ctx context.Context, opt *BatchImageAuditingOptions) (*BatchImageAuditingJobResult, *Response, error)
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
        },
})
opt := &cos.BatchImageAuditingOptions{
	Input: []cos.ImageAuditingInputOptions{
		cos.ImageAuditingInputOptions{
				DataId: "1",
				Object: "test.jpg",
		},
		cos.ImageAuditingInputOptions{
				DataId: "2",
				Url: "http://www.example.com/test.jpg",
		},
	},
	Conf: &cos.ImageAuditingJobConf{
		DetectType: "Porn,Ads",
	},
}
res, _, err := c.CI.BatchImageAuditing(context.Background(), opt)
```

#### Parameter description
```go
type ImageAuditingInputOptions struct {
	DataId           string
	Object           string
	Url              string
	Interval         int
	MaxFrames        int
	LargeImageDetect int
	UserInfo         *UserExtraInfo
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
type ImageAuditingJobConf struct {
	DetectType string
	BizType    string
	Async      int
	Callback   string
}
type BatchImageAuditingOptions struct {
	Input   []ImageAuditingInputOptions
	Conf    *ImageAuditingJobConf
}

```

| Parameter | Description | Type | Required |
| :---------- | ----- | ---- | ------------------------------------------------------------ |
| DataId     | Image ID. This field will return the original content in the result, which can contain up to 512 bytes. | String | No |
| Object     | Name of the image file stored in the COS bucket; for example, if the file is `image.jpg` in the `test` directory, then the filename is `test/image.jpg`. Either `Object` or `Url` can be selected at a time. | String | No |
| Url        | Full URL of the image file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/image.jpg`. Either `Object` or `Url` can be selected at a time. | String | No |
| Interval   | Frame capturing frequency, which takes effect for GIF images only. The default value is `5`, indicating to capture a frame every five frames starting from the first frame (included). | Integer | No |
| MaxFrames  | The maximum number of frames to be captured, which takes effect for GIF images only. The default value is `5`, indicating to capture only five frames of the GIF image for moderation. The parameter value must be greater than 0. | Integer | No |
| BizType    | Moderation policy. If this parameter is not specified, the default policy will be used. The policy can be configured in the console. For more information, see [Setting Moderation Policy](https://intl.cloud.tencent.com/document/product/436/52095). | String | No |
| DetectType  | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by comma, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| Async      | Whether to moderate asynchronously. Valid values: `0` (returns the result synchronously); `1` (moderates asynchronously). Default value: `0`.  | String    | No       |
| Callback | The moderation result (in `Detail` mode) can be sent to your callback address in the form of a callback. This parameter takes effect for async moderation. Addresses starting with `http://` or `https://` are supported, such as  `http://www.callback.com`.  | String | No |
| LargeImageDetect | Whether to compress the image that exceeds the size limit before moderation. Valid values: `0` (no), `1` (yes). Default value: `0`. Note: Images up to 32 MB in size can be compressed, and image compression fees will be charged. For large animated images such as GIF, the compression time is long, which may cause the moderation to fail due to timeout. | Integer | No |
| UserInfo   | Business field. | Object    | No       |

#### Response description

Calling the `BatchImageAuditing` function will parse the XML content returned by the API into the `BatchImageAuditingJobResult` structure. For specific response parameters, see [Batch Image Moderation](https://intl.cloud.tencent.com/document/product/436/48538).

### Querying image moderation job result

#### Feature description

This API is used to query the result of an image moderation job. The API request is a `GET` request.

#### Method prototype
```go
// Image moderation - job query
func (s *CIService) GetImageAuditingJob(ctx context.Context, jobid string) (*GetImageAuditingJobResult, *Response, error)
```

#### Sample request

```go
jobId := "iace25f391a72e11eb99f********"
res, _, err := c.CI.GetImageAuditingJob(context.Background(), jobId)
```

#### Parameter description

| Parameter | Description | Type |
| -------- | -------- | ------ |
| jobId    | Job ID   | String |

#### Response description

Calling the `GetImageAuditingJob` function will parse the XML content returned by the API into the `GetImageAuditingJobResult` structure. For specific response parameters, see [Querying Image Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48539).
