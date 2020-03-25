Video content analysis is an offline task that intelligently analyzes video content with the aid of AI. It intelligently gives suggestions on video categorization, tagging, and cover generating to help video platforms accurately and efficiently manage videos.

Video content analysis includes the following features:

| Feature Name | Description |
| -- | -- |
| Intelligent categorization | Gives suggestions on the category to which a video belongs. There are currently over ten categories, such as: <br/>news, entertainment, games, military, technology, food, sports, travel, animation, dance, music, television, and automobile. |
| Intelligent tagging | Gives suggestions on the tags that can be added to a video. There are currently over 3,000 tags, such as: <br/>game, vehicle, musician, racing car, pet, drum, bike, World of Warcraft, computer, school, and jacket. <br/> |
| Intelligent cover generating | Captures one or more screenshots of a video as the recommended cover. |
| Intelligent frame-specific tagging | Gives suggestions on frame-specific tags that can be added to a video. There are currently over 1,000 tags, such as: <br/>contemporary dance, water sports, steak, baby, kitten, annual plant, destroyer, comics, lawn, wedding dress, function room, and passport. |

## <span id = "sh"></span>Video Content Analysis Template

The analysis operations in a video content analysis task are subject to analysis parameters, which can be presented in the form of VOD video content analysis template as shown below:

- Whether to enable intelligent categorization.
- Whether to enable intelligent tagging.
- Whether to enable intelligent cover generating.
- Whether to enable intelligent frame-specific tagging.

For common combinations of operations, VOD provides a [preset video content analysis template](https://intl.cloud.tencent.com/document/product/266/33932#.E9.A2.84.E7.BD.AE.E8.A7.86.E9.A2.91.E5.86.85.E5.AE.B9.E5.88.86.E6.9E.90.E6.A8.A1.E6.9D.BF). <!--api In addition, you can also create and manage custom video content analysis templates by calling a [server API](https://intl.cloud.tencent.com/document/product/266/34463).-->

## Task Initiation

There are three ways to initiate a video content analysis task, namely, directly initiating through server API, directly initiating through the console, and specifying a task upon upload. For more information, please see [Task Initiation](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask) for video processing.

Below are instructions for initiating video content analysis tasks in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: specify the [video content analysis template](#sh) ID in the `AiAnalysisTask` parameter in the request.
* Call the server API [ProcessMediaByUrl](#APIhttps://intl.cloud.tencent.com/document/product/266/33426) to initiate a task: specify the [video content analysis template](#sh) ID in the `AiAnalysisTask` parameter in the request.
* Initiate a task on a video through the console: call a [server API](#APIhttps://intl.cloud.tencent.com/document/product/266/33897) to create a task flow, configure a video content analysis task in it (by specifying `MediaProcessTask.AiAnalysisTask`), and use it to [initiate video processing](https://intl.cloud.tencent.com/document/product/266/33890) in the console.
* Specify a task upon upload from server: call a [server API](#APIhttps://intl.cloud.tencent.com/document/product/266/33897) to create a task flow, configure a video content analysis task in it (by specifying `MediaProcessTask.AiAnalysisTask`), and specify it as the `procedure` in the [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) request.
* Specify a task upon upload from client: call a [server API](#APIhttps://intl.cloud.tencent.com/document/product/266/33897) to create a task flow, configure a video content analysis task in it (by specifying `MediaProcessTask.AiAnalysisTask`), and specify it as the `procedure` in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0).
* Upload through console: call a [server API](#APIhttps://intl.cloud.tencent.com/document/product/266/33897) to create a task flow, configure a video content analysis task in it (by specifying `MediaProcessTask.AiAnalysisTask`), upload a video through the console, select [Process Video During Upload](https://intl.cloud.tencent.com/document/product/266/33890), and specify to execute this task flow upon video upload completion.

## Getting Result

After initiating a video content analysis task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the content analysis task is initiated (the fields with null value are omitted):

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
        "AiAnalysisResultSet":[
            {
                "Type":"Classification",
                "ClassificationTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "ClassificationSet":[
                            {
                                "Classification":"Animals",
                                "Confidence":80
                            },
                            {
                                "Classification":"Travel",
                                "Confidence":34
                            }
                        ]
                    }
                }
            },
            {
                "Type":"Cover",
                "CoverTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "CoverSet":[
                            {
                                "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg",
                                "Confidence":79
                            },
                            {
                                "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx2.jpg",
                                "Confidence":70
                            },
                            {
                                "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx3.jpg",
                                "Confidence":66
                            }
                        ]
                    }
                }
            },
            {
                "Type":"Tag",
                "TagTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "TagSet":[
                            {
                                "Tag":"Horse",
                                "Confidence":34
                            },
                            {
                                "Tag":"Bird",
                                "Confidence":27
                            },
                            {
                                "Tag":"Plant",
                                "Confidence":13
                            },
                            {
                                "Tag":"Beach",
                                "Confidence":11
                            }
                        ]
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

In the callback result, `ProcedureStateChangeEvent.AiAnalysisResultSet` contains the analysis result in `Type` of `Classification`, `Cover`, and `Tag`, which represent intelligent categorization, intelligent cover generating, and intelligent tagging, respectively.

* The result in `Type` of `Classification` shows the `Output.ClassificationSet`, where the highest degree of confidence is of `animal`, followed by `travel`.
* The result in `Type` of `Cover` is `Output.CoverSet`, which gives 3 recommended covers, and `CoverUrl` is the download address of a corresponding cover.
* The result in `Type` of `Tag` is `Output.TagSet`, which gives 4 recommended tags for the video in descending order of confidence.
