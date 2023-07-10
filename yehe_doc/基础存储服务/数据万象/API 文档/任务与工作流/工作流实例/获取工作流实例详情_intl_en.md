## Feature Description

This API is used to get the details of a workflow instance.


## Request

#### Sample request

```shell
GET /workflowexecution/<RunId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml
```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <RequestId>NjJmMjA5MjZfZWM0YTYyNjRfN2U3ZF8yNzk1</RequestId>
    <WorkflowExecution>
        <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
        <Name>workflow-1</Name>
        <RunId>i166ee19017b011eda8a5525400c540df</RunId>
        <CreateTime>2022-08-09T14:54:17+08:00</CreateTime>
        <Object>wk-test/game.mp4</Object>
        <State>Success</State>
        <Topology>
            <Dependencies>
                <Start>Transcode_1581665960537</Start>
                <Snapshot_1581665960536>End</Snapshot_1581665960536>
                <Transcode_1581665960537>Snapshot_1581665960536</Transcode_1581665960537>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
                        <ObjectPrefix>/wk-test</ObjectPrefix>
                        <ExtFilter>
                            <State>On</State>
                            <Video>false</Video>
                            <Audio>false</Audio>
                            <ContentType>false</ContentType>
                            <Custom>true</Custom>
                            <CustomExts>mp4</CustomExts>
                            <AllFile>false</AllFile>
                            <Image>false</Image>
                        </ExtFilter>
                        <PicProcessQueueId>p2911917386e148639319e13c285cc774</PicProcessQueueId>
                    </Input>
                </Start>
                <Snapshot_1581665960536>
                    <Type>Snapshot</Type>
                    <Operation>
                        <TemplateId>t07740e32081b44ad7a0aea03adcffd54a</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>snapshot-${number}.jpg</Object>
                        </Output>
                    </Operation>
                </Snapshot_1581665960536>
                <Transcode_1581665960537>
                    <Type>Transcode</Type>
                    <Operation>
                        <TemplateId>t01e57db1c2d154d2fb57aa5de9313a897</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>trans1.mp4</Object>
                        </Output>
                    </Operation>
                </Transcode_1581665960537>
            </Nodes>
        </Topology>
        <Tasks>
            <Type>Snapshot</Type>
            <JobId>j23c11e1e17b011edaab4ab15ec33d076</JobId>
            <CreateTime>2022-08-09T14:54:40+08:00</CreateTime>
            <Name>Snapshot_1581665960536</Name>
            <State>Success</State>
            <StartTime>2022-08-09T14:54:40+08:00</StartTime>
            <EndTime>2022-08-09T14:54:42+08:00</EndTime>
            <Code>Success</Code>
            <Message></Message>
        </Tasks>
        <Tasks>
            <Type>Transcode</Type>
            <JobId>j168668b217b011ed8efb27bb229e2d11</JobId>
            <CreateTime>2022-08-09T14:54:18+08:00</CreateTime>
            <Name>Transcode_1581665960537</Name>
            <State>Success</State>
            <StartTime>2022-08-09T14:54:18+08:00</StartTime>
            <EndTime>2022-08-09T14:54:39+08:00</EndTime>
            <Code>Success</Code>
            <Message>success</Message>
        </Tasks>
    </WorkflowExecution>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------- | :-------- |
| RequestId             | Response | Request ID           | String |
| WorkflowExecution  | Response | Workflow instance details | Container |

`WorkflowExecution` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------- | :----------------------------------------------------------- | :-------- |
| WorkflowId         | Response.WorkflowExecution | Workflow ID                                                    | String    |
| WorkflowName       | Response.WorkflowExecution | Workflow name                                                   | String    |
| RunId              | Response.WorkflowExecution | Workflow instance ID                                                | String    |
| CreateTime         | Response.WorkflowExecution | Creation time                                                     | String    |
| Object             | Response.WorkflowExecution | COS object address                                                 | String    |
| State              | Response.WorkflowExecution | Workflow instance status                                               | String    |
| Topology           | Response.WorkflowExecution | <a href="https://intl.cloud.tencent.com/document/product/1045/43733" target="_blank">Same as `Topology` in the workflow creation API.</a> | Container |
| Tasks              | Response.WorkflowExecution | Workflow instance job                                               | Container array |

