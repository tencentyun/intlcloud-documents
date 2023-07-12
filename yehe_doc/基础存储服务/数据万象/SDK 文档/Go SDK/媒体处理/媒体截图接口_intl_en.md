## Overview

This document provides an overview of APIs and SDK code samples for media screenshot.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|   [GetSnapshot](https://intl.cloud.tencent.com/document/product/436/46912)     |  Querying screenshot	 |   Query the screenshot of media file at some time point     |


## Querying Screenshot

#### Feature description

This API is used to query the screenshot of a media file at some time point.

>! The COS Go SDK version must be at least v0.7.32.

#### Method prototype

```go
func (s *CIService) GetSnapshot(ctx context.Context, name string, opt *GetSnapshotOptions, id ...string) (*Response, error)
```

#### Sample request
```go
opt := &cos.GetSnapshotOptions{
	Time: 1,
} 
resp, err := c.CI.GetSnapshot(context.Background(), "test.mp4", opt)
if err != nil {
    // ERROR
}
  
fd, err := os.OpenFile("test.jpg", os.O_WRONLY|os.O_CREATE|os.O_TRUNC, 0660)
if err != nil {
    // ERROR
} 
_, err = io.Copy(fd, resp.Body)
fd.Close()
```

#### Parameter description

```go
type GetSnapshotOptions struct {
    Time   float32 
    Height int 
    Width  int  
    Format string
    Rotate string
    Mode   string
}
```

| Parameter | Description | Required | Type |
| ------- | ----------------------------------------------------------- | ------- | ----- |
| name | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | Yes | name |
| opt      | Screenshot parameter.       | No       | struct |
| id        | Object `VersionId` for versioning. | No | String  |
| Time   | Screenshot time point in seconds.        | Yes       | float  |
| Width | Screenshot width. Default value: 0.         | No       | Int    |
| Height | Screenshot height. Default value: 0. If `width` and `height` are both `0`, the width and height of the video are used. If one of them is `0`, the other value is used to automatically adapt to the aspect ratio of the video. | No       | Int    |
| Format | Screenshot format. Valid values: jpg, png. Default value: jpg. | No | String |
| Rotate | Image rotation method. auto: Rotate automatically according to the video rotation information. off: Do not rotate. Default value: auto. | No | String |
| Mode | Frame capturing method. keyframe: Capture the last keyframe before the specified time point. exactframe: Capture the frame at a specified time point. Default value: exactframe. | No | String |

#### Response description

| Parameter | Description | Required | Type |
| ------- | ----------------------------------------------------------- | ------- | ----- |
| Response     | HTTP response.  | Yes       | Struct  |
| Response.Header     | HTTP response header.  | Yes       | Struct  |
| Response.Body     | HTTP response body.  | Yes       | Struct  |
