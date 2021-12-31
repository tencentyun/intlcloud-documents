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

>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

#### Request body 1: audio/video transcoding, top speed codec, frame capturing, conversion to animated images, voice separation, video montage, audio/video concatenation, smart cover, video enhancement, SDR-to-HDR, function customization, super resolution, and audio/video segmentation


```plaintext
<Request>
    <MediaWorkflow>
        <Name>demo</Name>
        <State>Active</State>
        <Topology>
            <Dependencies>
                <Start>Snapshot_1581665960536,Transcode_1581665960537,Animation_1581665960538,Concat_1581665960539,SmartCover_1581665960539,VoiceSeparate_1581665960551,VideoMontage_1581665960551,SDRtoHDR_1581665960553,VideoProcess_1581665960554,SCF_1581665960566,SuperResolution_1581665960583,Segment_1581665960667</Start>
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
            </Nodes>
        </Topology>
    </MediaWorkflow>
</Request>
```

#### Request 2: HLS adaptive bitrate multi-streaming

```plaintext
<Request>
    <MediaWorkflow>
        <Name>demo</Name>
        <State>Active</State>
        <Topology>
            <Dependencies>
                <Start>HlsPackConfig_1581665960532</Start>
                <HlsPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</HlsPackConfig_1581665960532>
                <VideoStream_1581665960536>HlsPack</VideoStream_1581665960536>
                <VideoStream_1581665960537>HlsPack</VideoStream_1581665960537>
                <HlsPack_1581665960538>End</HlsPack_1581665960538>
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
                <HlsPackConfig_1581665960532>
                    <Type>HlsPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${InputPath}/${InputName}._${RunId}.${ext}</Object>
                        </Output>
                    </Operation>
                </HlsPackConfig_1581665960532>
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
                <HlsPack_1581665960538>
                    <Type>HlsPack</Type>
                    <Operation>
                        <HlsPackInfo>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960536</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960537</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                        </HlsPackInfo>
                    </Operation>
                </HlsPack_1581665960538>
            </Nodes>
        </Topology>
    </MediaWorkflow>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | -------- |
| Request            | None | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ---------- | --------- | -------- |
| MediaWorkflow      | Request | Workflow node | Container | Yes       |


`MediaWorkflow` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |                                                 |
| ------------------ | --------------------- | ---------- | --------- | -------- | ------------------------------------------- |
| Name               | Request.MediaWorkflow | Workflow name | String    | Yes       | The value can be up to 128 characters in length and contain Chinese characters, letters, digits, dashes (–), and underscores (_). |
| State              | Request.MediaWorkflow | Workflow status | String    | No       | Paused/Active                               |
| Topology           | Request.MediaWorkflow | Topology information   | Container | Yes       | None                                          |



`Topology` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |                                                 |
| ------------------ | ------- | ------| --------- | ---- | ---- |
| Dependencies      | Request.MediaWorkflow.</br>Topology | Node dependencies | Container    | Yes   | None |
| Nodes             | Request.MediaWorkflow.</br>Topology | Node list | Container    | Yes   | None |

`Nodes` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |                                                 |
| ------------------ | ------------------------------------ | --------------- | --------- | ------------ | ------------------------------------------------------------ |
| Start         | Request.MediaWorkflow.</br>Topology.Nodes | Start node | Container    | Yes   | There is only one start node. |
| Animation\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Animated image type node | Container    | No   | The node name must be prefixed with "Animation". There can be multiple animated image nodes. |
| Snapshot\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | Screenshot type node | Container    | No   | The node name must be prefixed with "Snapshot". There can be multiple screenshot nodes. |
| SmartCover\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Smart cover node | Container    | No   | The node name must be prefixed with "SmartCover". There can be multiple smart cover nodes. |
| Transcode\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | Transcoding node | Container    | No   | The node name must be prefixed with "Transcode". There can be multiple transcoding nodes. |
| Concat\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | Audio/video concatenation node | Container    | No   | The node name must be prefixed with "Concat". There can be multiple audio/video concatenation nodes. |
| VoiceSeparate\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | Voice node | Container    | No   | The node name must be prefixed with "VoiceSeparate". There can be multiple voice separation nodes. |
| VideoMontage\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | Video montage node | Container    | No   | The node name must be prefixed with "VideoMontage". There can be multiple video montage nodes. |
| HlsPackConfig\_\*\*\*| Request.MediaWorkflow.</br>Topology.Nodes | HLS packaging configuration node | Container    | No   | The node name must be prefixed with "HlsPackConfig". There can be only one HLS packaging configuration node. An HLS packaging configuration node must follow a start node and be followed by a video substream node. There can be multiple video substream nodes. |
| VideoStream\_\*\*\*| Request.MediaWorkflow.</br>Topology.Nodes | Video substream node | Container    | No   | The node name must be prefixed with "VideoStream". There can be multiple video substream nodes. A video substream node must follow a HlsPackConfig node and be followed by a HlsPack node. |
| HlsPack\_\*\*\*| Request.MediaWorkflow.</br>Topology.Nodes | HLS packaging node | Container    | No   | The node name must be prefixed with "HlsPack". There can be only one HLS packaging node. The HLS packaging node must follow a video substream node and be followed by an End node. |
| SDRtoHDR\_\*\*\*       | Request.MediaWorkflow.</br>Topology.Nodes | SDR-to-HDR node    | Container | No           | The node name must be prefixed with "SDRtoHDR". There can be multiple SDR-to-HDR nodes.              |
| VideoProcess\_\*\*\*   | Request.MediaWorkflow.</br>Topology.Nodes | video processing node    | Container | No           | The node name must be prefixed with "VideoProcess". There can be multiple video processing nodes.         |
| SCF\_\*\*\*            | Request.MediaWorkflow.</br>Topology.Nodes | SCF function node     | Container | No           | The node name must be prefixed with "SCF". There can be multiple SCF function nodes.                   |
| SuperResolution\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Super resolution node | Container| No | The node name must be prefixed with "SuperResolution". There can be multiple super resolution nodes. |
| Segment\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Audio/Video segmentation node | Container| No | The node name must be prefixed with "Segment". There can be multiple audio/video segmentation nodes. |

`Start` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ------| --------- | ---- | ---- |
| Type         | Request.MediaWorkflow.<br>Topology.Nodes.Start | Node type | String    | Yes   | Start |
| Input        | Request.MediaWorkflow.<br>Topology.Nodes.Start | Input information | Container | Yes   | None |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------ | ---------------------------------------- | --------- | -------- | ---- |
| ObjectPrefix       | Request.MediaWorkflow.<br>Topology.Nodes.Start.Input | Object prefix | String | Yes       | None   |
| QueueId            | Request.MediaWorkflow.<br>Topology.Nodes.Start.Input | Queue ID     | String | Yes       | None   |
| NotifyConfig       | Request.MediaWorkflow.<br>Topology.Nodes.Start.Input | Callback information. If none is specified, the queue callback information is used. | Container | No       | None   |
| ExtFilter          | Request.MediaWorkflow.<br>Topology.Nodes.Start.Input | Filename extension filter                           | Container | No       | None   |


`Start.Input.NotifyConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | ------ | ---- | ------------------------------------------------------------ |
| Url                | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.NotifyConfig | Callback address | String | Yes   | The callback address cannot be a private network address.                                               |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.NotifyConfig | Callback type | String | Yes   |  Url: URL callback                                         |
| Event              | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.NotifyConfig | Callback information | String | Yes   | 1. TaskFinish: task completed </br> 2. WorkflowFinish: workflow completed </br> 3. You can configure multiple events, separated with commas (,). |



