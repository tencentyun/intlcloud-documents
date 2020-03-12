Video content recognition is an offline task that intelligently recognizes video content with the aid of AI. It recognizes faces, objects, text, opening and closing credits, and speech in the video, helping you accurately and efficiently manage your videos. Specifically, it includes the following features:

| Feature Name | Description | Use Case |
| -- | -- | -- |
| Face recognition | Recognizes faces in video image | <li>Marks where celebrities appear in video image </li><li>Checks for sensitive figures in video image </li> |
| Full speech recognition | Recognizes all phrases in speech | <li>Generates subtitles for speech content </li><li>Performs data analysis on video speech content </li> |
| Full text recognition | Recognizes all text in video image | Performs data analysis on text in video image |
| Speech keyword recognition | Recognizes keywords in speech | <li>Checks for sensitive words in speech </li><li> Retrieves specific keywords in speech </li> |
| Text keyword recognition | Recognizes keywords in video image | <li>Checks for sensitive words in video image</li><li> Retrieves specific keywords in video image </li> |
| Opening and closing credits recognition | Recognizes opening and closing credits in video | <li>Marks the positions of opening credits, closing credits, and feature in the progress bar </li><li>Removes opening and closing credits of videos in batches</li> |
| Object recognition | Recognizes specific objects in video image | <li>Checks for sensitive objects in video image </li><li>Marks where specific objects appear in video image </li> |

Some content recognition features depend on a material library. There are two types of libraries: public library and custom library.

* Public library: VOD's preset material library.
* Custom library: a material library created and managed by user.

| Recognition Type | Public Library | Custom Library |
| -- | -- | -- |
| Face recognition | Supported. Figures in the library mainly include entertainment celebrities, sports celebrities, and politically sensitive figures | Supported. Call a [server API](https://intl.cloud.tencent.com/document/product/266/34800) to manage the custom face library |
| Speech recognition | Not supported yet | Supported. Call a server API <!--api (https://intl.cloud.tencent.com/document/product/266/34799)--> to manage the keyword library |
| Text recognition | Not supported yet | Supported. Call a server API <!--api (https://intl.cloud.tencent.com/document/product/266/34799)--> to manage the keyword library |
| Object recognition | Supported. Objects in the library mainly include politically sensitive icons | Not supported yet |

## <span id = "sh"></span>Video Content Recognition Template

Video content recognition integrates a number of recognition features that require fine-grained control through parameters as shown below:

* Recognition type enabled: which features in content recognition are enabled.
* Material library used: whether a public or custom library is used for face and object recognition.
* Filter score specified: at what confidence score a face recognition result will be returned.
* Filter tag specified: within what range a face tag result will be returned.

For common combinations of operations, VOD provides a [preset video content recognition template](https://intl.cloud.tencent.com/document/product/266/33932#.E9.A2.84.E7.BD.AE.E8.A7.86.E9.A2.91.E5.86.85.E5.AE.B9.E8.AF.86.E5.88.AB.E6.A8.A1.E6.9D.BF). In addition, you can also create and manage custom video recognition templates by calling a [server API](#APIhttps://intl.cloud.tencent.com/document/product/266/34791).

## Task Initiation

There are three ways to initiate a video content recognition task, namely, directly initiating through server API, directly initiating through the console, and specifying a task upon upload. For more information, please see [Task Initiation](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask) for video processing.
<!--api
Below are instructions for initiating video content recognition tasks in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: specify the [video content recognition template](#sh) ID in the `AiRecognitionTask` parameter in the request.
* Call the server API [ProcessMediaByUrl](#APIhttps://intl.cloud.tencent.com/document/product/266/33426) to initiate a task: specify the [video content recognition template](#sh) ID in the `AiRecognitionTask` parameter in the request.
* Initiate a task on a video through the console: call a [server API](#APIhttps://intl.cloud.tencent.com/document/product/266/33897) to create a task flow, configure a video content recognition task in it (by specifying `MediaProcessTask.AiRecognitionTask`), and use it to [initiate video processing](https://intl.cloud.tencent.com/document/product/266/33890) in the console.
* Specify a task upon upload from server: call a [server API](#APIhttps://intl.cloud.tencent.com/document/product/266/33897) to create a task flow, configure a video content recognition task in it (by specifying `MediaProcessTask.AiRecognitionTask`), and specify it as the `procedure` in the [ApplyUpload](#APIhttps://intl.cloud.tencent.com/document/api/266/31767#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) request.
* Specify a task upon upload from client: call a [server API](#APIhttps://intl.cloud.tencent.com/document/product/266/33897) to create a task flow, configure a video content recognition task in it (by specifying `MediaProcessTask.AiRecognitionTask`), and specify it as the `procedure` in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0).
* Upload through console: call a [server API](#APIhttps://intl.cloud.tencent.com/document/product/266/33897) to create a task flow, configure a video content recognition task in it (by specifying `MediaProcessTask.AiRecognitionTask`), upload a video through the console, select [Process Video During Upload](https://intl.cloud.tencent.com/document/product/266/33890), and specify to execute this task flow upon video upload completion.
-->
## Getting Result

After initiating a video content recognition task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the content recognition task is initiated (the fields with null value are omitted):

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

In the callback result, `ProcedureStateChangeEvent.AiRecognitionResultSet` contains the recognition result in `Type` of `FaceRecognition`, which represents face recognition.

The result in `Type` of `FaceRecognition` shows that `Output.ResultSet` contains two recognized figures `John Smith` and `Jane Smith`. `SegmentSet` indicates the time period (determined by `StartTimeOffset` and `EndTimeOffset`) during which a face appears in the video and the coordinates (determined by `AreaCoordSet`) in the video image.
