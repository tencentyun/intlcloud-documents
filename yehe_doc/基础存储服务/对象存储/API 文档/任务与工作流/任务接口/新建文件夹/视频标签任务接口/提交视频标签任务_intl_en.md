## Feature Description

This API (`CreateMediaJobs`) is used to submit a video tagging job.

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
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request requires the following request body:

```shell
<Request>
  <Tag>VideoTag</Tag>
  <Input>
    <Object></Object>
  </Input>
  <Operation>
    <VideoTag>
      <Scenario>
      </Scenario>
    </VideoTag>
  </Operation>
  <QueueId></QueueId>
  <CallBack></CallBack>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None     | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Job type: VideoTag                                   | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule. Up to six jobs can be performed on the same file.                                                | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | --------------- | ------ | ---- |
| Object             | Request.Input | Name of the media file on which to perform the video tagging job. Currently, .mp4, .avi, .mkv, .wmv, .rmvb, .flv, and .mov formats are supported. For videos longer than 30 minutes, submit a ticket for assistance. | String | Yes |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------| ----------------- | ------------------------------------------------------------ | --------- | ---- |
| VideoTag            | Request.Operation | `VideoTag` job parameter                                             | Container | Yes  |

`VideoTag` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | :------------------------ | -------------------------------------- | --------- | ---- |---- |
| Scenario           | Request.Operation.VideoTag | Scenario type. You can select the application scenario of the video tag. The used algorithm, input, and output vary by scenario. | string | Yes | The current version is only adapted to the `Stream` scenario |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <JobsDetail>
    <Code></Code>
    <Message></Message>
    <JobId></JobId>
    <State></State>
    <CreationTime></CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <QueueId></QueueId>
    <Tag>VideoTag</Tag>
    <Input>
      <Object></Object>
    </Input>
    <Operation>
      <VideoTag>
        <Scenario>
        </Scenario>
      </VideoTag>
    </Operation>
  </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| JobsDetail | Response | Job details |  Container |


`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Code               | Response.JobsDetail | Error code, which is meaningful only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error description, which is meaningful only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag                | Response.JobsDetail | Job type: VideoTag                              | String    |
| State | Response.JobsDetail | Job status. Valid values: Submitted, Running, Success, Failed, Pause, Cancel |  String |
| CreationTime | Response.JobsDetail | Job creation time |  String |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | Queue ID of the job                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation | Response.JobsDetail | Operation rule. Up to six jobs can be performed on the same file. |  Container |

`Input` has the following sub-nodes:
Same as the `Request.Input` node in the request.

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| VideoTag | Response.JobsDetail.Operation | Same as `Request.Operation.VideoTag` in the request. |  Container |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
POST /jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Tag>VideoTag</Tag>
  <Input>
    <Object>test.mp4</Object>
  </Input>
  <Operation>
    <VideoTag>
      <Scenario>Stream</Scenario>
    </VideoTag>
  </Operation>
  <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>je8f65004eb8511eaaed4f377124a303c</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>VideoTag</Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
      <VideoTag>
        <Scenario>Stream</Scenario>
      </VideoTag>
    </Operation>
  </JobsDetail>
</Response>
```
