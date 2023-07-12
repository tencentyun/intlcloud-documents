## Feature Description

This API (`DescribeSpeechQueues`) is used to query speech recognition queues.

## Request

#### Sample request

```shell
GET /asrqueue HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

The request body of this request is empty.

#### Request parameters

<table>
   <tr>
      <th nowrap="nowrap">Name	</th>
      <th>Type</th>
      <th>Description</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>queueIds</td>
      <td>string</td>
      <td>Queue ID. If you enter multiple IDs, separate them by comma. </td>
      <td>No</td>
   </tr>
   <tr>
      <td>state</td>
      <td>string</td>
      <td>
        1. Active: Jobs in the queue will be scheduled and executed by the speech recognition service. <br>2. Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will continue without being affected.</td>
      <td>No</td>
   </tr>
   <tr>
      <td>pageNumber</td>
      <td>string</td>
      <td>Page number</td>
      <td>No</td>
   </tr>
   <tr>
      <td>pageSize</td>
      <td>string</td>
      <td>Number of entries per page</td>
      <td>No</td>
   </tr>
</table>



## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610). 

#### Response body

The response body returns **application/xml** data. The following contains all the nodes when `pageNumber` and `pageSize` are specified:

```shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <QueueList>
        <QueueId>A</QueueId>
        <Name></Name>
        <State>Active</State>
        <MaxSize>10000</MaxSize>
        <MaxConcurrent>10</MaxConcurrent>
        <UpdateTime></UpdateTime>
        <CreateTime></CreateTime>
        <NotifyConfig>
            <Url></Url>
            <Type></Type>
            <State></State>
            <Event></Event>
        </NotifyConfig>
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
| PageNumber         | Response | Current page number. Same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page. Same as `pageSize` in the request.   | Int       |
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
| :----------------- | :------------------------------ | :-------------------------------- | :----- |
| Url                | Response.QueueList.NotifyConfig | Callback address                          | String |
| State              | Response.QueueList.NotifyConfig | Switch status: `On` or `Off`              | String |
| Type               | Response.QueueList.NotifyConfig | Callback type: Url                      | String |
| Event              | Response.QueueList.NotifyConfig | The event that triggered the callback                    | String |



The response body returns **application/xml** data. The following contains all the nodes when `queueIds` is specified:

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
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------------------- | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| QueueList          | Response | Queue array. Same as `QueueList` described above. | Container |
| NonExistPIDs       | Response | List of non-existing queue IDs             | Container |

`NonExistPIDs` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------- | :------ | :----- |
| QueueID            | Response.NonExistPIDs | Queue ID | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

