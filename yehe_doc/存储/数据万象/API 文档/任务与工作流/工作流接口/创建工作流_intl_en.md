## Feature Description

This API is used to create a workflow.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateTranscodeTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>



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

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

#### Request body 1: Screencapturing and transcoding the input video file, performing remuxing and intelligent thumbnail generation on the output file, and then performing image processing on the generated thumbnail

```plaintext
<Request>
    <MediaWorkflow>
        <Name>workflow-1</Name>
        <State>Active</State>
        <Topology>
            <Dependencies>
                <Start>Snapshot_1581665960536,Transcode_1581665960538</Start>
                <Snapshot_1581665960536>End</Snapshot_1581665960536>
                <Transcode_1581665960538>Segment_15816659605667,SmartCover_1581665960539</Transcode_1581665960538>
                <Segment_15816659605667>End</Segment_15816659605667>
                <SmartCover_1581665960539>PicProcess_15816659605668</SmartCover_1581665960539>
                <PicProcess_15816659605668>End</PicProcess_15816659605668>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
                        <PicProcessQueueId>p2911917386e148639319e13c285cc774</PicProcessQueueId>
                        <ObjectPrefix>input/workflow-1</ObjectPrefix>
                        <NotifyConfig>
                            <State>On</State>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat>JSON</ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>On</State>
                            <Video>true</Video>
                            <Audio>false</Audio>
                            <Image>false</Image>
                            <Custom>false</Custom>
                            <AllFile>false</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <Snapshot_1581665960536>
                    <Type>Snapshot</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>abc/${RunId}/snapshot-${number}.${Ext}</Object>
                            <SpriteObject>abc/${RunId}/sprite-${number}.${Ext}</SpriteObject>
                        </Output>
                    </Operation>
                </Snapshot_1581665960536>
                <Transcode_1581665960538>
                    <Type>Transcode</Type>
                    <Operation>
                        <TemplateId>t16e81a29fe48c4e23acefc247a7792b63</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>bcd/${RunId}/trans.{Ext}</Object>
                        </Output>
                    </Operation>
                </Transcode_1581665960538>
                <Segment_15816659605667>
                    <Type>Segment</Type>
                    <Operation>
                        <Segment>
                            <Format>mkv</Format>
                            <Duration>20</Duration>
                        </Segment>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>test-trans${Number}.{Ext}</Object>
                        </Output>
                    </Operation>
                </Segment_15816659605667>
                <SmartCover_1581665960539>
                    <Type>SmartCover</Type>
                    <Operation>
                        <TemplateId>t16e81a29fe48c4e23acefc247a7792b63</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>abc/${RunId}/cover-${Number}.{Ext}</Object>
                        </Output>
                    </Operation>
                </SmartCover_1581665960539>
                <PicProcess_15816659605668>
                    <Type>PicProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>bcd/${RunId}/pic.{Ext}</Object>
                        </Output>
                    </Operation>
                </PicProcess_15816659605668>
            </Nodes>
        </Topology>
    </MediaWorkflow>
</Request>
```

#### Request body 2: Adaptive bitrate streaming

