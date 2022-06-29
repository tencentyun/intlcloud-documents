## Feature Description

This API (`Create Workflow`) is used to create a workflow.

## Request

#### Sample request

```plaintext
POST /workflow HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
>

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

#### Request body 1: Audio/Video transcoding, TESHD, frame capturing, conversion to animated image, voice/sound separation, video montage, audio/video splicing, intelligent thumbnail, video enhancement, SDR-to-HDR, custom function, super resolution, audio/video remuxing, and image processing


```plaintext
<Request>
    <MediaWorkflow>
        <Name>demo</Name>
        <State>Active</State>
        <Topology>
            <Dependencies>
                <Start>Snapshot_1581665960536,Transcode_1581665960537,Animation_1581665960538,Concat_1581665960539,SmartCover_1581665960539,VoiceSeparate_1581665960551,VideoMontage_1581665960551,SDRtoHDR_1581665960553,VideoProcess_1581665960554,SCF_1581665960566,SuperResolution_1581665960583,Segment_1581665960667,PicProcess_1581665960668</Start>
                <Snapshot_1581665960536>End</Snapshot_1581665960536>
                <Transcode_1581665960537>End</Transcode_1581665960537>
                <Animation_1581665960538>End</Animation_1581665960538>
                <Concat_1581665960539>End</Concat_1581665960539>
                <SmartCover_1581665960539>End</SmartCover_1581665960539>
                <VoiceSeparate_1581665960551>End</VoiceSeparate_1581665960551>
                <VideoMontage_1581665960551>End</VideoMontage_1581665960551>
                <SDRtoHDR_1581665960553>End</SDRtoHDR_1581665960553>
                <VideoProcess_1581665960554>End</VideoProcess_1581665960554>
                <SCF_1581665960566>End</SCF_1581665960566>
                <SuperResolution_1581665960583>End</SuperResolution_1581665960583>
                <Segment_1581665960667>End</Segment_1581665960667>
                <PicProcess_1581665960668>End</PicProcess_1581665960668>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId></QueueId>
                        <PicProcessQueueId></PicProcessQueueId>
                        <ObjectPrefix></ObjectPrefix>
                        <NotifyConfig>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat></ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>on</State>
                            <Audio>true</Audio>
                            <Image>true</Image>
                            <Custom>true</Custom>
                            <CustomExts>mp4/mp3</CustomExts>
                            <AllFile>true</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <SmartCover_1581665960539>
                    <Type>SmartCover</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/cover-${Number}.jpg</Object>
                        </Output>
                        <SmartCover>
                            <Format>png</Format>
                            <Width>128</Width>
                            <Height>128</Height>
                            <Count>3</Count>
                            <DeleteDuplicates>false</DeleteDuplicates>
                        </SmartCover> 
                    </Operation>
                </SmartCover_1581665960539>
                <Snapshot_1581665960536>
                    <Type>Snapshot</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/snapshot-${number}.${Ext}</Object>
                            <SpriteObject>abc/${RunId}/snapshot-${number}.jpg</SpriteObject>
                        </Output>
                    </Operation>
                </Snapshot_1581665960536>
                <Transcode_1581665960537>
                    <Type>Transcode</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/trans.mp4</Object>
                        </Output>
                    </Operation>
                </Transcode_1581665960537>
                <Animation_1581665960538>
                    <Type>Animation</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/bcd.gif</Object>
                        </Output>
                    </Operation>
                </Animation_1581665960538>
                <Concat_1581665960539>
                    <Type>Concat</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/abc.${ext}</Object>
                        </Output>
                    </Operation>
                </Concat_1581665960539>
                <VoiceSeparate_1581665960551>
                    <Type>VoiceSeparate</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163b164</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <AuObject>bcd/${RunId}/audio.mp3</AuObject>
                            <Object>bcd/${RunId}/background.mp3</Object>
                        </Output>
                    </Operation>
                </VoiceSeparate_1581665960551>
                <VideoMontage_1581665960551>
                    <Type>VideoMontage</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba73l9</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/montage.mp4</Object>
                        </Output>
                    </Operation>
                </VideoMontage_1581665960551>
                <SDRtoHDR_1581665960553>
                    <Type>SDRtoHDR</Type>
                    <Operation>
                        <SDRtoHDR>
                            <HdrMode>HLG</HdrMode>
                        </SDRtoHDR>
                        <TranscodeTemplateId></TranscodeTemplateId>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/SDRtoHDR.mp4</Object>
                        </Output>
                    </Operation>
                </SDRtoHDR_1581665960553>
                <VideoProcess_1581665960554>
                    <Type>VideoProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55356fshb18</TemplateId>
                        <TranscodeTemplateId></TranscodeTemplateId>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/videoProcess.mp4</Object>
                        </Output>
                    </Operation>
                </VideoProcess_1581665960554>
                <SCF_1581665960566>
                    <Type>SCF</Type>
                    <Operation>
                        <SCF>
                            <Region>ap-chengdu</Region>
                            <FunctionName>test</FunctionName>
                            <Namespace>testspace</Namespace>
                        </SCF>
                    </Operation>
                </SCF_1581665960566>
                <SuperResolution_1581665960583>
                    <Type>SuperResolution</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}/SuperResolution.mkv</Object>
                        </Output>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <TranscodeTemplateId>t160606b9752148c4absdfaf2f55163b1f</TranscodeTemplateId>
                    </Operation>
                </SuperResolution_1581665960583>
                <Segment_1581665960667>
                    <Type>Segment</Type>
                    <Operation>
                        <Segment>
                            <Format>mp4</Format>
                            <Duration>5</Duration>
                        </Segment>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>test-trans${Number}</Object>
                        </Output>
                    </Operation>
                </Segment_1581665960667>
                <PicProcess_1581665960668>
                    <Type>PicProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/trans.jpg</Object>
                        </Output>
                    </Operation>
                </PicProcess_1581665960668>
            </Nodes>
        </Topology>
    </MediaWorkflow>
</Request>
```

#### Request body 2: Adaptive bitrate streaming

```plaintext
<Request>
    <MediaWorkflow>
        <Name>demo</Name>
        <State>Active</State>
        <Topology>
            <Dependencies>
                <Start>StreamPackConfig_1581665960532</Start>
                <StreamPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>StreamPack</VideoStream_1581665960536>
                <VideoStream_1581665960537>StreamPack</VideoStream_1581665960537>
                <StreamPack_1581665960538>End</StreamPack_1581665960538>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId></QueueId>
                        <ObjectPrefix></ObjectPrefix>
                        <NotifyConfig>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat></ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>on</State>
                            <Audio>true</Audio>
                            <Custom>true</Custom>
                            <CustomExts>mp4/mp3</CustomExts>
                            <AllFile>true</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <StreamPackConfig_1581665960532>
                    <Type>StreamPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${InputPath}/${InputName}._${RunId}.${ext}</Object>
                        </Output>
                        <StreamPackConfig>
                            <PackType>HLS</PackType>
                            <IgnoreFailedStream>true</IgnoreFailedStream>
                        </StreamPackConfig>
                    </Operation>
                </StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}_Substream_1/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960536>
                <VideoStream_1581665960537>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606bgfdg2148c4ab182f55163ba7bj</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}_Substream_2/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960537>
                <StreamPack_1581665960538>
                    <Type>StreamPack</Type>
                    <Operation>
                        <StreamPackInfo>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960536</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960537</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                        </StreamPackInfo>
                    </Operation>
                </StreamPack_1581665960538>
            </Nodes>
        </Topology>
    </MediaWorkflow>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | -------- |
