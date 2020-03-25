Animated image generating is an offline task that converts a video to an animated image such as in GIF or WEBP format. An animated image is a seamless cycle of continuous frames, which can deliver an animation effect with a small file size.

<span id = "zdt"></span>
## Animated Image Generating Template


The target specification of an animated image is subject to parameters such as animated image file format, width, height, and frame rate, which can be customized in the form of VOD animated image generating template as shown below:

| Parameter                     | Description                                                         |
| ---------------- | -------------------------------------------- |
| Format   | Output format of an animated image file. Currently, only GIF and WEBP are supported. |
| Width        | Animated image width. Value range: 128–4,096 px.                             |
| Height     | Animated image height. Value range: 128–4,096 px.                             |
| FPS      | Supported frame rate range: 1–60 fps.                  |

For common specifications, VOD provides a [preset animated image generating template](https://intl.cloud.tencent.com/document/product/266/33932#cinemagraph). In addition, you can also create and manage custom animated image generating templates in the console. For detailed directions, please see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059#.E8.BD.AC.E5.8A.A8.E5.9B.BE.E6.A8.A1.E6.9D.BF).

## Task Initiation
There are three ways to initiate an animated image generating task, namely, directly initiating through server API, directly initiating through the console, and specifying a task upon upload. For more information, please see [Task Initiation](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask) for video processing.

Below are instructions for initiating animated image generating tasks in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: specify the [animated image generating template](#zdt) ID in the `MediaProcessTask.AnimatedGraphicTaskSet` parameter in the request.
* Initiate a task on a video through the console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target animated image specification in the task flow, and use the task flow to [initiate video processing](https://intl.cloud.tencent.com/document/product/266/33890).
* Specify a task upon upload from server: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target animated image specification in the task flow, and specify this task flow as the `procedure` in the [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) request.
* Specify a task upon upload from client: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target animated image specification in the task flow, and specify this task flow as the `procedure` parameter in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0).
* Upload through console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target animated image specification in the task flow, upload a video through the console, select **[Process Video During Upload](https://intl.cloud.tencent.com/document/product/266/33890)**, and specify to execute this task flow upon video upload completion.

## Getting Result

After initiating an animated image generating task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the animated image generating task is initiated (the fields with null value are omitted):

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
                "Type":"AnimatedGraphics",
                "AnimatedGraphicTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":20001,
                        "StartTimeOffset":2,
                        "StartTimeOffset":5
                    },
                    "Output":{
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/v.f20001.webp",
                        "Definition":20001,
                        "Container":"webp",
                        "Height":480,
                        "Width":640,
                        "Bitrate":324271,
                        "Size":121601,
                        "Md5":"084d403c73930ca2f835679af1f37bd3",
                        "StartTimeOffset":3,
                        "EndTimeOffset":5
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

In the callback result, `ProcedureStateChangeEvent.MediaProcessResultSet` contains the transcoding result in `Type` of `AnimatedGraphics`, and `Definition` is 20001.
