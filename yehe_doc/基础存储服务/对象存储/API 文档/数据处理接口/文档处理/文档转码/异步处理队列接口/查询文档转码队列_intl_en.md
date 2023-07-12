## Feature Description

This API (`DescribeDocProcessQueues`) is used to query file transcoding queues.

## Request

#### Sample request

```shell
GET /docqueue?pageNumber=1&pageSize=2 HTTP/1.1
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

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ | -------- |
| queueIds   | Queue ID. If you enter multiple IDs, separate them by comma. | string | No       |
| state | 1. Active: Jobs in the queue will be scheduled and executed by the file preview service. <br>2. Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will continue without being affected. | String      | No |
| pageNumber | Page number. Default value: the first page.                                                       | string | No       |
| pageSize   | Number of entries per page. Default value: `10`.                                                     | string | No       |



## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610). 

#### Response body

The response body returns **application/xml** data.

Response body 1: The following contains all the nodes when `pageNumber` and `pageSize` are specified.

```shell
<Response>
        <TotalCount>1</TotalCount>
        <RequestId>RequestId</RequestId>
        <PageNumber>1</PageNumber>
        <PageSize>2</PageSize>
        <QueueList>
                <QueueId>QueueId</QueueId>
                <Name>QueueName</Name>
                <State>Active</State>
                <NotifyConfig>
                        <Url>url</Url>
                        <Event>Event</Event>
                        <Type/></Type>
                        <State>Off</State>
                </NotifyConfig>
                <MaxSize>10000</MaxSize>
                <MaxConcurrent>10</MaxConcurrent>
                <CreateTime>CreateTime</CreateTime>
                <UpdateTime>UpdateTime</UpdateTime>
                <BucketId>BucketId</BucketId>
                <Category>DocProcess</Category>
        </QueueList>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------------------ | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| TotalCount         | Response | Total number of queues                        | Int       |
| PageNumber         | Response | Current page number, which is the same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page, which is the same as `pageSize` in the request.   | Int       |
| QueueList          | Response | Queue array                        | Container |

`QueueList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------- | :--------------------------- | :-------- |
| QueueId            | Response.QueueList | Queue ID                      | String    |
| Name               | Response.QueueList | Queue name                     | String    |
| State              | Response.QueueList | Current status: `Active` or `Paused` | String    |
| NotifyConfig       | Response.QueueList | Callback configuration                     | Container |
| MaxSize            | Response.QueueList | Maximum length of the queue                 | Int       |
| MaxConcurrent      | Response.QueueList | Maximum number of concurrent jobs in the current queue | Int       |
| UpdateTime         | Response.QueueList | Update time                     | String    |
| CreateTime         | Response.QueueList | Creation time                     | String    |

`NotifyConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------ | :-------------------- | :----- |
| Url                | Response.QueueList.NotifyConfig | Callback address              | String |
| State              | Response.QueueList.NotifyConfig | Switch status: `On` or `Off`              | String |
| Type               | Response.QueueList.NotifyConfig | Callback type: Url                      | String |
| Event              | Response.QueueList.NotifyConfig | The event that triggered the callback                    | String |


Response body 2: The following contains all the nodes when `queueIds` is specified.

```shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <QueueList>
        <QueueId>A</QueueId>
        <Name></Name>
        <State>Active</State>
        <NotifyConfig>
            <Url></Url>
        </NotifyConfig>
    </QueueList>
    <NonExistPIDs>
        <QueueID>B</QueueID>
        <QueueID>C</QueueID>
    </NonExistPIDs>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------------------- | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| QueueList          | Response | Queue array, which is the same as `QueueList` described above. | Container |
| NonExistPIDs       | Response | List of non-existing queue IDs             | Container |

`NonExistPIDs` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :------ | :----- |
| QueueID            | Response.NonExistPIDs | Queue ID | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```plaintext
GET /docqueue?pageNumber=1&pageSize=2 HTTP/1.1
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: cos-python-sdk-v5.3.2
Host: examplebucket-1250000000.ci.ap-chongqing.myqcloud.com
Content-Type: application/xml
Authorization: Authorization
```

#### Response

```plaintext
HTTP/1.1 200 OK
Date: Mon, 27 Jul 2020 07:29:28 GMT
Content-Type: application/xml
Content-Length: 677
Connection: keep-alive
Server: tencent-ci
x-ci-request-id: NWYxZTgyNTdfYzc2OTQzNjRfMzUx****

<?xml version="1.0" encoding="utf-8"?>
<Response>
        <TotalCount>1</TotalCount>
        <RequestId>NWYxZTgyNTdfYzc2OTQzNjRfMzUx****</RequestId>
        <PageNumber>1</PageNumber>
        <PageSize>2</PageSize>
        <QueueList>
                <QueueId>p2505d57bdf4c4329804b58a6a5fb1572</QueueId>
                <Name>queue-doc-process-1</Name>
                <State>Active</State>
                <NotifyConfig>
                        <Url/>
                        <Event/>
                        <Type/>
                        <State>Off</State>
                </NotifyConfig>
                <MaxSize>10000</MaxSize>
                <MaxConcurrent>10</MaxConcurrent>
                <CreateTime>2020-07-24T22:42:27+0800</CreateTime>
                <UpdateTime>2020-07-24T22:42:27+0800</UpdateTime>
                <BucketId>examplebucket-1250000000.</BucketId>
                <Category>DocProcessing</Category>
        </QueueList>
</Response>
```