| Request            | None     | Request container | Container | Yes       |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ---------- | --------- | -------- |
| MediaWorkflow      | Request | Workflow node. | Container | Yes       |


`MediaWorkflow` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | --------------------- | ---------- | --------- | -------- | ------------------------------------------- |
| Name               | Request.MediaWorkflow | Workflow name. | String    | Yes       | The value can contain up to 128 letters, digits, hyphens, and underscores. |
| State              | Request.MediaWorkflow | Workflow status. | String    | No       | Paused/Active                               |
| Topology           | Request.MediaWorkflow | Topology information.   | Container | Yes       | None                                          |



`Topology` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ------| --------- | ---- | ---- |
| Dependencies      | Request.MediaWorkflow.</br>Topology | Node dependencies. | Container    | Yes   | None |
| Nodes             | Request.MediaWorkflow.</br>Topology | Node list. | Container    | Yes   | None |

`Nodes` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------ | --------------- | --------- | ------------ | ------------------------------------------------------------ |
| Start         | Request.MediaWorkflow.</br>Topology.Nodes | Start node. | Container    | Yes   | There is only one start node. |
| Animation\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Animated image type node | Container    | No   | The node name must be prefixed with "Animation". There can be multiple animated image nodes. |
| Snapshot\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | Screenshot type node | Container    | No   | The node name must be prefixed with "Snapshot". There can be multiple screenshot nodes. |
| SmartCover\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Intelligent thumbnail node | Container    | No   | The node name must be prefixed with "SmartCover". There can be multiple intelligent thumbnail nodes. |
| Transcode\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | Transcoding node | Container    | No   | The node name must be prefixed with "Transcode". There can be multiple transcoding nodes. |
| Concat\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | Audio/Video splicing node | Container    | No   | The node name must be prefixed with "Concat". There can be multiple audio/video splicing nodes. |
| VoiceSeparate\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | Voice/Sound separation node | Container    | No   | The node name must be prefixed with "VoiceSeparate". There can be multiple voice/sound separation nodes. |
| VideoMontage\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | Video montage node | Container    | No   | The node name must be prefixed with "VideoMontage". There can be multiple video montage nodes. |
| StreamPackConfig\_\*\*\*| Request.MediaWorkflow.</br>Topology.Nodes | Adaptive bitrate streaming node | Container    | No   | The node name must be prefixed with "StreamPackConfig". There can be only one adaptive bitrate streaming node. This node must follow a start node and be followed by a video substream node. There can be multiple video substream nodes. |
| VideoStream\_\*\*\*| Request.MediaWorkflow.</br>Topology.Nodes | Video substream node | Container    | No   | The node name must be prefixed with "VideoStream". There can be multiple video substream nodes. This node must follow a StreamPackConfig node and be followed by a StreamPack node. |
| StreamPack\_\*\*\*| Request.MediaWorkflow.</br>Topology.Nodes | Adaptive bitrate streaming packaging node | Container    | No   | The node name must be prefixed with "StreamPack". There can be only one adaptive bitrate streaming packaging node. This node must follow a video substream node and be followed by an end node. |
| SDRtoHDR\_\*\*\*       | Request.MediaWorkflow.</br>Topology.Nodes | SDR-to-HDR node    | Container | No           | The node name must be prefixed with "SDRtoHDR". There can be multiple SDR-to-HDR nodes.              |
| VideoProcess\_\*\*\*   | Request.MediaWorkflow.</br>Topology.Nodes | Video processing node    | Container | No           | The node name must be prefixed with "VideoProcess". There can be multiple video processing nodes.         |
| SCF\_\*\*\*            | Request.MediaWorkflow.</br>Topology.Nodes | SCF function node     | Container | No           | The node name must be prefixed with "SCF". There can be multiple SCF function nodes.                   |
| SuperResolution\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Super resolution node | Container| No | The node name must be prefixed with "SuperResolution". There can be multiple super resolution nodes. |
| Segment\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Audio/Video remuxing node | Container| No | The node name must be prefixed with `Segment`. There can be multiple audio/video remuxing nodes. |
| PicProcess\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Image processing node | Container| No | The node name must be prefixed with "PicProcess". There can be multiple image processing nodes. |

`Start` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ------| --------- | ---- | ---- |
| Type         | Request.MediaWorkflow.<br>Topology.Nodes.Start | Node type | String    | Yes   | Start |
| Input        | Request.MediaWorkflow.<br>Topology.Nodes.Start | Input information | Container | Yes   | None |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------ | ---------------------------------------- | --------- | -------- | ---- |
| ObjectPrefix       | Request.MediaWorkflow.<br>Topology.Nodes.Start.Input | Object prefix. | String | Yes       | None   |
| QueueId            | Request.MediaWorkflow.<br>Topology.Nodes.Start.Input | Queue ID     | String | Yes       | None   |
| PicProcessQueueId  | Request.MediaWorkflow.<br>Topology.Nodes.Start.Input | Image processing queue ID     | String | No       | This parameter is required when there is an image processing node.   |
| NotifyConfig       | Request.MediaWorkflow.<br>Topology.Nodes.Start.Input | Callback information. If none is specified, the queue callback information is used. | Container | No       | None   |
| ExtFilter          | Request.MediaWorkflow.<br>Topology.Nodes.Start.Input | Filename extension filter.                           | Container | No       | None   |


`Start.Input.NotifyConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| Url                | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.NotifyConfig | Callback address | String | Yes   | None | The callback address cannot be a private network address.                                               |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.NotifyConfig | Callback type | String | Yes   | None |  Url: URL callback                                         |
| Event              | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.NotifyConfig | Callback information | String | Yes   | None | 1. TaskFinish: Job completed </br> 2. WorkflowFinish: Workflow completed </br> 3. You can configure multiple events separated with commas. |
| ResultFormat       | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.NotifyConfig | Callback format | String | No   |  XML | 1. XML</br> 2. JSON |



`Start.Input.ExtFilter` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ---------------------------------------------------------- | ------------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| State              | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Switch.                | String | No   | Off    | On/Off                                                       |
| Video              | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Require a video extension.    | String | No   | false  | false/true                                                   |
| Audio              | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Require an audio extension.    | String | No   | false  | false/true                                                   |
| Image              | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Require an image extension    | String | No   | false  | false/true                                                   |
| ContentType        | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Require a content type. | String | No   | false  | false/true                                                   |
| Custom             | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Require a custom extension.  | String | No   | false  | false/true                                                   |
| CustomExts         | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Custom extension.          | String | No   | None     | 1. Separate filename extensions with slashes (/). Up to ten extensions are supported.</br>2. If `Custom` is `true`, this parameter is required. |
| AllFile    | Request.MediaWorkflow.Topology.Nodes.Start.Input.ExtFilter | All files          |  String  |  No   | false    |  false/true  |


`Animation\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Animation\_\*\*\* | Node type | String    | Yes       | Animation |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Animation\_\*\*\* | Operation rule | Container | Yes       | None        |