```plaintext
<Request>
    <MediaWorkflow>
        <Name>workflow-2</Name>
        <State>Active</State>
        <Topology>
            <Dependencies>
                <Start>StreamPackConfig_1581665960532</Start>
                <StreamPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>StreamPack_1581665960538</VideoStream_1581665960536>
                <VideoStream_1581665960537>StreamPack_1581665960538</VideoStream_1581665960537>
                <StreamPack_1581665960538>End</StreamPack_1581665960538>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
                        <ObjectPrefix>input/workflow-2</ObjectPrefix>
                        <NotifyConfig>
                            <State>On</State>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat>JSON</ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>On</State>
                            <Video>true</Video>
                            <Audio>false</Audio>
                            <Image>false</Image>
                            <Custom>false</Custom>
                            <AllFile>false</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <StreamPackConfig_1581665960532>
                    <Type>StreamPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
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
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>${RunId}_Substream_1/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960536>
                <VideoStream_1581665960537>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606bgfdg2148c4ab182f55163ba7bj</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
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
                                <BandWidth>200000000</BandWidth>
                            </VideoStreamConfig>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960537</VideoStreamName>
                                <BandWidth>200000000</BandWidth>
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

<span id="Request"></span>
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

<span id="Topology"></span>
`Topology` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ----------------------------------- | ------------ | --------- | -------- | ---- |
| Dependencies      | Request.MediaWorkflow.</br>Topology | Node dependencies. | Container    | Yes   | None |
| Nodes             | Request.MediaWorkflow.</br>Topology | Node list. | Container    | Yes   | None |

`Nodes` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------------ | ----------------------------------------- | ------------------ | --------- | ------------ | ------------------------------------------------------------ |
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
| SuperResolution\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Super resolution node | Container | No | The node name must be prefixed with "SuperResolution". There can be multiple super resolution nodes. |
| Segment\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Audio/Video remuxing node | Container | No | The node name must be prefixed with `Segment`. There can be multiple audio/video remuxing nodes. |
| PicProcess\_\*\*\* | Request.MediaWorkflow.</br>Topology.Nodes | Image processing node | Container | No | The node name must be prefixed with "PicProcess". There can be multiple image processing nodes. |
| Tts\_\*\*\*              | Request.MediaWorkflow.</br>Topology.Nodes | Text-to-speech node   | Container | No           | The node name must be prefixed with "Tts". There can be multiple text-to-speech nodes.              |
| SpeechRecognition\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | Speech recognition node       | Container | No           | The node name must be prefixed with "SpeechRecognition". There can be multiple speech recognition nodes.              |
| AIRecognition\_\*\*\*  | Request.MediaWorkflow.</br>Topology.Nodes | AI-based recognition node       | Container | No           | The node name must be prefixed with "AIRecognition".         |



`Start` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------- | -------- | --------- | -------- | ----- |
| Type         | Request.MediaWorkflow.<br>Topology.Nodes.Start | Node type | String    | Yes   | Start |
| Input        | Request.MediaWorkflow.<br>Topology.Nodes.Start | Input information. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes   | None |


Animation\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Animation\_\*\*\* | Node type | String    | Yes       | Animation |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Animation\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


Snapshot\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Snapshot\_\*\*\* | Node type | String    | Yes       | Snapshot |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Snapshot\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


SmartCover\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.SmartCover\_\*\*\* | Node type | String    | Yes       | SmartCover |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.SmartCover\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


Transcode\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Transcode\_\*\*\* | Node type | String    | Yes       | Transcode |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Transcode\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


Concat\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Concat\_\*\*\* | Node type | String    | Yes       | Concat |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Concat\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


VoiceSeparate\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.VoiceSeparate\_\*\*\* | Node type | String    | Yes       | VoiceSeparate |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.VoiceSeparate\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


VideoMontage\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.VideoMontage\_\*\*\* | Node type | String    | Yes       | VideoMontage |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.VideoMontage\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


StreamPackConfig\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.StreamPackConfig\_\*\*\* | Node type | String    | Yes       | StreamPackConfig |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.StreamPackConfig\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


VideoStream\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.VideoStream\_\*\*\* | Node type | String    | Yes       | VideoStream |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.VideoStream\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


StreamPack\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.StreamPack\_\*\*\* | Node type | String    | Yes       | StreamPack |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.StreamPack\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


SDRtoHDR\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.SDRtoHDR\_\*\*\* | Node type | String    | Yes       | SDRtoHDR |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.SDRtoHDR\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


VideoProcess\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.VideoProcess\_\*\*\* | Node type | String    | Yes       | VideoProcess |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.VideoProcess\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


SCF\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.SCF\_\*\*\* | Node type | String    | Yes   | SCF  |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.SCF\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


SuperResolution\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.SuperResolution\_\*\*\* | Node type | String    | Yes | SuperResolution |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.SuperResolution\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


Segment\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Segment\_\*\*\* | Node type | String    | Yes       | Segment |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Segment\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


PicProcess\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.PicProcess\_\*\*\* | Node type | String    | Yes       | PicProcess |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.PicProcess\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


Tts\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.Tts\_\*\*\* | Node type | String    | Yes       | Tts |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.Tts\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |


SpeechRecognition\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.SpeechRecognition\_\*\*\* | Node type | String    | Yes       | SpeechRecognition |
| Operation          | Request.MediaWorkflow.<br>Topology.Nodes.SpeechRecognition\_\*\*\* | Operation rule. For more information, see [Structure](https://intl.cloud.tencent.com/document/product/1045/49945). | Container | Yes       | None        |

AIRecognition\_\*\*\* has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ---------------------------------------------------------- | -------- | --------- | -------- | --------- |
| Type               | Request.MediaWorkflow.<br>Topology.Nodes.AIRecognition\_\*\*\* | Node type | String    | Yes       | AIRecognition |


The dependencies of workflow nodes are as follows:

| Workflow Node Type | Linkable Node Types |
| ----------------- | ---------------------------------------------------------- |
| Start             | Snapshot,Animation,SmartCover,Transcode,Concat,VoiceSeparate,VideoMontage,</br>StreamPackConfig,SDRtoHDR,VideoProcess,SCF,SuperResolution,Segment,PicProcess,Tts,SpeechRecognition,AIRecognition |
| Snapshot          | PicProcess,SCF,End |
| Animation         | SCF,End |
| SmartCover        | PicProcess,SCF,End |
| Transcode         | Snapshot,Animation,SmartCover,Concat,VideoMontage,SDRtoHDR,VideoProcess,SCF,Segment,SpeechRecognition,End |
| Concat            | Transcode,Snapshot,Animation,SmartCover,SDRtoHDR,VideoProcess,SCF,Segment,End |
| VoiceSeparate     | SCF,SpeechRecognition,End |
| VideoMontage      | Snapshot,Animation,SDRtoHDR,VideoProcess,SCF,SuperResolution,Segment,End |
| StreamPackConfig  | VideoStream |
| VideoStream       | StreamPack |
| StreamPack        | End |
| SDRtoHDR          | Transcode,Concat,VideoMontage,VoiceSeparate,SmartCover,Animation,VideoProcess,SCF,SuperResolution,End |
| VideoProcess      | Transcode,Concat,VideoMontage,VoiceSeparate,SmartCover,Animation,SDRtoHDR,SCF,Segment,SuperResolution,End |
| SCF               | SDRtoHDR,Snapshot,Transcode,HighSpeedHd,Concat,VideoMontage,VoiceSeparate,SmartCover,Animation,VideoProcess,End |
| SuperResolution   | VideoMontage,Transcode,SmartCover,Animation,Snapshot,SCF,Segment,SDRtoHDR,VideoProcess,End |
| Segment           | End |
| PicProcess        | SCF,End |
| Tts               | SCF,Transcode,End |
| SpeechRecognition | SCF,Tts,End |
| AIRecognition     | End |




Wildcards supported by workflow are as follows:

| Wildcard | Description |
| ----------------- | ------------------------------------ |
| ${InputPath}       | Input file path (excluding the filename)          |
| ${InputName}       | Input filename (excluding the extension)          |
| ${InputNameAndExt} | Input filename (including the extension)            |
| ${RunId}           | Instance ID                             |
| ${Ext}             | Codec extension                         |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49945).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

#### Response body 1: Screencapturing and transcoding the input video file, performing remuxing and intelligent thumbnail generation on the output file, and then performing image processing on the generated thumbnail


```plaintext
<Response>
    <RequestId>NjJmMWQxYjNfOTBmYTUwNjRfNWYyY18x</RequestId>
    <MediaWorkflow>
        <Name>workflow-1</Name>
        <State>Active</State>
        <WorkflowId>wc666d0b9f9dd47ae9137a096252d49f7</WorkflowId>
        <BucketId>test-1234567890</BucketId>
        <CreateTime>2022-07-14T12:37:28+0800</CreateTime>
        <UpdateTime>2022-07-14T12:37:28+0800</UpdateTime>
        <Topology>
            <Dependencies>
                <Start>Snapshot_1581665960536,Transcode_1581665960538</Start>
                <Snapshot_1581665960536>End</Snapshot_1581665960536>
                <Transcode_1581665960538>Segment_15816659605667,SmartCover_1581665960539</Transcode_1581665960538>
                <Segment_15816659605667>End</Segment_15816659605667>
                <SmartCover_1581665960539>PicProcess_15816659605668</SmartCover_1581665960539>
                <PicProcess_15816659605668>End</PicProcess_15816659605668>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
                        <PicProcessQueueId>p2911917386e148639319e13c285cc774</PicProcessQueueId>
                        <ObjectPrefix>input/workflow-1</ObjectPrefix>
                        <NotifyConfig>
                            <State>On</State>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat>JSON</ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>On</State>
                            <Video>true</Video>
                            <Audio>false</Audio>
                            <Image>false</Image>
                            <Custom>false</Custom>
                            <AllFile>false</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <Snapshot_1581665960536>
                    <Type>Snapshot</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>abc/${RunId}/snapshot-${number}.${Ext}</Object>
                            <SpriteObject>abc/${RunId}/sprite-${number}.${Ext}</SpriteObject>
                        </Output>
                    </Operation>
                </Snapshot_1581665960536>
                <Transcode_1581665960538>
                    <Type>Transcode</Type>
                    <Operation>
                        <TemplateId>t16e81a29fe48c4e23acefc247a7792b63</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>bcd/${RunId}/trans.{Ext}</Object>
                        </Output>
                    </Operation>
                </Transcode_1581665960538>
                <Segment_15816659605667>
                    <Type>Segment</Type>
                    <Operation>
                        <Segment>
                            <Format>mkv</Format>
                            <Duration>20</Duration>
                        </Segment>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>test-trans${Number}.{Ext}</Object>
                        </Output>
                    </Operation>
                </Segment_15816659605667>
                <SmartCover_1581665960539>
                    <Type>SmartCover</Type>
                    <Operation>
                        <TemplateId>t16e81a29fe48c4e23acefc247a7792b63</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>abc/${RunId}/cover-${Number}.{Ext}</Object>
                        </Output>
                    </Operation>
                </SmartCover_1581665960539>
                <PicProcess_15816659605668>
                    <Type>PicProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>bcd/${RunId}/pic.{Ext}</Object>
                        </Output>
                    </Operation>
                </PicProcess_15816659605668>
            </Nodes>
        </Topology>
    </MediaWorkflow>
