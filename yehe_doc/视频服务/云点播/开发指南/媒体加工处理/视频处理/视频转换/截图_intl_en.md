Screenshot taking is an offline task that takes screenshots of a video at specified times. VOD supports the following types of screenshots:
- Time point screenshot: Takes screenshots at specified time points.
- Sampled screenshot: Takes screenshots at regular intervals.
- Thumbnail: Takes a screenshot at a specified time point and uses it as the video’s thumbnail.
- Image sprite: Takes multiple screenshots at the specified interval and combines them into one image (image sprite).

Common use cases include the following:
- Video thumbnail generation: Take a screenshot of a video and use it as the video’s thumbnail.
- Image sprite generation: Generate an image sprite (a collection of small images), which is often used as the summary of a video.
- Preview: Use image sprites and VTT files to show previews above the progress bar.

## [](id:jt)Screenshot Templates

A screenshot template is a collection of screenshot parameters, including the output file format and image dimensions.

### Time point screenshot templates

You can use a time point screenshot template to take a screenshot at a specific time point or generate a thumbnail.

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| Format       | The screenshot format (only JPG is supported currently).                         |
| Width        | The screenshot width (px). Value range: 128-4096.                             |
| Height     | The screenshot height (px). Value range: 128-4096.                             |
| FillType | The fill mode (`FillType`) specifies how the source video is processed when its aspect ratio does not match the output aspect ratio. The following fill modes are supported: <li>Stretch: The source video is stretched to match the output aspect ratio. This may cause the video to appear distorted. </li><li>Fill with black: The original aspect ratio is retained, leaving black bars. </li><li>Fill with white: The original aspect ratio is retained, leaving white bars.</li><li>Gaussian blur: The original aspect ratio is retained, and Gaussian blur is applied to the blank spaces. </li> |

VOD provides [preset time point screenshot templates](https://intl.cloud.tencent.com/document/product/266/33932) for common parameter combinations. You can also create your own templates and manage them in the console. For details, see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059).

### Sampled screenshot templates

You can use a sampled screenshot template to take screenshots at regular intervals.

| Parameter                     | Description                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Format       | The screenshot format (only JPG is supported currently).                         |
| Width        | The screenshot width (px). Value range: 128-4096.                             |
| Height     | The screenshot height (px). Value range: 128-4096.                             |
| SampleType | How sampling intervals are measured. Sampling intervals can be measured in two ways: <li>By percent: Intervals are measured by percent. For example, if `Interval` is set to 5 (%), 20 screenshots will be generated for a video. </li><li>By time: Intervals are measured by time. For example, if `Interval` is set to 10 (sec), the number of screenshots generated will depend on the video length.</li> |
| Interval   | The sampling interval. <li>If the interval measurement (`SampleType`) is by percent, this parameter is a percent value. </li><li>If interval measurement is by time, this parameter is a time value (sec). </li> |
| FillType | The fill mode (`FillType`) specifies how the source video is processed when its aspect ratio does not match the output aspect ratio. The following fill modes are supported: <li>Stretch: The source video is stretched to match the output aspect ratio. This may cause the video to appear distorted. </li><li>Black-leaving: The original aspect ratio is retained, leaving black bars. </li><li>Blank-leaving: The original aspect ratio is retained, leaving blank spaces.</li><li>Gaussian blur: The original aspect ratio is retained, and Gaussian blur is applied to the blank spaces. </li> |

VOD provides [preset sampled screenshot templates](https://intl.cloud.tencent.com/document/product/266/33932) for common parameter combinations. You can also create your own templates and manage them in the console. For details, see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059).

### Image sprite screenshot templates

You can use an image sprite screenshot template to generate image sprites.

| Parameter                     | Description                                                         |
| ---------------------- | ------------------------------------------ |
| Format       | The format of the image sprite (only JPG is supported currently).                         |
| Width      | The width of the subimage in an image sprite.                       |
| Height     | The height of the subimage in an image sprite.                       |
| Rows       | The number of image rows in a sprite.                 |
| Columns    | The number of image columns in a sprite.                  |
| SampleType | How sampling intervals are measured. Currently, only sampling by time is supported. |
| Interval   | The time interval for image sampling.     |

>!
>- The result of multiplying `Width` x `Columns` (i.e., sprite width) should be within the range of 128-4096.
>- The result of multiplying `Height` x `Rows` (i.e., sprite height) should be in the range of 128-4096.

VOD provides [preset image sprite screenshot templates](https://intl.cloud.tencent.com/document/product/266/33932) for common parameter combinations. You can also create your own templates and manage them in the console. For details, see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059).

## Initiating a Screenshot Task

You can initiate a screenshot taking task by calling a server API, via the console, or by specifying the task when uploading videos. For details, see [Task Initiation](https://intl.cloud.tencent.com/document/product/266/33931).

Specifically, you can initiate a screenshot task by doing one of the following:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125), specifying the ID of the [screenshot template](#jt) in `MediaProcessTask.SnapshotByTimeOffsetTaskSet`.
* [Add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, specifying the screenshot parameters, and use the task flow to [process videos](https://intl.cloud.tencent.com/document/product/266/33892) in the console.
* [Add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, specifying the screenshot parameters. When uploading a video from the server, set the `procedure` parameter to the task flow you created.
* [Add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, specifying the screenshot parameters. When uploading a video from a client, set `procedure` in the [upload signature](https://intl.cloud.tencent.com/document/product/266/33922) to the task flow you created.
* [Add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, specifying the screenshot parameters. When uploading a video via the console, choose [Auto-processing after upload](https://intl.cloud.tencent.com/document/product/266/33890) and select the task flow you created.

## Getting the Result

After initiating a screenshot task, you can wait for the [result notification](https://intl.cloud.tencent.com/document/product/266/33931) asynchronously or perform a [task query](https://intl.cloud.tencent.com/document/product/266/33931) synchronously to get the task execution result. Below is an example of the notification received in normal callback mode after a screenshot task is initiated (the fields with null value are omitted):

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
                        "PicInfoSet":[
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
                        "SampleType": "Percent",
                        "Interval": 10,
                        "WaterMarkDefinition": [],
                        "ImageUrlSet":[
                                "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg",
                                "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx2.jpg",
                                "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx3.jpg",
                                "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx4.jpg",
                                "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx5.jpg",
                                "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx6.jpg",
                                "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx7.jpg",
                                "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx8.jpg",
                                "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx9.jpg"
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

In the above callback, `ProcedureStateChangeEvent.MediaProcessResultSet` contains four types of results, namely `SnapshotByTimeOffset`, `SampleSnapshot`, `ImageSprites`, and `CoverBySnapshot`, which represent a time point screenshot task, a sampled screenshot task, an image sprite screenshot task, and a thumbnail generation task respectively.