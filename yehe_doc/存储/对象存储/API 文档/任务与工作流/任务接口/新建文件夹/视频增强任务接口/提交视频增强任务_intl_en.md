## Feature Description

This API (`CreateMediaJobs`) is used to submit a video enhancement job.

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
  <Tag>VideoProcess</Tag>
  <Input>
    <Object></Object>
  </Input>
  <Operation>
    <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
    <TranscodeTemplateId></TranscodeTemplateId>
    <WatermarkTemplateId></WatermarkTemplateId>
    <Output>
      <Region></Region>
      <Bucket></Bucket>
      <Object></Object>
    </Output>
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
| Tag                | Request | Job type: VideoProcess                                | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule. Up to six jobs can be performed on the same file.                                                | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | --------------- | ------ | ---- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| VideoProcess       | Request.Operation | Video enhancement template parameter                                          | Container | No   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Transcode          | Request.Operation | Transcoding template parameter. This node and `TranscodeTemplateId` cannot be empty at the same time.             | Container | No   |
| TranscodeTemplateId| Request.Operation | Transcoding template ID. This node and `Transcode` cannot be empty at the same time. Use this node with priority.           | String  | No|
| Watermark          | Request.Operation | Watermark template parameter. Same as `Request.Watermark` in the watermark template creation API `CreateMediaTemplate`. Up to three watermarks can be passed in. | Container | No |
| WatermarkTemplateId| Request.Operation | Watermark template ID. Up to three watermark template IDs can be passed in. If `Watermark` and `WatermarkTemplateId` exist at the same time, use `WatermarkTemplateId` with priority.          | String    | No |
| DigitalWatermark   | Request.Operation | Specifies the digital watermark parameter                                                         | Container | No   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

>!`TemplateId` is used with priority. If `TemplateId` is unavailable, the corresponding job type parameter is used.

`VideoProcess` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description |
| ------------------ | :----------------------------- | -------------------------------------- |
| ColorEnhance       | Request.Operation.VideoProcess | Same as `Request.ColorEnhance` in the video enhancement template creation API `CreateMediaTemplate`. |
| MsSharpen          | Request.Operation.VideoProcess | Same as `Request.MsSharpen` in the video enhancement template creation API `CreateMediaTemplate`. |

`DigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :-------------------------- | -------------------------------------- | --------- | ---- |
| Message               | Request.Operation.DigitalWatermark |  The string embedded by the digital watermark, which can contain up to 64 letters, digits, underscores (\_), hyphens (-), and asterisks (\*)    | string | Yes   |
| Type               | Request.Operation.DigitalWatermark | Watermark type, which currently can be set to `Text` only      | String | Yes |
| Version            | Request.Operation.DigitalWatermark | Watermark version, which currently can be set to `V1` only       | String | Yes |
| IgnoreError        | Request.Operation.DigitalWatermark | Whether to ignore the watermarking failure and continue the job. Valid values: true, false (default)  |string | Yes   |


`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Output result filename                                             | String | Yes   |



## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

``` shell
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
    <Tag>VideoProcess</Tag>
    <Input>
      <Object></Object>
    </Input>
    <Operation>
      <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
      <TranscodeTemplateId></TranscodeTemplateId>
      <WatermarkTemplateId></WatermarkTemplateId>
      <DigitalWatermark>
        <Type>Text</Type>
        <Message>123456789ab</Message>
        <Version>V1</Version>
        <IgnoreError>false</IgnoreError>
      </DigitalWatermark>
      <Output>
        <Region></Region>
        <Bucket></Bucket>
        <Object></Object>
      </Output>
      <MediaInfo>
      </MeidaInfo>
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
| Tag| Response.JobsDetail | Job type: VideoProcess | String |
| State | Response.JobsDetail | Job status. Valid values: Submitted, Running, Success, Failed, Pause, Cancel |  String |
| CreationTime | Response.JobsDetail | Job creation time |  String |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | Queue ID of the job                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation          | Response.JobsDetail | Operation rule                           | Container |

`Input` has the following sub-nodes:
Same as the `Request.Input` node in the request.

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| TemplateId | Response.JobsDetail.Operation | Job template ID |  String |
| Output             | Response.JobsDetail.Operation | File output address               | Container |
| DigitalWatermark   | Request.Operation | Specifies the digital watermark parameter                                                         | Container | 
| MediaInfo          | Response.JobsDetail.Operation | Transcoding output video information. This node will not be returned when there is no output video. | Container |

`Output` has the following sub-nodes:
Same as the `Request.Operation.Output` node in the request.

`MediaInfo` has the following sub-nodes:
Same as the `Response.MediaInfo` node in the `GenerateMediaInfo` API.

`DigitalWatermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :-------------------------- | -------------------------------------- | --------- |
| Message               | Response.Operation.DigitalWatermark |  The string in the digital watermark successfully embedded in the video, which can contain up to 64 letters, digits, underscores (\_), hyphens (-), and asterisks (\*)    | string |
| Type               | Response.Operation.DigitalWatermark | Watermark type, which currently can be set to `Text` only      | String |
| Version            | Response.Operation.DigitalWatermark | Watermark version, which currently can be set to `V1` only      | String |
| IgnoreError        | Response.Operation.DigitalWatermark | Whether to ignore the watermarking failure and continue the job. Valid values: true, false (default)  |string |
| State        | Response.Operation.DigitalWatermark | Whether the watermark is added successfully. Valid values: Running, Success, Failed  | string |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Sample 1: Using the video enhancement template ID

