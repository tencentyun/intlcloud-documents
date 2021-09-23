[Media Processing Service](https://intl.cloud.tencent.com/document/product/1041) (MPS) is an on-cloud transcoding and audio/video processing service for massive amounts of multimedia data. You can write functions to process the callback information in MPS and dump, publish, and process relevant events and subsequent content in video tasks by receiving relevant callbacks.

Characteristics of MPS triggers:
- **Push model**: an MPS trigger listens on the callback information of video processing and pushes the event data to the SCF function through one single triggering action.
- **Async invocation**: an MPS trigger always invokes a function asynchronously, and the result is not returned to the invoker. For more information on invocation types, please see [Invocation Types](https://intl.cloud.tencent.com/document/product/583/9694).

## MPS Trigger Attributes

- **Event type**: an MPS trigger pushes events in the account-level event type. Currently, two event types are supported: workflow task (`WorkflowTask`) and video editing task (`EditMediaTask`).
- **Event processing**: an MPS trigger uses events generated at the service level as the event source, regardless of attributes such as region and resources. Each account can only create one MPS trigger in all regions. If you need multiple functions to handle a task, please see [SDK for Node.js](https://intl.cloud.tencent.com/zh/document/product/583/32747).

## Event Structure for MPS Trigger

When a specified MPS trigger receives a message, the event structure and fields will be as shown below (with the `WorkflowTask` task as an example):

```
{
    "EventType":"WorkflowTask",
    "WorkflowTaskEvent":{
        "TaskId":"245****654-WorkflowTask-f46dac7fe2436c47******d71946986t0",
        "Status":"FINISH",
        "ErrCode":0,
        "Message":"",
        "InputInfo":{
            "Type":"COS",
            "CosInputInfo":{
                "Bucket":"macgzptest-125****654",
                "Region":"ap-guangzhou",
                "Object":"/dianping2.mp4"
            }
        },
        "MetaData":{
            "AudioDuration":11.261677742004395,
            "AudioStreamSet":[
                {
                    "Bitrate":127771,
                    "Codec":"aac",
                    "SamplingRate":44100
                }
            ],
            "Bitrate":2681468,
            "Container":"mov,mp4,m4a,3gp,3g2,mj2",
            "Duration":11.261677742004395,
            "Height":720,
            "Rotate":90,
            "Size":3539987,
            "VideoDuration":10.510889053344727,
            "VideoStreamSet":[
                {
                    "Bitrate":2553697,
                    "Codec":"h264",
                    "Fps":29,
                    "Height":720,
                    "Width":1280
                }
            ],
            "Width":1280
        },
        "MediaProcessResultSet":[
            {
                "Type":"Transcode",
                "TranscodeTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"SUCCESS",
                    "Input":{
                        "Definition":10,
                        "WatermarkSet":[
                            {
                                "Definition":515247,
                                "TextContent":"",
                                "SvgContent":""
                            }
                        ],
                        "OutputStorage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "OutputObjectPath":"/dasda/dianping2_transcode_10",
                        "SegmentObjectName":"/dasda/dianping2_transcode_10_{number}",
                        "ObjectNumberFormat":{
                            "InitialValue":0,
                            "Increment":1,
                            "MinLength":1,
                            "PlaceHolder":"0"
                        }
                    },
                    "Output":{
                        "OutputStorage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "Path":"/dasda/dianping2_transcode_10.mp4",
                        "Definition":10,
                        "Bitrate":293022,
                        "Height":320,
                        "Width":180,
                        "Size":401637,
                        "Duration":11.26200008392334,
                        "Container":"mov,mp4,m4a,3gp,3g2,mj2",
                        "Md5":"31dcf904c03d0cd78346a12c25c0acc9",
                        "VideoStreamSet":[
                            {
                                "Bitrate":244608,
                                "Codec":"h264",
                                "Fps":24,
                                "Height":320,
                                "Width":180
                            }
                        ],
                        "AudioStreamSet":[
                            {
                                "Bitrate":48414,
                                "Codec":"aac",
                                "SamplingRate":44100
                            }
                        ]
                    }
                },
                "AnimatedGraphicTask":null,
                "SnapshotByTimeOffsetTask":null,
                "SampleSnapshotTask":null,
                "ImageSpriteTask":null
            },
            {
                "Type":"AnimatedGraphics",
                "TranscodeTask":null,
                "AnimatedGraphicTask":{
                    "Status":"FAIL",
                    "ErrCode":30010,
                    "Message":"TencentVodPlatErr Or Unkown",
                    "Input":{
                        "Definition":20000,
                        "StartTimeOffset":0,
                        "EndTimeOffset":600,
                        "OutputStorage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "OutputObjectPath":"/dasda/dianping2_animatedGraphic_20000"
                    },
                    "Output":null
                },
                "SnapshotByTimeOffsetTask":null,
                "SampleSnapshotTask":null,
                "ImageSpriteTask":null
            },
            {
                "Type":"SnapshotByTimeOffset",
                "TranscodeTask":null,
                "AnimatedGraphicTask":null,
                "SnapshotByTimeOffsetTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"SUCCESS",
                    "Input":{
                        "Definition":10,
                        "TimeOffsetSet":[

                        ],
                        "WatermarkSet":[
                            {
                                "Definition":515247,
                                "TextContent":"",
                                "SvgContent":""
                            }
                        ],
                        "OutputStorage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "OutputObjectPath":"/dasda/dianping2_snapshotByOffset_10_{number}",
                        "ObjectNumberFormat":{
                            "InitialValue":0,
                            "Increment":1,
                            "MinLength":1,
                            "PlaceHolder":"0"
                        }
                    },
                    "Output":{
                        "Storage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "Definition":0,
                        "PicInfoSet":[
                            {
                                "TimeOffset":0,
                                "Path":"/dasda/dianping2_snapshotByOffset_10_0.jpg",
                                "WaterMarkDefinition":[
                                    515247
                                ]
                            }
                        ]
                    }
                },
                "SampleSnapshotTask":null,
                "ImageSpriteTask":null
            },
            {
                "Type":"ImageSprites",
                "TranscodeTask":null,
                "AnimatedGraphicTask":null,
                "SnapshotByTimeOffsetTask":null,
                "SampleSnapshotTask":null,
                "ImageSpriteTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"SUCCESS",
                    "Input":{
                        "Definition":10,
                        "OutputStorage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "OutputObjectPath":"/dasda/dianping2_imageSprite_10_{number}",
                        "WebVttObjectName":"/dasda/dianping2_imageSprite_10",
                        "ObjectNumberFormat":{
                            "InitialValue":0,
                            "Increment":1,
                            "MinLength":1,
                            "PlaceHolder":"0"
                        }
                    },
                    "Output":{
                        "Storage":{
                            "Type":"COS",
                            "CosOutputStorage":{
                                "Bucket":"gztest-125****654",
                                "Region":"ap-guangzhou"
                            }
                        },
                        "Definition":10,
                        "Height":80,
                        "Width":142,
                        "TotalCount":2,
                        "ImagePathSet":[
                            "/dasda/imageSprite/dianping2_imageSprite_10_0.jpg"
                        ],
                        "WebVttPath":"/dasda/imageSprite/dianping2_imageSprite_10.vtt"
                    }
                }
            }
        ]
    }
}
```

### WorkflowTask event

The detailed fields of a `WorkflowTask` event message body are as follows:
```
{
    "EventType":"WorkflowTask",
    "WorkflowTaskEvent":{
        // WorkflowTaskEvent field
     }
}
```

The data structure and fields of `WorkflowTask` are as detailed below:

| Name | Type | Description |
|:----|:----|:----|
| TaskId | String | ID of video processing task. |
| Status | String | Task flow status. Valid values:<br><li>PROCESSING: processing.<br><li>FINISH: finished. |
| ErrCode | Integer | Disused. Please use `ErrCode` of each specific task. |
| Message | String | Disused. Please use `Message` of each specific task. |
| InputInfo | [MediaInputInfo](https://intl.cloud.tencent.com/document/product/1041/33690#MediaInputInfo) | Information of the target file of video processing. Note: this field may return null, indicating that no valid values can be obtained. |
| MetaData | [MediaMetaData](https://intl.cloud.tencent.com/document/product/1041/33690#MediaMetaData) | Source video metadata. Note: this field may return null, indicating that no valid values can be obtained. |
| MediaProcessResultSet | Array of [MediaProcessTaskResult](https://intl.cloud.tencent.com/document/product/1041/33690#MediaProcessTaskResult) | Execution status and result of video processing task. |
| AiContentReviewResultSet | Array of [AiContentReviewResult](https://intl.cloud.tencent.com/document/product/1041/33690#AiContentReviewResult) | Execution status and result of video content moderation task. |
| AiAnalysisResultSet | Array of [AiAnalysisResult](https://intl.cloud.tencent.com/document/product/1041/33690#AiAnalysisResult) | Execution status and result of video content analysis task. |
| AiRecognitionResultSet | Array of [AiRecognitionResult](https://intl.cloud.tencent.com/document/product/1041/33690#AiRecognitionResult) | Execution status and result of video content recognition task. |


### EditMediaTask event

The detailed fields of an `EditMediaTask` event message body are as follows:
```
{
    "EventType":"EditMediaTask",
    "EditMediaTaskEvent":{
        // EditMediaTask field
     }
}
```

The data structure and fields of `EditMediaTask` are as detailed below:

<table>
<thead>
<tr>
<th>Name</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>TaskId</td>
<td>String</td>
<td>Task ID.</td>
</tr>
<tr>
<td>Status</td>
<td>String</td>
<td>Task status. Valid values:<br><li>PROCESSING: processing.<br></li><li>FINISH: finished.</li></td>
</tr>
<tr>
<td>ErrCode</td>
<td>Integer</td>
<td>Error code. 0: success; other values: failure.</td>
</tr>
<tr>
<td>Message</td>
<td>String</td>
<td>Error message.</td>
</tr>
<tr>
<td>Input</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1041/33690#EditMediaTaskInput">EditMediaTaskInput</a></td>
<td>Input of video editing task.</td>
</tr>
<tr>
<td>Output</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1041/33690#EditMediaTaskOutput">EditMediaTaskOutput</a></td>
<td>Output of video editing task. Note: this field may return null, indicating that no valid values can be obtained.</td>
</tr>
</tbody></table>