`Animation\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | ---- | ---- |
| TemplateId         | Request.MediaWorkflow.Topology.<br>Nodes.Animation\_\*\*\*.Operation | Template ID   | String    | Yes   | None   |
| Output             | Request.MediaWorkflow.Topology.<br>Nodes.Animation\_\*\*\*.Operation | Output address | Container | Yes   | None   |


`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | ---- | ------------------------------------------------------------ |
| Region             | Request.MediaWorkflow.Topology.<br>Nodes.Animation\_\*\*\*.Operation.Output | Bucket region | String | Yes   | None                                                           |
| Bucket             | Request.MediaWorkflow.Topology.<br>Nodes.Animation\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None |
| Object             | Request.MediaWorkflow.Topology.<br>Nodes.Animation\_\*\*\*.Operation.Output | Result filename | String | Yes   | 1. bcd/${RunId}/bcd.gif <br/> 2. bcd/${RunId}/bcd.webp <br/> |

`Snapshot\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | -------- |
| Type               | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*\*\*\* | Node type | String    | Yes       | Snapshot |
| Operation          | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*\*\*\* | Operation rule | Container | Yes       | None       |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| TemplateId         | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation | Template ID  | String    | Yes       | None   |
| Output             | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation | Output address | Container | Yes       | None   |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | ------------ | ------------------------------------------------------------ |
| Region             | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation.Output | Bucket region | String | Yes           | None                                                           |
| Bucket             | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None |
| Object             | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation.Output | Result filename | String | No           | <li>abc/${RunId}/snapshot-${number}.${Ext}<br/><li>bcd/${RunId}/snapshot-${number}.jpg |
| SpriteObject       | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation.Output | Image sprite name | String | No           | <li>abc/${RunId}/snapshot-${number}.jpg<br/><li>bcd/${RunId}/snapshot-${number}.jpg  |

`SmartCover_***` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------- | -------- | --------- | -------- | ---------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.SmartCover_*** | Node type | String    | Yes       | SmartCover |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.SmartCover_*** | Operation rule | Container | Yes       | None        |

`SmartCover_***.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| Output             | Request.MediaWorkflow.Topology.<br>Nodes.SmartCover_***.Operation | Output address | Container | Yes       | None   |
| SmartCover         | Request.MediaWorkflow.Topology.<br>Nodes.SmartCover_***.Operation | Thumbnail configuration      | Container | No   | None   |

`SmartCover_***.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ------------------------------- |
| Region             | Request.MediaWorkflow.Topology.<br>Nodes.SmartCover_***.Operation.Output | Bucket region | String | Yes       | None                              |
| Bucket             | Request.MediaWorkflow.Topology.<br>Nodes.SmartCover_***.Operation.Output | Bucket name | String | Yes       | None |
| Object             | Request.MediaWorkflow.Topology.<br>Nodes.SmartCover_***.Operation.Output | Result filename | String | Yes       | The parameters ${Number} and ${RunId} must be included. |

`SmartCover_***.SmartCover` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- | ---- | ---- |
| Format             | Request.Operation.SmartCover | Thumbnail image type.    | String | Yes  | None | png, jpg, webp  |
| Width              | Request.Operation.SmartCover | Thumbnail image width    | String | Yes  | None | 1. Value range: [128, 4096]<br/> 2. Unit: px<br/> |
| Height             | Request.Operation.SmartCover | Thumbnail image height    | String | Yes  | None | 1. Value range: [128, 4096]<br/> 2. Unit: px<br/> |
| Count              | Request.Operation.SmartCover | Number of thumbnails.        | String | No  | 3 | Value range: [1, 10] |
| DeleteDuplicates   | Request.Operation.SmartCover | Whether to deduplicate thumbnails.    | String | No  | false | true/false |

`Transcode_***` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------ | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Transcode_*** | Node type | String    | Yes       | Transcode |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Transcode_*** | Operation rule | Container | Yes       | None        |

`Transcode_***.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------- | ------------------------------------------------------------ | ------------ | --------- | -------- | ------------------------------ |
| TemplateId          | Request.MediaWorkflow.Topology.</br>Nodes.Transcode_***.Operation | Transcoding template ID   | String    | Yes       | None                             |
| WatermarkTemplateId | Request.MediaWorkflow.Topology.</br>Nodes.Transcode_***.Operation | Watermark template ID   | String    | No       | Up to three watermark template IDs are supported. |
| RemoveWatermark       | Request.MediaWorkflow.Topology.</br>Nodes.Transcode\_\*\*\*.Operation | Watermark removal parameter        | Container | No   |None|
| DigitalWatermark    | Request.MediaWorkflow.Topology.</br>Nodes.Transcode\_\*\*\*.Operation | Digital watermark parameter | Container | No | None |
| Output       | Request.MediaWorkflow.Topology.</br>Nodes.Transcode\_\*\*\*.Operation | Output address | Container | Yes   | None |

`Transcode\_\*\*\*.RemoveWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | :----------------------------------------------------------- | --------------------- | ------ | -------- | ------------------------------------ |
| Dx                 | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.RemoveWatermark | X-axis offset of the top-left corner origin. | string | Yes       | 1. Value range: [0, 4096]<br/>2. Unit: px |
| Dy                 | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.RemoveWatermark | Y-axis offset of the top-left corner origin. | string | Yes       | 1. Value range: [0, 4096]<br/>2. Unit: px |
| Width              | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.RemoveWatermark | Watermark width            | string | Yes       | 1. Value range: (0, 4096]<br/>2. Unit: px |
| Height             | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.RemoveWatermark | Watermark height            | string | Yes       | 1. Value range: (0, 4096]<br/>2. Unit: px |

`Transcode\_\*\*\*.DigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| Message            | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.DigitalWatermark | The watermark information embedded by the digital watermark | String | Yes       | It can contain up to 64 letters, digits, underscores (\_), hyphens (-), and asterisks (*)   |
| Type            | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.DigitalWatermark | Digital watermark type | String | Yes       | It currently can be set to `Text` only.   |
| Version            | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.DigitalWatermark | Digital watermark version | String | Yes       | It currently can be set to `V1` only.   |
| IgnoreError            | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.DigitalWatermark | Whether to ignore the watermarking failure and continue the job. | String | Yes       | Valid values: true, false   |

`Transcode\_\*\*\*.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| Region             | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.Output | Bucket region | String | Yes       | None   |
| Bucket             | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None |
| Object             | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.Output | Result filename | String | Yes       | None   |

`Concat\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------- | -------- | --------- | -------- | ------ |
| Type               | Request.MediaWorkflow.Topology.<br>Nodes.Concat\_\*\*\* | Node type | String    | Yes       | Concat |
| Operation          | Request.MediaWorkflow.Topology.<br>Nodes.Concat\_\*\*\* | Operation rule | Container | Yes       | None     |

`Concat\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| TemplateId         | Request.MediaWorkflow.Topology.</br>Nodes.Concat\_\*\*\*.Operation | Template ID  | String    | Yes       | None   |
| Output             | Request.MediaWorkflow.Topology.</br>Nodes.Concat\_\*\*\*.Operation | Output address | Container | Yes       | None   |

`VoiceSeparate\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | ------------- |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\* | Node type | String    | Yes       | VoiceSeparate |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\* | Operation rule | Container | Yes       | None            |

`VoiceSeparate\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| TemplateId         | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation | Template ID  | String    | Yes       | None   |
| Output             | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation | Output address | Container | Yes       | None   |

`VoiceSeparate\_\*\*\*.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------------ | ------ | -------- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation.Output | Bucket region       | String | Yes       | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation.Output | Background sound result filename | String | Yes       | None   |
| AuObject           | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation.Output | Voice result filename   | String | Yes       | None   |