`Start.Input.ExtFilter` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ---------------------------------------------------------- | ------------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| State              | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Switch                | String | No   | Off    | On/Off                                                       |
| Video              | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Require a video extension    | String | No   | false  | false/true                                                   |
| Audio              | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Require an audio extension    | String | No   | false  | false/true                                                   |
| ContentType        | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Require a content type | String | No   | false  | false/true                                                   |
| Custom             | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Require a custom extension  | String | No   | false  | false/true                                                   |
| CustomExts         | Request.MediaWorkflow.Topology.</br>Nodes.Start.Input.ExtFilter | Custom extension          | String | No   | None     | 1. Separate filename extensions with slashes (/). Up to 10 extensions are supported.</br>2. If `Custom` is `true`, this parameter is required. |
| AllFile    | Request.MediaWorkflow.Topology.Nodes.Start.Input.ExtFilter | All files          |  String  |  No   | false    |  false/true  |


`Animation\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Animation\_\*\*\* | Node type | String    | Yes       | Animation |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Animation\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes       | None        |

`Animation\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | ---- | ---- |
| TemplateId         | Request.MediaWorkflow.Topology.<br>Nodes.Animation\_\*\*\*.Operation | Template ID   | String    | Yes   | None   |
| Output             | Request.MediaWorkflow.Topology.<br>Nodes.Animation\_\*\*\*.Operation | Output address | Container | Yes   | None   |


