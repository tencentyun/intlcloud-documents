## Feature Description

This API is used to submit a media information query job.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateAnimationTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
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
POST /jobs HTTP/1.1
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

```shell
<Request>
    <Tag>MediaInfo</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | -------- |
| Request            | None     | Request container | Container | Yes       |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ------------------------- | --------- | -------- |
| Tag                | Request | Job tag: MediaInfo                          | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default value). It has a higher priority than that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default value) or `TDMQ`. It has a higher priority than that of the queue.                    | String | No |
| CallBack           | Request | Job callback address, which has a higher priority than that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://intl.cloud.tencent.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |



<span id="operation"></span>
`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ---------------- | --------- | -------- |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |


`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | ---------- | ------ | -------- |
| Object             | Request.Input | Media filename | String | Yes   |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j229ed9e2f60c11ec8525e36307395bf9</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>MediaInfo</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| JobsDetail         | Response | Job details | Container |

<span id="jobsDetail"></span>
`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag | Response.JobsDetail | Job tag: MediaInfo | String |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | ID of the queue which the job is in                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation          | Response.JobsDetail | Operation rule                           | Container |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------ | ---------------- | ------ |
| Region             | Response.JobsDetail.Input | Bucket region     | String |
| Bucket             | Response.JobsDetail.Input | Result storage bucket | String |
| Object             | Response.JobsDetail.Input | Output result filename | String |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :--------------------------------- | :-------- |
| MediaInfo | Response.JobsDetail.Operation | Output video information, which will not be returned when the job is not completed. |  Container |
| UserData           | Response.JobsDetail.Operation | The user information passed through.                      | String |
| JobLevel    | Response.JobsDetail.Operation | Job priority                                                         | String |

`MediaInfo` has the following sub-nodes:
Same as the `Response.MediaInfo` node in the `GenerateMediaInfo` API.

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples


#### Request

```shell
POST /jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>MediaInfo</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j229ed9e2f60c11ec8525e36307395bf9</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>MediaInfo</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```

