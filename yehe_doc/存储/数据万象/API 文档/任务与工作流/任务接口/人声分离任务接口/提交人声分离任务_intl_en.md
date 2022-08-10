## Feature Description
This API (`CreateMediaJobs`) is used to submit a task.

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

>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request requires the following request body:

```shell
<Request>
  <Tag>VoiceSeparate</Tag>
  <Input>
    <Object></Object>
  </Input>
  <Operation>
    <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
    <Output>
      <Region></Region>
      <Bucket></Bucket>
      <Object></Object>
      <AuObject></AuObject>
    </Output>
  </Operation>
  <QueueId></QueueId>
  <CallBack></CallBack>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Task type: VoiceSeparate                              | String    | Yes   |
| Input              | Request | Information about the media to be operated                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | ID of the queue where the task is in                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | --------------- | ------ | ---- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| VoiceSeparate                | Request.Operation | Transcoding template parameter                                    | Container | No   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

>!`TemplateId` is used with priority. If `TemplateId` is unavailable, the corresponding task type parameter is used.
>

`VoiceSeparate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ---------------- | :-------------------------- | -------------------------------------- | --------- | ---- |
| AudioMode        | Request.Operation.VoiceSeparate | Same as `Request.AudioMode` in the voice separation template creation API `CreateMediaTemplate`.  | Container | No   |
| AudioConfig        | Request.Operation.VoiceSeparate | Same as `Request.AudioConfig` in the voice separation template creation API `CreateMediaTemplate`.  | Container | No   |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Background audio result file name. This node and `AuObject` cannot be empty at the same time.                  | String | No   |
| AuObject             | Request.Operation.AuObject | Voice result file name. This node and `Object` cannot be empty at the same time.                  | String | No   |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

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
    <EndTime></EndTime>
    <QueueId></QueueId>
    <Tag>VoiceSeparate</Tag>
    <Input>
      <Object></Object>
    </Input>
    <Operation>
      <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
      <Output>
        <Region></Region>
        <Bucket></Bucket>
        <Object></Object>
        <AuObject></AuObject>
      </Output>
      <MediaInfo>
      </MeidaInfo>
    </Operation>
  </JobsDetail>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| JobsDetail | Response | Task details |  Container |


`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Code               | Response.JobsDetail | Error code, which is meaningful only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error description, which is meaningful only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Task ID                               | String    |
| Tag                | Response.JobsDetail | Task type: VoiceSeparate                              | String    |
| State | Response.JobsDetail | Task status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel` |  String |
| CreationTime | Response.JobsDetail | Task creation time |  String |
| StartTime | Response.JobsDetail | Task start time |  String |
| EndTime | Response.JobsDetail | Task end time |  String |
| QueueId            | Response.JobsDetail | ID of the queue where the task is in                       | String    |
| Input              | Response.JobsDetail | Input resource address of the task                   | Container |
| Operation          | Response.JobsDetail | Task rule                           | Container |

`Input` has the following sub-nodes:
Same as the `Request.Input` node in the request.

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| TemplateId | Response.JobsDetail.Operation | Task template ID |  String |
| Output             | Response.JobsDetail.Operation | File output address               | Container |
| MediaInfo          | Response.JobsDetail.Operation | Transcoding output video information. Not returned when there is no output video. | Container |

`Output` has the following sub-nodes:
Same as the `Request.Operation.Output` node in the request.

`MediaInfo` has the following sub-nodes:
Same as the `Response.MediaInfo` node in the `GenerateMediaInfo` API.

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

#### Example 1: using the voice separation template ID

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Tag>VoiceSeparate</Tag>
  <Input>
    <Object>test.mp4</Object>
  </Input>
  <Operation>
    <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
    <Output>
        <Region>ap-beijing</Region>
        <Bucket>abc-1250000000</Bucket>
        <Object></Object>
        <AuObject></AuObject>
    </Output>
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
    <Tag>VoiceSeparate</Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Output>
            <Region>ap-beijing</Region>
            <Bucket>abc-1250000000</Bucket>
            <Object></Object>
            <AuObject></AuObject>
        </Output>
    </Operation>
  </JobsDetail>
</Response>
```



#### Example 2: using the voice separation processing parameter

#### Request


```shell
POST /jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml



<Request>
  <Tag>VoiceSeparate</Tag>
  <Input>
    <Object>test.mp4</Object>
  </Input>
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
    <JobId>jabcxxxxfeipplsdfwe</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>VoiceSeparate</Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
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

