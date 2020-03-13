Watermarking is an offline task that adds an image or text at the specified position of the video during video transcoding or screencapturing. VOD supports the following types of watermarks:
- Static image watermark: this refers to an image watermark in PNG format. It can be a copyright owner's or TV station's logo and is generally used to indicate the video copyright ownership.
- Animated image watermark: this refers to an image watermark in APNG format, which can be animated.
- Text watermark: this refers to a multi-lingual text watermark. It can be a user's nickname and is generally used to identify the producer of UGSV content.

VOD can add multiple watermarks to a video or screenshot. The size and position can be customized individually.

## <span id = "sy"></span>Watermarking Template

The target specification of a watermark is subject to parameters such as watermark type, width, height, and position, which can be customized in the form of VOD watermarking template as shown below:

| Parameter                     | Description                                                         |
| ------------------------ | ------------------------------------------------------------ |
| Type  | Image and text watermarks are supported: <li>Image watermark: Static or animated images are supported. </li><li>Text watermark: Texts in various languages are supported.</li> |
| Position     | Relative position of a watermark in the video.                                 |
| ImageSize    | Size of a watermark in the video.                                |
| ImageContent | Binary content of a watermark.                                 |
| FontSize     | Font size of a text watermark. |
| FontType     | Font of a text watermark, e.g., Times New Roman. |
| FontColor    | Color of a text watermark, e.g., 0xRRGGBB.   |
| FontAlpha  | Transparency of text watermark. Value range: 0–100%. |

You can use the console (for detailed directions, please see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059#.E6.B0.B4.E5.8D.B0.E6.A8.A1.E6.9D.BF)) or call a [server API](#APIhttps://intl.cloud.tencent.com/document/product/266/33772) to create and manage custom watermarking templates.

## Task Initiation

There are three ways to initiate a transcoding task with watermark, namely, directly initiating through server API, directly initiating through the console, and specifying a task upon upload. For more information, please see [Task Initiation](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask) for video processing.

Below are instructions for initiating transcoding tasks with watermark in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: specify the [watermarking template](#sy) ID in the `MediaProcessTask.TranscodeTaskSet` parameter in the request.
* Initiate a task on a video through the console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the watermark specification in the task flow, and use the task flow to [initiate video processing](https://intl.cloud.tencent.com/document/product/266/33890).
* Specify a task upon upload from server: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target watermark specification in the task flow, and specify this task flow as the `procedure` in the [ApplyUpload](#APIhttps://intl.cloud.tencent.com/document/api/266/31767#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) request.
* Specify a task upon upload from client: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target watermark specification in the task flow, and specify this task flow as the `procedure` parameter in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0).
* Upload through console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target watermark specification in the task flow, upload a video through the console, select [Process Video During Upload](https://intl.cloud.tencent.com/document/product/266/33890), and specify to execute this task flow upon video upload completion.

## Getting Result

After initiating a transcoding task with watermark, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the transcoding task with watermark is initiated (the fields with null value are omitted):

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
                "Type":"Transcode",
                "TranscodeTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":220,
                        "WatermarkSet": [
                            {
                                "Definition": 23120
                            }
                        ]
                    },
                    "Output":{
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/v.f20.m3u8",
                        "Size":63120997,
                        "Container":"mov,mp4,m4a,3gp,3g2,mj2",
                        "Height":1086,
                        "Width":1920,
                        "Bitrate":513402,
                        "Md5":"084d403c73930ca2f835679af1f37bd3",
                        "Duration":60,
                        "VideoStreamSet":[
                            {
                                "Bitrate":473101,
                                "Codec":"h264",
                                "Fps":24,
                                "Height":480,
                                "Width":640
                            }
                        ],
                        "AudioStreamSet":[
                            {
                                "Bitrate":48581,
                                "Codec":"aac",
                                "SamplingRate":44100
                            }
                        ],
                        "Definition":220
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

In the callback result, `ProcedureStateChangeEvent.MediaProcessResultSet` contains the transcoding result in `Type` of `Transcode`: the transcoding specification `Definition` is 220, and a watermark is added during transcoding, whose specification `Definition` is 23120.
