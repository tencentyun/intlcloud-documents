Video content moderation is an offline task that intelligently moderates video content with the aid of AI. The task execution results include confidence score, moderation suggestion, and suspected video segments. According to the suggestion, you can decide whether to allow a video to be published, effectively avoiding potential legal risks and brand image damage caused by illegal videos.

VOD can intelligently detect porn, terrorism, and politically sensitive information in video image, speech (ASR), and text (OCR).

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
            Porn information detection
        </td>
        <td>
				    Performs porn information detection on video image, including:
				    <li>vulgar: vulgarity</li>
				    <li>intimacy: intimacy</li>
				    <li>sexy: sexiness</li>
        </td>
    </tr>
    <tr>
        <td>
            Terrorism information detection
        </td>
        <td>
				    Performs terrorism information detection on video image, including:
				    <li>militant: militants</li>
				    <li>guns: weapons and guns</li>
				    <li>bloody: bloody scenes</li>
				    <li>police: police force</li>
				    <li>crowd: crowd</li>
        </td>
    </tr>
    <tr>
        <td>
            Politically sensitive information detection
        </td>
        <td>
            Performs politically sensitive information detection on video image, including:
				    <li>violation_photo: violating photo</li>
				    <li>politician: particular people</li>
        </td>
    </tr>
    <tr>
        <td rowspan=2>
            ASR phrase (phrase in speech)
        </td>
        <td>
				    Porn information detection
        <td>
            Performs porn information detection on phrases in speech to identify suspect keywords
        </td>
    </tr>
    <tr>
        <td>
            Politically sensitive information detection
        </td>
        <td>
            Performs politically sensitive information detection on phrases in speech to identify suspect keywords
        </td>
    </tr>
    <tr>
        <td rowspan=2>
            OCR text (text in video image)
        </td>
        <td>
				    Porn information detection
        </td>
        <td>
            Performs porn information detection on text in video image to identify suspect keywords
        </td>
    </tr>
    <tr>
        <td>
            Politically sensitive information detection
        </td>
        <td>
            Performs politically sensitive information detection on text in video image to identify suspect keywords
        </td>
    </tr>
</table>


| Field Name | Type | Description |
| ---------- | ------ | ------------------------------------------------------------ |
| confidence | Float | Confidence score (0–100). The higher the score, the greater the suspicion |
| suggestion | String | There are three types of moderation suggestions: <ul><li>`pass`: the degree of suspicion is not high, and approval is recommended.</li><li>`review`: the degree of suspicion is high, and human moderation is recommended.</li><li>`block`: the degree of suspicion is very high, and blocking is recommended.</li></ul> |
| segments | Array | Suspected video segments, helping locate specific segments in the video that are suspected of violations |

## [](id:sh)Video Content Moderation Template

A video moderation template represents a set of video moderation parameters. You can use a template to specify which of the following video moderation tasks you want VOD to perform:
- Porn information detection on video image
- Terrorism information detection on video image
- Politically sensitive information detection on video image
- ASR-based porn information detection on phrases in speech
- ASR-based politically sensitive information detection on phrases in speech
- OCR-based porn information detection on text in video image
- OCR-based politically sensitive information detection on text in video image

VOD provides [preset video moderation templates](https://intl.cloud.tencent.com/document/product/266/33932) for common parameter combinations. You can also use a [server API](https://intl.cloud.tencent.com/document/product/266/37566) to create and manage custom templates.

## Initiating a Task

You can initiate a video moderation task by calling a server API, via the console, or by specifying the task when uploading videos. For details, see [Task Initiation](https://intl.cloud.tencent.com/document/product/266/33931).

Below are instructions for initiating video content moderation tasks in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: specify the [video content moderation template](#sh) ID in the `AiContentReviewTask` parameter in the request.
* Call the server API [ProcessMediaByUrl](https://intl.cloud.tencent.com/document/product/266/34123) to initiate a task: specify the [video content moderation template](#sh) ID in the `AiContentReviewTask` parameter in the request.
* Initiate a task via the console: [create a task flow](https://intl.cloud.tencent.com/document/product/266/14058) with video moderation enabled in the console and use it to [process videos](https://intl.cloud.tencent.com/document/product/266/33892).
* Specify a task upon upload from server: [create a task flow](https://intl.cloud.tencent.com/document/product/266/14058) with video moderation enabled in the console and set `procedure` to the name of the task flow when calling [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0).
* Specify a task upon upload from client: [create a task flow](https://intl.cloud.tencent.com/document/product/266/14058) with video moderation enabled in the console and set `procedure` to the name of the task flow in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922).
* Specify a task upon upload from the console: in the console, [create a task flow](https://intl.cloud.tencent.com/document/product/266/14058) with video moderation enabled and, during video upload, choose [Automatic Processing After Upload](https://intl.cloud.tencent.com/document/product/266/33890) and select the task flow created.

## Obtaining Result

After initiating a video moderation task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the video moderation task is initiated (the fields with null value are omitted):
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

In the callback result, `ProcedureStateChangeEvent.AiContentReviewResultSet` contains three types of moderation results, namely `Porn`, `Terrorism`, and `Political`, which represent the detection of porn, terrorism, and politically sensitive information in video images, respectively.

* The result in `Type` of `Porn` shows that `Output.Suggestion` is `block`, that is, the possibility of porn information presence is high and blocking is recommended, the confidence of porn information is 98, and the reason is `sexy` (sexiness).
* The result `Output.SegmentSet` in `Type` of `Porn` lists three video segments suspected of containing porn information. The start time and end time of each segment are marked by `StartTimeOffset` and `EndTimeOffset`, respectively.
* The result in `Type` of `Terrorism` and `Political` shows that the video is not suspected of containing terrorism and politically sensitive information.


