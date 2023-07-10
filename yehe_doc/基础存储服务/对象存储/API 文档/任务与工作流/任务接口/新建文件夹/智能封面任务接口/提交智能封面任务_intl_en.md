## Feature Description

This API (`CreateMediaJobs`) is used to submit a job.

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

>? Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
>


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
  <Tag>SmartCover</Tag>
  <Input>
    <Object></Object>
  </Input>
  <Operation>
    <Output>
      <Region></Region>
      <Bucket></Bucket>
      <Object></Object>
    </Output>
    <SmartCover>
      <Format></Format>
      <Width></Width>
      <Height></Height>
      <Count></Count>
      <DeleteDuplicates></DeleteDuplicates>
    </SmartCover>    
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
| Tag                | Request | Job type. Valid values: Transcode (transcoding), Animation (animated image), SmartCover (intelligent thumbnail), Snapshot (screenshot), Concat (splicing)                                 | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule. Up to six operation rules are supported.                                                | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | --------------- | ------ | ---- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| SmartCover                   | Request.Operation | Thumbnail configuration        | Container | No   |
| Output                       | Request.Operation | Result output address                                | Container | Yes   |


`SmartCover` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- | ---- | ---- |
| Format             | Request.Operation.SmartCover | Thumbnail image type.    | String | Yes  | None | png, jpg, webp  |
| Width              | Request.Operation.SmartCover | Thumbnail image width    | String | Yes  | None | 1. Value range: [128, 4096]<br/> 2. Unit: px<br/> |
| Height             | Request.Operation.SmartCover | Thumbnail image height    | String | Yes  | None | 1. Value range: [128, 4096]<br/> 2. Unit: px<br/> |
| Count              | Request.Operation.SmartCover | Number of thumbnails.        | String | No  | 3 | 1. Value range: [1, 10]<br/> |
| DeleteDuplicates   | Request.Operation.SmartCover | Whether to deduplicate thumbnails.    | String | No  | false | true/false |


`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result filename. <br/>**If the job type is `SmartCover`, ${Number} must be included in the filename.**<br/> For example, if `Object` is `my-new-cover-${Number}.jpg`, and there are three result files, the output result filenames are as follows: <br/>my-new-cover-0.jpg<br/>my-new-cover-1.jpg<br/>my-new-cover-2.jpg | String | Yes   |



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
    <EndTime></EndTime>
    <QueueId></QueueId>
    <Tag>SmartCover</Tag>
    <Input>
      <Object></Object>
    </Input>
    <Operation>
      <Output>
        <Region></Region>
        <Bucket></Bucket>
        <Object></Object>
      </Output>
      <SmartCover>
        <Format></Format>
        <Width></Width>
        <Height></Height>
        <Count></Count>
        <DeleteDuplicates></DeleteDuplicates>
      </SmartCover> 
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
| Tag | Response.JobsDetail | Job type. Valid values: Transcode (transcoding), Animation (animated image), SmartCover (intelligent thumbnail), Snapshot (screenshot), Concat (splicing)                                 | String    |
| State | Response.JobsDetail | Job status. Valid values: Submitted, Running, Success, Failed, Pause, Cancel |  String |
| CreationTime | Response.JobsDetail | Job creation time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | Queue ID of the job                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation | Response.JobsDetail | Operation rule. Up to six operation rules are supported. |  Container |

`Input` has the following sub-nodes:
Same as the `Request.Input` node in the request.

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| TemplateId | Response.JobsDetail.Operation | Job template ID |  String |
| Output             | Response.JobsDetail.Operation | File output address               | Container |
| MediaInfo          | Response.JobsDetail.Operation | Transcoding output video information. This node will not be returned when there is no output video. | Container |

`Output` has the following sub-nodes:
Same as the `Request.Operation.Output` node in the request.

`MediaInfo` has the following sub-nodes:
Same as the `Response.MediaInfo` node in the `GenerateMediaInfo` API.

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Use Cases

**Using a template ID**

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml



<Request>
  <Tag>SmartCover</Tag>
  <Input>
    <Object>test.mp4</Object>
  </Input>
  <Operation>
    <Output>
      <Region>ap-beijing</Region>
      <Bucket>abc-1250000000</Bucket>
      <Object>my-new-cover-${Number}.jpg</Object>
    </Output>
    <SmartCover>
      <Format>png</Format>
      <Width>128</Width>
      <Height>128</Height>
      <Count>3</Count>
      <DeleteDuplicates>false</DeleteDuplicates>
    </SmartCover> 
  </Operation>
  <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
  <CallBack>https://www.callback.com</CallBack>
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
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=



<Response>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>je8f65004eb8511eaaed4f377124a303c</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>SmartCover</Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
      <Output>
        <Region>ap-beijing</Region>
        <Bucket>abc-1250000000</Bucket>
        <Object>my-new-cover-${Number}.jpg</Object>
      </Output>
      <SmartCover>
        <Format>png</Format>
        <Width>128</Width>
        <Height>128</Height>
        <Count>3</Count>
        <DeleteDuplicates>false</DeleteDuplicates>
      </SmartCover> 
    </Operation>
  </JobsDetail>
</Response>
```
