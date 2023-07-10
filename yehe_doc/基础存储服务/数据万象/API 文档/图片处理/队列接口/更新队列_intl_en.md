## Feature Description

This API is used to update an image processing queue.

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
PUT /picqueue/<queueId> HTTP/1.1
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

```plaintext
<Request>
    <Name>My-Queue-Pic</Name>
    <State>Active</State>
    <NotifyConfig>
        <State>On</State>
        <Url>http://callback.demo.com</Url>
        <Type>Url</Type>
        <Event>TaskFinish,WorkflowFinish</Event>
        <ResultFormat>JSON</ResultFormat>
    </NotifyConfig>
</Request>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ---------------- | ------- | ----------------- | ------ | -------- | ------ | ----- |
| Request            | None     | Response container | Container | Yes        | None     |  None   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| :--------------- | :------- | :------------------------------ | :-------- | -------- | ------ | ----- |
| Name             | Request | Queue name, which can contain up to 128 bytes.             | String    | Yes       | None     |  None   |
| State            | Request | 1. Active: Jobs in the queue will be scheduled and executed by the media processing service. <br>2. Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will not be affected. | String      | Yes | None | None |
| NotifyConfig     | Request | Callback configuration                          | Container | Yes       | None     |  None   |


`NotifyConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| :--------------- | :------- | :------------------------------ | :-------- | -------- | ------ | ----- |
| State        | Request.NotifyConfig | Callback status: `Off` or `On`. | String | No                 | Off  | On/Off |
| Event        | Request.NotifyConfig | Callback event         | String | Yes if `State` is `On`  | None   | Job completion: `TaskFinish`; workflow completion: `WorkflowFinish`. |
| ResultFormat | Request.NotifyConfig | Callback format         | String | No | XML   | JSON/XML |
| Type         | Request.NotifyConfig | Callback type         | String | Yes if `State` is `On` | None   | `Url` or `TDMQ` |
| Url          | Request.NotifyConfig | Callback address         | String | Yes if `State` is `On` and `Type` is `Url` | None   | The callback address cannot be a private network address. |
| MqMode       | Request.NotifyConfig | TDMQ queue mode    | String | Yes if `State` is `On` and `Type` is `TDMQ` | Queue | `Topic`: Topic subscription <br/>`Queue`: Queue service </td> |
| MqRegion     | Request.NotifyConfig | TDMQ region    | String | Yes if `State` is `On` and `Type` is `TDMQ` | None   | Valid values: `sh` (Shanghai), `bj` (Beijing), `gz` (Guangzhou), `cd` (Chengdu), `hk` (Hong Kong, China). |
| MqName       | Request.NotifyConfig | TDMQ topic name    | String | Yes if `State` is `On` and `Type` is `TDMQ` | None   | None |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610). 

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <RequestId>NjJmNDczY2RfOTBmYTUwNjRfNTA4ZV85</RequestId>
    <Queue>
        <QueueId>pb926e1dce3ed4e47a4f08692164f4869</QueueId>
        <Name>My-Queue-Pic</Name>
        <State>Active</State>
        <NotifyConfig>
            <Url>http://callback.demo.com</Url>
            <Event>TaskFinish,WorkflowFinish</Event>
            <Type>Url</Type>
            <State>On</State>
            <ResultFormat>JSON</ResultFormat>
        </NotifyConfig>
        <UpdateTime>2022-08-09T16:23:11+0800</UpdateTime>
        <CreateTime>2022-08-09T16:13:05+0800</CreateTime>
    </Queue>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| RequestId          | Response | Unique ID of the request                                                | String    |
| Queue              | Response | Queue information                                                     | Container |

`Queue` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------- | :--------------------------- | :-------- |
| QueueId            | Response.Queue | Queue ID                      | String    |
| Name               | Response.Queue | Queue name                     | String    |
| State              | Response.Queue | Current status: `Active` or `Paused`. | String    |
| NotifyConfig       | Response.Queue | Callback configuration, which is the same as `Request.NotifyConfig`. | Container |
| MaxSize            | Response.Queue | Maximum length of the queue                 | Int       |
| MaxConcurrent      | Response.Queue | Maximum number of concurrent jobs in the current queue | Int       |
| Category           | Response.Queue | Queue type                     | String    |
| UpdateTime         | Response.Queue | Update time                     | String    |
| CreateTime         | Response.Queue | Creation time                     | String    |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Samples

#### Request

```plaintext
PUT /picqueue/pb926e1dce3ed4e47a4f08692164f4869 HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 162
Content-Type: application/xml

<Request>
    <Name>My-Queue-Pic</Name>
    <State>Active</State>
    <NotifyConfig>
        <State>On</State>
        <Url>http://callback.demo.com</Url>
        <Type>Url</Type>
        <Event>TaskFinish,WorkflowFinish</Event>
        <ResultFormat>JSON</ResultFormat>
    </NotifyConfig>
</Request>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 09 Aug 2022 16:23:12 GMT
Server: tencent-ci
x-ci-request-id: NjJmNDczY2RfOTBmYTUwNjRfNTA4ZV85

<Response>
    <RequestId>NjJmNDczY2RfOTBmYTUwNjRfNTA4ZV85</RequestId>
    <Queue>
        <QueueId>pb926e1dce3ed4e47a4f08692164f4869</QueueId>
        <Name>My-Queue-Pic</Name>
        <State>Active</State>
        <NotifyConfig>
            <Url>http://callback.demo.com</Url>
            <Event>TaskFinish,WorkflowFinish</Event>
            <Type>Url</Type>
            <State>On</State>
            <ResultFormat>JSON</ResultFormat>
        </NotifyConfig>
        <UpdateTime>2022-08-09T16:23:11+0800</UpdateTime>
        <CreateTime>2022-08-09T16:13:05+0800</CreateTime>
    </Queue>
</Response>
```
