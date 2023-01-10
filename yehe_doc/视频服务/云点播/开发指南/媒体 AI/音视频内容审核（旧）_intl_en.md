Audio/Video content moderation is an offline task that intelligently moderates audio/video content with the aid of AI. The task execution results include confidence score, moderation suggestion, and suspected audio/video segments. According to the suggestion, you can decide whether to allow an audio/video to be published, effectively avoiding potential legal risks and damage to your brand’s reputation.

VOD can intelligently detect porn, terrorism, and politically sensitive information in video images, speech (ASR), and text (OCR).

<table>
    <tr>
        <th style="width:20%">
            Object
        </th>
        <th style="width:10%">
            Operation
        </th>
        <th>
            Description
        </th>
    </tr>
    <tr>
        <td rowspan=4>
            Video image (figures and objects)
        </td>
    </tr>
    <tr>
        <td>
            Pornographic content detection
        </td>
        <td>
				    Detects pornographic content in video images, including:
				    <li>`vulgar`: Vulgar content</li>
				    <li>`intimacy`: Content that displays intimacy</li>
				    <li>`sexy`: Content that displays sexiness</li>
        </td>
    </tr>
    <tr>
        <td>
            Terrorism content detection
        </td>
        <td>
				    Detects terrorism content in video images, including:
				    <li>militant: militants</li>
				    <li>`guns`: Weapons and guns</li>
				    <li>`bloody`: Bloodiness</li>
				    <li>police: Police force</li>
				    <li>crowd: Crowd</li>
        </td>
    </tr>
    <tr>
        <td>
            Politically sensitive content detection
        </td>
        <td>
            Detects politically sensitive content in video images, including:
				    <li>`violation_photo`: Banned icons</li>
				    <li>politician: Particular people</li>
        </td>
    </tr>
    <tr>
        <td rowspan=2>
            ASR phrase (phrase in speech)
        </td>
        <td>
				    Pornographic content detection
        <td>
            Detects pornographic phrases in speech to identify suspected keywords
        </td>
    </tr>
    <tr>
        <td>
            Politically sensitive content detection
        </td>
        <td>
            Detects politically sensitive phrases in speech to identify suspected keywords
        </td>
    </tr>
    <tr>
        <td rowspan=2>
            OCR text (text in video images)
        </td>
        <td>
				    Pornographic content detection
        </td>
        <td>
            Detects pornographic content in text in video images to identify suspected keywords
        </td>
    </tr>
    <tr>
        <td>
            Politically sensitive content detection
        </td>
        <td>
            Detects politically sensitive content in text in video images to identify suspected keywords
        </td>
    </tr>
</table>


| Field Name | Type | Description |
| ---------- | ------ | ------------------------------------------------------------ |
| confidence | Float | Confidence score (0–100). The higher the score, the greater the suspicion. |
| suggestion | String | There are three types of moderation suggestions: <ul><li>`pass`: There is not a high suspicion of inappropriate content, and it is recommended to allow the content to pass.</li><li>`review`: There is a high suspicion of inappropriate content, and manual review is recommended.</li><li>`block`: There is a very high suspicion of inappropriate content, and blocking is recommended.</li></ul> |
| segments | Array | Suspected video segments, which help to locate the specific segments in the video that are suspected of violations. |

## [](id:sh)Video Moderation Template

A video moderation template represents a set of video moderation parameters. You can use a template to specify which of the following video moderation tasks you want VOD to perform:
- Recognition of pornographic content in video images
- Recognition of terrorist content in video images
- Recognition of politically sensitive content in video images
- Recognition of pornographic keywords in speech (ASR)
- Recognition of politically sensitive keywords in speech (ASR)
- Recognition of pornographic text keywords in video images (OCR)
- Recognition of politically sensitive text keywords in video images (OCR)

