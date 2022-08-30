Audio/Video content analysis is an offline task that intelligently analyzes audio/video content with the aid of AI. It intelligently gives suggestions for video categorization, tagging, and thumbnail generation to help video platforms manage videos more accurately and efficiently.

Audio/Video content analysis includes the following features:

| Feature | Description |
| -- | -- |
| Intelligent categorization | Gives suggestions for the category to which a video belongs. There are currently over ten categories, such as <br/>news, entertainment, game, technology, food, sports, travel, animation, dance, music, television, and automobile. |
| Intelligent tagging | Gives suggestions for the tags that can be added to a video. There are currently over 3,000 tags, such as <br/>game, vehicle, musician, racing car, pet, drum, bike, World of Warcraft, computer, school, and jacket. <br/> |
| Intelligent thumbnail generation | Captures one or more screenshots of a video as the recommended cover. |
| Intelligent frame-specific tagging | Gives suggestions for frame-specific tags that can be added to a video. There are currently over 1,000 tags, such as: <br/>contemporary dance, water sports, steak, baby, kitten, annual plant, destroyer, comics, lawn, wedding dress, function room, and passport. |

## [](id:sh)Audio/Video Content Analysis Template

An audio/video content analysis template represents a set of audio/video content analysis parameters. You can use a template to specify which of the following audio/video content analysis tasks you want VOD to perform:

- Whether to enable intelligent categorization.
- Whether to enable intelligent tagging.
- Whether to enable intelligent thumbnail generation.
- Whether to enable intelligent frame-specific tagging.

VOD provides [preset audio/video content analysis templates](https://intl.cloud.tencent.com/document/product/266/33932) for common parameter combinations. You can also use a [server API](https://intl.cloud.tencent.com/document/product/266/34170) to create and manage custom templates.

## Initiating a Task

You can initiate an audio/video content analysis task by calling a server API, via the console, or by specifying the task when uploading videos. For more information, see [Video Processing Task System](https://intl.cloud.tencent.com/document/product/266/33931).

Below are instructions for initiating audio/video content analysis tasks in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: Specify the [audio/video content analysis template](#sh) ID in the `AiAnalysisTask` parameter in the request.
* Call the server API [ProcessMediaByUrl](https://intl.cloud.tencent.com/document/product/266/34123) to initiate a task: Specify the [audio/video content analysis template](#sh) ID in the `AiAnalysisTask` parameter in the request.
* Initiate a task on a video via the console: Call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create an audio/video content analysis task flow (by specifying `MediaProcessTask.AiAnalysisTask`), and use it to [process videos](https://intl.cloud.tencent.com/document/product/266/33892) in the console.
* Specify a task upon upload from server: Call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create an audio/video content analysis task flow (by specifying `MediaProcessTask.AiAnalysisTask`), and set `procedure` to the name of the task flow when calling [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120).
* Specify a task upon upload from client: Call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create an audio/video content analysis task flow (by specifying `MediaProcessTask.AiAnalysisTask`), and set `procedure` to the name of the task flow in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922).
* Specify a task upon upload from the console: Call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create an audio/video content analysis task flow (by specifying `MediaProcessTask.AiAnalysisTask`) and, when uploading videos via the console, choose [Automatic Processing After Upload](https://intl.cloud.tencent.com/document/product/266/33890) and select the created task flow.

## Getting the Result

After initiating an audio/video content analysis task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931) asynchronously or perform a [task query](https://intl.cloud.tencent.com/document/product/266/33931) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the content analysis task is initiated (the fields with null value are omitted):

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

In the callback result, `ProcedureStateChangeEvent.AiAnalysisResultSet` contains the analysis result in `Type` of `Classification`, `Cover`, and `Tag`, which represent intelligent categorization, intelligent thumbnail generation, and intelligent tagging, respectively.

* The result in `Type` of `Classification` shows the `Output.ClassificationSet`, where the highest degree of confidence is of `animal`, followed by `travel`.
* The result in `Type` of `Cover` is `Output.CoverSet`, which gives 3 recommended covers, and `CoverUrl` is the download address of a corresponding cover.
* The result in `Type` of `Tag` is `Output.TagSet`, which gives 4 recommended tags for the video in descending order of confidence.