`VideoMontage\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | --------------------------------------------------------- | -------- | --------- | -------- | ------------ |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\* | Node type | String    | Yes       | VideoMontage |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\* | Operation rule | Container | Yes       | None           |

`VideoMontage\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| TemplateId         | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation | Template ID  | String    | Yes       | None   |
| Output             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation | Output address | Container | Yes       | None   |



`VideoMontage\_\*\*\*.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Bucket region | String | Yes       | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Result filename | String | Yes       | None   |

`StreamPackConfig\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | ------------- |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.StreamPackConfig\_\*\*\* | Node type | String    | Yes       | StreamPackConfig |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.StreamPackConfig\_\*\*\* | Operation rule | Container | Yes       | None            |

`StreamPackConfig\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| Output             | Request.MediaWorkflow.Topology.</br>Nodes.StreamPackConfig\_\*\*\*.Operation | Output address | Container | Yes       | None   |
| StreamPackConfig   | Request.MediaWorkflow.Topology.</br>Nodes.StreamPackConfig\_\*\*\*.Operation | Packaging configuration | Container | Yes       | None   |

`StreamPackConfig\_\*\*\*.Operation.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.StreamPackConfig\_\*\*\*.Operation.Output | Bucket region | String | Yes       | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.StreamPackConfig\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None   |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.StreamPackConfig\_\*\*\*.Operation.Output | Result filename | String | Yes       | None   |

`StreamPackConfig\_\*\*\*.Operation.StreamPackConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| PackType | Request.MediaWorkflow.Topology.</br>Nodes.StreamPackConfig\_\*\*\*.Operation.StreamPackConfig | Packaging type. Default value: HLS. | string | No   | HLS/DASH   |
| IgnoreFailedStream | Request.MediaWorkflow.Topology.</br>Nodes.StreamPackConfig\_\*\*\*.Operation.StreamPackConfig | Whether to ignore the substream failed to be transcoded and continue packaging. Default value: true. | string | No   | true/false   |

`VideoStream\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ------| --------- | ---- | ---- |
| Type       | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\* | Node type | String    | Yes   | VideoStream |
| Operation  | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\* | Operation rule | Container | Yes   | None |

`VideoStream\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ------| --------- | ---- | ---- |
| TemplateId   | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\*.Operation | Template ID  | String    | Yes   | None |
| Output       | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\*.Operation | Output address | Container | Yes   | None |
| WatermarkTemplateId   | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\*.Operation | Watermark template ID  | String    | Yes   | Up to three watermark template IDs are supported. |
| RemoveWatermark       | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\*.Operation | Watermark removal parameter        | Container | No   |None|

`VideoStream\_\*\*\*.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Bucket region | String | Yes       | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Result filename | String | Yes       | None   |

`VideoStream\_\*\*\*.RemoveWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | :----------------------------------------------------------- | --------------------- | ------ | -------- | ------------------------------------ |
| Dx                 | Request.MediaWorkflow.Topology.Nodes.</br>VideoStream\_\*\*\*.Operation.RemoveWatermark | X-axis offset of the top-left corner origin. | string | Yes       | 1. Value range: [0, 4096]<br/>2. Unit: px |
| Dy                 | Request.MediaWorkflow.Topology.Nodes.</br>VideoStream\_\*\*\*.Operation.RemoveWatermark | Y-axis offset of the top-left corner origin. | string | Yes       | 1. Value range: [0, 4096]<br/>2. Unit: px |
| Width              | Request.MediaWorkflow.Topology.Nodes.</br>VideoStream\_\*\*\*.Operation.RemoveWatermark | Width                    | string | Yes       | 1. Value range: (0, 4096]<br/>2. Unit: px |
| Height             | Request.MediaWorkflow.Topology.Nodes.</br>VideoStream\_\*\*\*.Operation.RemoveWatermark | Height                    | string | Yes       | 1. Value range: (0, 4096]<br/>2. Unit: px |


`StreamPack\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------ | -------- | --------- | -------- | ------- |
| Type       | Request.MediaWorkflow.Topology.</br>Nodes.StreamPack\_\*\*\* | Node type | String    | Yes   | StreamPack |
| Operation          | Request.MediaWorkflow.</br>Topology.Nodes.StreamPack\_\*\*\* | Operation rule | Container | Yes       | None      |

`StreamPack\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | ---- | ---- |
| StreamPackInfo        | Request.MediaWorkflow.Topology.</br>Nodes.StreamPack\_\*\*\*.Operation | Packaging rule | Container | No   | None   |

`StreamPack\_\*\*\*.Operation.StreamPackInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | --------- | ---- | ---- |
| VideoStreamConfig  | Request.MediaWorkflow.Topology.</br>Nodes.StreamPack\_\*\*\*.Operation.StreamPackInfo | Video substream configuration | Container | No   | None   |

`StreamPack\_\*\*\*.Operation.StreamPackInfo.VideoStreamConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | --------------------------------------------------------- | --------- | ---- | ------------------------ |
| VideoStreamName    | Request.MediaWorkflow.Topology.Nodes.</br>StreamPack\_\*\*\*.Operation.StreamPackInfo.VideoStreamConfig | Video substream name                                              | Container | Yes   | It must be consistent with the existing video node. |
| BandWidth          | Request.MediaWorkflow.Topology.Nodes.</br>StreamPack\_\*\*\*.Operation.StreamPackInfo.VideoStreamConfig | Video substream bandwidth limit. Unit: b/s. Value range: [0, 2000000000], where 0 indicates no limit. | Container | No   | The value must be equal to or greater than 0. The default value is 0.     |


`SDRtoHDR\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------- | -------- | --------- | ---- | -------- |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\* | Node type | Container | Yes   | SDRtoHDR |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\* | Operation rule | Container | Yes   | None       |

`SDRtoHDR\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------- | ----------------------------------------------------------- | ------------ | --------- | ---- | ------------------------------ |
| SDRtoHDR            | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation | SDR-to-HDR configuration | Container | Yes   | None                             |
| TranscodeTemplateId | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation | Transcoding template ID   | String    | Yes   | None                             |
| WatermarkTemplateId | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation | Watermark template ID   | String    | No   | Up to three watermark template IDs are supported. |
| Output              | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation | Output address     | Container | Yes   | None                             |

`SDRtoHDR\_\*\*\*.SDRtoHDR` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------- | ------ | ---- | ------------------- |
| HdrMode            | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation.SDRtoHDR | HDR mode | String | Yes   | 1. HLG<br/>2. HDR10 |

`SDRtoHDR\_\*\*\*.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | ---- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation.Output | Bucket region | String | Yes   | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation.Output | Result filename | String | Yes   | None   |



`VideoProcess\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ----------------------------------------------------- | -------- | --------- | ---- | ------------ |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\* | Node type | String    | Yes   | VideoProcess |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\* | Operation rule | Container | Yes   | None           |

`VideoProcess\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------- | ------------------------------------------------------------ | ---------- | --------- | ---- | ------------------------------ |
| TemplateId          | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation | Template ID     | String    | Yes   | None                             |
| TranscodeTemplateId | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation | Transcoding template ID | String    | Yes   | None                             |
| WatermarkTemplateId | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation | Watermark template ID | String    | No   | Up to three watermark template IDs are supported. |
| DigitalWatermark   | Request.MediaWorkflow.Topology..<br>Nodes.VideoProcess\_\*\*\*.Operation | Digital watermark parameter | Container | No   | None |
| Output              | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation | Output address   | Container | Yes   | None                             |