VOD provides [preset video moderation templates](https://www.tencentcloud.com/document/product/266/52735) for common parameter combinations. You can also use a [server API](https://intl.cloud.tencent.com/document/product/266/37566) to create and manage custom templates.

## Initiating a Task

You can initiate an audio/video moderation task by calling a server API, via the console, or by specifying the task when uploading videos. For details, see [Video Processing Task System](https://www.tencentcloud.com/document/product/266/52736).

Below are instructions for initiating audio/video content moderation tasks in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: Specify the [audio/video content moderation template](#sh) ID in the `AiContentReviewTask` parameter in the request.
* Call the server API [ProcessMediaByUrl](https://intl.cloud.tencent.com/document/product/266/34123) to initiate a task: Specify the [audio/video content moderation template](#sh) ID in the `AiContentReviewTask` parameter in the request.
* Initiate a task via the console: [Create a task flow](https://intl.cloud.tencent.com/document/product/266/14058) with audio/video moderation enabled in the console and use it to [process videos](https://intl.cloud.tencent.com/document/product/266/33892).
* Specify a task upon upload from server: [Create a task flow](https://intl.cloud.tencent.com/document/product/266/14058) with audio/video moderation enabled in the console and set `procedure` to the name of the task flow when calling [ApplyUpload](intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0).
* Specify a task upon upload from client: [Create a task flow](https://intl.cloud.tencent.com/document/product/266/14058) with audio/video moderation enabled in the console and set `procedure` to the name of the task flow in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922).
* Specify a task upon upload from the console: In the console, [create a task flow](https://intl.cloud.tencent.com/document/product/266/14058) with audio/video moderation enabled and, during video upload, select [Auto-processing after upload](https://intl.cloud.tencent.com/document/product/266/33890) and select the task flow created.

## Getting the Result

After initiating a video moderation task, you can wait for the [result notification](https://intl.cloud.tencent.com/document/product/266/33931) asynchronously or perform a [task query](https://intl.cloud.tencent.com/document/product/266/33931) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the video moderation task is initiated (the fields with null value are omitted):
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
        "AiContentReviewResultSet":[
            {
                "Type":"Porn",
                "PornTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Confidence":98,
                        "Suggestion":"block",
                        "Label":"sexy",
                        "SegmentSet":[
                            {
                                "StartTimeOffset":9.5,
                                "EndTimeOffset":14,
                                "Confidence":98,
                                "Suggestion":"block",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcluod.com/xxx/xxx/xx1.jpg",
                                "PicUrlExpireTimeStamp":1530005146
                            },
                            {
                                "StartTimeOffset":16.5,
                                "EndTimeOffset":18,
                                "Confidence":80,
                                "Suggestion":"review",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcluod.com/xxx/xxx/xx2.jpg",
                                "PicUrlExpireTimeStamp":1530005146
                            },
                            {
                                "StartTimeOffset":41,
                                "EndTimeOffset":49,
                                "Confidence":97,
                                "Suggestion":"block",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcluod.com/xxx/xxx/xx3.jpg",
                                "PicUrlExpireTimeStamp":1530005146
                            }
                        ]
                    }
                }
            },
            {
                "Type":"Terrorism",
                "TerrorismTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Confidence":0,
                        "Suggestion":"pass",
                        "SegmentSet":[

                        ]
                    }
                }
            },
            {
                "Type":"Political",
                "PoliticalTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Confidence":0,
                        "Suggestion":"pass",
                        "SegmentSet":[

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

In the callback result, `ProcedureStateChangeEvent.AiContentReviewResultSet` contains three types of moderation results, namely `Porn`, `Terrorism`, and `Political`, which represent the detection of pornographic, terrorist, and politically sensitive content in video images.

* The result in `Type` of `Porn` shows that `Output.Suggestion` is `block` (i.e., there is a high suspicion of pornographic content and blocking is recommended), the confidence of the detection of pornographic content is 98, and the reason is `sexy`.
* The result `Output.SegmentSet` in `Type` of `Porn` lists three video segments suspected of containing pornographic content. The start time and end time of each segment are marked by `StartTimeOffset` and `EndTimeOffset`, respectively.
* The results in `Type` of `Terrorism` and `Political` show that the video is not suspected of containing terrorist and politically sensitive content.