</Response>
```

#### Response body 2: Adaptive bitrate streaming

```
<Response>
    <MediaWorkflow>
        <Name>workflow-2</Name>
        <State>Active</State>
        <WorkflowId>w93aa43ba105347169fa093ed857b2a90</WorkflowId>
        <BucketId>test-1234567890</BucketId>
        <CreateTime>2022-07-14T12:37:28+0800</CreateTime>
        <UpdateTime>2022-07-14T12:37:28+0800</UpdateTime>
        <Topology>
            <Dependencies>
                <Start>StreamPackConfig_1581665960532</Start>
                <StreamPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>StreamPack_1581665960538</VideoStream_1581665960536>
                <VideoStream_1581665960537>StreamPack_1581665960538</VideoStream_1581665960537>
                <StreamPack_1581665960538>End</StreamPack_1581665960538>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
                        <ObjectPrefix>input/workflow-2</ObjectPrefix>
                        <NotifyConfig>
                            <State>On</State>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat>JSON</ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>On</State>
                            <Video>true</Video>
                            <Audio>false</Audio>
                            <Image>false</Image>
                            <Custom>false</Custom>
                            <AllFile>false</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <StreamPackConfig_1581665960532>
                    <Type>StreamPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
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
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>${RunId}_Substream_1/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960536>
                <VideoStream_1581665960537>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606bgfdg2148c4ab182f55163ba7bj</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
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
                                <BandWidth>200000000</BandWidth>
                            </VideoStreamConfig>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960537</VideoStreamName>
                                <BandWidth>200000000</BandWidth>
                            </VideoStreamConfig>
                        </StreamPackInfo>
                    </Operation>
                </StreamPack_1581665960538>
            </Nodes>
        </Topology>
    </MediaWorkflow>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

