## Overview

This document provides an overview of APIs and SDK code samples for media information.

| API | Operation |  Description |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
|  [GetMediaInfo](https://intl.cloud.tencent.com/document/product/436/46915)    |   Querying file information | Queries media file information      |


## Querying File Information

#### Feature description

This API is used to query the information of a media file.

>! The COS Go SDK version must be at least v0.7.32.

#### Method prototype

```go
func (s *CIService) GetMediaInfo(ctx context.Context, name string, opt *ObjectGetOptions, id ...string) (*GetMediaInfoResult, *Response, error)
```

#### Sample request
```go
res, _, err := c.CI.GetMediaInfo(context.Background(), "test.mp4", nil)
if err != nil {
    // ERROR
}
fmt.Printf("res: %+v\n", res)
```

#### Parameter description

| Parameter | Description | Type | Required |
| :------- | :----------------------------------------------------------- | :----- | :------- |
| name | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | name | Yes |
| opt      | Common request headers and parameters. For more information, see [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436/43549). | struct | No       |
| id       | Object `VersionId` for versioning.                                | string | No       |

#### Response description

```go
type GetMediaInfoResult struct {
    XMLName   xml.Name
    MediaInfo struct {
        Format struct {
            Bitrate        float32
            Duration       float32
            FormatLongName string
            FormatName     string
            NumProgram     int
            NumStream      int
            Size           int
            StartTime      float32
        }
        Stream struct {
            Audio []struct {
                Index          int 
                CodecName      string
                CodecLongName  string
                CodecTimeBase  string
                CodecTagString string
                CodecTag       string
                SampleFmt      string
                SampleRate     int
                Channel        int
                ChannelLayout  string
                Timebase       string
                StartTime      float32
                Duration       float32
                Bitrate        float32
                Language       string
            }
            Subtitle struct {
                Index    int
                Language string
            }
            Video struct {
                Index          int
                CodecName      string
                CodecLongName  string
                CodecTimeBase  string
                CodecTagString string
                CodecTag       string
                Profile        string
                Height         int
                Width          int
                HasBFrame      int
                RefFrames      int
                Sar            string
                Dar            string
                PixFormat      string
                FieldOrder     string
                Level          int
                Fps            float32
                AvgFps         string
                Timebase       string
                StartTime      float32
                Duration       float32
                Bitrate        float32
                NumFrames      int
                Language       string
            }
        }
    }
}
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| MediaInfo | Response | Media details. |  Container |

`MediaInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------- | :------- | :-------- |
| Stream | Response.MediaInfo | Stream information. |  Container |
| Format | Response.MediaInfo | Format information. |  Container |

`Stream` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------- | :------- | :-------- |
| Video              | Response.MediaInfo. Stream | Video information. | Container |
| Audio              | Response.MediaInfo. Stream | Audio information. | Container |
| Subtitle           | Response.MediaInfo. Stream | Subtitles information. | Container |

`Format` has the following sub-nodes (certain nodes may not be returned during video information query):

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------- | :------------------------------------------ | :----- |
| NumStream          | Response.MediaInfo. Format | Number of streams (including videos, audios, and subtitles). | Int    |
| NumProgram         | Response.MediaInfo. Format | Number of programs.                                  | Int    |
| FormatName         | Response.MediaInfo. Format | Container format name.                                | String |
| FormatLongName     | Response. MediaInfo.Format | Detailed name of the container format.                          | String |
| StartTime          | Response.MediaInfo. Format | Start time in seconds.                          | Float  |
| Duration           | Response.MediaInfo. Format | Duration in seconds.                              | Float  |
| Bitrate            | Response.MediaInfo. Format | Bitrate in Kbps.                         | Int    |
| Size               | Response.MediaInfo. Format | Size in bytes.                           | Int    |

`Video` has the following sub-nodes (certain nodes may not be returned during video information query):

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------- | :-------------------------- | :----- |
| Index              | Response.MediaInfo. Stream.Video | Stream number.                  | Int    |
| CodecName          | Response.MediaInfo. Stream.Video | Codec format name.              | String |
| CodecLongName      | Response.MediaInfo. Stream.Video | Detailed name of the codec format.        | String |
| CodecTimeBase      | Response.MediaInfo. Stream.Video | Codec timebase.                    | String |
| CodecTagString     | Response.MediaInfo. Stream.Video | Codec tag name.                  | String |
| CodecTag           | Response.MediaInfo. Stream.Video | Codec tag.                    | String |
| Profile            | Response.MediaInfo. Stream.Video | Video codec profile.                | String |
| Height             | Response.MediaInfo. Stream.Video | Video height in px.             | Int    |
| Width              | Response.MediaInfo. Stream.Video | Video width in px.             | Int    |
| HasBFrame          | Response.MediaInfo. Stream.Video | Whether B-frames exist. 1: yes; 0: no. | Int    |
| RefFrames          | Response.MediaInfo. Stream.Video | Number of reference frames for video codec.         | Int    |
| Sar                | Response.MediaInfo. Stream.Video | Sample aspect ratio.                  | String |
| Dar                | Response.MediaInfo. Stream.Video | Display aspect ratio.                  | String |
| PixFormat          | Response.MediaInfo. Stream.Video | Pixel format.                    | String |
| FieldOrder         | Response.MediaInfo. Stream.Video | Field order.                    | String |
| Level              | Response.MediaInfo. Stream.Video | Video codec level.                | Int    |
| Fps                | Response.MediaInfo. Stream.Video | Video frame rate.                    | Int    |
| AvgFps             | Response.MediaInfo. Stream.Video | Average frame rate.                    | String |
| Timebase           | Response.MediaInfo. Stream.Video | Timebase.                         | String |
| StartTime          | Response.MediaInfo. Stream.Video | Video start time in seconds.      | Float  |
| Duration           | Response.MediaInfo. Stream.Video | Video duration in seconds.          | Float  |
| Bitrate            | Response.MediaInfo. Stream.Video | Bitrate in Kbps.         | Float  |
| NumFrames          | Response.MediaInfo. Stream.Video | Total number of frames.                      | Int    |
| Language           | Response.MediaInfo. Stream.Video | Language.                         | String |

`Audio` has the following sub-nodes (certain nodes may not be returned during video information query):

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------- | :------------------- | :----- |
| Index              | Response.MediaInfo. Stream.Audio | Stream number.           | Int    |
| CodecName          | Response.MediaInfo. Stream.Audio | Codec format name.       | String |
| CodecLongName      | Response.MediaInfo. Stream.Audio | Detailed name of the codec format. | String |
| CodecTimeBase      | Response.MediaInfo. Stream.Audio | Codec timebase.             | String |
| CodecTagString     | Response.MediaInfo. Stream.Audio | Codec tag name.           | String |
| CodecTag           | Response.MediaInfo. Stream.Audio | Codec tag.             | String |
| SampleFmt          | Response.MediaInfo. Stream.Audio | Sample format.             | String |
| SampleRate         | Response.MediaInfo. Stream.Audio | Sample rate.               | Int    |
| Channel            | Response.MediaInfo. Stream.Audio | Number of channels.             | Int    |
| ChannelLayout      | Response.MediaInfo. Stream.Audio | Channel layout.             | String |
| Timebase           | Response.MediaInfo. Stream.Audio | Timebase.                  | String |
| StartTime          | Response.MediaInfo. Stream.Audio | Audio start time in seconds. | Float  |
| Duration           | Response.MediaInfo. Stream.Audio | Audio duration in seconds.     | Float  |
| Bitrate            | Response.MediaInfo. Stream.Audio | Bitrate in Kbps.    | Float  |
| Language           | Response.MediaInfo. Stream.Audio | Language.                  | String |

`Subtitle` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------------- | :----------------------- | :----- |
| Index              | Response.MediaInfo. Stream.Subtitle | Stream number.               | Int    |
| Language           | Response.MediaInfo. Stream.Subtitle | Language. `und` indicates no query result. | String |