`VideoProcess\_\*\*\*.Operation.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | ---- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation.Output | Bucket region | String | Yes   | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation.Output | Result filename | String | Yes   | None   |


`VideoProcess\_\*\*\*.Operation..DigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| Message            | Request.MediaWorkflow.Topology.<br>Nodes.VideoProcess\_\*\*\*.Operation.<br>DigitalWatermark | The watermark information embedded by the digital watermark | String | Yes       | It can contain up to 64 letters, digits, underscores (\_), hyphens (-), and asterisks (*)   |
| Type            | Request.MediaWorkflow.Topology.<br>Nodes.VideoProcess\_\*\*\*.Operation.<br>DigitalWatermark | Digital watermark type | String | Yes       | It currently can be set to `Text` only.   |
| Version            | Request.MediaWorkflow.Topology.<br>Nodes.VideoProcess\_\*\*\*.Operation.<br>DigitalWatermark | Digital watermark version | String | Yes       | It currently can be set to `V1` only.   |
| IgnoreError            | Request.MediaWorkflow.Topology.<br>Nodes.VideoProcess\_\*\*\*.Operation.<br>DigitalWatermark | Whether to ignore the watermarking failure and continue the job. | String | Yes       | Valid values: true, false   |

`SCF\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | -------------------------------------------- | -------- | --------- | ---- | ---- |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.SCF\_\*\*\* | Node type | String    | Yes   | SCF  |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.SCF\_\*\*\* | Operation rule | Container | Yes   | None   |

`SCF\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------ | ----------- | --------- | ---- | ---- |
| SCF                | Request.MediaWorkflow.Topology.</br>Nodes.SCF\_\*\*\*.Operation | SCF function information | Container | Yes   | None   |

`SCF\_\*\*\*.Operation.SCF` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.SCF\_\*\*\*.Operation.SCF | Function region | String | Yes   | None   |
| FunctionName       | Request.MediaWorkflow.Topology.</br>Nodes.SCF\_\*\*\*.Operation.SCF | Function name | String | Yes   | None   |
| Namespace          | Request.MediaWorkflow.Topology.</br>Nodes.SCF\_\*\*\*.Operation.SCF | Namespace | String | No   | None   |
| Alias              | Request.MediaWorkflow.Topology.</br>Nodes.SCF\_\*\*\*.Operation.SCF | Function alias | String | No   | None   |

`SuperResolution\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.SuperResolution\_\*\*\* | Node type | String    | Yes | SuperResolution |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.SuperResolution\_\*\*\* | Operation rule | Container | Yes     | None       |

`SuperResolution\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| TemplateId   | Request.MediaWorkflow.Topology.Nodes.<br>SuperResolution\_\*\*\*.Operation | Template ID   | String    | Yes   | None   |
| TranscodeTemplateId | Request.MediaWorkflow.Topology.Nodes.<br>SuperResolution\_\*\*\*.Operation | Transcoding template ID   | String    | Yes   | None |
| WatermarkTemplateId | Request.MediaWorkflow.Topology.Nodes.<br>SuperResolution***.Operation | Watermark template ID   | String    | No       | Up to three watermark template IDs are supported. |
| DigitalWatermark   | Request.MediaWorkflow.Topology.Nodes.<br>SuperResolution\_\*\*\*.Operation | Digital watermark parameter | Container | No   | None |
| Output       | Request.MediaWorkflow.Topology.Nodes.<br>SuperResolution\_\*\*\*.Operation | Output address | Container | Yes       | None   |

`SuperResolution\_\*\*\*\*.DigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| Message            | Request.MediaWorkflow.Topology.Nodes.<br>SuperResolution\_\*\*\*.Operation.DigitalWatermark | The watermark information embedded by the digital watermark | String | Yes       | It can contain up to 64 letters, digits, underscores (\_), hyphens (-), and asterisks (*)   |
| Type            | Request.MediaWorkflow.Topology.Nodes.<br>SuperResolution\_\*\*\*.Operation.DigitalWatermark | Digital watermark type | String | Yes       | It currently can be set to `Text` only.   |
| Version            | Request.MediaWorkflow.Topology.Nodes.<br>SuperResolution\_\*\*\*.Operation.DigitalWatermark | Digital watermark version | String | Yes       | It currently can be set to `V1` only.   |
| IgnoreError            | Request.MediaWorkflow.Topology.Nodes.<br>SuperResolution\_\*\*\*.Operation.DigitalWatermark | Whether to ignore the watermarking failure and continue the job. | String | Yes       | Valid values: true, false   |


`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Region             | Request.MediaWorkflow.Topology.<br>Nodes.SuperResolution\_\*\*\*.Operation.Output | Bucket region | String | Yes           | None                                                     |
| Bucket             | Request.MediaWorkflow.Topology.<br>Nodes.SuperResolution\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None |
| Object   | Request.MediaWorkflow.Topology.<br>Nodes.SuperResolution\_\*\*\*.Operation.Output | Result filename  | String  | Yes  | None |


`Segment\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Segment\_\*\*\* | Node type | String    | Yes       | Segment |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Segment\_\*\*\* | Operation rule | Container | Yes       | None        |

`Segment\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Segment   | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation | Audio/Video remuxing parameter.  | Container    | Yes   | None |
| Output   | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation | Output address | Container | Yes   | None |

`Segment` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Format            | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation.Segment | Container format. | String | Yes | aac, mp3, flac, mp4, ts, mkv, avi |
| Duration          | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation.Segment | Remuxing duration in seconds | String | No  | The value must be an integer equal to or greater than 5. |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Region             | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation.Output | Bucket region. | String | Yes     | None                                                     |
| Bucket             | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None |
| Object   | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation.Output | Result filename  | String  | Yes  | The `${Number}` parameter must be included and used as the output sequence number of each audio/video segment after custom remuxing. |