<span id="Response"></span>
`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------ | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| MediaWorkflow      | Response | Workflow array.   | Container |

`MediaWorkflow` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ---------------------- | ------------------------------------------------------------ | --------- |
| Name               | Response.MediaWorkflow | Workflow name.                                                  | String    |
| WorkflowId         | Response.MediaWorkflow | Workflow ID.                                                    | String    |
| State              | Response.MediaWorkflow | Workflow status.                                                  | String    |
| CreateTime         | Response.MediaWorkflow | Creation time.                                                    | String    |
| UpdateTime         | Response.MediaWorkflow | Update time.                                                    | String    |
| Topology           | Response.MediaWorkflow | Topology information, which is the same as `Request.MediaWorkflow.Topology` in the request.  | Container |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Samples

#### Request 1: Screencapturing and transcoding the input video file, performing remuxing and intelligent thumbnail generation on the output file, and then performing image processing on the generated thumbnail

```plaintext
POST /workflow HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <MediaWorkflow>
        <Name>workflow-1</Name>
        <State>Active</State>
        <Topology>
            <Dependencies>
                <Start>Snapshot_1581665960536,Transcode_1581665960538</Start>
                <Snapshot_1581665960536>End</Snapshot_1581665960536>
                <Transcode_1581665960538>Segment_15816659605667,SmartCover_1581665960539</Transcode_1581665960538>
                <Segment_15816659605667>End</Segment_15816659605667>
                <SmartCover_1581665960539>PicProcess_15816659605668</SmartCover_1581665960539>
                <PicProcess_15816659605668>End</PicProcess_15816659605668>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
                        <PicProcessQueueId>p2911917386e148639319e13c285cc774</PicProcessQueueId>
                        <ObjectPrefix>input/workflow-1</ObjectPrefix>
                        <NotifyConfig>
                            <State>On</State>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat>JSON</ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>On</State>
                            <Video>true</Video>
                            <Audio>false</Audio>
                            <Image>false</Image>
                            <Custom>false</Custom>
                            <AllFile>false</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <Snapshot_1581665960536>
                    <Type>Snapshot</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>abc/${RunId}/snapshot-${number}.${Ext}</Object>
                            <SpriteObject>abc/${RunId}/sprite-${number}.${Ext}</SpriteObject>
                        </Output>
                    </Operation>
                </Snapshot_1581665960536>
                <Transcode_1581665960538>
                    <Type>Transcode</Type>
                    <Operation>
                        <TemplateId>t16e81a29fe48c4e23acefc247a7792b63</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>bcd/${RunId}/trans.{Ext}</Object>
                        </Output>
                    </Operation>
                </Transcode_1581665960538>
                <Segment_15816659605667>
                    <Type>Segment</Type>
                    <Operation>
                        <Segment>
                            <Format>mkv</Format>
                            <Duration>20</Duration>
                        </Segment>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>test-trans${Number}.{Ext}</Object>
                        </Output>
                    </Operation>
                </Segment_15816659605667>
                <SmartCover_1581665960539>
                    <Type>SmartCover</Type>
                    <Operation>
                        <TemplateId>t16e81a29fe48c4e23acefc247a7792b63</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>abc/${RunId}/cover-${Number}.{Ext}</Object>
                        </Output>
                    </Operation>
                </SmartCover_1581665960539>
                <PicProcess_15816659605668>
                    <Type>PicProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>bcd/${RunId}/pic.{Ext}</Object>
                        </Output>
                    </Operation>
                </PicProcess_15816659605668>
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
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NjJmMWQxYjNfOTBmYTUwNjRfNWYyY18x