#### Request

```shell
POST /jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Tag>VideoProcess</Tag>
  <Input>
    <Object>test.mp4</Object>
  </Input>
  <Operation>
    <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
    <TranscodeTemplateId></TranscodeTemplateId>
    <WatermarkTemplateId></WatermarkTemplateId>
    <DigitalWatermark>
        <Type>Text</Type>
        <Message>123456789ab</Message>
        <Version>V1</Version>
        <IgnoreError>false</IgnoreError>
    </DigitalWatermark>
    <Output>
        <Region>ap-beijing</Region>
        <Bucket>examplebucket-1250000000</Bucket>
        <Object>test-montage.mkv</Object>
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
    <Tag>VideoProcess</Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <TranscodeTemplateId></TranscodeTemplateId>
        <WatermarkTemplateId></WatermarkTemplateId>
        <DigitalWatermark>
            <Type>Text</Type>
            <Message>123456789ab</Message>
            <Version>V1</Version>
            <IgnoreError>false</IgnoreError>
        </DigitalWatermark>
        <Output>
            <Region>ap-beijing</Region>
            <Bucket>examplebucket-1250000000</Bucket>
            <Object>test-montage.mkv</Object>
        </Output>
    </Operation>
  </JobsDetail>
</Response>
```



#### Sample 2: Using the video enhancement processing parameter

#### Request


```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Tag>VideoProcess</Tag>
  <Input>
    <Object>test.mp4</Object>
  </Input>
  <Operation>
    <VideoProcess>
      <ColorEnhance>
        <Enable>true</Enable>
        <Contrast></Contrast>
        <Correction></Correction>
        <Saturation></Saturation>
      </ColorEnhance>
      <MsSharpen>
        <Enable>true</Enable>
        <SharpenLevel></SharpenLevel>
      </MsSharpen>
    <VideoProcess>
    <TranscodeTemplateId></TranscodeTemplateId>
    <WatermarkTemplateId></WatermarkTemplateId>
    <DigitalWatermark>
        <Type>Text</Type>
        <Message>123456789ab</Message>
        <Version>V1</Version>
        <IgnoreError>false</IgnoreError>
    </DigitalWatermark>
    <Output>
      <Region>ap-beijing</Region>
      <Bucket>examplebucket-1250000000</Bucket>
      <Object>test-montage.gif</Object>
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
    <Tag>VideoProcess</Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
      <VideoProcess>
        <ColorEnhance>
          <Enable>true</Enable>
          <Contrast></Contrast>
          <Correction></Correction>
          <Saturation></Saturation>
        </ColorEnhance>
        <MsSharpen>
          <Enable>true</Enable>
          <SharpenLevel></SharpenLevel>
        </MsSharpen>
      <VideoProcess>
      <TranscodeTemplateId></TranscodeTemplateId>
      <WatermarkTemplateId></WatermarkTemplateId>
      <DigitalWatermark>
        <State>Success</State>
        <Type>Text</Type>
        <Message>123456789ab</Message>
        <Version>V1</Version>
        <IgnoreError>false</IgnoreError>
      </DigitalWatermark>
      <Output>
        <Region>ap-beijing</Region>
        <Bucket>examplebucket-1250000000</Bucket>
        <Object>test-montage.gif</Object>
      </Output>
    </Operation>
  </JobsDetail>
</Response>
```