`PicProcess\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | -------- |
| Type               | Request.MediaWorkflow.Topology.<br>Nodes.PicProcess\_\*\*\*\*\*\* | Node type | String    | Yes       | PicProcess |
| Operation          | Request.MediaWorkflow.Topology.<br>Nodes.PicProcess\_\*\*\*\*\*\* | Operation rule | Container | Yes       | None     |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| TemplateId         | Request.MediaWorkflow.Topology.<br>Nodes.PicProcess\_\*\*\*.Operation | Template ID   | String    | Yes   | None   |
| Output             | Request.MediaWorkflow.Topology.<br>Nodes.PicProcess\_\*\*\*.Operation | Output address | Container | Yes       | None   |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | ------------ | ------------------------------------------------------------ |
| Region             | Request.MediaWorkflow.Topology.<br>Nodes.PicProcess\_\*\*\*.Operation.Output | Bucket region | String | Yes       | None                                                           |
| Bucket             | Request.MediaWorkflow.Topology.<br>Nodes.PicProcess\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None                                                           |
| Object             | Request.MediaWorkflow.Topology.<br>Nodes.PicProcess\_\*\*\*.Operation.Output | Result filename | String | No           | 1. The `${InputName}` parameter must be included. <br/>2. For example: ${InputName}-process.jpg |
</br>

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

#### Response body 1: Audio/Video transcoding, TESHD, frame capturing, conversion to animated image, voice/sound separation, video montage, audio/video splicing, intelligent thumbnail, video enhancement, SDR-to-HDR, custom function, super resolution, audio/video remuxing, and image processing


```plaintext
<Response>
    <MediaWorkflow>
        <Name>demo</Name>
        <State>Active</State>
        <WorkflowId></WorkflowId>
        <Topology>
            <Dependencies>
                <Start>Snapshot_1581665960536,Transcode_1581665960537,Animation_1581665960538,Concat_1581665960539,SmartCover_1581665960539,VoiceSeparate_1581665960551,VideoMontage_1581665960551,SDRtoHDR_1581665960553,VideoProcess_1581665960554,SCF_1581665960566,SuperResolution_1581665960583,Segment_1581665960667,PicProcess_1581665960668</Start>
                <Snapshot_1581665960536>End</Snapshot_1581665960536>
                <Transcode_1581665960537>End</Transcode_1581665960537>
                <Animation_1581665960538>End</Animation_1581665960538>
                <Concat_1581665960539>End</Concat_1581665960539>
                <SmartCover_1581665960539>End</SmartCover_1581665960539>
                <VoiceSeparate_1581665960551>End</VoiceSeparate_1581665960551>
                <VideoMontage_1581665960551>End</VideoMontage_1581665960551>
                <SDRtoHDR_1581665960553>End</SDRtoHDR_1581665960553>
                <VideoProcess_1581665960554>End</VideoProcess_1581665960554>
                <SCF_1581665960566>End</SCF_1581665960566>
                <SuperResolution_1581665960583>End</SuperResolution_1581665960583>
                <Segment_1581665960667>End</Segment_1581665960667>
                <PicProcess_1581665960668>End</PicProcess_1581665960668>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId></QueueId>
                        <PicProcessQueueId></PicProcessQueueId>
                        <ObjectPrefix></ObjectPrefix>
                        <NotifyConfig>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat></ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>on</State>
                            <Audio>true</Audio>
                            <Image>true</Image>
                            <Custom>true</Custom>
                            <CustomExts>mp4/mp3</CustomExts>
                            <AllFile>true</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <SmartCover_1581665960539>
                    <Type>SmartCover</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/cover-${Number}.jpg</Object>
                        </Output>
                        <SmartCover>
                            <Format>png</Format>
                            <Width>128</Width>
                            <Height>128</Height>
                            <Count>3</Count>
                            <DeleteDuplicates>false</DeleteDuplicates>
                        </SmartCover> 
                    </Operation>
                </SmartCover_1581665960539>
                <Snapshot_1581665960536>
                    <Type>Snapshot</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/snapshot-${number}.${Ext}</Object>
                            <SpriteObject>abc/${RunId}/snapshot-${number}.jpg</SpriteObject>                         
                        </Output>
                    </Operation>
                </Snapshot_1581665960536>
                <Transcode_1581665960537>
                    <Type>Transcode</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/trans.mp4</Object>
                        </Output>
                    </Operation>
                </Transcode_1581665960537>
                <Animation_1581665960538>
                    <Type>Animation</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/bcd.gif</Object>
                        </Output>
                    </Operation>
                </Animation_1581665960538>
                <Concat_1581665960539>
                    <Type>Concat</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/abc.${ext}</Object>
                        </Output>
                    </Operation>
                </Concat_1581665960539>
                <VoiceSeparate_1581665960551>
                    <Type>VoiceSeparate</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163b164</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <AuObject>bcd/${RunId}/audio.mp3</AuObject>
                            <Object>bcd/${RunId}/background.mp3</Object>
                        </Output>
                    </Operation>
                </VoiceSeparate_1581665960551>
                <VideoMontage_1581665960551>
                    <Type>VideoMontage</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba73l9</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/montage.mp4</Object>
                        </Output>
                    </Operation>
                </VideoMontage_1581665960551>
                <SDRtoHDR_1581665960553>
                    <Type>SDRtoHDR</Type>
                    <Operation>
                        <SDRtoHDR>
                            <HdrMode>HLG</HdrMode>
                        </SDRtoHDR>
                        <TranscodeTemplateId></TranscodeTemplateId>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/SDRtoHDR.mp4</Object>
                        </Output>
                    </Operation>
                </SDRtoHDR_1581665960553>
                <VideoProcess_1581665960554>
                    <Type>VideoProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55356fshb18</TemplateId>
                        <TranscodeTemplateId></TranscodeTemplateId>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/videoProcess.mp4</Object>
                        </Output>
                    </Operation>
                </VideoProcess_1581665960554>
                <SCF_1581665960566>
                    <Type>SCF</Type>
                    <Operation>
                        <SCF>
                            <Region>ap-chengdu</Region>
                            <FunctionName>test</FunctionName>
                            <Namespace>testspace</Namespace>
                        </SCF>
                    </Operation>
                </SCF_1581665960566>
                <SuperResolution_1581665960583>
                    <Type>SuperResolution</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}/SuperResolution.mkv</Object>
                        </Output>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <TranscodeTemplateId>t160606b9752148c4absdfaf2f55163b1f</TranscodeTemplateId>
                    </Operation>
                </SuperResolution_1581665960583>
                <Segment_1581665960667>
                    <Type>Segment</Type>
                    <Operation>
                        <Segment>
                            <Format>mp4</Format>
                            <Duration>5</Duration>
                        </Segment>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>test-trans${Number}</Object>
                        </Output>
                    </Operation>
                </Segment_1581665960667>
                <PicProcess_1581665960668>
                    <Type>PicProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/trans.jpg</Object>
                        </Output>
                    </Operation>
                </PicProcess_1581665960668>
            </Nodes>
        </Topology>
        <BucketId></BucketId>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </MediaWorkflow>
</Response>
```

#### Response body 2: Adaptive bitrate streaming

```
<Response>
    <MediaWorkflow>
        <Name>demo</Name>
        <State>Active</State>
        <WorkflowId></WorkflowId>
        <BucketId></BucketId>
        <Topology>
            <Dependencies>
                <Start>StreamPackConfig_1581665960532</Start>
                <StreamPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>StreamPack</VideoStream_1581665960536>
                <VideoStream_1581665960537>StreamPack</VideoStream_1581665960537>
                <StreamPack_1581665960538>End</StreamPack_1581665960538>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId></QueueId>
                        <ObjectPrefix></ObjectPrefix>
                        <NotifyConfig>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat></ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>on</State>
                            <Audio>true</Audio>
                            <Custom>true</Custom>
                            <CustomExts>mp4/mp3</CustomExts>
                            <AllFile>true</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <StreamPackConfig_1581665960532>
                    <Type>StreamPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${InputPath}/${InputName}._${RunId}.${ext}</Object>
                        </Output>
                        <StreamPackConfig>
                            <PackType>HLS</PackType>
                            <IgnoreFailedStream>true</IgnoreFailedStream>
                        </StreamPackConfig>
                    </Operation>
                </StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}_Substream_1/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960536>
                <VideoStream_1581665960537>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606bgfdg2148c4ab182f55163ba7bj</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}_Substream_2/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960537>
                <StreamPack_1581665960538>
                    <Type>StreamPack</Type>
                    <Operation>
                        <StreamPackInfo>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960536</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960537</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                        </StreamPackInfo>
                    </Operation>
                </StreamPack_1581665960538>
            </Nodes>
        </Topology>
        <BucketId></BucketId>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </MediaWorkflow>
</Response>

