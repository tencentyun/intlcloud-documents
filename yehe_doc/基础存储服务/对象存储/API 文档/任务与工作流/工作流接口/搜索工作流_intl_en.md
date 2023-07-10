## Feature Description

This API (`Describe Workflow`) is used to search for a workflow.

## Request

#### Sample request

```shell
GET /workflow HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

The request body of this request is empty.

#### Request parameters

| Parameter Name (Keyword) | Description                                                         | Type   | Required |
| :----------------- | :--------------------------- | :----- | :------- |
| ids                |  Workflow ID. If you enter multiple IDs, separate them by comma. | string | No       |
| name               |  Workflow name                   | string | No       |
| pageNumber         | Page number                       | string | No       |
| pageSize           | Number of entries per page                     | string | No       |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <MediaWorkflowList>
        <Name>demo</Name>
        <WorkflowId></WorkflowId>
        <State></State>
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
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </MediaWorkflowList>
    <MediaWorkflowList>
        <Name>demo</Name>
        <State>Active</State>
        <WorkflowId></WorkflowId>
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
    </MediaWorkflowList>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------------------ | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| TotalCount         | Response | Total number of workflows                       | Int       |
| PageNumber         | Response | Current page number. Same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page. Same as `pageSize` in the request.   | Int       |
| MediaWorkflowList  | Response | Workflow array                      | Container |

`MediaWorkflowList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | -------------------------- | ---------- | --------- | -------- | ---------------------------------------------------- |
| Name               | Response.MediaWorkflowList | Workflow name. | String    | Yes       | The value can contain up to 128 letters, digits, hyphens, and underscores. |
| WorkflowId         | Response.MediaWorkflowList | Workflow ID  | String    | Yes       | Unique workflow ID                                        |
| State              | Response.MediaWorkflowList | Workflow status | String    | Yes       | 1. Active <br/>2. Paused<br/>                        |
| CreateTime         | Response.MediaWorkflowList | Creation time   | String    | Yes       | None                                                   |
| UpdateTime         | Response.MediaWorkflowList | Update time   | String    | Yes       | None                                                   |
| Topology           | Response.MediaWorkflowList | Topology information   | Container | Yes       | Same as `Request.MediaWorkflow.Topology` in `POST Workflow`. |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request 1: Workflow ID

```shell
GET /workflow?ids=demo,demo1 HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
```

#### Response 1

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <MediaWorkflowList>
        <Name>demo</Name>
        <WorkflowId></WorkflowId>
        <State></State>
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
                            <Object>bcd/${RunId}/trans-${number}.mp4</Object>
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
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </MediaWorkflowList>
</Response>
```

#### Request 2: Workflow list

```shell
GET /workflow?pageNumber=1&pageSize=1 HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
```

#### Response 2

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=

<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>11</PageSize>
    <MediaWorkflowList>
        <Name>demo</Name>
        <WorkflowId></WorkflowId>
        <State></State>
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
                            <Object>bcd/${RunId}/trans-${number}.mp4</Object>
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
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </MediaWorkflowList>
    <MediaWorkflowList>
        <Name>demo</Name>
        <State>Active</State>
        <WorkflowId></WorkflowId>
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
    </MediaWorkflowList>
</Response>
```
