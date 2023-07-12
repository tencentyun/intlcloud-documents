## MediaWorkflow_Topology_Nodes_Start_Input 
<span id="MediaWorkflow_Topology_Nodes_Start_Input"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| ---------------   | ------------------------------------------ | --------- | -------- | ------------------------ |
| ObjectPrefix      | Object prefix                                | String    | Yes       | None                       |
| QueueId           | Queue ID                                    | String    | Yes       | None                       |
| PicProcessQueueId | Image processing queue ID                             | String    | Yes if there is an image processing node        | None |
| SpeechRecognitionQueueId | Speech recognition queue ID                      | String    | Yes if there is a speech recognition node        | None |
| AIProcessQueueId | AI processing queue ID                      | String    | Yes if there is an AI-based recognition node        | None |
| NotifyConfig      | Callback information. If none is specified, the queue callback information is used. | Container | No       | None   |
| ExtFilter         | Filename extension filter.                           | Container | No       | None   |

<span id="MediaWorkflow_Topology_Nodes_Start_Input_NotifyConfig"></span>
`NotifyConfig` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required | Default Value | Constraints |
| ------------------  | -------- | ------ | -------- | ------ | ------------------------------------------------------------ |
| Url                 | Callback address | String | Yes   | None | The callback address cannot be a private network address.                                               |
| Type                | Callback type | String | Yes   | None |  <ul  style="margin: 0;"><li>Url: URL callback </li><li>TDMQ: TDMQ message callback</li></ul> |
| Event               | Callback information | String | Yes       | None     | <ul  style="margin: 0;"><li>TaskFinish: Job completed </li><li>WorkflowFinish: Workflow completed </li><li>You can configure multiple events separated by comma. |
| ResultFormat        | Callback format | String | No       | XML    | <ul  style="margin: 0;"><li>XML </li><li>JSON</li></ul>                      |
| MqRegion            | TDMQ region | String | No  | None    | Yes if the callback type is TDMQ. For supported regions, see <a href="https://intl.cloud.tencent.com/document/product/406/12667">Request Domain Description</a>. |
| MqMode              | TDMQ mode | String | No  | None    | Yes if the callback type is TDMQ. <ul  style="margin: 0;"><li>Topic: Topic subscription </li><li>Queue: Queue service </li></ul>           |
| MqName              | TDMQ topic name | String | No  | None    | Yes if the callback type is TDMQ.                      |

<span id="MediaWorkflow_Topology_Nodes_Start_Input_ExtFilter"></span>
`ExtFilter` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required | Default Value | Constraints |
| ------------------ | --------------------- | ------ | -------- | ------ | ------------------------------------------------------------ |
| State              | Switch.                | String | No   | Off    | On/Off                                                       |
| Video              | Require a video extension.    | String | No   | false  | false/true                                                   |
| Audio              | Require an audio extension.    | String | No   | false  | false/true                                                   |
| Image              | Require an image extension.    | String | No   | false  | false/true                                                   |
| ContentType        | Require a content type. | String | No   | false  | false/true                                                   |
| Custom             | Require a custom extension.  | String | No   | false  | false/true                                                   |
| CustomExts         | Custom extension.          | String | No   | None     | <ul  style="margin: 0;"><li>Separate filename extensions by slash (/). Up to ten extensions are supported.</li><li>If `Custom` is `true`, this parameter is required. </li></ul> |
| AllFile    | All files          |  String  |  No   | false    |  false/true  |

## MediaWorkflow_Topology_Nodes_\*\*\*_Operation_Output
<span id="Operation_Output"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| Region             | Bucket region | String | Yes       | None                              |
| Bucket             | Bucket name | String | Yes       | None |
| Object             | Result filename | String  | Yes       | <ul  style="margin: 0;"><li>If the workflow node type is `Snapshot` or `SmartCover`, and there are more than one result file, `${Number} $` must be included. </li><li>If the workflow node type is `Segment`, `Duration` is specified, and `Format` is not `HLS` or `m3u8`, `${Number}` must be included. </li></ul>   |
| SpriteObject       | Image sprite name | String  | No       | If the workflow node type is `Snapshot` and the image sprite feature is enabled, this field is required. |
| AuObject           | Voice result filename | String | No     | If the workflow node type is `VoiceSeparate` and there is a voice output, this field is required.  |

