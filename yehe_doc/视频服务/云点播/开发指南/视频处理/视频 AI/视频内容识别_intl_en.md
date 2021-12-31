Video content recognition is an offline task that intelligently recognizes video content including faces, text, opening and closing credits, and speech with the aid of AI. See the table below for details:

| Feature | Description | Use Case |
| -- | -- | -- |
| Face recognition | Recognizes faces in video image | <li>Marks where celebrities appear in video image </li><li>Checks for particular people in video image </li> |
| Full speech recognition | Recognizes all phrases in speech | <li>Generates subtitles for speech content </li><li>Performs data analysis on video speech content </li> |
| Full text recognition | Recognizes all text in video image | Performs data analysis on text in video image |
| Speech keyword recognition | Recognizes keywords in speech | <li>Checks for sensitive words in speech </li><li> Retrieves specific keywords in speech </li> |
| Text keyword recognition | Recognizes keywords in video image | <li>Checks for sensitive words in video image</li><li> Retrieves specific keywords in video image </li> |
| Opening and closing credits recognition | Recognizes opening and closing credits in video | <li>Marks the positions of opening credits, closing credits, and feature in the progress bar </li><li>Removes opening and closing credits of videos in batches</li> |


Some content recognition features depend on a material library. There are two types of libraries: public library and custom library.

* Public library: VOD's preset material library.
* Custom library: a material library created and managed by user.

| Recognition Type | Public Library | Custom Library |
| -- | -- | -- |
| Face recognition | Supported. The library includes celebrities in sports and the entertainment industry and other people. | Supported. Call a [server API](https://intl.cloud.tencent.com/document/product/266/37584) to manage the custom face library |
| Speech recognition | Not supported yet | Supported. Call a [server API](https://intl.cloud.tencent.com/document/product/266/37583) to manage the keyword library |
| Text recognition | Not supported yet | Supported. Call a [server API](https://intl.cloud.tencent.com/document/product/266/37583) to manage the keyword library |

[](id:sh)
## Video Content Recognition Template

Video content recognition integrates a number of recognition features that require fine-grained control through parameters as described below:

* Recognition types to enable: which content recognition features to enable
* Library to use: whether to use the public library or a custom library for face recognition
* Filter score: the confidence score threshold to return face recognition results
* Filter tag: tags to filter the returned results by

VOD provides [preset video content recognition templates](https://intl.cloud.tencent.com/document/product/266/33932) for common parameter combinations. You can also use a [server API](https://intl.cloud.tencent.com/document/product/266/37568) to create and manage custom templates.

## Initiating a Task

You can initiate a video content recognition task by calling a server API, via the console, or by specifying the task when uploading videos. For details, see [Task Initiation](https://intl.cloud.tencent.com/document/product/266/33931).

Below are instructions for initiating video content recognition tasks in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: specify the [video content recognition template](#sh) ID in the `AiRecognitionTask` parameter in the request.
* Call the server API [ProcessMediaByUrl](https://intl.cloud.tencent.com/document/product/266/34123) to initiate a task: specify the [video content recognition template](#sh) ID in the `AiRecognitionTask` parameter in the request.
* Initiate a task via the console: call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create a video content recognition task flow (by specifying `MediaProcessTask.AiRecognitionTask`), and use it to [process videos](https://intl.cloud.tencent.com/document/product/266/33892) in the console.
* Specify a task upon upload from server: call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create a video content recognition task flow (by specifying `MediaProcessTask.AiRecognitionTask`), and set `procedure` to the name of the task flow when calling [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0).
* Specify a task upon upload from client: call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create a video content recognition task flow (by specifying `MediaProcessTask.AiRecognitionTask`), and set `procedure` to the name of the task flow in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922).
* Specify a task upon upload from the console: call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create a video content recognition task flow (by specifying `MediaProcessTask.AiRecognitionTask`) and, when uploading videos via the console, choose [Automatic Processing After Upload](https://intl.cloud.tencent.com/document/product/266/33890) and select the task flow created.

## Obtaining Result

After initiating a video content recognition task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the content recognition task is initiated (the fields with null value are omitted):

```json
{
    "EventType":"ProcedureStateChanged",
    "ProcedureStateChangeEvent":{
        "TaskId":"1400155958-Procedure-2e1af2456351812be963e309cc133403t0",
        "Status":"FINISH",
        "FileId":"5285890784363430543",
        "FileName":"Collection",
        "FileUrl":"http://1400155958.vod2.myqcloud.com/xxx/xxx/aHjWUx5Xo1EA.mp4",
        "MetaData":{
            "AudioDuration":243,
            "AudioStreamSet":[
                {
                    "Bitrate":125599,
                    "Codec":"aac",
                    "SamplingRate":48000
                }
            ],
            "Bitrate":1459299,
            "Container":"mov,mp4,m4a,3gp,3g2,mj2",
            "Duration":243,
            "Height":1080,
            "Rotate":0,
            "Size":44583593,
            "VideoDuration":243,
            "VideoStreamSet":[
                {
                    "Bitrate":1333700,
                    "Codec":"h264",
                    "Fps":29,
                    "Height":1080,
                    "Width":1920
                }
            ],
            "Width":1920
        },
        "AiRecognitionResultSet":[
            {
                "Type":"FaceRecognition",
                "FaceRecognitionTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "ResultSet":[
                            {
                                "Id":183213,
                                "Type":"Default",
                                "Name":"John Smith",
                                "SegmentSet":[
                                    {
                                        "StartTimeOffset":10,
                                        "EndTimeOffset":12,
                                        "Confidence":97,
                                        "AreaCoordSet":[
                                            830,
                                            783,
                                            1030,
                                            599
                                        ]
                                    },
                                    {
                                        "StartTimeOffset":12,
                                        "EndTimeOffset":14,
                                        "Confidence":97,
                                        "AreaCoordSet":[
                                            844,
                                            791,
                                            1040,
                                            614
                                        ]
                                    }
                                ]
                            },
                            {
                                "Id":236099,
                                "Type":"Default",
                                "Name":"Jane Smith",
                                "SegmentSet":[
                                    {
                                        "StartTimeOffset":120,
                                        "EndTimeOffset":122,
                                        "Confidence":96,
                                        "AreaCoordSet":[
                                            579,
                                            903,
                                            812,
                                            730
                                        ]
                                    }
                                ]
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

In the callback result, `ProcedureStateChangeEvent.AiRecognitionResultSet` contains the result of face recognition (`Type` is `FaceRecognition`).

According to the content of `Output.ResultSet`, two people are recognized: `John Smith` and `Jane Smith`. `SegmentSet` indicates when (from `StartTimeOffset` to `EndTimeOffset`) and where (coordinates specified by `AreaCoordSet`) the two people appear in the video.