`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | ---- | ------------------------------------------------------------ |
| Region             | Request.MediaWorkflow.Topology.<br>Nodes.Animation\_\*\*\*.Operation.Output | Bucket region | String | Yes   | None                                                           |
| Bucket             | Request.MediaWorkflow.Topology.<br>Nodes.Animation\_\*\*\*.Operation.Output | Bucket name | String | Yes   | None                                                           |
| Object             | Request.MediaWorkflow.Topology.<br>Nodes.Animation\_\*\*\*.Operation.Output | Result file name | String | Yes   | 1. bcd/${RunId}/bcd.gif <br/> 2. bcd/${RunId}/bcd.webp <br/> |

`Snapshot\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | -------- |
| Type               | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*\*\*\* | Node type | String    | Yes       | Snapshot |
| Operation          | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes       | None       |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| TemplateId         | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation | Template ID  | String    | Yes       | None   |
| Output             | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation | Output address | Container | Yes       | None   |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | ------------ | ------------------------------------------------------------ |
| Region             | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation.Output | Bucket region | String | Yes           | None                                                           |
| Bucket             | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation.Output | Bucket name | String | Yes           | None                                                           |
| Object             | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation.Output | Result file name | String | No           | <li>abc/${RunId}/snapshot-${number}.${Ext}<br/><li>bcd/${RunId}/snapshot-${number}.jpg |
| SpriteObject       | Request.MediaWorkflow.Topology.<br>Nodes.Snapshot\_\*\*\*.Operation.Output | Image sprite name | String | No           | <li>abc/${RunId}/snapshot-${number}.jpg<br/><li>bcd/${RunId}/snapshot-${number}.jpg  |

`SmartCover_***` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------- | -------- | --------- | -------- | ---------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.SmartCover_*** | Node type | String    | Yes       | SmartCover |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.SmartCover_*** | Operation rule. Up to 6 operation rules are supported. | Container | Yes       | None         |

`SmartCover_***.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| Output             | Request.MediaWorkflow.Topology.<br>Nodes.SmartCover_***.Operation | Output address | Container | Yes       | None   |
| SmartCover         | Request.MediaWorkflow.Topology.<br>Nodes.SmartCover_***.Operation | Cover configuration      | Container | No   | None   |

`SmartCover_***.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ------------------------------- |
| Region             | Request.MediaWorkflow.Topology.<br>Nodes.SmartCover_***.Operation.Output | Bucket region | String | Yes       | None                              |
| Bucket             | Request.MediaWorkflow.Topology.<br>Nodes.SmartCover_***.Operation.Output | Bucket name | String | Yes       | None                              |
| Object             | Request.MediaWorkflow.Topology.<br>Nodes.SmartCover_***.Operation.Output | Result file name | String | Yes       | The parameters ${Number} and ${RunId} must be included. |