## MediaWorkflow_Topology_Nodes_Snapshot\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_Snapshot_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId         | Screenshot template ID  | String                                       | Yes       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |

## MediaWorkflow_Topology_Nodes_Animation\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_Animation_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId         | Video-to-animated image conversion template ID  | String                                       | Yes       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |

## MediaWorkflow_Topology_Nodes_SmartCover\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_SmartCover_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId         | Intelligent thumbnail template ID  | String                                       | No       | None   |
| SmartCover         | Intelligent thumbnail parameter     | Container. For more information, see [SmartCover](#SmartCover). | No       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |

>? Both `TemplateId` and `SmartCover` can be left empty, in which case three thumbnails will be generated according to the original video size by default. If both of them are specified, `TemplateId` will take effect.
>

## MediaWorkflow_Topology_Nodes_Transcode\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_Transcode_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId          | Audio/Video transcoding template ID  | String                                       | No       | None   |
| WatermarkTemplateId | Watermark template ID  | String array | No       | Up to three watermark template IDs are supported. |
| RemoveWatermark     | Watermark removal parameter | Container. For more information, see [RemoveWatermark](#RemoveWatermark). | No       | None   |
| DigitalWatermark    | Digital watermark parameter | Container. For more information, see [DigitalWatermark](#DigitalWatermark). | No       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |
| Input               | Input configuration     | Container | No       | None   |

`MediaWorkflow_Topology_Nodes_Transcode_\*\*\*_Operation.Input` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required | Constraints |
| ------------------ | --------------- | ------ | ---- | ----------------- |
| SpeedTranscodingQueueId  | Accelerated transcoding queue  | String | No   | None        |

## MediaWorkflow_Topology_Nodes_Concat\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_Concat_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId         | Splicing template ID  | String                                       | Yes       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |


## MediaWorkflow_Topology_Nodes_VoiceSeparate\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_VoiceSeparate_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId         | Voice/Sound separation template ID  | String                                       | Yes       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |


## MediaWorkflow_Topology_Nodes_VideoMontage\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_VideoMontage_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId         | Video montage template ID  | String                                       | Yes       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |


## MediaWorkflow_Topology_Nodes_SDRtoHDR\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_SDRtoHDR_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| SDRtoHDR            | SDR-to-HDR configuration | Container | Yes       | None                             |
| TranscodeTemplateId | Audio/Video transcoding template ID   | String    | Yes       | None                             |
| WatermarkTemplateId | Watermark template ID  | String array | No       | Up to three watermark template IDs are supported. |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |

`SDRtoHDR` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required | Constraints |
| ------------------ | -------- | ------ | -------- | ------------------- |
| HdrMode            | HDR mode | String | Yes       | <ul  style="margin: 0;"><li>HLG</li><li>HDR10 </li></ul> |


## MediaWorkflow_Topology_Nodes_VideoProcess\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_VideoProcess_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId         | Video enhancement template ID  | String                                       | Yes       | None   |
| TranscodeTemplateId | Audio/Video transcoding template ID   | String    | Yes       | None                             |
| WatermarkTemplateId | Watermark template ID  | String array | No       | Up to three watermark template IDs are supported. |
| DigitalWatermark    | Digital watermark parameter | Container. For more information, see [DigitalWatermark](#DigitalWatermark). | No       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |


## MediaWorkflow_Topology_Nodes_SCF\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_SCF_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| SCF                | SCF function information | Container | Yes   | None   |

`SCF` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required | Constraints |
| ------------------ | -------- | ------ | -------- | ---- |
| Region             | Function region | String | Yes   | None   |
| FunctionName       | Function name | String | Yes   | None   |
| Namespace          | Namespace | String | No   | None   |
| Alias              | Function alias | String | No   | None   |


## MediaWorkflow_Topology_Nodes_SuperResolution\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_SuperResolution_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId         | Super resolution template ID  | String                                       | Yes       | None   |
| TranscodeTemplateId | Audio/Video transcoding template ID   | String    | Yes       | None                             |
| WatermarkTemplateId | Watermark template ID  | String array | No       | Up to three watermark template IDs are supported. |
| DigitalWatermark    | Digital watermark parameter | Container. For more information, see [DigitalWatermark](#DigitalWatermark). | No       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |


## MediaWorkflow_Topology_Nodes_Segment\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_Segment_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| Segment            | Audio/Video remuxing parameter  | Container    | Yes   | None |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |

`Segment` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required | Constraints |
| ------------------ | ------------------ | ------ | -------- | --------------------------------- |
| Format             | Container format             | String    | Yes       | aac, mp3, flac, mp4, ts, mkv, avi, hls, m3u8 |
| Duration           | Remuxing duration in seconds | String | No  | The value must be an integer equal to or greater than 5. |
| HlsEncrypt         | HLS encryption configuration                            | Container | No       | This parameter takes effect only when the container format is `hls`. For more information, see [HlsEncrypt](#HlsEncrypt).    |


## MediaWorkflow_Topology_Nodes_PicProcess\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_PicProcess_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId         | Image processing template ID  | String                                       | Yes       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |


## MediaWorkflow_Topology_Nodes_Tts\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_Tts_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId         | Text-to-speech template ID  | String                                       | Yes       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |


## MediaWorkflow_Topology_Nodes_SpeechRecognition\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_SpeechRecognition_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |
| StreamPackConfig   | Packaging configuration | Container | Yes       | None   |


## MediaWorkflow_Topology_Nodes_StreamPackConfig\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_StreamPackConfig_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| StreamPackConfig   | Packaging configuration | Container | No       | None   |

`StreamPackConfig` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------- | ------ | -------- | ---------- |
| PackType           | Packaging type. Default value: `HLS`. | String | No   | HLS/DASH   |
| IgnoreFailedStream | Whether to ignore the substream failed to be transcoded and continue packaging. Default value: `true`. | String | No   | true/false   |


## MediaWorkflow_Topology_Nodes_VideoStream\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_VideoStream_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| TemplateId          | Audio/Video transcoding template ID  | String                                       | No       | None   |
| WatermarkTemplateId | Watermark template ID  | String array | No       | Up to three watermark template IDs are supported. |
| RemoveWatermark     | Watermark removal parameter | Container. For more information, see [RemoveWatermark](#RemoveWatermark). | No       | None   |
| Output             | Output address     | Container. For more information, see [Output](#Operation_Output). | Yes       | None   |


## MediaWorkflow_Topology_Nodes_StreamPack\_\*\*\*_Operation
<span id="MediaWorkflow_Topology_Nodes_StreamPack_Operation"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| -----------------  | ------------ | ------ | -------- | ------------------------------- |
| StreamPackInfo     | Packaging rule | Container | No   | None   |

`StreamPackInfo` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required | Constraints |
| ------------------ | ------------ | --------- | -------- | ---- |
| VideoStreamConfig  | Video substream configuration | Container | No   | None   |

`VideoStreamConfig` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required | Constraints |
| ------------------ | ----------------------------------------------------------- | --------- | -------- | ------------------------ |
| VideoStreamName    | Video substream name                                              | String | Yes   | It must be consistent with the existing video node. |
| BandWidth          | Video substream bandwidth limit. Unit: b/s. Value range: [0, 2000000000], where 0 indicates no limit. | String | No   | The value must be equal to or greater than 0. The default value is 0.     |

## AudioMix
<span id="AudioMix"></span>

| Node Name (Keyword) | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------------------------------------- | --------- | ---- | ------ | ------------------------------------------------- |
| AudioSource        | Address of the audio track file to be mixed | String | Yes | None | It must be stored in the same bucket as the input media file. |
| MixMode            | Audio mix mode  | String | No   | Repeat | <li>Repeat: Repeats the background sound <br/><li>Once: Plays back the background sound once |
| Replace            | Whether to replace the original audio of the input media file with the mixed audio track | String | No | false  | true/false                                        |
| EffectConfig       | Audio mix transition configuration  | Container | No   | false  | None |

`EffectConfig ` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required | Default Value | Constraints |
| ------------------ | --------------- | ------ | ---- | ------ | ----------------- |
| EnableStartFadein  | Enables fade-in  | String | No   | false       | true/false |
| StartFadeinTime    | Fade-in duration  | String | No   | None    | A floating point number above 0 |
| EnableEndFadeout   | Enables fade-out  | String | No   | false       | true/false |
| EndFadeoutTime     | Fade-out duration  | String | No   | None    | A floating point number above 0 |
| EnableBgmFade      | Enables fade-in for background music transition  | String | No   | false       | true/false |
| BgmFadeTime        | Fade-in duration for background music transition  | String | No   | None    | A floating point number above 0 |


## CallBackMqConfig
<span id="CallBackMqConfig"></span>

| Node Name (Keyword) | Description | Type | Required |
| ------------------ | ---------------- | ------ | -------- |
| MqRegion           | Message queue region. Valid values: `sh` (Shanghai), `bj` (Beijing), `gz` (Guangzhou), `cd` (Chengdu), `hk` (Hong Kong, China). | String | Yes |
| MqMode             | Message queue mode. Default value: `Queue`. <br/>Topic: Topic subscription <br/>Queue: Queue service </td> | String | Yes |
| MqName             | TDMQ topic name                                                                        | String | Yes |


## DigitalWatermark
<span id="DigitalWatermark"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| ------------------ | -------------------------------------- | ------ | -------- | ------------------------------------------------------- |
| Message            | The watermark information embedded by the digital watermark | String | Yes       | It can contain up to 64 letters, digits, underscores (_), hyphens (-), and asterisks (*).   |
| Type               | Digital watermark type | String | Yes       | It currently can be set to `Text` only.   |
| Version            | Digital watermark version | String | Yes       | It currently can be set to `V1` only.   |
| IgnoreError        | Whether to ignore the watermarking failure and continue the job. | String | Yes       | Valid values: `true`, `false`.   |
| State              | Whether the watermark is added successfully. Valid values: `Running`, `Success`, `Failed`.  | string | No | This field cannot be set actively; instead, it will be returned after the job is submitted successfully. |


## DashEncrypt
<span id="DashEncrypt"></span>

| Node Name (Keyword) | Description | Type | Required | Default Value | Constraints |
| -----------------| --------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| IsEncrypt        | Whether to enable DASH encryption | String    | No       | false  | true/false                                                   |
| UriKey           | DASH encryption key    | String | No   | None     | This parameter will take effect only when `IsEncrypt` is `true`.                       |


## HlsEncrypt 
<span id="HlsEncrypt"></span>

| Node Name (Keyword) | Description | Type | Required | Default Value | Constraints |
| -----------------| --------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| IsEncrypt        | Whether to enable HLS encryption | String    | No       | false  | true/false                                                   |
| UriKey           | HLS encryption key    | String | No   | None     | This parameter will take effect only when `IsEncrypt` is `true`.                       |


## RemoveWatermark
<span id="RemoveWatermark"></span>

| Node Name (Keyword) | Description | Type | Required | Constraints |
| ------------------ | --------------------- | ------ | -------- | ------------------------------------ |
| Dx                 | X-axis offset of the top-left corner origin | String | Yes        | <ul  style="margin: 0;"><li>Value range: [0, 4096]</li><li>Unit: px</li></ul> |
| Dy                 | Y-axis offset of the top-left corner origin | String | Yes        | <ul  style="margin: 0;"><li>Value range: [0, 4096]</li><li>Unit: px</li></ul> |
| Width              | Watermark width            | String | Yes       | <ul  style="margin: 0;"><li>Value range: (0, 4096]</li><li>Unit: px</li></ul> |
| Height              | Watermark height            | String | Yes       | <ul  style="margin: 0;"><li>Value range: (0, 4096]</li><li>Unit: px</li></ul> |


## SmartCover
<span id="SmartCover"></span>

| Node Name (Keyword) | Description | Type | Required | Default Value | Constraints |
| -------------------- | -------------------- | --------- | -------- | ----------------- | ------------------------------------------------------------ |
| Format                | Image format             | String    | No       | jpg          | jpg, png, webp |
| Width                 | Width | String    | No   |  Original video width | <ul  style="margin: 0;"><li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Width` is set, `Height` is calculated based on the original video aspect ratio. </li></ul> |
| Height               | Height | String    | No  | Original video height  | <ul  style="margin: 0;"><li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Height` is set, `Width` is calculated based on the original video aspect ratio.</li></ul> |
| Count                | Number of screenshots             | String    | No       | 3                | [1,10]  |
| DeleteDuplicates     | Whether to deduplicate thumbnails.    | String | No  | false | true/false |

