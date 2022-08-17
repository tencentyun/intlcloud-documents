## Feature Description
This API (`DescribeMediaJob`) is used to query a specified job.

## Request

#### Sample request

```shell
GET /jobs/<jobId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 



#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request does not have a request body.


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <JobsDetail>
  </JobsDetail>
  <NonExistJobIds></NonExistJobIds>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| JobsDetail | Response | Job details. Same as `Response.JobsDetail` in `CreateMediaJobs`. |  Container |
| NonExistJobIds | Response | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is meaningful only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error description, which is meaningful only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag | Response.JobsDetail | Job type: VoiceSeparate | String |
| State | Response.JobsDetail | Job status. Valid values: Submitted, Running, Success, Failed, Pause, Cancel |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime          | Response.JobsDetail | Job start time                                               | String    |
| EndTime          | Response.JobsDetail | Job end time                                               | String    |
| QueueId            | Response.JobsDetail | Queue ID of the job                                             | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation          | Response.JobsDetail | Operation rule                           | Container |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :------------------------------- | :-------- |
| TemplateId         | Response.JobsDetail.Operation | Job template ID                     | String    |
| Output             | Response.JobsDetail.Operation | File output address   | Container |
| VoiceSeparate      | Response.JobsDetail.Operation | Transcoding template parameter                                             | Container |

`VoiceSeparate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :------------------------------------------ | ------------------------------------------------------------ | --------- |
| AudioMode          | Response.JobsDetail.Operation.VoiceSeparate | Same as `Request.AudioMode` in the voice/sound separation template creation API `CreateMediaTemplate`.  | Container |
| AudioConfig        | Response.JobsDetail.Operation.VoiceSeparate | Same as `Request.AudioConfig` in the voice/sound separation template creation API `CreateMediaTemplate`.  | Container |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | -------------------------------------- | ---------------------------------------------- | ------ |
| Region             | Response.JobsDetail.Operation.Output   | Bucket region                                 | String |
| Bucket             | Response.JobsDetail.Operation.Output   | Result storage bucket                               | String |
| Object             | Response.JobsDetail.Operation.Output   | Background sound result filename. This node and `AuObject` cannot be empty at the same time. | String |
| AuObject           | Response.JobsDetail.Operation.AuObject | Voice result filename. This node and `Object` cannot be empty at the same time.     | String |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Samples

#### Request

```shell
GET /jobs/jabcsdssfeipplsdfwe HTTP/1.1
Accept: */*
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
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
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>jabcxxxxfeipplsdfwe</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>VoiceSeparate<Tag>
    <Operation>
        <VoiceSeparate>
          <AudioMode>IsAudio</AudioMode>
          <AudioConfig>
            <Codec>mp3</Codec>
            <Samplerate>44100</Samplerate>
            <Bitrate>12</Bitrate>
            <Channels>2</Channels>
          </AudioConfig>
        </VoiceSeparate>
        <Output>
            <Region>ap-beijing</Region>
            <Bucket>abc-1250000000</Bucket>
            <Object>test-trans.mp3</Object>
            <AuObject></AuObject>
        </Output>
    </Operation>
  </JobsDetail>
</Response>
```


