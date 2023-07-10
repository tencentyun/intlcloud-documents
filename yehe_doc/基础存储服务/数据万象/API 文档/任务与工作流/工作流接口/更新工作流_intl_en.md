## Feature Description

This API is used to update a workflow.


## Request

#### Sample request

```shell
PUT /workflow/<WorkflowId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/49351).

#### Request body

This request requires the following request body: 

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
                            <Duration>25</Duration>
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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :--------------------------------------------- | :-------- | -------- |
| Request            | None     | <a href="https://intl.cloud.tencent.com/document/product/1045/43733" target="_blank">Same as `Request` in the workflow creation API.</a> | Container | Yes   |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

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
                            <Duration>25</Duration>
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

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :----------------------------------------------------------- | :-------- | -------- |
| Response            | None     | <a href="https://intl.cloud.tencent.com/document/product/1045/43733" target="_blank">Same as `Response` in the workflow creation API.</a> | Container | Yes   |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request 1: Updating the workflow configuration

```plaintext
PUT /workflow/wc666d0b9f9dd47ae9137a096252d49f7 HTTP/1.1
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
                            <Duration>25</Duration>
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
Content-Length: 100
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
                            <Duration>25</Duration>
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

#### Request 2: Disabling a workflow

```plaintext
PUT /workflow/wc666d0b9f9dd47ae9137a096252d49f7?paused HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-chongqing.myqcloud.com
```

#### Response 2

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: keep-alive
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NjJmMWRiMDlfOTBmYTUwNjRfNWYzMl80
```

#### Request 3: Enabling a workflow

```plaintext
PUT /workflow/wc666d0b9f9dd47ae9137a096252d49f7?active HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-chongqing.myqcloud.com
```

#### Response 3

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: keep-alive
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NjJmMWRiMDlfOTBmYTUwNjRfNWYzMl80
```
