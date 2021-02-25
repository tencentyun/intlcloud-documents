Intelligent video content recognition is an offline task that intelligently recognizes video content with the aid of AI. The task execution results include intelligent recognition score, intelligent recognition suggestion, and suspected video segments. According to the "intelligent recognition suggestion", you can decide whether to allow a video to be published, effectively avoiding potential legal risks and brand image damage caused by non-compliant videos.

VOD can intelligently recognize video image, speech recognized by ASR, and text recognized by OCR. The intelligent recognition operations include recognition of porn, terrorism, and politically sensitive information.

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
            Porn information
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
            Terrorism information
        </td>
        <td>
				    Performs terrorism information detection on video image, including:
				    <li>militant: militants</li>
				    <li>guns: weapons and guns</li>
				    <li>bloody: bloody scenes</li>
				    <li>police: police force</li>
				    <li>crowd: crowd gathering</li>
        </td>
    </tr>
    <tr>
        <td>
            Politically sensitive information
        </td>
        <td>
            Performs politically sensitive information detection on video image, including:
				    <li>violation_photo: violation icon</li>
				    <li>politician: political figure</li>
        </td>
    </tr>
    <tr>
        <td rowspan=2>
            ASR phrase (phrase in speech)
        </td>
        <td>
				    Porn information
        <td>
            Performs porn information detection on phrases in speech to identify suspect keywords
        </td>
    </tr>
    <tr>
        <td>
            Politically sensitive information
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
				    Porn information
        </td>
        <td>
            Performs porn information detection on text in video image to identify suspect keywords
        </td>
    </tr>
    <tr>
        <td>
            Politically sensitive information
        </td>
        <td>
            Performs politically sensitive information detection on text in video image to identify suspect keywords
        </td>
    </tr>
</table>


| Field | Type | Meaning |
| ---------- | ------ | ------------------------------------------------------------ |
| confidence | Float | Intelligent recognition score (0–100). The higher the score, the greater the suspicion |
| suggestion | String | There are three types of intelligent recognition suggestions: `pass`, `review`, and `block`: <ul><li>pass: the degree of suspicion is not high, and approval is recommended. </li><li>review: the degree of suspicion is high, and human review is recommended </li><li>block: the degree of suspicion is very high, and blocking is recommended </li></ul> |
| segments | Array | Suspected video segments, helping locate specific segments in the video that are suspected of violations |

## <span id = "sh"></span>Intelligent Video Recognition Template

The intelligent recognition operations in an intelligent recognition task are subject to intelligent video recognition parameters, which can be presented in the form of VOD intelligent video recognition template as shown below. Such a template specifies what operations will be performed in an intelligent recognition task:
- Performs porn information detection on video image
- Performs terrorism information detection on video image
- Performs politically sensitive information detection on video image
- Performs porn information detection on phrases in speech based on ASR
- Performs politically sensitive information detection on phrases in speech based on ASR
- Performs porn information detection on text in video image based on OCR
- Performs politically sensitive information detection on text in video image based on OCR

For common combinations of operations, VOD provides a [preset intelligent video recognition template](https://intl.cloud.tencent.com/document/product/266/33932). In addition, you can also create and manage custom intelligent video recognition templates by calling a [server API](https://intl.cloud.tencent.com/document/product/266/37568).

## Task Initiation

There are three ways to initiate an intelligent video recognition task, namely, directly initiating through server API, directly initiating through the console, and specifying a task upon upload. For more information, please see [Video Processing Task System](https://intl.cloud.tencent.com/document/product/266/33931) for video processing.

Below are instructions for initiating intelligent video recognition tasks in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: specify the [intelligent video recognition template](#sh) ID in the `AiContentReviewTask` parameter in the request.
* Call the server API [ProcessMediaByUrl](https://intl.cloud.tencent.com/document/product/266/34123) to initiate a task: specify the [intelligent video recognition template](#sh) ID in the `AiContentReviewTask` parameter in the request.
* Initiate a task on a video through the console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, enable intelligent video recognition in it, and use it to [initiate video processing](https://intl.cloud.tencent.com/document/product/266/33892).
* Specify a task upon upload from server: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, enable intelligent video recognition in it, and specify it as the `procedure` in the [ApplyUpload](https://intl.cloud.tencent.com/zh/document/product/266/34120) request.
* Specify a task upon upload from client: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, enable intelligent video recognition in it, and specify it as the `procedure` parameter in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922).
* Upload through console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, enable intelligent video recognition in it, upload a video through the console, select [Process Video During Upload](https://intl.cloud.tencent.com/document/product/266/33890), and specify to execute this task flow upon video upload completion.

## Result Getting

After initiating an intelligent video recognition task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the intelligent video recognition task is initiated (the fields with null value are omitted):
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

In the callback result, `ProcedureStateChangeEvent.AiContentReviewResultSet` contains three types of intelligent recognition results in `Type` of `Porn`, `Terrorism`, and `Political`, which represent the detection of porn, terrorism, and politically sensitive information in video image, respectively.

* The result in `Type` of `Porn` shows that `Output.Suggestion` is `block`, that is, the possibility of porn information presence is high and blocking is recommended, the confidence of porn information is 98, and the reason is `sexy` (sexiness).
* The result `Output.SegmentSet` in `Type` of `Porn` lists three video segments suspected of containing porn information. The start time and end time of each segment are marked by `StartTimeOffset` and `EndTimeOffset`.
* The result in `Type` of `Terrorism` and `Political` shows that the video is not suspected of containing terrorism and politically sensitive information.


