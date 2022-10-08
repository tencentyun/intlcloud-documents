## Feature Description

This API (`Describe WorkflowExecution`) is used to get the details of a workflow instance.

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
> - When this feature is used by a sub-account, relevant permissions must be granted.
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
  <WorkflowExecution>
    <RunId>37145b2919714156bd97f91dc03fa2b4</RunId>
    <WorkflowId>we65e4d260e1042debdfb7e4560a19d3d</WorkflowId>
    <WorkflowName></WorkflowName>
    <State>Success</State>
    <CreateTime>2019-07-07T12:12:12+0800</CreateTime>
    <Object>https://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/mars_white_test.mp4</Object>
    <Topology>
        <Dependencies>
            <Start>Snapshot_1581665960536,Animation_1581665960538</Start>
            <Snapshot_1581665960536>End</Snapshot_1581665960536>
            <Animation_1581665960538>End</Animation_1581665960538>
        </Dependencies>
        <Nodes>
            <Start>
                <Type>Start</Type>
                <Input>
                    <QueueId></QueueId>
                    <ObjectPrefix></ObjectPrefix>
                </Input>
            </Start>
            <Snapshot_1581665960536>
                <Type>Snapshot</Type>
                <Operation>
                    <TemplateId></TemplateId>
                    <Output>
                        <Region></Region>
                        <Bucket></Bucket>
                        <Object>abc/${RunId}/snapshot-${number}.${Ext}</Object>
                    </Output>
                </Operation>
            </Snapshot_1581665960536>
            <Animation_1581665960538>
                <Type>Animation</Type>
                <Operation>
                    <TemplateId></TemplateId>
                    <Output>
                        <Region></Region>
                        <Bucket></Bucket>
                        <Object>bcd/${RunId}/bcd.gif</Object>
                    </Output>
                </Operation>
            </Animation_1581665960538>
        </Nodes>
    </Topology>
    <Tasks>
        <Type>Start</Type>
        <CreateTime>2019-07-07T12:12:12+0800</CreateTime>
        <EndTime></EndTime>
        <State>Success</State>
        <JobId>f9ddcf74ebfd4f0caa0bb78692432d69</JobId>
        <Name>Start</Name>
    </Tasks>
    <Tasks>
        <Type>Snapshot</Type>
        <CreateTime>2019-07-07T12:12:12+0800</CreateTime>
        <EndTime></EndTime>
        <State>Success</State>
        <JobId>f9ddcf74ebfd4f0caa0bb78692432d69</JobId>
        <Name>Snapshot_1581665960536</Name>
    </Tasks>
    <Tasks>
        <Type>Animation</Type>
        <CreateTime>2019-07-07T12:12:12+0800</CreateTime>
        <EndTime></EndTime>
        <State>Failed</State>
        <JobId>f9ddcf74ebfd4f0caa0bb78692432d69</JobId>
        <Name>Animation_1581665960538</Name>
    </Tasks>
  </WorkflowExecution>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------- | :-------- |
| WorkflowExecution  | Response | Workflow instance details | Container |

`WorkflowExecution` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------- | :----------------------------------------------------------- | :-------- |
| RunId              | Response.WorkflowExecution | Workflow instance ID                                                | string    |
| WorkflowId         | Response.WorkflowExecution | Workflow ID                                                    | string    |
| WorkflowName       | Response.WorkflowExecution | Workflow name                                                   | string    |
| State              | Response.WorkflowExecution | Workflow instance status                                               | string    |
| CreateTime         | Response.WorkflowExecution | Creation time                                                    | string    |
| Object             | Response.WorkflowExecution | COS object address                                                 | string    |
| Topology           | Response.WorkflowExecution | Topology information. Same as `Response.MediaWorkflowList.Topology` in `GetWorkflow`. | Container |
| Tasks              | Response.WorkflowExecution | Workflow instance job                                               | Container |

`Tasks` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------- | :--------------- | :----- |
| Type               | Response.WorkflowExecution.Tasks | Job node type | string |
| CreateTime         | Response.WorkflowExecution.Tasks | Creation time         | string |
| EndTime            | Response.WorkflowExecution.Tasks | End time         | string |
| State              | Response.WorkflowExecution.Tasks | Job status         | string |
| JobId              | Response.WorkflowExecution.Tasks | Job ID          | string |
| Name               | Response.WorkflowExecution.Tasks | Node name         | string |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
GET /workflowexecution/37145b2919714156bd97f91dc03fa2b4 HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
  <WorkflowExecution>
    <RunId>37145b2919714156bd97f91dc03fa2b4</RunId>
    <WorkflowId>we65e4d260e1042debdfb7e4560a19d3d</WorkflowId>
    <WorkflowName></WorkflowName>
    <State>Success</State>
    <CreateTime>2019-07-07T12:12:12+0800</CreateTime>
    <Object>https://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/mars_white_test.mp4</Object>
    <Topology>
        <Dependencies>
            <Start>Snapshot_1581665960536,Animation_1581665960538</Start>
            <Snapshot_1581665960536>End</Snapshot_1581665960536>
            <Animation_1581665960538>End</Animation_1581665960538>
        </Dependencies>
        <Nodes>
            <Start>
                <Type>Start</Type>
                <Input>
                    <QueueId></QueueId>
                    <ObjectPrefix></ObjectPrefix>
                </Input>
            </Start>
            <Snapshot_1581665960536>
                <Type>Snapshot</Type>
                <Operation>
                    <TemplateId></TemplateId>
                    <Output>
                        <Region></Region>
                        <Bucket></Bucket>
                        <Object>abc/${RunId}/snapshot-${number}.${Ext}</Object>
                    </Output>
                </Operation>
            </Snapshot_1581665960536>
            <Animation_1581665960538>
                <Type>Animation</Type>
                <Operation>
                    <TemplateId></TemplateId>
                    <Output>
                        <Region></Region>
                        <Bucket></Bucket>
                        <Object>bcd/${RunId}/bcd.gif</Object>
                    </Output>
                </Operation>
            </Animation_1581665960538>
        </Nodes>
    </Topology>
    <Tasks>
        <Type>Start</Type>
        <CreateTime>2019-07-07T12:12:12+0800</CreateTime>
        <EndTime></EndTime>
        <State>Success</State>
        <JobId>f9ddcf74ebfd4f0caa0bb78692432d69</JobId>
        <Name>Start</Name>
    </Tasks>
    <Tasks>
        <Type>Snapshot</Type>
        <CreateTime>2019-07-07T12:12:12+0800</CreateTime>
        <EndTime></EndTime>
        <State>Success</State>
        <JobId>f9ddcf74ebfd4f0caa0bb78692432d69</JobId>
        <Name>Snapshot_1581665960536</Name>
    </Tasks>
    <Tasks>
        <Type>Animation</Type>
        <CreateTime>2019-07-07T12:12:12+0800</CreateTime>
        <EndTime></EndTime>
        <State>Failed</State>
        <JobId>f9ddcf74ebfd4f0caa0bb78692432d69</JobId>
        <Name>Animation_1581665960538</Name>
    </Tasks>
  </WorkflowExecution>
</Response>
```
