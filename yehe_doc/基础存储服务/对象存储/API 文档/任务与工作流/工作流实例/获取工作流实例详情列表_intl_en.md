## Feature Description

This API is used to get the list of workflow instances.

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
GET /workflowexecution HTTP/1.1
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

#### Request parameters

| Parameter (Keyword) | Description | Type | Required |
| :----------------- | :----------------------------------------------------------- | :----- | :------- |
| workflowId         | Workflow ID                                                    | String | Yes       |
| name               | Filename                                                     | String | No       |
| orderByTime        | `Desc` (default) or `Asc`                                   | String | No       |
| size               | Maximum number of jobs that can be pulled. Default value: `10`; maximum value: `100`.                      | String | No       |
| states             | Workflow instance status. If you enter multiple statuses, separate them by comma.<br> Valid values: `All`, `Success`, `Failed`, `Running`, `Cancel`. Default value: `All`. | String | No       |
| startCreationTime  | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`        | String | No       |
| endCreationTime    | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`        | String | No       |
| nextToken          | Context token for pagination                   | String | No       |
| jobId              | Batch data processing job ID, which is used to scan the workflow instance executed accordingly.  | String | No       |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <RequestId>NjJmMjEyMmFfZWM0YTYyNjRfN2U2NV8yNmI0</RequestId>
    <WorkflowExecutionList>
        <RunId>i166ee19017b011eda8a5525400c540df</RunId>
        <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
        <Object>wk-test/game.mp4</Object>
        <CreateTime>2022-08-09T14:54:17+08:00</CreateTime>
        <State>Success</State>
    </WorkflowExecutionList>
    <WorkflowExecutionList>
        <RunId>i769bd26517af11ed917f525400a3c59f</RunId>
        <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
        <Object>wk-test/game.mp4</Object>
        <CreateTime>2022-08-09T14:49:49+08:00</CreateTime>
        <State>Success</State>
    </WorkflowExecutionList>
    <NextToken>115716</NextToken>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :-------------------- | :------- | :----------------- | :-------- |
| WorkflowExecutionList | Response | Workflow instance details | Container |
| RequestId             | Response | Request ID           | String |
| NextToken             | Response | Context token for pagination | String    |

`WorkflowExecutionList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :------------- | :----- |
| RunId              | Response.WorkflowExecutionList | Workflow instance ID  | String |
| WorkflowId         | Response.WorkflowExecutionList | Workflow ID      | String |
| State              | Response.WorkflowExecutionList | Workflow instance status | String |
| CreateTime         | Response.WorkflowExecutionList | Creation time       | String |
| Object             | Response.WorkflowExecutionList | COS object address   | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Samples

#### Request

```shell
GET /workflowexecution?workflowId=web6ac56c1ef54dbfa44d7f4103203be9 HTTP/1.1
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
x-ci-request-id: NjJmMjEyMmFfZWM0YTYyNjRfN2U2NV8yNmI0

<Response>
    <RequestId>NjJmMjEyMmFfZWM0YTYyNjRfN2U2NV8yNmI0</RequestId>
    <WorkflowExecutionList>
        <RunId>i166ee19017b011eda8a5525400c540df</RunId>
        <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
        <Object>wk-test/game.mp4</Object>
        <CreateTime>2022-08-09T14:54:17+08:00</CreateTime>
        <State>Success</State>
    </WorkflowExecutionList>
    <WorkflowExecutionList>
        <RunId>i769bd26517af11ed917f525400a3c59f</RunId>
        <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
        <Object>wk-test/game.mp4</Object>
        <CreateTime>2022-08-09T14:49:49+08:00</CreateTime>
        <State>Success</State>
    </WorkflowExecutionList>
    <NextToken>115716</NextToken>
</Response>
```