```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------- | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| MediaWorkflow      | Response | Workflow array.   | Container |

`MediaWorkflow` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ---------------------- | ----------------------------------------------------------- | --------- |
| Name               | Response.MediaWorkflow | Workflow name.                                                  | String    |
| WorkflowId         | Response.MediaWorkflow | Workflow ID.                                                    | String    |
| State              | Response.MediaWorkflow | Workflow status.                                                  | String    |
| CreateTime         | Response.MediaWorkflow | Creation time.                                                    | String    |
| UpdateTime         | Response.MediaWorkflow | Update time.                                                    | String    |
| Topology           | Response.MediaWorkflow | Topology information. Same as `Request.MediaWorkflow.Topology` in `POST Workflow`.  | Container |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Use Cases

#### Request 1: Sample for audio/video transcoding, TESHD, frame capturing, conversion to animated image, voice/sound separation, video montage, intelligent thumbnail, audio/video splicing, custom function, super resolution, audio/video remuxing, and image processing

```plaintext
POST /workflow HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <MediaWorkflow>
        <Name>demo</Name>
        <State>Active</State>
        <Topology>
            <Dependencies>
                <Start>Snapshot_1581665960536,Transcode_1581665960537,Animation_1581665960538,Concat_1581665960539,SmartCover_1581665960539,VoiceSeparate_1581665960551,VideoMontage_1581665960551,SDRtoHDR_1581665960553,VideoProcess_1581665960554,SCF_1581665960566,SuperResolution_1581665960583,Segment_1581665960667,PicProcess_1581665960668</Start>
                <Snapshot_1581665960536>End</Snapshot_1581665960536>
                <Transcode_1581665960537>End</Transcode_1581665960537>
                <Animation_1581665960538>End</Animation_1581665960538>
                <Concat_1581665960539>End</Concat_1581665960539>
                <SmartCover_1581665960539>End</SmartCover_1581665960539>
                <VoiceSeparate_1581665960551>End</VoiceSeparate_1581665960551>
                <VideoMontage_1581665960551>End</VideoMontage_1581665960551>
                <SDRtoHDR_1581665960553>End</SDRtoHDR_1581665960553>
                <VideoProcess_1581665960554>End</VideoProcess_1581665960554>
                <SCF_1581665960566>End</SCF_1581665960566>
                <SuperResolution_1581665960583>End</SuperResolution_1581665960583>
                <Segment_1581665960667>End</Segment_1581665960667>
                <PicProcess_1581665960668>End</PicProcess_1581665960668>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId></QueueId>
                        <PicProcessQueueId></PicProcessQueueId>
                        <ObjectPrefix></ObjectPrefix>
                        <NotifyConfig>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat>XML</ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>on</State>
                            <Audio>true</Audio>
                            <Image>true</Image>
                            <Custom>true</Custom>
                            <CustomExts>mp4/mp3</CustomExts>
                            <AllFile>true</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <SmartCover_1581665960539>
                    <Type>SmartCover</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/cover-${Number}.jpg</Object>
                        </Output>
                        <SmartCover>
                            <Format>png</Format>
                            <Width>128</Width>
                            <Height>128</Height>
                            <Count>3</Count>
                            <DeleteDuplicates>false</DeleteDuplicates>
                        </SmartCover> 
                    </Operation>
                </SmartCover_1581665960539>
                <Snapshot_1581665960536>
                    <Type>Snapshot</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/snapshot-${number}.${Ext}</Object>
                            <SpriteObject>abc/${RunId}/snapshot-${number}.jpg</SpriteObject>
                        </Output>
                    </Operation>
                </Snapshot_1581665960536>
                <Transcode_1581665960537>
                    <Type>Transcode</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/trans.mp4</Object>
                        </Output>
                    </Operation>
                </Transcode_1581665960537>
                <Animation_1581665960538>
                    <Type>Animation</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/bcd.gif</Object>
                        </Output>
                    </Operation>
                </Animation_1581665960538>
                <Concat_1581665960539>
                    <Type>Concat</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/abc.${ext}</Object>
                        </Output>
                    </Operation>
                </Concat_1581665960539>
                <VoiceSeparate_1581665960551>
                    <Type>VoiceSeparate</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163b164</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <AuObject>bcd/${RunId}/audio.mp3</AuObject>
                            <Object>bcd/${RunId}/background.mp3</Object>
                        </Output>
                    </Operation>
                </VoiceSeparate_1581665960551>
                <VideoMontage_1581665960551>
                    <Type>VideoMontage</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba73l9</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/montage.mp4</Object>
                        </Output>
                    </Operation>
                </VideoMontage_1581665960551>
                <SDRtoHDR_1581665960553>
                    <Type>SDRtoHDR</Type>
                    <Operation>
                        <SDRtoHDR>
                            <HdrMode>HLG</HdrMode>
                        </SDRtoHDR>
                        <TranscodeTemplateId></TranscodeTemplateId>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/SDRtoHDR.mp4</Object>
                        </Output>
                    </Operation>
                </SDRtoHDR_1581665960553>
                <VideoProcess_1581665960554>
                    <Type>VideoProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55356fshb18</TemplateId>
                        <TranscodeTemplateId></TranscodeTemplateId>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/videoProcess.mp4</Object>
                        </Output>
                    </Operation>
                </VideoProcess_1581665960554>
                <SCF_1581665960566>
                    <Type>SCF</Type>
                    <Operation>
                        <SCF>
                            <Region>ap-chengdu</Region>
                            <FunctionName>test</FunctionName>
                            <Namespace>testspace</Namespace>
                        </SCF>
                    </Operation>
                </SCF_1581665960566>
                <SuperResolution_1581665960583>
                    <Type>SuperResolution</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}/SuperResolution.mkv</Object>
                        </Output>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <TranscodeTemplateId>t160606b9752148c4absdfaf2f55163b1f</TranscodeTemplateId>
                    </Operation>
                </SuperResolution_1581665960583>
                <Segment_1581665960667>
                    <Type>Segment</Type>
                    <Operation>
                        <Segment>
                            <Format>mp4</Format>
                            <Duration>5</Duration>
                        </Segment>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>test-trans${Number}</Object>
                        </Output>
                    </Operation>
                </Segment_1581665960667>
                <PicProcess_1581665960668>
                    <Type>PicProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/trans.jpg</Object>
                        </Output>
                    </Operation>
                </PicProcess_1581665960668>
            </Nodes>
        </Topology>
    </MediaWorkflow>
