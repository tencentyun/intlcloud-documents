
云点播在2019年对事件通知的格式进行了改版：
- 改版后新注册用户的事件通知格式为3.0版本（现行格式）。
- 改版前注册的部分用户可能仍然在使用2.0版本（历史格式）。

本文的目的是提供2.0格式和3.0格式事件通知的对照。阅读本文前，请先登录控制台，选择【云产品】>【云点播】>[【回调设置】](https://console.cloud.tencent.com/vod/callback)，在该页面确认：
- 如果仅可见【回调 URL】，说明您的普通回调默认已是3.0格式的，无需阅读本文。
- 如果同时可见【2.0回调 URL】和【3.0回调 URL】，说明您正在使用2.0格式的普通回调，**请继续阅读下面的内容**。

>!如果您仍在使用2.0格式的普通回调，建议您将使用的事件通知版本逐步迁移到3.0格式，2.0格式事件通知的文档将不再维护。

**3.0格式和2.0格式的事件通知对照表**如下所示：

| 事件通知 | 3.0格式 | 2.0格式 |
| -- | -- | -- |
| 视频上传完成 | [链接](https://intl.cloud.tencent.com/document/product/266/33950) | [链接](#NewFileUpload) | 
| URL 拉取视频上传完成 | [链接](https://intl.cloud.tencent.com/document/product/266/33951) | [链接](#PullComplete) | 
| 视频删除完成 | [链接](https://intl.cloud.tencent.com/document/product/266/33952) | [链接](#FileDeleted) |  
| 任务流状态变更 | [链接](https://intl.cloud.tencent.com/document/product/266/33953) | [链接](#ProcedureStateChanged) | 
| 视频编辑完成 | [链接](https://intl.cloud.tencent.com/document/product/266/33954) | - | 
| 视频转码完成 | [链接](https://intl.cloud.tencent.com/document/product/266/33957) | [链接](#TranscodeComplete) | 
| 指定时间点截图完成 | [链接](https://intl.cloud.tencent.com/document/product/266/33958) | [链接](#CreateSnapshotByTimeOffsetComplete) | 
| 视频截取雪碧图完成 | [链接](https://intl.cloud.tencent.com/document/product/266/33959) | [链接](#CreateImageSpriteComplete) | 
| 视频剪辑完成 | [链接](https://intl.cloud.tencent.com/document/product/266/33960) | [链接](#ClipComplete) | 
| 视频拼接完成 | [链接](https://intl.cloud.tencent.com/document/product/266/33961) | [链接](#ConcatComplete) | 

## 2.0格式事件通知列表
<span id="NewFileUpload"></span>
### 视频上传完成
#### 参数说明
| 参数名称 | 类型 | 说明 |
| -- | -- | -- |
| version | String | 回调版本号，固定为`4.0`。 |
| eventType | String | 回调类型，固定为`NewFileUpload`。 |
| data.fileId | String | 文件唯一 ID。 |
| data.fileName | String | 文件展示名称。 |
| data.coverUrl | String | 文件封面地址。 |
| data.fileUrl  | String | 文件播放地址。 |
| data.author | String | 作者信息。 |
| data.sourceType | String | 文件的上传来源。目前有 Record：录制；ClientUpload：客户端上传；ServerUpload：服务端上传。 |
| data.sourceContext | String | 上传时指定透传的字段，该字段目前最多256字节。 |
| data.streamId | String | 推流 ID，录制上传特有。 |
| data.procedureTaskId | String | 该视频上传之后进行了指定流程，则该参数为流程任务 ID。 |
| data.transcodeTaskId | String | 如果该视频上传之后发起了转码，则该参数为转码任务 ID。 |

#### 示例
```
{
	"version": "4.0",
	"eventType": "NewFileUpload",
	"data": {
		"fileId": "5285890784273533167",
		"fileName": "动物世界",
		"coverUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.jpg",
		"fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.flv",
		"transcodeTaskId": "transcode-0bee89b07a248e27c83fc3d5951213c1",
		"procedureTaskId": "125676836723-mango-fa2fdf6a0f850d673be119cf51a7603a",
		"sourceType": "Record",
		"sourceContext": "rtmp://54xx.livepush.myqcloud.com/live?bizid=54xx&record=mp4&xx",
		"author": "CCTV录制",
		"streamId": "54xx_45"
	}
}
```

<span id="PullComplete"></span>
### URL 拉取视频上传完成
#### 参数说明
| 参数名称 | 类型 | 说明 |
| -- | -- | -- |
| version | String | 回调版本号，固定为`4.0`。 |
| eventType | String | 回调类型，固定为`PullComplete`。 |
| data | Object | 具体回调数据。 |
| data.vodTaskId | String | 拉取上传任务 ID。 |
| data.status | Integer | 错误码。0：成功。其他值：失败。 |
| data.message | String | 错误信息。  |
| data.fileId | String | 发起拼接请求后获取到的唯一 ID。 |
| data.fileUrl | String | 视频上传完成之后的 URL。 |
| data.transcodeTaskId | String | 如果该视频上传之后发起了转码，则该参数为转码任务 ID。 |

#### 示例
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
### 视频删除完成
#### 参数说明
| 参数名称 | 类型 | 说明 |
| -- | -- | -- |
| version | String | 回调版本号，固定为`4.0`。 |
| eventType | String | 回调类型，固定为`FileDeleted`。 |
| data.status | Integer | 删除的返回值，0：成功；其他：失败。 |
| data.message | String | 删除的错误信息。 |
| data.fileInfo | Array | 被删除的文件信息。 |
| data.fileInfo.n.fileId | String | 被删除的文件 ID。 |

#### 示例
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
### 任务流状态变更
#### 参数说明
| 参数名称 | 类型 | 说明 |
| -- | -- | -- |
| version | String | 事件通知版本号，固定为`4.0`。 |
| eventType | String | 事件类型，固定为`ProcedureStateChanged`。 |
| data | Object | 具体回调数据。 |
| data.status | String | 任务流状态，有 PROCESSING 和 FINISH。 |
| data.errCode | Integer | 错误码。0：成功；其他值：失败。 |
| data.message | String | 错误信息。 |
| data.fileId | String | 文件 ID。 |
| data.metaData | Object | 视频元信息，该字段一定存在，字段信息参见 [metaData（视频元信息）](#metadata.EF.BC.88.E8.A7.86.E9.A2.91.E5.85.83.E4.BF.A1.E6.81.AF.EF.BC.89)。 |
| data.contentReviewList | Array | 内容审核结果列表，字段信息参见 [contentReviewList（内容审核列表）](#contentreviewlist.EF.BC.88.E5.86.85.E5.AE.B9.E5.AE.A1.E6.A0.B8.E5.88.97.E8.A1.A8.EF.BC.89)。 |
| data.aIAnalysisList | Array | 智能分析结果列表，字段信息参见 [aIAnalysisList（智能分析列表）](#aianalysislist.EF.BC.88.E6.99.BA.E8.83.BD.E5.88.86.E6.9E.90.E5.88.97.E8.A1.A8.EF.BC.89)。 |
| data.drm | Object | 文件加密信息，用户在发起任务流时在 [转码控制参数](https://intl.cloud.tencent.com/document/product/266/34125#transcode.EF.BC.88.E8.BD.AC.E7.A0.81.E6.8E.A7.E5.88.B6.E5.8F.82.E6.95.B0.EF.BC.89) 指定了加密，该字段才存在。 字段信息参见 [drm（视频加密信息）](#drm.EF.BC.88.E8.A7.86.E9.A2.91.E5.8A.A0.E5.AF.86.E4.BF.A1.E6.81.AF.EF.BC.89)。 |
| data.processTaskList | Array | 任务流包含的任务列表，字段信息参见 [processTaskList（任务列表）](#processtasklist.EF.BC.88.E4.BB.BB.E5.8A.A1.E5.88.97.E8.A1.A8.EF.BC.89)。 |

##### metaData（视频元信息）
| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| size | Integer | 视频大小。单位：字节。 |
| container | String | 容器类型，例如 M4A 和 MP4 等。 |
| bitrate | Integer | 视频流码率平均值与音频流码率平均值之和。单位：kbps。 |
| height | Integer | 视频流高度的最大值。单位：px。 |
| width | Integer | 视频流宽度的最大值。单位：px。 |
| md5 | String | 视频的 MD5 值。 |
| duration | Integer | 视频时长。单位：秒。 |
| rotate | Integer | 视频拍摄时的选择角度。单位：度。 |
| videoStreamList | Array | 视频流信息。 |
| videoStreamList.bitrate | Integer | 视频流的码率，单位：kbps。 |
| videoStreamList.height | Integer | 视频流的高度，单位：px。 |
| videoStreamList.width | Integer | 视频流的宽度，单位：px。 |
| videoStreamList.codec | String | 视频流的编码格式，例如 H.264。 |
| videoStreamList.fps | Integer | 帧率，单位：Hz。 |
| audioStreamList | Array | 音频流信息。 |
| audioStreamList.bitrate | Integer | 音频流的码率。 单位：kbps。 |
| audioStreamList.samplingRate | Integer | 音频流的采样率。 单位：Hz。 |
| audioStreamList.codec | String | 音频流的编码格式，例如 AAC。 |

##### drm（视频加密信息）
| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| definition | Integer | 加密模板 ID。 |
| keySource | String | KMS 的类型，固定为`VodBuildInKMS`。 |
| getKeyUrl | String | 获取解密密钥的 URL。 |
| edkList | Array | 加密后的数据密钥列表。 |

##### contentReviewList（内容审核列表）
内容审核信息列表，目前仅支持 [Porn（鉴黄）](#porn.EF.BC.88.E9.89.B4.E9.BB.84.EF.BC.89)。

##### Porn（鉴黄）
| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| taskType | String | 任务类型，固定为`Porn`。 |
| status | String | 任务状态，有 PROCESSING、SUCCESS 和 FAIL。 |
| errCode | Integer | 错误码。0：成功。其他值：失败，其中30009为原文件异常失败，30010为系统失败或未知。 |
| message | String | 错误信息。 |
| input | Object | 任务的输入信息。 |
| input.definition | Integer | 鉴黄模板 ID。 |
| output | Object | 任务的输出信息，任务成功时会有该字段，失败则没有。 |
| output.confidence | Float | 视频鉴黄评分，分值为0到100。 |
| output.suggestion | String | 鉴黄结果建议，有 pass、review 和 block。 |
| output.segments | Array | 有涉黄嫌疑的视频片段。 |
| output.segments.startTimeOffset | Float | 嫌疑片段起始的偏移时间，单位秒。 |
| output.segments.endTimeOffset | Float | 嫌疑片段结束的偏移时间，单位秒。 |
| output.segments.confidence | Float | 嫌疑片段涉黄分数。 |
| output.segments.suggestion | Float | 嫌疑片段鉴黄结果建议，有 pass、review 和 block。 |
| output.segments.url | String | 涉黄嫌疑图片 URL（图片不会永久存储，在一段时间后失效）。 |
| output.segments.picUrlExpireTimeStamp | Integer | 涉黄嫌疑图片 URL 失效时间（Unix 时间戳）。 |

##### aIAnalysisList（智能分析列表）
智能分析信息列表，目前有以下种类：
- [Classification（智能分类）](#classification.EF.BC.88.E6.99.BA.E8.83.BD.E5.88.86.E7.B1.BB.EF.BC.89)
- [Tag（智能标签）](#tag.EF.BC.88.E6.99.BA.E8.83.BD.E6.A0.87.E7.AD.BE.EF.BC.89)

##### Classification（智能分类）
| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| taskType | String | 任务类型，固定为`Classification`。 |
| status | String | 任务状态，有 PROCESSING、SUCCESS 和 FAIL。 |
| errCode | Integer | 错误码。0：成功；其他值：失败，其中`30009`为原文件异常失败，`30010`为系统失败或未知。 |
| message | String | 错误信息。 |
| input | Object | 任务的输入信息。 |
| input.definition | Integer | 智能分类模板 ID。 |
| output | Object | 任务的输出信息，任务成功时会有该字段，失败则没有。 |
| output.classifications | Array | 分类信息列表。 |
| output.classifications.classification | String | 分类类别名称。 |
| output.classifications.confidence | Float | 分类的可信度。 |

##### Tag（智能标签）
| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| taskType | String | 任务类型，固定为`Tag`。 |
| status | String | 任务状态，有 PROCESSING、SUCCESS 和 FAIL。 |
| errCode | Integer | 错误码。0：成功；其他值：失败，其中`30009`为原文件异常失败，`30010`为系统失败或未知。 |
| message | String | 错误信息。 |
| input | Object | 任务的输入信息。 |
| input.definition | Integer | 智能标签模板 ID。 |
| output | Object | 任务的输出信息，任务成功时会有该字段，失败则没有。 |
| output.tags | Array | 标签信息列表。 |
| output.tags.tag | String | 标签名。 |
| output.tags.confidence | Float | 标签的可信度。 |

##### processTaskList（任务列表）
任务信息列表，目前有以下几种：
- [Trancode（转码任务）](#trancode.EF.BC.88.E8.BD.AC.E7.A0.81.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [AnimatedGraphics（转动图任务）](#animatedgraphics.EF.BC.88.E8.BD.AC.E5.8A.A8.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [SampleSnapshot（采样截图任务）](#samplesnapshot.EF.BC.88.E9.87.87.E6.A0.B7.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [CoverBySnapshot（截图图片作为视频封面任务）](#coverbysnapshot.EF.BC.88.E6.88.AA.E5.9B.BE.E5.9B.BE.E7.89.87.E4.BD.9C.E4.B8.BA.E8.A7.86.E9.A2.91.E5.B0.81.E9.9D.A2.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [SnapshotByTimeOffset（按时间点截图任务）](#snapshotbytimeoffset.EF.BC.88.E6.8C.89.E6.97.B6.E9.97.B4.E7.82.B9.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [ImageSprites（雪碧图截图任务）](#imagesprites.EF.BC.88.E9.9B.AA.E7.A2.A7.E5.9B.BE.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)


##### Trancode（转码任务）
| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| taskType | String | 任务类型，固定为`Transcode`。 |
| status | String | 任务状态，有 PROCESSING、SUCCESS 和 FAIL。 |
| errCode | Integer | 错误码。0：成功；其他值：失败，其中`30009`为原文件异常失败，`30010`为系统失败或未知。 |
| message | String | 错误信息。 |
| input | Object | 任务的输入信息。 |
| input.definition | Integer | 转码模板 ID。 |
| input.watermark | Integer | 是否设置水印，1为设置，0为没设置。 是否设置取决于用户转码配置。 |
| input.mosaicList | Array | 马赛克遮标列表，元素是单个遮标的马赛克信息。 |
| input.mosaicList.width | String | 马赛克的宽度。 |
| input.mosaicList.height | String | 马赛克的高度。 |
| input.mosaicList.left | String | 马赛克的左上角在视频中的水平位置。 |
| input.mosaicList.top | String | 马赛克的左上角在视频中的垂直位置。 |
| input.mosaicList.startTimeOffset | Float | 马赛克在视频中的开始时间。 |
| input.mosaicList.endTimeOffset | Float | 马赛克在视频中的结束时间。 |
| output | Object | 任务的输出信息，任务成功时会有该字段，失败则没有。 |
| output.url | String | 视频 URL。 |
| output.size | Integer | 视频大小。单位：字节。 |
| output.container | String | 容器类型，例如 M4A 和 MP4 等。 |
| output.bitrate | Integer | 视频流码率和音频流码率之和，单位：kbps。 |
| output.height | Integer | 视频流高度的最大值。单位：px。 |
| output.width | Integer | 视频流宽度的最大值。单位：px。 |
| output.md5 | String | 视频的 MD5 值。 |
| output.duration | Integer | 视频时长。单位：秒。 |
| output.videoStreamList | Array | 视频流信息，元素字段和元信息中 videoStreamList 相同。 |
| output.audioStreamList | Array | 音频流信息，元素字段和元信息中 audioStreamList 相同。 |

#### AnimatedGraphics（转动图任务）
| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| taskType | String | 任务类型，固定为`AnimatedGraphics`。 |
| status | String | 任务状态，有 PROCESSING、SUCCESS 和 FAIL。 |
| errCode | Integer | 错误码。0：成功；其他值：失败，其中`30009`为原文件异常失败，`30010`为系统失败或未知。 |
| message | String | 错误信息。 |
| input | Object | 任务的输入信息。 |
| input.definition | Integer | 转动图模板 ID。 |
| input.startTime | Integer | 动图在视频中的起始时间。单位：秒。 |
| input.endTime | Integer | 动图在视频中的结束时间。单位：秒。 |
| output | Object | 任务的输出信息，任务成功时会有该字段，失败则没有。 |
| output.url | String | 动图 URL。 |
| output.container | String | 动图类型，有 GIF 和 WEBP。 |
| output.fps | Integer | 动图帧率。单位：fps。 |
| output.height | Integer | 动图高度。单位：px。 |
| output.width | Integer | 动图宽度。单位：px。 |

#### SampleSnapshot（采样截图任务）
| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| taskType | String | 任务类型，固定为`SampleSnapshot`。 |
| status | String | 任务状态，有 PROCESSING、SUCCESS 和 FAIL。 |
| errCode | Integer | 错误码。0：成功；其他值：失败，其中`30009`为原文件异常失败，`30010`为系统失败或未知。 |
| message | String | 错误信息。 |
| input | Object | 任务的输入信息。 |
| input.definition | Integer | 采样截图模板 ID。 |
| input.watermarkDefinition | Array | 整形数组，水印模板 ID 列表。 |
| output | Object | 任务的输出信息，任务成功时会有该字段，失败则没有。 |
| output.imageUrls | Array | 字符串数组，生成的截图 URL 列表。 |

#### SnapshotByTimeOffset（按时间点截图任务）
| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| taskType | String | 任务类型，固定为`SnapshotByTimeOffset`。 |
| status | String | 任务状态，有 PROCESSING、SUCCESS 和 FAIL。 |
| errCode | Integer | 错误码。0：成功；其他值：失败，其中`30009`为原文件异常失败，`30010`为系统失败或未知。 |
| message | String | 错误信息。 |
| input | Object | 任务的输入信息。 |
| input.definition | Integer | 按时间点截图模板 ID。 |
| input.timeOffset | Array | 整形数组，截图的时间偏移，单位为毫秒。 |
| input.watermarkDefinition | Array | 整形数组，水印模板 ID 列表。 |
| output | Object | 任务的输出信息，任务成功时会有该字段，失败则没有。 |
| output.imgInfo | Array | 生成的截图信息列表。 |
| output.imgInfo.timeOffset | Integer | 该张截图的时间偏移，单位毫秒。 |
| output.imgInfo.url | String | 截图 URL。 |

#### CoverBySnapshot（截图图片作为视频封面任务）

| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| taskType | String | 任务类型，固定为`CoverBySnapshot`。 |
| status | String | 任务状态，有 PROCESSING、SUCCESS 和 FAIL。 |
| errCode | Integer | 错误码。0：成功；其他值：失败，其中`30009`为原文件异常失败，`30010`为系统失败或未知。 |
| message | String | 错误信息。 |
| input | Object | 任务的输入信息。 |
| input.definition | Integer | 采样截图模板 ID。 |
| input.positionType | String | 截图方式。Time：依照时间点截图。Percent：依照百分比截图。 |
| input.position | Integer | 截图位置。对于依照时间点截图，该值表示指定视频第几秒的截图作为封面。对于依照百分比截图，该值表示使用视频百分之多少的截图作为封面。 |
| input.watermarkDefinition | Array | 整形数组，水印模板 ID 列表。 |
| output | Object | 任务的输出信息，任务成功时会有该字段，失败则没有。 |
| output.imageUrl | Array | 作为视频封面的截图 URL。 |

#### PullFile（拉取视频文件任务）
| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| taskType | String | 任务类型，固定为`PullFile`。 |
| status | String | 任务状态，有 PROCESSING、SUCCESS 和 FAIL。 |
| errCode | Integer | 错误码。 0：成功；其他值：失败。 |
| message | String | 错误信息。 |
| input | Object | 任务的输入信息。 |
| input.url | String | 需要拉取的视频的 URL。 |
| input.fileName | String | 视频文件的名称。 |
| input.md5 | Integer | 视频文件的 MD5。 |
| output | Object | 任务的输出信息，任务成功时会有该字段，失败则没有。 |
| output.fileId | String | 视频文件 ID。 |
| output.fileSize | String | 视频文件大小。 |
| output.url | String | 视频文件的播放地址。 |

#### ImageSprites（雪碧图截图任务）
| **参数名称** | **类型** | **描述** |
| -- | -- | -- |
| taskType | String | 任务类型，固定为`ImageSprites`。 |
| status | String | 任务状态，有 PROCESSING、SUCCESS 和 FAIL。 |
| errCode | Integer | 错误码。 0：成功；其他值：失败。 |
| message | String | 错误信息。 |
| input | Object | 任务的输入信息，任务成功时会有该字段，失败则没有。 |
| input.definition | Integer | 雪碧图模板 ID。 |
| output | Object | 任务的输出信息。 |
| output.totalCount | Integer | 雪碧图小图总数。 |
| output.urlList | Array | 字符串数组，生成的雪碧图的 URL 列表。 |
| output.webVttUrl | String | 雪碧图子图位置与时间关系 WebVtt 文件地址。 |

#### 示例
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
### 视频转码完成
#### 参数说明
| 参数名称 | 类型 | 说明 |
| -- | -- | -- |
| version | String | 事件通知版本号，固定为`4.0`。 |
| eventType | String | 事件类型，固定`TranscodeComplete`。 |
| data | Object | 具体回调数据。 |
| data.status | Integer | 错误码。0：成功；其他值：失败。 |
| data.message | String | 错误信息。  |
| data.fileId | String | 被转码的文件 ID。 |
| data.vodTaskId | String | 转码任务 ID。 |

#### 示例
```json
{
    "version": "4.0",
    "eventType": "TranscodeComplete",
    "data": {
        "status": 0,
        "message": "",
        "vodTaskId": "Transcode-1edb7eb88a599d05abe451cfc541cfbd",
        "fileId": "14508071098244931831",
        "fileName": "动物世界",
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
### 指定时间点截图完成
#### 参数说明
| 参数名称 | 类型 | 说明 |
| -- | -- | -- |
| version | String | 回调版本号，固定为`4.0`。 |
| eventType | String | 回调类型，固定为`CreateSnapshotByTimeOffsetComplete`。 |
| data | Object | 具体回调数据。 |
| data.vodTaskId | String | 指定时间点截图任务 ID。  |
| data.fileId | String | 指定时间点截图的 FileId。  |
| data.definition | Integer | 截图规格，请参考 [指定时间点截图参数模板](https://intl.cloud.tencent.com/document/product/266/33940#.E6.97.B6.E9.97.B4.E7.82.B9.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF)。 |
| data.picInfo | Array | 指定时间点截图输出的截图信息。 |

data.picInfo 数组中每个元素均为 Object，参数含义如下：

| 参数名称 | 类型 | 说明 |
| -- | -- | -- |
| timeOffset | Integer | 截图的具体时间点，单位：毫秒。 |
| url | String | 截图文件 URL。  |
| status | Integer | 错误码。0：成功；其他值：失败。 |

#### 示例
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
### 视频截取雪碧图完成
#### 参数说明
| 参数名称 | 类型 | 说明 |
| -- | -- | -- |
| version | String | 回调版本号，固定为`4.0`。 |
| eventType | String | 回调类型，固定为`CreateImageSpriteComplete`。 |
| data | Object | 具体回调数据。 |
| data.status | Integer | 错误码。0：成功；其他值：失败。 |
| data.message | String | 错误信息。 |
| data.vodTaskId | String | 截取雪碧图任务 ID。 |
| data.fileId | String | 截取雪碧图的 FileId。 |
| data.definition | Integer | 雪碧图规格，请参考 [雪碧图截图模板](https://intl.cloud.tencent.com/document/product/266/33940#.E9.9B.AA.E7.A2.A7.E5.9B.BE.E6.A8.A1.E6.9D.BF)。 |
| data.totalCount | Integer | 雪碧图小图总数量。 |
| data.imageSpriteUrl | Array | 截图雪碧图输出的雪碧图信息。 |
| data.webVttUrl | String | 雪碧图子图位置与时间关系 WebVtt 文件地址。 |

#### 示例
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
### 视频剪辑完成
#### 参数说明
| 参数名称 | 类型 | 说明 |
| -- | -- | -- |
| version | String | 回调版本号，固定为`4.0`。 |
| eventType | String | 回调类型，固定为`ClipComplete`。 |
| data | Object | 具体回调数据。 |
| data.vodTaskId | String | 剪辑任务 ID。  |
| data.srcFileId | String | 剪辑任务源文件 FileId。 |
| data.fileInfo | Object | 剪辑输出的视频文件信息。 |

data.fileInfo 每个参数含义如下：

| 参数名称 | 类型 | 说明 |
|---------|---------|---------|
| fileType | String | 剪辑的文件类型。 |
| status | Integer | 该类型文件的错误信息。0：成功；其他：失败。 |
| message | String | 错误信息。 |
| fileId | String | 剪辑的文件的 fileId。 |
| fileUrl | String | 剪辑的文件 URL。 |

#### 示例
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
### 视频拼接完成
#### 参数说明
| 参数名称 | 类型 | 说明 |
|---------|---------|---------|
| version | String | 回调版本号，固定为`4.0`。 |
| eventType | String | 回调类型，固定为`ConcatComplete`。 |
| data | Object | 具体回调数据。 |
| data.vodTaskId | String | 拼接任务 ID。 |
| data.fileInfo | Array | 拼接输出的视频文件信息。 |

data.fileInfo 数组中每个元素均为 Object，参数含义如下：

| 参数名称 | 类型 | 说明 |
|---------|---------|---------|
| fileType | String | 拼接出的文件类型。 |
| status | Integer | 任务执行结果，0为成功，-1或4为失败。 |
| message | String | 错误信息。 |
| fileId | String | 拼接出的文件的 FileId。 |
| fileUrl | String | 拼接出的文件 URL。 |

#### 示例
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
