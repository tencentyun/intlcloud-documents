## Feature Description

This API (`DescribeMediaJob`) is used to query a specified task.

## Request

#### Sample request

```plaintext
GET /jobs/<jobId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```

>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request does not have a request body.


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

``` plaintext
<Response>
      <JobsDetail>
      </JobsDetail>
      <NonExistJobIds></NonExistJobIds>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| JobsDetail | Response | Task details. Same as the `Response.JobsDetail` node in the [CreateMediaJobs](https://intl.cloud.tencent.com/document/product/1045/43687) API. |  Container |
| NonExistJobIds | Response | List of non-existing task IDs queried. If all tasks exist, this node is not returned. |  String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is meaningful only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error description, which is meaningful only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Task ID                               | String    |
| Tag                | Response.JobsDetail | Task type: Transcode                               | String    |
| State | Response.JobsDetail | Task status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel` |  String |
| CreationTime       | Response.JobsDetail | Task creation time                         | String    |
| StartTime          | Response.JobsDetail | Task start time                                               | String    |
| EndTime          | Response.JobsDetail | Task end time                                               | String    |
| QueueId            | Response.JobsDetail | ID of the queue where the task is in                                             | String    |
| Input              | Response.JobsDetail | Input resource address of the task                   | Container |
| Operation          | Response.JobsDetail | Operation rule. Up to 6 operation rules are supported.                           | Container |


`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | 
| ------------------- | ----------------------------- | ------------------------------------------------------------ | --------- | 
| Transcode           | Response.JobsDetail.Operation | Transcoding template parameters                                             | Container | 
| Watermark          | Response.JobsDetail.Operation | Watermark template parameters. Same as `Request.Watermark` in the watermark template creation API `CreateMediaTemplate`. | Container | 
| RemoveWatermark     | Response.JobsDetail.Operation | Whether to remove the watermark                                             | Container | 
| TemplateId          | Response.JobsDetail.Operation | Template ID                                                 | String    | 
| WatermarkTemplateId| Response.JobsDetail.Operation | Watermark template ID. Multiple watermark template IDs are supported.           | String    | 
| Output              | Response.JobsDetail.Operation | Result output address                                                 | Container | 

>!`TemplateId` is used with priority. If `TemplateId` is unavailable, the corresponding task type parameter is used.

`Transcode` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | 
| ------------------ | :-------------------------------------- | ------------------------------------------------------------ | --------- | 
| Container          | Response.JobsDetail.Operation.Transcode | Same as `Request.Container` in the transcoding template creation API `CreateMediaTemplate`.    | Container | 
| Video          | Response.JobsDetail.Operation.Transcode | Same as `Request.Video` in the transcoding template creation API `CreateMediaTemplate`.    | Container | 
| TimeInterval          | Response.JobsDetail.Operation.Transcode | Same as `Request.TimeInterval` in the transcoding template creation API `CreateMediaTemplate`.    | Container | 
| Audio          | Response.JobsDetail.Operation.Transcode | Same as `Request.Audio` in the transcoding template creation API `CreateMediaTemplate`.    | Container | 
| TransConfig          | Response.JobsDetail.Operation.Transcode | Same as `Request.TransConfig` in the transcoding template creation API `CreateMediaTemplate`.    | Container | 

`Watermark` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | 
| ------------------ | :-------------------------------------------- | ------------------------------ | ------ | 
| Dx                 | Response.JobsDetail.Operation.Watermark | X-axis offset of the top-left corner origin. Value range: [1, 4096] | string |
| Dy                 | Response.JobsDetail.Operation.Watermark | Y-axis offset of the top-left corner origin. Value range: [1, 4096] | string | 
| Width                 | Response.JobsDetail.Operation.Watermark | Width. Value range: [1, 4096] | string | 
| Height                 | Response.JobsDetail.Operation.Watermark | Height. Value range: [1, 4096] | string | 

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | 
| ------------------ | ------------------------------------- | ---------------- | ------ |
| Region             | Response.JobsDetail.Operation.Output   | Bucket region                                 | String | 
| Bucket             | Response.JobsDetail.Operation.Output   | Result storage bucket                               | String | 
| Object             | Response.JobsDetail.Operationn.Output | Result file name | String | 

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Examples

#### Request

```plaintext
GET /jobs/jabcsdssfeipplsdfwe HTTP/1.1
Accept: */*
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
```

#### Response

```plaintext
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
    <Tag>Transcode<Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
        <Transcode>
            <Container>
                <Format>mp4</Format>
            </Container>
            <Video>
                <Codec>H.264</Codec>
                <Profile>high</Profile>
                <Bitrate>1000</Bitrate>
                <Crf></Crf>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
                <Gop></Gop>
                <Preset>medium</Preset>
                <ScanMode></ScanMode>
                <Bufsize>0</Bufsize>
                <Maxrate>0</Maxrate>
            </Video>
            <Audio>
                <Codec>aac</Codec>
                <Samplerate>44100</Samplerate>
                <Bitrate>128</Bitrate>
                <Channels>4</Channels>
            </Audio>
            <TransConfig>
                <AdjDarMethod>rescale</AdjDarMethod>
                <IsCheckReso>false</IsCheckReso>
                <ResoAdjMethod>1</ResoAdjMethod>
            </TransConfig>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </Transcode>
        <Watermark>
            <Type>Text</Type>
            <LocMode>Absolute</LocMode>
            <Dx>128</Dx>
            <Dy>128</Dy>
            <Pos>TopRight</Pos>
            <StartTime>0</StartTime>
            <EndTime>100.5</EndTime>
            <Text>
                <Text>Watermark content</Text>
                <FontSize>30</FontSize>
                <FontType></FontType>
                <FontColor>0xRRGGBB</FontColor>
                <Transparency>30</Transparency>
            </Text>
        </Watermark>
        <Watermark>
            <Type>Image</Type>
            <LocMode>Absolute</LocMode>
            <Dx>128</Dx>
            <Dy>128</Dy>
            <Pos>TopRight</Pos>
            <StartTime>0</StartTime>
            <EndTime>100.5</EndTime>
            <Image>
                <Url>http://bucket-1250000000.ci.ap-beijing.myqcloud.com/shuiyin_2.png</Url>
                <Mode>Proportion</Mode>
                <Width>10</Width>
                <Height>10</Height>
                <Transparency>30</Transparency>
            </Image>
        </Watermark>
        <Output>
            <Region>ap-beijing</Region>
            <Bucket>abc-1250000000</Bucket>
            <Object>test-trans.mp4</Object>
        </Output>
    </Operation>
  </JobsDetail>
</Response>
```