<Response>
    <RequestId>NjJmMWQxYjNfOTBmYTUwNjRfNWYyY18x</RequestId>
    <MediaWorkflow>
        <Name>workflow-1</Name>
        <State>Active</State>
        <WorkflowId>wc666d0b9f9dd47ae9137a096252d49f7</WorkflowId>
        <BucketId>test-1234567890</BucketId>
        <CreateTime>2022-07-14T12:37:28+0800</CreateTime>
        <UpdateTime>2022-07-14T12:37:28+0800</UpdateTime>
        <Topology>
            <Dependencies>
                <Start>Snapshot_1581665960536,Transcode_1581665960538</Start>
                <Snapshot_1581665960536>End</Snapshot_1581665960536>
                <Transcode_1581665960538>Segment_15816659605667,SmartCover_1581665960539</Transcode_1581665960538>
                <Segment_15816659605667>End</Segment_15816659605667>
                <SmartCover_1581665960539>PicProcess_15816659605668</SmartCover_1581665960539>
                <PicProcess_15816659605668>End</PicProcess_15816659605668>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
                        <PicProcessQueueId>p2911917386e148639319e13c285cc774</PicProcessQueueId>
                        <ObjectPrefix>input/workflow-1</ObjectPrefix>
                        <NotifyConfig>
                            <State>On</State>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat>JSON</ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>On</State>
                            <Video>true</Video>
                            <Audio>false</Audio>
                            <Image>false</Image>
                            <Custom>false</Custom>
                            <AllFile>false</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <Snapshot_1581665960536>
                    <Type>Snapshot</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>abc/${RunId}/snapshot-${number}.${Ext}</Object>
                            <SpriteObject>abc/${RunId}/sprite-${number}.${Ext}</SpriteObject>
                        </Output>
                    </Operation>
                </Snapshot_1581665960536>
                <Transcode_1581665960538>
                    <Type>Transcode</Type>
                    <Operation>
                        <TemplateId>t16e81a29fe48c4e23acefc247a7792b63</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>bcd/${RunId}/trans.{Ext}</Object>
                        </Output>
                    </Operation>
                </Transcode_1581665960538>
                <Segment_15816659605667>
                    <Type>Segment</Type>
                    <Operation>
                        <Segment>
                            <Format>mkv</Format>
                            <Duration>20</Duration>
                        </Segment>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>test-trans${Number}.{Ext}</Object>
                        </Output>
                    </Operation>
                </Segment_15816659605667>
                <SmartCover_1581665960539>
                    <Type>SmartCover</Type>
                    <Operation>
                        <TemplateId>t16e81a29fe48c4e23acefc247a7792b63</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>abc/${RunId}/cover-${Number}.{Ext}</Object>
                        </Output>
                    </Operation>
                </SmartCover_1581665960539>
                <PicProcess_15816659605668>
                    <Type>PicProcess</Type>
                    <Operation>
                        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>bcd/${RunId}/pic.{Ext}</Object>
                        </Output>
                    </Operation>
                </PicProcess_15816659605668>
            </Nodes>
        </Topology>
    </MediaWorkflow>