`SmartCover_***.SmartCover` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- | ---- | ---- |
| Format             | Request.Operation.SmartCover | Cover image type    | String | Yes  | None | png, jpg, webp  |
| Width              | Request.Operation.SmartCover | Cover image width    | String | Yes  | None | 1. Value range: [128, 4096]<br/> 2. Unit: px<br/> |
| Height             | Request.Operation.SmartCover | Cover image height    | String | Yes  | None | 1. Value range: [128, 4096]<br/> 2. Unit: px<br/> |
| Count              | Request.Operation.SmartCover | Number of covers        | String | No  | 3 | Value range: [1, 10] |
| DeleteDuplicates   | Request.Operation.SmartCover | Whether to deduplicate covers    | String | No  | false | true/false |

`Transcode_***` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------ | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Transcode_*** | Node type | String    | Yes       | Transcode |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Transcode_*** | Operation rule. Up to 6 operation rules are supported. | Container | Yes       | None        |

`Transcode_***.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------- | ------------------------------------------------------------ | ------------ | --------- | -------- | ------------------------------ |
| TemplateId          | Request.MediaWorkflow.Topology.</br>Nodes.Transcode_***.Operation | Transcoding template ID   | String    | Yes       | None                             |
| WatermarkTemplateId | Request.MediaWorkflow.Topology.</br>Nodes.Transcode_***.Operation | Watermark template ID   | String    | No       | Up to 3 watermark template IDs are supported. |
| RemoveWatermark       | Request.MediaWorkflow.Topology.</br>Nodes.Transcode\_\*\*\*.Operation | Watermark removal parameter        | Container | No   |None|
| Output       | Request.MediaWorkflow.Topology.</br>Nodes.Transcode\_\*\*\*.Operation | Output address | Container | Yes   | None |

`Transcode\_\*\*\*.RemoveWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | :----------------------------------------------------------- | --------------------- | ------ | -------- | ------------------------------------ |
| Dx                 | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.RemoveWatermark | X-axis offset of the top-left corner origin | string | Yes       | 1. Value range: [0, 4096]<br/>2. Unit: px |
| Dy                 | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.RemoveWatermark | Y-axis offset of the top-left corner origin | string | Yes       | 1. Value range: [0, 4096]<br/>2. Unit: px |
| Width              | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.RemoveWatermark | Watermark width            | string | Yes       | 1. Value range: (0, 4096]<br/>2. Unit: px |
| Height             | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.RemoveWatermark | Watermark height            | string | Yes       | 1. Value range: (0, 4096]<br/>2. Unit: px |

`Transcode\_\*\*\*.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| Region             | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.Output | Bucket region | String | Yes       | None   |
| Bucket             | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None   |
| Object             | Request.MediaWorkflow.Topology.Nodes.<br>Transcode\_\*\*\*.Operation.Output | Result file name | String | Yes       | None   |

`Concat\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------- | -------- | --------- | -------- | ------ |
| Type               | Request.MediaWorkflow.Topology.<br>Nodes.Concat\_\*\*\* | Node type | String    | Yes       | Concat |
| Operation          | Request.MediaWorkflow.Topology.<br>Nodes.Concat\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes       | None     |

`Concat\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| TemplateId         | Request.MediaWorkflow.Topology.</br>Nodes.Concat\_\*\*\*.Operation | Template ID  | String    | Yes       | None   |
| Output             | Request.MediaWorkflow.Topology.</br>Nodes.Concat\_\*\*\*.Operation | Output address | Container | Yes       | None   |

`VoiceSeparate\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | ------------- |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\* | Node type | String    | Yes       | VoiceSeparate |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes       | None            |

`VoiceSeparate\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| TemplateId         | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation | Template ID  | String    | Yes       | None   |
| Output             | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation | Output address | Container | Yes       | None   |

`VoiceSeparate\_\*\*\*.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------------ | ------ | -------- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation.Output | Bucket region       | String | Yes       | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation.Output | Bucket name       | String | Yes       | None   |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation.Output | Background audio result file name | String | Yes       | None   |
| AuObject           | Request.MediaWorkflow.Topology.</br>Nodes.VoiceSeparate\_\*\*\*.Operation.Output | Voice result file name   | String | Yes       | None   |


