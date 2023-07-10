## Feature Description

This API is used to search for an AI-based content recognition queue.

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
GET /ai_queue HTTP/1.1
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
| :----------------- | :------------------------- | :----- | :------- |
| queueId            | Queue ID. If you enter multiple IDs, separate them by comma. | String | No     |
| state              | 1. Active: Jobs in the queue will be scheduled and executed by the media processing service. <br>2. Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will not be affected. | String | No     |
| pageNumber         | Page number. Default value: `1`.   | String | No     |
| pageSize           | Number of entries per page. Default value: `10`. | String | No     |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352). 

#### Response body

The response body returns **application/xml** data. The following contains all the nodes when `pageNumber` and `pageSize` are specified:

```shell
<Response>
    <RequestId>NjJmMzI5MmRfOTBmYTUwNjRfNjcwM18x</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <QueueList>
        <QueueId>p23f69f4779e64b18aa61e70d5416c071</QueueId>
        <Name>queue-ai-process-1</Name>
        <State>Active</State>
        <NotifyConfig>
            <Url>http://callback.demo.com</Url>
            <Event>TaskFinish,WorkflowFinish</Event>
            <Type>Url</Type>
            <State>On</State>
            <ResultFormat>JSON</ResultFormat>
        </NotifyConfig>
        <MaxSize>10000</MaxSize>
        <MaxConcurrent>10</MaxConcurrent>
        <UpdateTime>2022-08-09T16:23:11+0800</UpdateTime>
        <CreateTime>2022-08-09T16:23:11+0800</CreateTime>
        <Category>AIProcess</Category>
    </QueueList>
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
| TotalCount         | Response | Total number of queues                        | Int       |
| PageNumber         | Response | Current page number, which is the same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page, which is the same as `pageSize` in the request.   | Int       |
| QueueList          | Response | Queue array                        | Container array |
| NonExistPIDs       | Response | List of IDs of non-existent queues             | String array |

`QueueList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------- | :--------------------------- | :-------- |
| QueueId            | Response.QueueList | Queue ID                      | String    |
| Name               | Response.QueueList | Queue name                     | String    |
| State              | Response.QueueList | Current status: `Active` or `Paused` | String    |
| NotifyConfig       | Response.QueueList | Callback configuration                     | Container |
| MaxSize            | Response.QueueList | Maximum length of the queue                 | Int       |
| MaxConcurrent      | Response.QueueList | Maximum number of concurrent jobs in the current queue | Int       |
| Category           | Response.QueueList | Queue type                     | String    |
| UpdateTime         | Response.QueueList | Update time                     | String    |
| CreateTime         | Response.QueueList | Creation time                     | String    |

`NotifyConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------ | :-------------------------------- | :----- |
| Url                | Response.QueueList.NotifyConfig | Callback address                          | String |
| State              | Response.QueueList.NotifyConfig | Switch status: `On` or `Off`              | String |
| Type               | Response.QueueList.NotifyConfig | Callback type: Url                      | String |
| Event              | Response.QueueList.NotifyConfig | Job completed: `TaskFinish`; workflow completed: `WorkflowFinish` | String |
| ResultFormat       | Response.QueueList.NotifyConfig | Callback type: `XML` or `JSON`.          | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request 1: Searching for the specified queue

```shell
GET /ai_queue?queueIds=p23f69f4779e64b18aa61e70d5416c071,A,B HTTP/1.1
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
Date: Thu, 09 Aug 2022 16:23:12 GMT
Server: tencent-ci
x-ci-request-id: NjJmMzJjNDFfOTBmYTUwNjRfNjQ5NF8x

<Response>
    <RequestId>NjJmMzJjNDFfOTBmYTUwNjRfNjQ5NF8x</RequestId>
    <QueueList>
        <QueueId>p23f69f4779e64b18aa61e70d5416c071</QueueId>
        <Name>queue-ai-process-1</Name>
        <State>Active</State>
        <NotifyConfig>
            <Url>http://callback.demo.com</Url>
            <Event>TaskFinish,WorkflowFinish</Event>
            <Type>Url</Type>
            <State>On</State>
            <ResultFormat>JSON</ResultFormat>
        </NotifyConfig>
        <MaxSize>10000</MaxSize>
        <MaxConcurrent>10</MaxConcurrent>
        <UpdateTime>2022-08-09T16:23:11+0800</UpdateTime>
        <CreateTime>2022-08-09T16:23:11+0800</CreateTime>
        <Category>AIProcess</Category>
    </QueueList>
    <NonExistPIDs>A</NonExistPIDs>
    <NonExistPIDs>B</NonExistPIDs>
</Response>
```

#### Request 2: Querying the list of queues

```shell
GET /ai_queue?pageSize=10&pageNumber=1&category=CateAll HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
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
Date: Thu, 09 Aug 2022 16:23:12 GMT
Server: tencent-ci
x-ci-request-id: NjJmMzI5MmRfOTBmYTUwNjRfNjcwM18x

<Response>
    <RequestId>NjJmMzI5MmRfOTBmYTUwNjRfNjcwM18x</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <QueueList>
        <QueueId>p23f69f4779e64b18aa61e70d5416c071</QueueId>
        <Name>queue-ai-process-1</Name>
        <State>Active</State>
        <NotifyConfig>
            <Url>http://callback.demo.com</Url>
            <Event>TaskFinish,WorkflowFinish</Event>
            <Type>Url</Type>
            <State>On</State>
            <ResultFormat>JSON</ResultFormat>
        </NotifyConfig>
        <MaxSize>10000</MaxSize>
        <MaxConcurrent>10</MaxConcurrent>
        <UpdateTime>2022-08-09T16:23:11+0800</UpdateTime>
        <CreateTime>2022-08-09T16:23:11+0800</CreateTime>
        <Category>AIProcess</Category>
    </QueueList>
</Response>
```