</Response>
```


#### Request 2: Adaptive bitrate streaming


```plaintext
POST /workflow HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <MediaWorkflow>
        <Name>workflow-2</Name>
        <State>Active</State>
        <Topology>
            <Dependencies>
                <Start>StreamPackConfig_1581665960532</Start>
                <StreamPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>StreamPack_1581665960538</VideoStream_1581665960536>
                <VideoStream_1581665960537>StreamPack_1581665960538</VideoStream_1581665960537>
                <StreamPack_1581665960538>End</StreamPack_1581665960538>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
                        <ObjectPrefix>input/workflow-2</ObjectPrefix>
                        <NotifyConfig>
                            <State>On</State>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat>JSON</ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>On</State>
                            <Video>true</Video>
                            <Audio>false</Audio>
                            <Image>false</Image>
                            <Custom>false</Custom>
                            <AllFile>false</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <StreamPackConfig_1581665960532>
                    <Type>StreamPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
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
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>${RunId}_Substream_1/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960536>
                <VideoStream_1581665960537>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606bgfdg2148c4ab182f55163ba7bj</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
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
                                <BandWidth>200000000</BandWidth>
                            </VideoStreamConfig>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960537</VideoStreamName>
                                <BandWidth>200000000</BandWidth>
                            </VideoStreamConfig>
                        </StreamPackInfo>
                    </Operation>
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
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf95s=

<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf95s=</RequestId>
    <MediaWorkflow>
        <Name>workflow-2</Name>
        <State>Active</State>
        <WorkflowId>w93aa43ba105347169fa093ed857b2a90</WorkflowId>
        <BucketId>test-1234567890</BucketId>
        <CreateTime>2022-07-14T12:37:28+0800</CreateTime>
        <UpdateTime>2022-07-14T12:37:28+0800</UpdateTime>
        <Topology>
            <Dependencies>
                <Start>StreamPackConfig_1581665960532</Start>
                <StreamPackConfig_1581665960532>VideoStream_1581665960536,VideoStream_1581665960537</StreamPackConfig_1581665960532>
                <VideoStream_1581665960536>StreamPack_1581665960538</VideoStream_1581665960536>
                <VideoStream_1581665960537>StreamPack_1581665960538</VideoStream_1581665960537>
                <StreamPack_1581665960538>End</StreamPack_1581665960538>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
                        <ObjectPrefix>input/workflow-2</ObjectPrefix>
                        <NotifyConfig>
                            <State>On</State>
                            <Url>http://www.callback.com</Url>
                            <Event>TaskFinish,WorkflowFinish</Event>
                            <Type>Url</Type>
                            <ResultFormat>JSON</ResultFormat>
                        </NotifyConfig>
                        <ExtFilter>
                            <State>On</State>
                            <Video>true</Video>
                            <Audio>false</Audio>
                            <Image>false</Image>
                            <Custom>false</Custom>
                            <AllFile>false</AllFile>
                        </ExtFilter>
                    </Input>
                </Start>
                <StreamPackConfig_1581665960532>
                    <Type>StreamPackConfig</Type>
                    <Operation>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
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
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>${RunId}_Substream_1/video.m3u8</Object>
                        </Output>
                    </Operation>
                </VideoStream_1581665960536>
                <VideoStream_1581665960537>
                    <Type>VideoStream</Type>
                    <Operation>
                        <TemplateId>t1460606bgfdg2148c4ab182f55163ba7bj</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
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
                                <BandWidth>200000000</BandWidth>
                            </VideoStreamConfig>
                            <VideoStreamConfig>
                                <VideoStreamName>VideoStream_1581665960537</VideoStreamName>
                                <BandWidth>200000000</BandWidth>
                            </VideoStreamConfig>
                        </StreamPackInfo>
                    </Operation>
                </StreamPack_1581665960538>
            </Nodes>
        </Topology>
    </MediaWorkflow>
</Response>
```