`VideoMontage\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | --------------------------------------------------------- | -------- | --------- | -------- | ------------ |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\* | Node type | String    | Yes       | VideoMontage |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes       | None           |

`VideoMontage\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| TemplateId         | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation | Template ID  | String    | Yes       | None   |
| Output             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation | Output address | Container | Yes       | None   |

`VideoMontage\_\*\*\*.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Bucket region | String | Yes       | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None   |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Result file name | String | Yes       | None   |

`HlsPackConfig\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | ------------- |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.HlsPackConfig\_\*\*\* | Node type | String    | Yes       | HlsPackConfig |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.HlsPackConfig\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes       | None            |

`HlsPackConfig\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | -------- | --------- | -------- | ---- |
| Output             | Request.MediaWorkflow.Topology.</br>Nodes.HlsPackConfig\_\*\*\*.Operation | Output address | Container | Yes       | None   |

`HlsPackConfig\_\*\*\*.Operation.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.HlsPackConfig\_\*\*\*.Operation.Output | Bucket region | String | Yes       | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.HlsPackConfig\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None   |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.HlsPackConfig\_\*\*\*.Operation.Output | Result file name | String | Yes       | None   |


`VideoStream\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ------| --------- | ---- | ---- |
| Type       | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\* | Node type | String    | Yes   | VideoStream |
| Operation  | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes   | None |

`VideoStream\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ------| --------- | ---- | ---- |
| TemplateId   | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\*.Operation | Template ID  | String    | Yes   | None |
| Output       | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\*.Operation | Output address | Container | Yes   | None |
| WatermarkTemplateId   | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\*.Operation | Watermark template ID  | String    | Yes   | Up to 3 watermark template IDs are supported. |
| RemoveWatermark       | Request.MediaWorkflow.Topology.</br>Nodes.VideoStream\_\*\*\*.Operation | Watermark removal parameter        | Container | No   |None|

`VideoStream\_\*\*\*.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | -------- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Bucket region | String | Yes       | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Bucket name | String | Yes       | None   |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.VideoMontage\_\*\*\*.Operation.Output | Result file name | String | Yes       | None   |

`VideoStream\_\*\*\*.RemoveWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | :----------------------------------------------------------- | --------------------- | ------ | -------- | ------------------------------------ |
| Dx                 | Request.MediaWorkflow.Topology.Nodes.</br>VideoStream\_\*\*\*.Operation.RemoveWatermark | X-axis offset of the top-left corner origin | string | Yes       | 1. Value range: [0, 4096]<br/>2. Unit: px |
| Dy                 | Request.MediaWorkflow.Topology.Nodes.</br>VideoStream\_\*\*\*.Operation.RemoveWatermark | Y-axis offset of the top-left corner origin | string | Yes       | 1. Value range: [0, 4096]<br/>2. Unit: px |
| Width              | Request.MediaWorkflow.Topology.Nodes.</br>VideoStream\_\*\*\*.Operation.RemoveWatermark | Width                    | string | Yes       | 1. Value range: (0, 4096]<br/>2. Unit: px |
| Height             | Request.MediaWorkflow.Topology.Nodes.</br>VideoStream\_\*\*\*.Operation.RemoveWatermark | Height                    | string | Yes       | 1. Value range: (0, 4096]<br/>2. Unit: px |


`HlsPack\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------ | -------- | --------- | -------- | ------- |
| Type       | Request.MediaWorkflow.Topology.</br>Nodes.HlsPack\_\*\*\* | Node type | String    | Yes   | HlsPack |
| Operation          | Request.MediaWorkflow.</br>Topology.Nodes.HlsPack\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes       | None      |

`HlsPack\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | ---- | ---- |
| HlsPackInfo        | Request.MediaWorkflow.Topology.</br>Nodes.HlsPack\_\*\*\*.Operation | Packaging rule | Container | No   | None   |