`Tasks` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------- | :--------------- | :----- |
| Type               | Response.WorkflowExecution.Tasks | Job node type | String |
| State              | Response.WorkflowExecution.Tasks | Job status         | String |
| JobId              | Response.WorkflowExecution.Tasks | Job ID          | String |
| CreateTime         | Response.WorkflowExecution.Tasks | Job creation time         | String |
| StartTime          | Response.WorkflowExecution.Tasks | Job start time         | String |
| EndTime            | Response.WorkflowExecution.Tasks | Job end time         | String |
| Code               | Response.WorkflowExecution.Tasks | Job error code         | String |
| Message            | Response.WorkflowExecution.Tasks | Job error message         | String |
| Name               | Response.WorkflowExecution.Tasks | Workflow node name   | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Samples

#### Request

```shell
GET /workflowexecution/i166ee19017b011eda8a5525400c540df HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-chongqing.myqcloud.com
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Thu, 09 Aug 2022 16:23:12 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <RequestId>NjJmMjA5MjZfZWM0YTYyNjRfN2U3ZF8yNzk1</RequestId>
    <WorkflowExecution>
        <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
        <Name>workflow-1</Name>
        <RunId>i166ee19017b011eda8a5525400c540df</RunId>
        <CreateTime>2022-08-09T14:54:17+08:00</CreateTime>
        <Object>wk-test/game.mp4</Object>
        <State>Success</State>
        <Topology>
            <Dependencies>
                <Start>Transcode_1581665960537</Start>
                <Snapshot_1581665960536>End</Snapshot_1581665960536>
                <Transcode_1581665960537>Snapshot_1581665960536</Transcode_1581665960537>
            </Dependencies>
            <Nodes>
                <Start>
                    <Type>Start</Type>
                    <Input>
                        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
                        <ObjectPrefix>/wk-test</ObjectPrefix>
                        <ExtFilter>
                            <State>On</State>
                            <Video>false</Video>
                            <Audio>false</Audio>
                            <ContentType>false</ContentType>
                            <Custom>true</Custom>
                            <CustomExts>mp4</CustomExts>
                            <AllFile>false</AllFile>
                            <Image>false</Image>
                        </ExtFilter>
                        <PicProcessQueueId>p2911917386e148639319e13c285cc774</PicProcessQueueId>
                    </Input>
                </Start>
                <Snapshot_1581665960536>
                    <Type>Snapshot</Type>
                    <Operation>
                        <TemplateId>t07740e32081b44ad7a0aea03adcffd54a</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>snapshot-${number}.jpg</Object>
                        </Output>
                    </Operation>
                </Snapshot_1581665960536>
                <Transcode_1581665960537>
                    <Type>Transcode</Type>
                    <Operation>
                        <TemplateId>t01e57db1c2d154d2fb57aa5de9313a897</TemplateId>
                        <Output>
                            <Region>ap-chongqing</Region>
                            <Bucket>test-1234567890</Bucket>
                            <Object>trans1.mp4</Object>
                        </Output>
                    </Operation>
                </Transcode_1581665960537>
            </Nodes>
        </Topology>
        <Tasks>
            <Type>Snapshot</Type>
            <JobId>j23c11e1e17b011edaab4ab15ec33d076</JobId>
            <CreateTime>2022-08-09T14:54:40+08:00</CreateTime>
            <Name>Snapshot_1581665960536</Name>
            <State>Success</State>
            <StartTime>2022-08-09T14:54:40+08:00</StartTime>
            <EndTime>2022-08-09T14:54:42+08:00</EndTime>
            <Code>Success</Code>
            <Message></Message>
        </Tasks>
        <Tasks>
            <Type>Transcode</Type>
            <JobId>j168668b217b011ed8efb27bb229e2d11</JobId>
            <CreateTime>2022-08-09T14:54:18+08:00</CreateTime>
            <Name>Transcode_1581665960537</Name>
            <State>Success</State>
            <StartTime>2022-08-09T14:54:18+08:00</StartTime>
            <EndTime>2022-08-09T14:54:39+08:00</EndTime>
            <Code>Success</Code>
            <Message>success</Message>
        </Tasks>
    </WorkflowExecution>
```
