Screencapturing is an offline task that captures a screenshot of a video at a certain point in time. VOD provides the following types of screenshots:
- Time point screenshot: VOD can capture screenshots of a video at the specified set of time points.
- Sampled screenshot: VOD can capture a set of screenshots of a video at the specified time interval.
- Cover screenshot: VOD can capture a screenshot of a video at the specified time point and use its URL as the video cover in the media asset management system.
- Image sprite: VOD can capture a set of screenshots of a video (subimages) at the specified time interval and splice them together to generate a large image (i.e., image sprite).

The screencapturing feature can meet your needs in the following application scenarios:
- Video cover generation: a screenshot of a video can be used as its cover.
- Thumbnail: an image sprite is a large image composed of multiple subimages (i.e., thumbnails), which is usually used to represent a video overview.
- Playback preview: together with a VTT file, an image sprite can be used to achieve preview effect on the player progress bar.

## <span id = "jt"></span>Screencapturing Template

The target specification of a screenshot is subject to parameters such as screenshot file format, width, and height, which can be customized in the form of VOD screencapturing template as shown below:

### Time point screencapturing template

A time point screencapturing template is used to take a screenshot at a specified time point or take a screenshot as a cover.

| Parameter             | Description       |
| -------------------- | ------------------------------------------------------------ |
| Format       | Output format of a screenshot file. Currently, only JPG is supported.                         |
| Width        | Screenshot width. Value range: 128–4,096 px.                             |
| Height     | Screenshot height. Value range: 128–4,096 px.                             |
| FillType | Filling refers to the way of processing a screenshot when its aspect ratio is different from that of the source video. Generally, the following filling types are supported: <li>Stretch: the screenshot is stretched to match the aspect ratio of the source video, which may make the screenshot "shorter" or "longer". </li><li>Fill with black: this option retains the aspect ratio of the source video for the screenshot and fill the unmatched area with black color blocks. </li><li>Fill with white: this option retains the aspect ratio of the source video for the screenshot and fill the unmatched area with white color blocks. </li><li>Gaussian blur: this option retains the aspect ratio of the source video for the screenshot and fills the unmatched area with Gaussian blur. </li> |