`HlsPack\_\*\*\*.Operation.HlsPackInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | --------- | ---- | ---- |
| VideoStreamConfig  | Request.MediaWorkflow.Topology.</br>Nodes.HlsPack\_\*\*\*.Operation.HlsPackInfo | Video substream configuration | Container | No   | None   |

`HlsPack\_\*\*\*.Operation.HlsPackInfo.VideoStreamConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | --------------------------------------------------------- | --------- | ---- | ------------------------ |
| VideoStreamName    | Request.MediaWorkflow.Topology.Nodes.</br>HlsPack\_\*\*\*.Operation.HlsPackInfo.VideoStreamConfig | Video substream name                                              | Container | Yes   | The name must be consistent with the existing video node. |
| BandWidth          | Request.MediaWorkflow.Topology.Nodes.</br>HlsPack\_\*\*\*.Operation.HlsPackInfo.VideoStreamConfig | Video substream bandwidth limit. Unit: b/s. Value range: [0, 2000000000], where 0 indicates no limit | Container | No   | The value must be equal to or greater than 0. The default value is `0`.     |


`SDRtoHDR\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------- | -------- | --------- | ---- | -------- |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\* | Node type | Container | Yes   | SDRtoHDR |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes   | None       |

`SDRtoHDR\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------- | ----------------------------------------------------------- | ------------ | --------- | ---- | ------------------------------ |
| SDRtoHDR            | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation | SDR-to-HDR configuration | Container | Yes   | None                             |
| TranscodeTemplateId | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation | Transcoding template ID   | String    | Yes   | None                             |
| WatermarkTemplateId | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation | Watermark template ID   | String    | No   | Up to 3 watermark template IDs are supported. |
| Output              | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation | Output address     | Container | Yes   | None                             |

`SDRtoHDR\_\*\*\*.SDRtoHDR` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------- | ------ | ---- | ------------------- |
| HdrMode            | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation.SDRtoHDR | HDR mode | String | Yes   | 1. HLG<br/>2. HDR10 |

`SDRtoHDR\_\*\*\*.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | ---- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation.Output | Bucket region | String | Yes   | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation.Output | Bucket name | String | Yes   | None   |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.SDRtoHDR\_\*\*\*.Operation.Output | Result file name | String | Yes   | None   |



`VideoProcess\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ----------------------------------------------------- | -------- | --------- | ---- | ------------ |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\* | Node type | String    | Yes   | VideoProcess |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes   | None           |

`VideoProcess\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------- | ------------------------------------------------------------ | ---------- | --------- | ---- | ------------------------------ |
| TemplateId          | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation | Template ID     | String    | Yes   | None                             |
| TranscodeTemplateId | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation | Transcoding template ID | String    | Yes   | None                             |
| WatermarkTemplateId | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation | Watermark template ID | String    | No   | Up to 3 watermark template IDs are supported. |
| Output              | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation | Output address   | Container | Yes   | None                             |

`VideoProcess\_\*\*\*.Operation.Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------------------------------------------------------ | ------------ | ------ | ---- | ---- |
| Region             | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation.Output | Bucket region | String | Yes   | None   |
| Bucket             | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation.Output | Bucket name | String | Yes   | None   |
| Object             | Request.MediaWorkflow.Topology.</br>Nodes.VideoProcess\_\*\*\*.Operation.Output | Result file name | String | Yes   | None   |

`SCF\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | -------------------------------------------- | -------- | --------- | ---- | ---- |
| Type               | Request.MediaWorkflow.Topology.</br>Nodes.SCF\_\*\*\* | Node type | String    | Yes   | SCF  |
| Operation          | Request.MediaWorkflow.Topology.</br>Nodes.SCF\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes   | None   |

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
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.SuperResolution\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes     | None       |

`SuperResolution\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| TemplateId   | Request.MediaWorkflow.Topology.<br>Nodes.SuperResolution\_\*\*\*.Operation | Template ID  | String    | Yes   | None |
| TranscodeTemplateId | Request.MediaWorkflow.Topology..<br>Nodes.SuperResolution\_\*\*\*.Operation | Transcoding template ID  | String    | Yes   | None |
| WatermarkTemplateId | Request.MediaWorkflow.Topology..<br>Nodes.SuperResolution***.Operation | Watermark template ID  | String    | No   | Up to 3 watermark template IDs are supported. |
| Output       | Request.MediaWorkflow.Topology.<br>Nodes.SuperResolution\_\*\*\*.Operation | Output address | Container | Yes   | None |