</Request>
```

#### Response 1

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <MediaWorkflow>
        <Name>demo</Name>
        <State>Active</State>
        <WorkflowId></WorkflowId>
        <Topology>
            <Dependencies>
                <Start>Snapshot_1581665960536,Transcode_1581665960537,Animation_1581665960538,Concat_1581665960539,SmartCover_1581665960539,VoiceSeparate_1581665960551,VideoMontage_1581665960551,SDRtoHDR_1581665960553,VideoProcess_1581665960554,SCF_1581665960566,SuperResolution_1581665960583,Segment_1581665960667,PicProcess_1581665960668</Start>
                <Snapshot_1581665960536>End</Snapshot_1581665960536>
                <Transcode_1581665960537>End</Transcode_1581665960537>
                <Animation_1581665960538>End</Animation_1581665960538>
                <Concat_1581665960539>End</Concat_1581665960539>
                <SmartCover_1581665960539>End</SmartCover_1581665960539>
                <VoiceSeparate_1581665960551>End</VoiceSeparate_1581665960551>
                <VideoMontage_1581665960551>End</VideoMontage_1581665960551>
                <SDRtoHDR_1581665960553>End</SDRtoHDR_1581665960553>
                <VideoProcess_1581665960554>End</VideoProcess_1581665960554>
                <SCF_1581665960566>End</SCF_1581665960566>
                <SuperResolution_1581665960583>End</SuperResolution_1581665960583>
                <Segment_1581665960667>End</Segment_1581665960667>
                <PicProcess_1581665960668>End</PicProcess_1581665960668>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId></QueueId>
                        <PicProcessQueueId></PicProcessQueueId>
                        <ObjectPrefix></ObjectPrefix>
                        <NotifyConfig>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat>XML</ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>on</State>
                            <Audio>true</Audio>
                            <Image>true</Image>
                            <Custom>true</Custom>
                            <CustomExts>mp4/mp3</CustomExts>
                            <AllFile>true</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <SmartCover_1581665960539>
                    <Type>SmartCover</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/cover-${Number}.jpg</Object>
                        </Output>
                        <SmartCover>
                            <Format>png</Format>
                            <Width>128</Width>
                            <Height>128</Height>
                            <Count>3</Count>
                            <DeleteDuplicates>false</DeleteDuplicates>
                        </SmartCover> 
                    </Operation>
                </SmartCover_1581665960539>
                <Snapshot_1581665960536>
                    <Type>Snapshot</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/snapshot-${number}.${Ext}</Object>
                            <SpriteObject>abc/${RunId}/snapshot-${number}.jpg</SpriteObject>
                        </Output>
                    </Operation>
                </Snapshot_1581665960536>
                <Transcode_1581665960537>
                    <Type>Transcode</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/trans.mp4</Object>
                        </Output>
                    </Operation>
                </Transcode_1581665960537>
                <Animation_1581665960538>
                    <Type>Animation</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/bcd.gif</Object>
                        </Output>
                    </Operation>
                </Animation_1581665960538>
                <Concat_1581665960539>
                    <Type>Concat</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>abc/${RunId}/abc.${ext}</Object>
                        </Output>
                    </Operation>
                </Concat_1581665960539>
                <VoiceSeparate_1581665960551>
                    <Type>VoiceSeparate</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163b164</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <AuObject>bcd/${RunId}/audio.mp3</AuObject>
                            <Object>bcd/${RunId}/background.mp3</Object>
                        </Output>
                    </Operation>
                </VoiceSeparate_1581665960551>
                <VideoMontage_1581665960551>
                    <Type>VideoMontage</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba73l9</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/montage.mp4</Object>
                        </Output>
                    </Operation>
                </VideoMontage_1581665960551>
                <SDRtoHDR_1581665960553>
                    <Type>SDRtoHDR</Type>
                    <Operation>
                        <SDRtoHDR>
                            <HdrMode>HLG</HdrMode>
                        </SDRtoHDR>
                        <TranscodeTemplateId></TranscodeTemplateId>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/SDRtoHDR.mp4</Object>
                        </Output>
                    </Operation>
                </SDRtoHDR_1581665960553>
                <VideoProcess_1581665960554>
                    <Type>VideoProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55356fshb18</TemplateId>
                        <TranscodeTemplateId></TranscodeTemplateId>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/videoProcess.mp4</Object>
                        </Output>
                    </Operation>
                </VideoProcess_1581665960554>
                <SCF_1581665960566>
                    <Type>SCF</Type>
                    <Operation>
                        <SCF>
                            <Region>ap-chengdu</Region>
                            <FunctionName>test</FunctionName>
                            <Namespace>testspace</Namespace>
                        </SCF>
                    </Operation>
                </SCF_1581665960566>
                <SuperResolution_1581665960583>
                    <Type>SuperResolution</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}/SuperResolution.mkv</Object>
                        </Output>
                        <WatermarkTemplateId></WatermarkTemplateId>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <TranscodeTemplateId>t160606b9752148c4absdfaf2f55163b1f</TranscodeTemplateId>
                    </Operation>
                </SuperResolution_1581665960583>
                <Segment_1581665960667>
                    <Type>Segment</Type>
                    <Operation>
                        <Segment>
                            <Format>mp4</Format>
                            <Duration>5</Duration>
                        </Segment>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>test-trans${Number}</Object>
                        </Output>
                    </Operation>
                </Segment_1581665960667>
                <PicProcess_1581665960668>
                    <Type>PicProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>bcd/${RunId}/trans.jpg</Object>
                        </Output>
                    </Operation>
                </PicProcess_1581665960668>
            </Nodes>
        </Topology>
        <BucketId></BucketId>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </MediaWorkflow>
</Response>
```


#### Request 2: Sample for adaptive bitrate streaming


```plaintext
POST /workflow HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <MediaWorkflow>
        <Name>demo</Name>
        <Topology>
            <Dependencies>
                <Start>StreamPackConfig_1581665960532</Start>
                <StreamPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>StreamPack</VideoStream_1581665960536>
                <VideoStream_1581665960537>StreamPack</VideoStream_1581665960537>
                <StreamPack_1581665960538>End</StreamPack_1581665960538>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId></QueueId>
                        <ObjectPrefix></ObjectPrefix>
                    </Input>
                </Start>
                <StreamPackConfig_1581665960532>
                    <Type>StreamPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${InputPath}/${InputName}._${RunId}.${ext}</Object>
                        </Output>
                    </Operation>
                </StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}_Substream_1/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960536>
                <VideoStream_1581665960537>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606bgfdg2148c4ab182f55163ba7bj</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}_Substream_2/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960537>
                <StreamPack_1581665960538>
                    <Type>StreamPack</Type>
                </StreamPack_1581665960538>
            </Nodes>
        </Topology>
    </MediaWorkflow>
</Request>
```


#### Response 2

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <MediaWorkflow>
        <Name>demo</Name>
        <State>Active</State>
        <WorkflowId></WorkflowId>
        <BucketId></BucketId>
        <Topology>
            <Dependencies>
                <Start>StreamPackConfig_1581665960532</Start>
                <StreamPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>StreamPack</VideoStream_1581665960536>
                <VideoStream_1581665960537>StreamPack</VideoStream_1581665960537>
                <StreamPack_1581665960538>End</StreamPack_1581665960538>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId></QueueId>
                        <PicProcessQueueId></PicProcessQueueId>
                        <ObjectPrefix></ObjectPrefix>
                        <NotifyConfig>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat>XML</ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>on</State>
                            <Audio>true</Audio>
                            <Custom>true</Custom>
                            <CustomExts>mp4/mp3</CustomExts>
                            <AllFile>true</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <StreamPackConfig_1581665960532>
                    <Type>StreamPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${InputPath}/${InputName}._${RunId}.${ext}</Object>
                        </Output>
                        <StreamPackConfig>
                            <PackType>HLS</PackType>
                            <IgnoreFailedStream>true</IgnoreFailedStream>
                        </StreamPackConfig>
                    </Operation>
                </StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}_Substream_1/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960536>
                <VideoStream_1581665960537>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606bgfdg2148c4ab182f55163ba7bj</TemplateId>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${RunId}_Substream_2/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960537>
                <StreamPack_1581665960538>
                    <Type>StreamPack</Type>
                    <Operation>
                        <StreamPackInfo>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960536</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960537</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                        </StreamPackInfo>
                    </Operation>
                </StreamPack_1581665960538>
            </Nodes>
        </Topology>
        <BucketId></BucketId>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </MediaWorkflow>
</Response>
```