For common specifications, VOD provides a [preset time point screencapturing template](https://intl.cloud.tencent.com/document/product/266/33932#screenshot01). In addition, you can also create and manage custom screencapturing templates in the console. For detailed directions, please see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059#.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF).

### Sampled screencapturing template

A sampled screencapturing template is used to take sampled screenshots.

| Parameter                     | Description                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Format       | Output format of a screenshot file. Currently, only JPG is supported.                         |
| Width        | Screenshot width. Value range: 128–4,096 px.                             |
| Height     | Screenshot height. Value range: 128–4,096 px.                             |
| SampleType | The following two types are supported: <li>Sample by percent: if this type is selected and `Interval` is set to `5%` for example, 20 screenshots will be generated. </li><li>Sample by time: if this type is selected and `Interval` is set to `10s` for example, the number of generated screenshots will depend on the video length. </li> |
| Interval   | Sampling interval. <li>If the sampling type is by percent, this parameter will be a percent value. </li><li>If the sampling type is by time, this parameter will be a second value. </li> |
| FillType | Filling refers to the way of processing a screenshot when its aspect ratio is different from that of the source video. Generally, the following filling types are supported: <li>Stretch: the screenshot is stretched to match the aspect ratio of the source video, which may make the screenshot "shorter" or "longer". </li><li>Fill with black: this option retains the aspect ratio of the source video for the screenshot and fill the unmatched area with black color blocks. </li><li>Fill with white: this option retains the aspect ratio of the source video for the screenshot and fill the unmatched area with white color blocks. </li><li>Gaussian blur: this option retains the aspect ratio of the source video for the screenshot and fills the unmatched area with Gaussian blur. </li> |

For common specifications, VOD provides a [preset sample screencapturing template](https://intl.cloud.tencent.com/document/product/266/33932#screenshot02). In addition, you can also create and manage custom screencapturing templates in the console. For detailed directions, please see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059#.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF).

### Image sprite generating template

An image sprite generating template is used to take screenshots and combine them to generate an image sprite.

| Parameter                     | Description                                                         |
| ---------------------- | ------------------------------------------ |
| Format       | Output format of an image sprite file. Currently, only JPG is supported.                         |
| Width      | Subimage width of an image sprite.                       |
| Height   | Subimage height of an image sprite.                       |
| Rows       | Number of rows of subimages in an image sprite.                  |
| Columns    | Number of columns of subimages in an image sprite.                   |
| SampleType | Sampling type of subimages. Currently, only sampling by time is supported. |
| Interval   | Time interval for capturing a screenshot as a subimage.     |

>
>- The value of `Width` * `Columns` should be between 128 and 4,096 px (i.e., the range of the image sprite width).
>- The value of `Height` * `Rows` should be between 128 and 4,096 px (i.e., the range of the image sprite height).

For common specifications, VOD provides a [preset image sprite generating template](https://intl.cloud.tencent.com/document/product/266/33932#screenshot03). In addition, you can also create and manage custom screencapturing templates in the console. For detailed directions, please see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059#.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF).

## Task Initiation

There are three ways to initiate a screencapturing task, namely, directly initiating through server API, directly initiating through the console, and specifying a task upon upload. For more information, please see [Task Initiation](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask) for video processing.

Below are instructions for initiating screencapturing tasks in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: specify the [screencapturing template](#jt) ID in the `MediaProcessTask.SnapshotByTimeOffsetTaskSet` parameter in the request.
* Initiate a task on a video through the console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target screenshot specification in the task flow, and use the task flow to [initiate video processing](https://intl.cloud.tencent.com/document/product/266/33890).
* Specify a task upon upload from server: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target screenshot specification in the task flow, and specify this task flow as the `procedure` in the [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) request.
* Specify a task upon upload from client: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target screenshot specification in the task flow, and specify this task flow as the `procedure` parameter in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0).
* Upload through console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target screenshot specification in the task flow, upload a video through the console, select [Process Video During Upload](https://intl.cloud.tencent.com/document/product/266/33890#.E6.9C.AC.E5.9C.B0.E4.B8.8A.E4.BC.A0.E6.AD.A5.E9.AA.A4), and specify to execute this task flow upon video upload completion.

## Getting Result

After initiating a screencapturing task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the screencapturing task is initiated (the fields with null value are omitted):

```json
{
    "EventType":"ProcedureStateChanged",
    "ProcedureStateChangeEvent":{
        "TaskId":"1256768367-Procedure-2e1af2456351812be963e309cc133403t0",
        "Status":"FINISH",
        "FileId":"5285890784246869930",
        "FileName":"Animal World",
        "FileUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/AtUCmy6gmIYA.mp4",
        "MetaData":{
            "AudioDuration":60,
            "AudioStreamSet":[
                {
                    "Bitrate":383854,
                    "Codec":"aac",
                    "SamplingRate":48000
                }
            ],
            "Bitrate":1021028,
            "Container":"mov,mp4,m4a,3gp,3g2,mj2",
            "Duration":60,
            "Height":480,
            "Rotate":0,
            "Size":7700180,
            "VideoDuration":60,
            "VideoStreamSet":[
                {
                    "Bitrate":637174,
                    "Codec":"h264",
                    "Fps":23,
                    "Height":480,
                    "Width":640
                }
            ],
            "Width":640
        },
        "MediaProcessResultSet":[
            {
                "Type":"SnapshotByTimeOffset",
                "SnapshotByTimeOffsetTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10,
                        "Definition":[3, 6, 9]
                    },
                    "Output":{
                        "Definition":10,
                        "PicInfoSet": [
                            {
                                "TimeOffset":3,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg"
                            },
                            {
                                "TimeOffset":6,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx2.jpg"
                            },
                            {
                                "TimeOffset":9,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx3.jpg"
                            }
                        ]
                    }
                }
            },
            {
                "Type":"SampleSnapshot",
                "SampleSnapshotTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Definition":10,
                        "PicInfoSet": [
                            {
                                "TimeOffset":6,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg"
                            },
                            {
                                "TimeOffset":12,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx2.jpg"
                            },
                            {
                                "TimeOffset":18,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx3.jpg"
                            },
                            {
                                "TimeOffset":24,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx4.jpg"
                            },
                            {
                                "TimeOffset":30,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx5.jpg"
                            },
                            {
                                "TimeOffset":36,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx6.jpg"
                            },
                            {
                                "TimeOffset":42,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx7.jpg"
                            },
                            {
                                "TimeOffset":48,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx8.jpg"
                            },
                            {
                                "TimeOffset":54,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx9.jpg"
                            },
                            {
                                "TimeOffset":60,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx10.jpg"
                            }
                        ]
                    }
                }
            },
            {
                "Type":"ImageSprites",
                "ImageSpriteTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Definition":10,
                        "Height":80,
                        "Width":142,
                        "TotalCount":1,
                        "ImageUrlSet":[
                            "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg"
                        ],
                        "WebVttUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx.vtt"
                    }
                }
            },
            {
                "Type":"CoverBySnapshot",
                "CoverBySnapshotTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10,
                        "PositionType":"Time",
                        "PositionValue":0
                    },
                    "Output":{
                        "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx.jpg"
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

In the callback result, `ProcedureStateChangeEvent.MediaProcessResultSet` contains the result in `Type` of `SnapshotByTimeOffset`, `SampleSnapshot`, `ImageSprites`, and `CoverBySnapshot`, which represent time point screencapturing, sampled screencapturing, image sprite generating, and cover generating tasks, respectively.