`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Region             | Request.MediaWorkflow.Topology.<br>Nodes.SuperResolution\_\*\*\*.Operation.Output | Bucket region | String | Yes           | None                                                     |
| Bucket             | Request.MediaWorkflow.Topology.<br>Nodes.SuperResolution\_\*\*\*.Operation.Output | Bucket name | String | Yes           | None                                                     |
| Object   | Request.MediaWorkflow.Topology.<br>Nodes.SuperResolution\_\*\*\*.Operation.Output | Result file name  | String  | Yes  | None |


`Segment\_\*\*\*` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Segment\_\*\*\* | Node type | String    | Yes       | Segment |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Segment\_\*\*\* | Operation rule. Up to 6 operation rules are supported. | Container | Yes       | None        |

`Segment\_\*\*\*.Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Segment   | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation | Audio/Video segmentation parameter  | Container    | Yes   | None |
| Output   | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation | Output address | Container | Yes   | None |

`Segment` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Format            | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation.Segment | Encapsulation format | String | Yes  | AAC, MP3, FLAC, MP4, TS, MKV, AVI |
| Duration          | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation.Segment | Segment duration, in seconds | String | Yes  | The value must be an integer equal to or greater than 5. |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | ------ | ---- | ---- |
| Region             | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation.Output | Bucket region | String | Yes     | None                                                     |
| Bucket             | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation.Output | Bucket name | String | Yes     | None                                                     |
| Object   | Request.MediaWorkflow.Topology.<br>Nodes.Segment\_\*\*\*.Operation.Output | Result file name  | String  | Yes  | The ${Number} parameter must be included and used as the output sequence number of each audio/video segment after custom segmentation. |


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

#### Response 1: audio/video transcoding, top speed codec, frame capturing, conversion to animated images, voice separation, video montage, audio/video concatenation, smart cover, video enhancement, SDR-to-HDR, function customization, super resolution, and audio/video segmentation


```plaintext
<Response>
    <MediaWorkflow>
        <Name>demo</Name>
        <State>Active</State>
        <WorkflowId></WorkflowId>
        <Topology>
            <Dependencies>
                <Start>Snapshot_1581665960536,Transcode_1581665960537,Animation_1581665960538,Concat_1581665960539,SmartCover_1581665960539,VoiceSeparate_1581665960551,VideoMontage_1581665960551,SDRtoHDR_1581665960553,VideoProcess_1581665960554,SCF_1581665960566,SuperResolution_1581665960583,Segment_1581665960667</Start>
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
            </Nodes>
        </Topology>
        <BucketId></BucketId>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </MediaWorkflow>
</Response>
```

#### Response body 2: updating the HLS adaptive packaging workflow

```
<Response>
    <MediaWorkflow>
        <Name>demo</Name>
        <State>Active</State>
        <WorkflowId></WorkflowId>
        <BucketId></BucketId>
        <Topology>
            <Dependencies>
                <Start>HlsPackConfig_1581665960532</Start>
                <HlsPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</HlsPackConfig_1581665960532>
                <VideoStream_1581665960536>HlsPack</VideoStream_1581665960536>
                <VideoStream_1581665960537>HlsPack</VideoStream_1581665960537>
                <HlsPack_1581665960538>End</HlsPack_1581665960538>
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
                <HlsPackConfig_1581665960532>
                    <Type>HlsPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${InputPath}/${InputName}._${RunId}.${ext}</Object>
                        </Output>
                    </Operation>
                </HlsPackConfig_1581665960532>
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
                <HlsPack_1581665960538>
                    <Type>HlsPack</Type>
                    <Operation>
                        <HlsPackInfo>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960536</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960537</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                        </HlsPackInfo>
                    </Operation>
                </HlsPack_1581665960538>
            </Nodes>
        </Topology>
        <BucketId></BucketId>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </MediaWorkflow>
</Response>

```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------- | :-------- |
| RequestId          | Response | Unique ID of the request                   | String    |
| MediaWorkflow      | Response | Workflow array   | Container |

