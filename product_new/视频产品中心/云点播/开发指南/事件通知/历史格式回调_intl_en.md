
The format of event notifications in VOD was revised in 2019:
- After the revision, the callback format for newly registered users is v3.0 (current format).
- Users registered before the revision may still be using v2.0 (legacy format).

The purpose of this document is to provide a comparison between callback v2.0 and v3.0. Before reading this document, please log in to the console, select **Cloud Products** > **Video on Demand** > **[Callback Settings](https://console.cloud.tencent.com/vod/callback)**, and confirm on this page:
- If only **Callback URL** is visible, your normal callback is already in v3.0 by default, and you don't need to read this document.
- If both **v2.0 Callback URL** and **v3.0 Callback URL** are visible, you are using the normal callback v2.0, **so please continue reading below**.

>If you are still using the normal callback v2.0, you are recommended to gradually migrate the callback to v3.0, as the documentation for callback v2.0 will no longer be updated.

Below is the **table of comparison between callback v2.0 and v3.0**:

| Event Notification | v3.0 | v2.0 |
| -- | -- | -- |
| Video upload completion | [Link](https://intl.cloud.tencent.com/document/product/266/33950) | [Link](#NewFileUpload) | 
| Video pull from URL completion | [Link](https://intl.cloud.tencent.com/document/product/266/33951) | [Link](#PullComplete) | 
| Video deletion completion | [Link](https://intl.cloud.tencent.com/document/product/266/33952) | [Link](#FileDeleted) |  
| Task flow status change | [Link](https://intl.cloud.tencent.com/document/product/266/33953) | [Link](#ProcedureStateChanged) | 
| Video editing completion | [Link](https://intl.cloud.tencent.com/document/product/266/33954) | - | 
| Release on WeChat completion | [Link](https://intl.cloud.tencent.com/document/product/266/33955) | - | 
| Video transcoding completion | [Link](https://intl.cloud.tencent.com/document/product/266/33957) | [Link](#TranscodeComplete) | 
| Time point screencapturing completion | [Link](https://intl.cloud.tencent.com/document/product/266/33958) | [Link](#CreateSnapshotByTimeOffsetComplete) | 
| Image sprite generating completion | [Link](https://intl.cloud.tencent.com/document/product/266/33959) | [Link](#CreateImageSpriteComplete) | 
| Video clipping completion | [Link](https://intl.cloud.tencent.com/document/product/266/33960) | [Link](#ClipComplete) | 
| Video splicing completion | [Link](https://intl.cloud.tencent.com/document/product/266/33961) | [Link](#ConcatComplete) | 

## Table of v2.0 Callbacks
<span id="NewFileUpload"></span>
### Video upload completion
#### Parameter descriptions
| Parameter Name | Type | Description |
| -- | -- | -- |
| version | String | Callback version number, which is always `4.0`. |
| eventType | String | Callback type, which is always `NewFileUpload`. |
| data.fileId | String | Unique ID of a file. |
| data.fileName | String | File display name. |
| data.coverUrl | String | File cover address. |
| data.fileUrl  | String | File playback address. |
| data.author | String | Author information. |
| data.sourceType | String | File upload source. Valid values: Record (recorder); ClientUpload (upload from client); ServerUpload (upload from server). |
| data.sourceContext | String | Specifies the field for passthrough when uploading. This field currently can contain up to 256 bytes. |
| data.streamId | String | Stream ID, which is only used for upload from recorder. |
| data.procedureTaskId | String | If a specified process is performed after the video is uploaded, this parameter will be the process task ID. |
| data.transcodeTaskId | String | If transcoding is initiated after the video is uploaded, this parameter will be the transcoding task ID. |

#### Sample
```
{
	"version": "4.0",
	"eventType": "NewFileUpload",
	"data": {
		"fileId": "5285890784273533167",
		"fileName": "Animal World",
		"coverUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.jpg",
		"fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.flv",
		"transcodeTaskId": "transcode-0bee89b07a248e27c83fc3d5951213c1",
		"procedureTaskId": "125676836723-mango-fa2fdf6a0f850d673be119cf51a7603a",
		"sourceType": "Record",
		"sourceContext": "rtmp://54xx.livepush.myqcloud.com/live?bizid=54xx&record=mp4&xx",
		"author": "CCTV recording",
		"streamId": "54xx_45"
	}
}
```

<span id="PullComplete"></span>
### Video pull from URL completion
#### Parameter descriptions
| Parameter Name | Type | Description |
| -- | -- | -- |
| version | String | Callback version number, which is always `4.0`. |
| eventType | String | Callback type, which is always `PullComplete`. |
| data | Object | Specific callback data. |
| data.vodTaskId | String | Pull upload task ID. |
| data.status | Integer | Error code. 0: success; other values: failure. |
| data.message | String | Error message.  |
| data.fileId | String | Unique ID obtained after a splicing request is initiated. |
| data.fileUrl | String | URL obtained after video upload is completed. |
| data.transcodeTaskId | String | If transcoding is initiated after the video is uploaded, this parameter will be the transcoding task ID. |

#### Sample
```json
{
    "version":"4.0",
    "eventType":"PullComplete",
    "data":{
        "status":0,
        "message":"",
        "vodTaskId":"Pull-f5ac8127b3b6b85cdc13f237c6005d8",
        "fileId":"14508071098244959037",
        "fileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.flv",
        "transcodeTaskId":"transcode-0bee89b07a248e27c83fc3d5951213c1"
    }
}
```

<span id="FileDeleted"></span>
### Video deletion completion
#### Parameter descriptions
| Parameter Name | Type | Description |
| -- | -- | -- |
| version | String | Callback version number, which is always `4.0`. |
| eventType | String | Callback type, which is always `FileDeleted`. |
| data.status | Integer | Return value for a deletion. 0: success; other values: failure. |
| data.message | String | Error message for a deletion. |
| data.fileInfo | Array | Information of a deleted file. |
| data.fileInfo.n.fileId | String | ID of a deleted file. |

#### Sample
```json
{
    "version":"4.0",
    "eventType":"FileDeleted",
    "data":{
        "status":0,
        "message":"",
        "fileInfo":[
            {
                "fileId":"24961954183381008"
            }
        ]
    }
}
```

<span id="ProcedureStateChanged"></span>
### Task flow status change
#### Parameter descriptions
| Parameter Name | Type | Description |
| -- | -- | -- |
| version | String | Event notification version number, which is always `4.0`. |
| eventType | String | Event type, which is always `ProcedureStateChanged`. |
| data | Object | Specific callback data. |
| data.status | String | Task flow status. Valid values: PROCESSING, FINISH. |
| data.errCode | Integer | Error code. 0: success; other values: failure. |
| data.message | String | Error message. |
| data.fileId | String | File ID. |
| data.metaData | Object | Video metadata, which must be specified. For more information on this field, please see [metaData (Video Metadata)](#metadata.EF.BC.88.E8.A7.86.E9.A2.91.E5.85.83.E4.BF.A1.E6.81.AF.EF.BC.89). |
| data.contentReviewList | Array | List of content audit results. For more information on this field, please see [contentReviewList (Content Audit List)](#contentreviewlist.EF.BC.88.E5.86.85.E5.AE.B9.E5.AE.A1.E6.A0.B8.E5.88.97.E8.A1.A8.EF.BC.89). |
| data.aIAnalysisList | Array | List of intelligent analysis results. For more information on this field, please see [aIAnalysisList (Intelligent Analysis List)](#aianalysislist.EF.BC.88.E6.99.BA.E8.83.BD.E5.88.86.E6.9E.90.E5.88.97.E8.A1.A8.EF.BC.89). |
| data.drm | Object | File encryption information. This field exists only if you specify encryption in the [transcoding control parameters](https://intl.cloud.tencent.com/document/product/266/34125#transcode.EF.BC.88.E8.BD.AC.E7.A0.81.E6.8E.A7.E5.88.B6.E5.8F.82.E6.95.B0.EF.BC.89) when you initiate a task flow. For more information on this field, please see [drm (Video Encryption Information)](#drm.EF.BC.88.E8.A7.86.E9.A2.91.E5.8A.A0.E5.AF.86.E4.BF.A1.E6.81.AF.EF.BC.89). |
| data.processTaskList | Array | List of tasks contained in a task flow. For more information on this field, please see [processTaskList (Task List)](#processtasklist.EF.BC.88.E4.BB.BB.E5.8A.A1.E5.88.97.E8.A1.A8.EF.BC.89). |

##### metaData (video metadata)
| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| size | Integer | Video size in bytes. |
| container | String | Container type, such as M4A and MP4. |
| bitrate | Integer | Sum of the average bitrate of the video stream and that of the audio stream in kbps. |
| height | Integer | Maximum height value of a video stream in px. |
| width | Integer | Maximum width value of a video stream in px. |
| md5 | String | MD5 value of a video. |
| duration | Integer | Video duration in seconds. |
| rotate | Integer | Selected angle during video recording in degrees. |
| videoStreamList | Array | Video stream information. |
| videoStreamList.bitrate | Integer | Bitrate of a video stream in kbps. |
| videoStreamList.height | Integer | Height of a video stream in px. |
| videoStreamList.width | Integer | Width of a video stream in px. |
| videoStreamList.codec | String | Encoder of a video stream, such as H.264. |
| videoStreamList.fps | Integer | Frame rate in Hz. |
| audioStreamList | Array | Audio stream information. |
| audioStreamList.bitrate | Integer | Bitrate of an audio stream in kbps. |
| audioStreamList.samplingRate | Integer | Sample rate of an audio stream in Hz. |
| audioStreamList.codec | String | Encoder of an audio stream, such as AAC. |

##### drm (video encryption information)
| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| definition | Integer | Encryption template ID. |
| keySource | String | KMS type, which is always `VodBuildInKMS`. |
| getKeyUrl | String | URL for getting a decryption key. |
| edkList | Array | List of encrypted data keys. |

##### contentReviewList (content audit list)
List of content audit information. Currently, only [porn information detection](#porn.EF.BC.88.E9.89.B4.E9.BB.84.EF.BC.89) is supported.

##### Porn (porn information detection)
| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| taskType | String | Task type, which is always `Porn`. |
| status | String | Task status. Valid values: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | Error code. 0: success; other values: failure. Specifically, 30009: failure due to source file exception; 30010: system failure or unknown failure. |
| message | String | Error message. |
| input | Object | Input information of a task. |
| input.definition | Integer | Porn information detection template ID. |
| output | Object | Output information of a task, which exists only if the task succeeds. |
| output.confidence | Float | Score of the detected porn information in a video. Value range: 0–100. |
| output.suggestion | String | Suggestion for the detected porn information. Valid values: pass, review, block. |
| output.segments | Array | Video segment that contains the detected porn information. |
| output.segments.startTimeOffset | Float | Start time offset of a suspected segment in seconds. |
| output.segments.endTimeOffset | Float | End time offset of a suspected segment in seconds. |
| output.segments.confidence | Float | Score of a suspected porn segment. |
| output.segments.suggestion | Float | Suggestion for porn information detection of a suspected segment. Valid values: pass, review, block. |
| output.segments.url | String | URL of a suspected image (which will not be permanently stored and will expire after a certain amount of time). |
| output.segments.picUrlExpireTimeStamp | Integer | Expiration time of a suspected image URL in the format of Unix timestamp. |

##### aIAnalysisList (intelligent analysis list)
List of intelligent analysis information. Currently, the following types are available:
- [Classification (intelligent categorization)](#classification.EF.BC.88.E6.99.BA.E8.83.BD.E5.88.86.E7.B1.BB.EF.BC.89)
- [Tag (intelligent tagging)](#tag.EF.BC.88.E6.99.BA.E8.83.BD.E6.A0.87.E7.AD.BE.EF.BC.89)

##### Classification (intelligent categorization)
| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| taskType | String | Task type, which is always `Classification`. |
| status | String | Task status. Valid values: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | Error code. 0: success; other values: failure. Specifically, `30009`: failure due to source file exception; `30010`: system failure or unknown failure. |
| message | String | Error message. |
| input | Object | Input information of a task. |
| input.definition | Integer | Intelligent categorization template ID. |
| output | Object | Output information of a task, which exists only if the task succeeds. |
| output.classifications | Array | Category information list. |
| output.classifications.classification | String | Category name. |
| output.classifications.confidence | Float | Categorization confidence. |

##### Tag (intelligent tagging)
| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| taskType | String | Task type, which is always `Tag`. |
| status | String | Task status. Valid values: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | Error code. 0: success; other values: failure. Specifically, `30009`: failure due to source file exception; `30010`: system failure or unknown failure. |
| message | String | Error message. |
| input | Object | Input information of a task. |
| input.definition | Integer | Intelligent tagging template ID. |
| output | Object | Output information of a task, which exists only if the task succeeds. |
| output.tags | Array | Array | Tag information list. |
| output.tags.tag | String | Tag name. |
| output.tags.confidence | Float | Tagging confidence. |

##### processTaskList (task list)
List of task information. Currently, the following types are available:
- [Transcode (transcoding task)](#trancode.EF.BC.88.E8.BD.AC.E7.A0.81.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [AnimatedGraphics (animated image generating task)](#animatedgraphics.EF.BC.88.E8.BD.AC.E5.8A.A8.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [SampleSnapshot (sampled screencapturing task)](#samplesnapshot.EF.BC.88.E9.87.87.E6.A0.B7.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [CoverBySnapshot (cover generating task)](#coverbysnapshot.EF.BC.88.E6.88.AA.E5.9B.BE.E5.9B.BE.E7.89.87.E4.BD.9C.E4.B8.BA.E8.A7.86.E9.A2.91.E5.B0.81.E9.9D.A2.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [SnapshotByTimeOffset (time point screencapturing task)](#snapshotbytimeoffset.EF.BC.88.E6.8C.89.E6.97.B6.E9.97.B4.E7.82.B9.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [PullFile (video file pulling task)](/document/product/266/7817)
- [ImageSprites (image sprite generating task)](#imagesprites.EF.BC.88.E9.9B.AA.E7.A2.A7.E5.9B.BE.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)


##### Transcode (transcoding task)
| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| taskType | String | Task type, which is always `Transcode`. |
| status | String | Task status. Valid values: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | Error code. 0: success; other values: failure. Specifically, `30009`: failure due to source file exception; `30010`: system failure or unknown failure. |
| message | String | Error message. |
| input | Object | Input information of a task. |
| input.definition | Integer | Transcoding template ID. |
| input.watermark | Integer | Whether to set a watermark. 1: yes; 0: no. This depends on your transcoding configuration. |
| input.mosaicList | Array | List of blur masks, where an element is the information of a single blur mask. |
| input.mosaicList.width | String | Blur width. |
| input.mosaicList.height | String | Blur height. |
| input.mosaicList.left | String | Horizontal position of the top-left corner of a blur in a video. |
| input.mosaicList.top | String | Vertical position of the top-left corner of a blur in a video. |
| input.mosaicList.startTimeOffset | Float | Start time of a blur in a video. |
| input.mosaicList.endTimeOffset | Float | End time of a blur in a video. |
| output | Object | Output information of a task, which exists only if the task succeeds. |
| output.url | String | Video URL. |
| output.size | Integer | Video size in bytes. |
| output.container | String | Container type, such as M4A and MP4. |
| output.bitrate | Integer | Sum of the bitrate of the video stream and that of the audio stream in kbps. |
| output.height | Integer | Maximum height value of a video stream in px. |
| output.width | Integer | Maximum width value of a video stream in px. |
| output.md5 | String | MD5 value of a video. |
| output.duration | Integer | Video duration in seconds. |
| output.videoStreamList | Array | Video stream information, where the element field is the same as the `videoStreamList` in the metadata. |
| output.audioStreamList | Array | Audio stream information, where the element field is the same as the `audioStreamList` in the metadata. |

#### AnimatedGraphics (animated image generating task)
| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| taskType | String | Task type, which is always `AnimatedGraphics`. |
| status | String | Task status. Valid values: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | Error code. 0: success; other values: failure. Specifically, `30009`: failure due to source file exception; `30010`: system failure or unknown failure. |
| message | String | Error message. |
| input | Object | Input information of a task. |
| input.definition | Integer | Animated image generating template ID. |
| input.startTime | Integer | Start time of an animated image in the video in seconds. |
| input.endTime | Integer | End time of an animated image in the video in seconds. |
| output | Object | Output information of a task, which exists only if the task succeeds. |
| output.url | String | Animated image URL. |
| output.container | String | Animated image type. Valid values: GIF, WEBP. |
| output.fps | Integer | Frame rate of an animated image in fps. |
| output.height | Integer | Height of an animated image in px. |
| output.width | Integer | Width of an animated image in px. |

#### SampleSnapshot (sampled screencapturing task)
| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| taskType | String | Task type, which is always `SampleSnapshot`. |
| status | String | Task status. Valid values: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | Error code. 0: success; other values: failure. Specifically, `30009`: failure due to source file exception; `30010`: system failure or unknown failure. |
| message | String | Error message. |
| input | Object | Input information of a task. |
| input.definition | Integer | Sampled screencapturing template ID. |
| input.watermarkDefinition | Array | List of watermarking template IDs, which is an array of integers. |
| output | Object | Output information of a task, which exists only if the task succeeds. |
| output.imageUrls | Array | List of URLs of the generated screenshots, which is an array of strings. |

#### SnapshotByTimeOffset (time point screencapturing task)
| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| taskType | String | Task type, which is always `SnapshotByTimeOffset`. |
| status | String | Task status. Valid values: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | Error code. 0: success; other values: failure. Specifically, `30009`: failure due to source file exception; `30010`: system failure or unknown failure. |
| message | String | Error message. |
| input | Object | Input information of a task. |
| input.definition | Integer | Time point screencapturing template ID. |
| input.timeOffset | Array | Screencapturing time offsets in milliseconds, which is an array of integers. |
| input.watermarkDefinition | Array | List of watermarking template IDs, which is an array of integers. |
| output | Object | Output information of a task, which exists only if the task succeeds. |
| output.imgInfo | Array | Information list of the generated screenshots. |
| output.imgInfo.timeOffset | Integer | Time offset of a screenshot in milliseconds. |
| output.imgInfo.url | String | Screenshot URL. |

#### CoverBySnapshot (cover generating task)

| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| taskType | String | Task type, which is always `CoverBySnapshot`. |
| status | String | Task status. Valid values: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | Error code. 0: success; other values: failure. Specifically, `30009`: failure due to source file exception; `30010`: system failure or unknown failure. |
| message | String | Error message. |
| input | Object | Input information of a task. |
| input.definition | Integer | Sampled screencapturing template ID. |
| input.positionType | String | Screencapturing mode. Time: screencapture by time point. Percent: screencapture by percentage. |
| input.position | Integer | Screencapturing position. For time point screencapturing, this means to take a screenshot at the specified time point (in seconds) and use it as the cover. For percentage screencapturing, this means to take a screenshot at the specified percentage of the video duration and use it as the cover. |
| input.watermarkDefinition | Array | List of watermarking template IDs, which is an array of integers. |
| output | Object | Output information of a task, which exists only if the task succeeds. |
| output.imageUrl | Array | URL of the screenshot as cover. |

#### PullFile (video file pulling task)
| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| taskType | String | Task type, which is always `PullFile`. |
| status | String | Task status. Valid values: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | Error code. 0: success; other values: failure. |
| message | String | Error message. |
| input | Object | Input information of a task. |
| input.url | String | URL of a video to be pulled. |
| input.fileName | String | Video file name. |
| input.md5 | Integer | MD5 value of a video file. |
| output | Object | Output information of a task, which exists only if the task succeeds. |
| output.fileId | String | Video file ID. |
| output.fileSize | String | Video file size. |
| output.url | String | Video file playback address. |

#### ImageSprites (image sprite generating task)
| **Parameter Name** | **Type** | **Description** |
| -- | -- | -- |
| taskType | String | Task type, which is always `ImageSprites`. |
| status | String | Task status. Valid values: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | Error code. 0: success; other values: failure. |
| message | String | Error message. |
| input | Object | Input information of a task, which exists only if the task succeeds. |
| input.definition | Integer | Image sprite generating template ID. |
| output | Object | Output information of a task. |
| output.totalCount | Integer | Total number of subimages in an image sprite. |
| output.urlList | Array | List of URLs of the generated image sprites, which is an array of strings. |
| output.webVttUrl | String | Address of the WebVtt file for the position-time relationship among subimages in an image sprite. |

#### Sample
```json
{
    "version":"4.0",
    "eventType":"ProcedureStateChanged",
    "data":{
        "vodTaskId":"125676836723-xxx-25f5aac63",
        "status":"PROCESSING",
        "message":"",
        "errCode":0,
        "fileId":"14508071098244959037",
        "metaData":{
            "size":10556,
            "container":"m4a",
            "bitrate":246035,
            "height":480,
            "width":640,
            "md5":"b3ae6ed07d9bf4efeeb94ed2d37ff3e3",
            "duration":3601,
            "videoStreamList":[
                {
                    "bitrate":246000,
                    "height":480,
                    "width":640,
                    "codec":"h264",
                    "fps":22
                }
            ],
            "audioStreamList":[
                {
                    "codec":"aac",
                    "samplingRate":44100,
                    "bitrate":35
                }
            ]
        },
        "drm":{
            "definition":10,
            "getKeyUrl":"https://123.xxx.com/getkey",
            "keySource":"VodBuildInKMS",
            "edkList":[
                "232abc30"
            ]
        },
        "contentReviewList":[
            {
                "taskType":"Porn",
                "status":"SUCCESS",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":10
                },
                "output":{
                    "confidence":98,
                    "suggestion":"block",
                    "segments":[
                        {
                            "startTimeOffset":20,
                            "endTimeOffset":120,
                            "confidence":98,
                            "suggestion":"block",
                            "url":"http://125676836723.vod2.myqcluod.com/xxx/xxx/xx.jpg",
                            "picUrlExpireTimeStamp":1530005146
                        },
                        {
                            "startTimeOffset":120,
                            "endTimeOffset":130,
                            "confidence":54,
                            "suggestion":"review",
                            "url":"http://125676836723.vod2.myqcluod.com/xxx/xxx/xx.jpg",
                            "picUrlExpireTimeStamp":1530005146
                        }
                    ]
                }
            }
        ],
        "processTaskList":[
            {
                "taskType":"Transcode",
                "status":"PROCESSING",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":10,
                    "watermark":1
                }
            },
            {
                "taskType":"Transcode",
                "status":"SUCCESS",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":20,
                    "watermark":1
                },
                "output":{
                    "url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f20.mp4",
                    "size":10556,
                    "container":"m4a",
                    "md5":"b3ae6ed07d9bf4efeeb94ed2d37ff3e3",
                    "bitrate":246035,
                    "height":480,
                    "width":640,
                    "duration":3601,
                    "videoStreamList":[
                        {
                            "bitrate":246000,
                            "height":480,
                            "width":640,
                            "codec":"h264",
                            "fps":20
                        }
                    ],
                    "audioStreamList":[
                        {
                            "codec":"aac",
                            "samplingRate":44100,
                            "bitrate":35
                        }
                    ]
                }
            },
            {
                "taskType":"SampleSnapshot",
                "status":"SUCCESS",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":10
                },
                "output":{
                    "imageUrls":[
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/shotup/xx1.png",
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/shotup/xx2.png",
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/shotup/xx3.png"
                    ]
                }
            }
        ]
    }
}
```

<span id="TranscodeComplete"></span>
### Video transcoding completion
#### Parameter descriptions
| Parameter Name | Type | Description |
| -- | -- | -- |
| version | String | Event notification version number, which is always `4.0`. |
| eventType | String | Event type, which is always `TranscodeComplete`. |
| data | Object | Specific callback data. |
| data.status | Integer | Error code. 0: success; other values: failure. |
| data.message | String | Error message.  |
| data.fileId | String | Transcoded file ID. |
| data.vodTaskId | String | Transcoding task ID. |

#### Sample
```json
{
    "version": "4.0",
    "eventType": "TranscodeComplete",
    "data": {
        "status": 0,
        "message": "",
        "vodTaskId": "Transcode-1edb7eb88a599d05abe451cfc541cfbd",
        "fileId": "14508071098244931831",
        "fileName": "Animal World",
        "duration": 599,
        "coverUrl": "http://125676836723.vod2.myqcloud.com/0/xxx/640",
        "playSet": [
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                "definition": 0,
                "vbitrate": 246000,
                "vheight": 480,
                "vwidth": 640
            },
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f10.mp4",
                "definition": 10,
                "vbitrate": 149193,
                "vheight": 240,
                "vwidth": 320
            },
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f20.mp4",
                "definition": 20,
                "vbitrate": 297656,
                "vheight": 480,
                "vwidth": 640
            },
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f30.mp4",
                "definition": 30,
                "vbitrate": 899976,
                "vheight": 960,
                "vwidth": 1280
            }
        ]
    }
}
```

<span id="CreateSnapshotByTimeOffsetComplete"></span>
### Time point screencapturing completion
#### Parameter descriptions
| Parameter Name | Type | Description |
| -- | -- | -- |
| version | String | Callback version number, which is always `4.0`. |
| eventType | String | Callback type, which is always `CreateSnapshotByTimeOffsetComplete`. |
| data | Object | Specific callback data. |
| data.vodTaskId | String |  Time point screencapturing task ID. |
| data.fileId | String | FileId of a specified time point screenshot. |
| data.definition | Integer | Time point screenshot specification. For more information, please see [Parameter Template for Time Point Screencapturing](https://intl.cloud.tencent.com/document/product/266/33940#.E6.97.B6.E9.97.B4.E7.82.B9.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF). |
| data.picInfo | Array | Information of a specified time point screenshot. |

Each element in the `data.picInfo` array is an `Object`, and the meanings of the parameters are as follows:

| Parameter Name | Type | Description |
| -- | -- | -- |
| timeOffset | Integer | Specific time point of a screenshot in milliseconds. |
| url | String | Screenshot file URL. |
| status | Integer | Error code. 0: success; other values: failure. |

#### Sample
```json
{
    "version": "4.0",
    "eventType": "CreateSnapshotByTimeOffsetComplete",
    "data": {
        "vodTaskId": "CreateSnapshotByTimeOffset-1edb7eb88a599d05abe451cfc541cfbd",
        "fileId": "14508071098244929440",
        "definition": 10,
        "picInfo": [
            {
                "status": 0,
                "timeOffset": 10000,
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/1.png"
            },
            {
                "status": 0,
                "timeOffset": 20000,
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/2.png"
            }
        ]
    }
}
```

<span id="CreateImageSpriteComplete"></span>
### Image sprite generating completion
#### Parameter descriptions
| Parameter Name | Type | Description |
| -- | -- | -- |
| version | String | Callback version number, which is always `4.0`. |
| eventType | String | Callback type, which is always `CreateImageSpriteComplete`. |
| data | Object | Specific callback data. |
| data.status | Integer | Error code. 0: success; other values: failure. |
| data.message | String | Error message. |
| data.vodTaskId | String | Image sprite generating task ID. |
| data.fileId | String | FileId of a generated image sprite. |
| data.definition | Integer | Image sprite specification. For more information, please see [Image Sprite Generating Template](https://intl.cloud.tencent.com/document/product/266/33940#.E9.9B.AA.E7.A2.A7.E5.9B.BE.E6.A8.A1.E6.9D.BF). |
| data.totalCount | Integer | Total number of subimages in an image sprite. |
| data.imageSpriteUrl | Array | Information of a generated image sprite. |
| data.webVttUrl | String | Address of the WebVtt file for the position-time relationship among subimages in an image sprite. |

#### Sample
```json
{
    "version":"4.0",
    "eventType":"CreateImageSpriteComplete",
    "data":{
        "status":0,
        "message":"",
        "vodTaskId":"CreateImageSprite-1edb7eb88a599d05abe451cfc541cfbd",
        "fileId":"14508071098244929440",
        "definition":10,
        "totalCount":106,
        "imageSpriteUrl":[
            "http://125676836723.vod2.myqcloud.com/xxx/xxx/1.png",
            "http://125676836723.vod2.myqcloud.com/xxx/xxx/2.png"
        ],
        "webVttUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.vtt"
    }
}
```

<span id="ClipComplete"></span>
### Video clipping completion
#### Parameter descriptions
| Parameter Name | Type | Description |
| -- | -- | -- |
| version | String | Callback version number, which is always `4.0`. |
| eventType | String | Callback type, which is always `ClipComplete`. |
| data | Object | Specific callback data. |
| data.vodTaskId | String | Clipping task ID. |
| data.srcFileId | String | FileId of a source file for a clipping task. |
| data.fileInfo | Object | Information of an output video file. |

The specific meanings of the parameters in `data.fileInfo` are as follows:

| Parameter Name | Type | Description |
|---------|---------|---------|
| fileType | String | Type of a clipped file. |
| status | Integer | Error code for this type of files. 0: success; other values: failure. |
| message | String | Error message. |
| fileType | String | fileId of a clipped file. |
| fileUrl | String | URL of a clipped file. |

#### Sample
```json
{
    "version": "4.0",
    "eventType": "ClipComplete",
    "data": {
        "vodTaskId": "clipVideo-0a78cf44c4285026a4c",
        "srcFileId": "16092504232103571364",
        "fileInfo": {
            "fileType": "mp4",
            "status": 0,
            "message": "",
            "fileId": "14508071098244929440",
            "fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
        }
    }
}
```


<span id="ConcatComplete"></span>
### Video splicing completion
#### Parameter descriptions
| Parameter Name | Type | Description |
|---------|---------|---------|
| version | String | Callback version number, which is always `4.0`. |
| eventType | String | Callback type, which is always `ConcatComplete`. |
| data | Object | Specific callback data. |
| data.vodTaskId | String | Splicing task ID. |
| data.fileInfo | Array | Information of a spliced video file. |

Each element in the `data.fileInfo` array is an `Object`, and the meanings of the parameters are as follows:

| Parameter Name | Type | Description |
|---------|---------|---------|
| fileType | String | Type of a spliced file. |
| status | Integer | Task execution result. 0: success; -1 or 4: failure. |
| message | String | Error message. |
| fileId | String | FileId of a spliced file. |
| fileUrl | String | URL of a spliced file. |

#### Sample
```json
{
    "version": "4.0",
    "eventType": "ConcatComplete",
    "data": {
        "vodTaskId": "Concat-1edb7eb88a599d05abe451cfc541cfbd",
        "fileInfo": [
            {
                "fileType": "m3u8",
                "status": 0,
                "message": "",
                "fileId": "14508071098244931831",
                "fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/playlist.f6.m3u8"
            },
            {
                "fileType": "mp4",
                "status": 0,
                "message": "",
                "fileId": "14508071098244929440",
                "fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
            }
        ]
    }
}
```
