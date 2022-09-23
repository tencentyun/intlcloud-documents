## Feature Description

This API is used to query a workflow.

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
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/49351).

#### Request body

The request body of this request is empty.

#### Request parameters

| Parameter (Keyword) | Description | Type | Required |
| :----------------- | :----------------------------- | :----- | :------- |
| ids                |  Workflow ID. If you enter multiple IDs, separate them by comma. | string | No       |
| name               |  Workflow name                   | string | No       |
| pageNumber  | Page number.                  |  string | No       |
| pageSize    | Number of entries per page.                | string | No       |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <RequestId>NjJmMWZiZTFfOTBmYTUwNjRfNjVmNl8x</RequestId>
    <TotalCount>2</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <MediaWorkflowList>
        <Name>workflow-1</Name>
        <State>Active</State>
        <WorkflowId>wc666d0b9f9dd47ae9137a096252d49f7</WorkflowId>
        <BucketId>test-1234567890</BucketId>
        <CreateTime>2022-06-29T14:37:44+0800</CreateTime>
        <UpdateTime>2022-06-29T14:37:44+0800</UpdateTime>
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
                            <Event>TaskFinish,WorkflowFinish,WorkflowStart</Event>
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
    </MediaWorkflowList>
    <MediaWorkflowList>
        <Name>workflow-2</Name>
        <State>Active</State>
        <WorkflowId>w93aa43ba105347169fa093ed857b2a90</WorkflowId>
        <BucketId>test-1234567890</BucketId>
        <CreateTime>2022-06-29T14:37:44+0800</CreateTime>
        <UpdateTime>2022-06-29T14:37:44+0800</UpdateTime>
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
                            <Event>TaskFinish,WorkflowFinish,WorkflowStart</Event>
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
| PageNumber         | Response | Current page number, which is the same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page, which is the same as `pageSize` in the request.   | Int       |
| MediaWorkflowList  | Response | Workflow array                      | Container |

`MediaWorkflowList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | -------------------------- | ---------- | --------- | -------- | ---------------------------------------------------- |
| Name               | Response.MediaWorkflowList | Workflow name. | String    | Yes       | The value can contain up to 128 letters, digits, hyphens, and underscores. |
| WorkflowId         | Response.MediaWorkflowList | Workflow ID  | String    | Yes       | Unique workflow ID                                        |
| State              | Response.MediaWorkflowList | Workflow status | String    | Yes       | 1. Active <br/>2. Paused<br/>                        |
| CreateTime         | Response.MediaWorkflowList | Creation time   | String    | Yes       | None                                                   |
| UpdateTime         | Response.MediaWorkflowList | Update time   | String    | Yes       | None                                                   |
| Topology           | Response.MediaWorkflowList | Topology information   | Container | Yes       | <a href="https://intl.cloud.tencent.com/document/product/1045/43733" target="_blank">Same as `Topology` in the workflow creation API.</a> |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request 1: Workflow ID

```shell
GET /workflow?ids=wc666d0b9f9dd47ae9137a096252d49f7,A,B HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
```

#### Response 1

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NjJmMWZmMzRfOTBmYTUwNjRfNjVmOF8x

<Response>
    <RequestId>NjJmMWZmMzRfOTBmYTUwNjRfNjVmOF8x</RequestId>
        <MediaWorkflowList>
        <Name>workflow-1</Name>
        <State>Active</State>
        <WorkflowId>wc666d0b9f9dd47ae9137a096252d49f7</WorkflowId>
        <BucketId>test-1234567890</BucketId>
        <CreateTime>2022-06-29T14:37:44+0800</CreateTime>
        <UpdateTime>2022-06-29T14:37:44+0800</UpdateTime>
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
                            <Event>TaskFinish,WorkflowFinish,WorkflowStart</Event>
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
    </MediaWorkflowList>
    <NonExistIDs>A</NonExistIDs>
    <NonExistIDs>B</NonExistIDs>
</Response>
```

#### Request 2: Workflow list

```shell
GET /workflow?pageNumber=1&pageSize=10 HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
```

#### Response 2

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=

<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=</RequestId>
    <TotalCount>2</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <MediaWorkflowList>
        <Name>workflow-1</Name>
        <State>Active</State>
        <WorkflowId>wc666d0b9f9dd47ae9137a096252d49f7</WorkflowId>
        <BucketId>test-1234567890</BucketId>
        <CreateTime>2022-06-29T14:37:44+0800</CreateTime>
        <UpdateTime>2022-06-29T14:37:44+0800</UpdateTime>
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
                            <Event>TaskFinish,WorkflowFinish,WorkflowStart</Event>
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
    </MediaWorkflowList>
    <MediaWorkflowList>
        <Name>workflow-2</Name>
        <State>Active</State>
        <WorkflowId>w93aa43ba105347169fa093ed857b2a90</WorkflowId>
        <BucketId>test-1234567890</BucketId>
        <CreateTime>2022-06-29T14:37:44+0800</CreateTime>
        <UpdateTime>2022-06-29T14:37:44+0800</UpdateTime>
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
                            <Event>TaskFinish,WorkflowFinish,WorkflowStart</Event>
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
    </MediaWorkflowList>
</Response>
```