`MediaWorkflow` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ---------------------- | ----------------------------------------------------------- | --------- |
| Name               | Response.MediaWorkflow | Workflow name                                                  | String    |
| WorkflowId         | Response.MediaWorkflow | Workflow ID                                                    | String    |
| State              | Response.MediaWorkflow | Workflow status                                                  | String    |
| CreateTime         | Response.MediaWorkflow | Creation time                                                    | String    |
| UpdateTime         | Response.MediaWorkflow | Update time                                                    | String    |
| Topology           | Response.MediaWorkflow | Topology information. Same as `Request.MediaWorkflow.Topology` in `POST Workflow`.  | Container |

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

#### Request 1: audio/video transcoding, top speed codec, frame capturing, conversion to animated images, voice separation, video montage, smart cover, audio/video concatenation, function customization, super resolution, and audio/video segmentation

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
                <Start>Snapshot_1581665960536,Transcode_1581665960537,Animation_1581665960538,Concat_1581665960539,SmartCover_1581665960539,VoiceSeparate_1581665960551,VideoMontage_1581665960551,SDRtoHDR_1581665960553,VideoProcess_1581665960554,SCF_1581665960566,SuperResolution_1581665960583,Segment_1581665960667</Start>
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
                <Start>Snapshot_1581665960536,Transcode_1581665960537,Animation_1581665960538,Concat_1581665960539,SmartCover_1581665960539,VoiceSeparate_1581665960551,VideoMontage_1581665960551,SDRtoHDR_1581665960553,VideoProcess_1581665960554,SCF_1581665960566,SuperResolution_1581665960583,Segment_1581665960667</Start>
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
            </Nodes>
        </Topology>
        <BucketId></BucketId>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </MediaWorkflow>
</Response>
```


#### Request 2: HLS adaptive packaging


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
                <Start>HlsPackConfig_1581665960532</Start>
                <HlsPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</HlsPackConfig_1581665960532>
                <VideoStream_1581665960536>HlsPack</VideoStream_1581665960536>
                <VideoStream_1581665960537>HlsPack</VideoStream_1581665960537>
                <HlsPack_1581665960538>End</HlsPack_1581665960538>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId></QueueId>
                        <ObjectPrefix></ObjectPrefix>
                    </Input>
                </Start>
                <HlsPackConfig_1581665960532>
                    <Type>HlsPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${InputPath}/${InputName}._${RunId}.${ext}</Object>
                        </Output>
                    </Operation>
                </HlsPackConfig_1581665960532>
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
                <HlsPack_1581665960538>
                    <Type>HlsPack</Type>
                </HlsPack_1581665960538>
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
                <Start>HlsPackConfig_1581665960532</Start>
                <HlsPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</HlsPackConfig_1581665960532>
                <VideoStream_1581665960536>HlsPack</VideoStream_1581665960536>
                <VideoStream_1581665960537>HlsPack</VideoStream_1581665960537>
                <HlsPack_1581665960538>End</HlsPack_1581665960538>
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
                <HlsPackConfig_1581665960532>
                    <Type>HlsPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region></Region>
                            <Bucket></Bucket>
                            <Object>${InputPath}/${InputName}._${RunId}.${ext}</Object>
                        </Output>
                    </Operation>
                </HlsPackConfig_1581665960532>
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
                <HlsPack_1581665960538>
                    <Type>HlsPack</Type>
                    <Operation>
                        <HlsPackInfo>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960536</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960537</VideoStreamName>
                                <BandWidth>0</BandWidth>
                            </VideoStreamConfig>
                        </HlsPackInfo>
                    </Operation>
                </HlsPack_1581665960538>
            </Nodes>
        </Topology>
        <BucketId></BucketId>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </MediaWorkflow>
</Response>
```

