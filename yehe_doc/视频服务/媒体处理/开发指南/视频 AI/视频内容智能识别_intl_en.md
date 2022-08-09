MPS leverages AI technologies to recognize video content. The result of an intelligent video recognition task includes a recognition score, suggestion, and suspicious video segments. You can decide whether to expose a video based on the suggestion.

## Result
MPS can intelligently recognize video images, speech (ASR), and optical characters (OCR).

<table>
<tr>
<th style="text-align:center">Object</th><th >Operation</th><th>Description</th>
</tr><tr>
<td rowspan=4 style="text-align:center">Video images<br>(People and objects)</td>
</tr><tr>
<td>Pornographic content</td>
<td>Checks for pornographic content in video images, including:
    <li>`vulgar`: vulgarity</li>
    <li>`intimacy`: intimacy</li>
    <li>`sexy`: sexiness</li>
</td>
</tr><tr>
<td>Politically sensitive content</td>
<td>Checks for politically sensitive content in video images, including:
    <li>`bloody`: bloodiness</li>
    <li>`explosion`: explosions and fires</li>
    <li>`violation_photo`: banned icons</li>
    <li>`guns`: weapons and guns</li>
</td>
</tr><tr>
</tr><tr>
<td rowspan=2 style="text-align:center">Speech<br>(Speech to text)</td>
<td>Pornographic content
<td>Checks for keywords for pornographic content in speech</td>
</tr><tr>
<td>Politically sensitive content</td>
<td>Checks for keywords for politically sensitive content in speech</td>
</tr><tr>
<td rowspan=2 style="text-align:center">Optical characters<br>Image to text</td>
<td>Pornographic content</td>
<td>Checks for keywords for pornographic content in images</td>
</tr><tr>
<td>Politically sensitive content</td>
<td>Checks for keywords for politically sensitive content in images</td>
</tr>
</table>

#### Parameter description

| Field Name | Type | Description |
| ---------- | ------ | ------------------------------------------------------------ |
| confidence | Float | Intelligent recognition score (0-100). The higher the score, the more suspicious the content. |
| suggestion | String | There are three types of intelligent recognition suggestions: <ul style="margin:0;"><li >`pass`: The degree of suspicion is not high, and approval is recommended. </li><li>`review`: The degree of suspicion is high, and human review is recommended. </li><li>`block`: The degree of suspicion is very high, and blocking is recommended. </li></ul> |
| segments | Array | Suspicious video segments, which help you locate suspicious content in a video |



## Initiating Task
### Directions
You can call an API to initiate an intelligent video recognition task or configure automatic triggering of the task upon video upload.

- **API**: Call the [ProcessMedia](https://intl.cloud.tencent.com/document/product/1041/33640) API, setting `AiContentReviewTask` to the ID of your [intelligent video recognition template](#sh).
- **Automatic triggering upon upload**: In the console, [create a workflow](https://intl.cloud.tencent.com/document/product/1041/33485) with intelligent video recognition enabled and upload videos to the bucket bound to the workflow. 

[](id:sh)
### Creating template
MPS uses templates to represent combinations of intelligent video recognition parameters, which determine which of the following operations MPS performs.
- Recognition of pornographic content in video images
- Recognition of politically sensitive content in video images
- Recognition of pornographic keywords in speech (ASR)
- Recognition of politically sensitive keywords in speech (ASR)
- Recognition of pornographic keywords in images (OCR)
- Recognition of politically sensitive keywords in images (OCR)

MPS provides [preset intelligent video recognition templates](https://intl.cloud.tencent.com/document/product/1041/33476) for common parameter combinations. You can also use a [server API](https://intl.cloud.tencent.com/document/product/1041/33675) to create and manage custom templates.

## Obtaining Result
After initiating an intelligent video recognition task, you can wait for the [result notification](https://intl.cloud.tencent.com/document/product/1041/33499) asynchronously or [query the result](https://intl.cloud.tencent.com/document/product/1041/33497) synchronously.

Below is an example of the result returned after query (fields with null values are omitted):
```json
{
    "TaskType":"WorkflowTask",
    "Status":"FINISH",
    "CreateTime":"2019-07-16T06:21:27Z",
    "BeginProcessTime":"2019-07-16T06:21:28Z",
    "FinishTime":"2019-07-16T06:21:46Z",
    "WorkflowTask":{
        "TaskId":"2356768367-WorkflowTask-2e1af2456351812be963e309cc133403t0",
        "Status":"FINISH",
        "InputInfo":{
            "Type":"COS",
            "CosInputInfo":{
                "Bucket":"MyVideoBucket-235303****",
                "Region":"ap-beijing",
                "Object":"/input/AnimalWorld.mp4"
            }
        },
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

        ],
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
                                "Url":"http://xxx.vod2.myqcloud.com/xxx/xxx/xx1.jpg",
                                "PicUrlExpireTime":"2019-07-23T06:21:46Z"
                            },
                            {
                                "StartTimeOffset":16.5,
                                "EndTimeOffset":18,
                                "Confidence":80,
                                "Suggestion":"review",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcloud.com/xxx/xxx/xx2.jpg",
                                "PicUrlExpireTime":"2019-07-23T06:21:46Z"
                            },
                            {
                                "StartTimeOffset":41,
                                "EndTimeOffset":49,
                                "Confidence":97,
                                "Suggestion":"block",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcloud.com/xxx/xxx/xx3.jpg",
                                "PicUrlExpireTime":"2019-07-23T06:21:46Z"
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
        "AiAnalysisResultSet":[

        ],
        "AiRecognitionResultSet":[

        ]
    },
    "TasksPriority":0,
    "SessionId":"",
    "SessionContext":"",
    "RequestId":"xxx-xxx-xxx"
}
```

As shown above, there are three types of results under `WorkflowTask.AiContentReviewResultSet`: `Porn`, `Terrorism`, and `Political`.

- For `Porn`, `Output.Suggestion` is `block`, which indicates a very high likelihood that the content is pornographic, and you are advised to block it. The confidence score is 98, and the label for the content is `sexy`.
- Three suspicious video segments are identified for `Porn`, whose start and end times are specified by `StartTimeOffset` and `EndTimeOffset`.
- According to the results for `Terrorism` and `Political`, no inappropriate content is detected in the video.
