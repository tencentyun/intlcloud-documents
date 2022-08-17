## Feature Description

The API (`DescribeMediaJobs`) is used to pull jobs that meet specified conditions.

## Request

#### Sample request

```shell
GET /jobs?size=&states=&queueId=&startCreationTime=&endCreationTime= HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request does not have a request body.

#### Request parameters
The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
| queueId | None | ID of the queue from which jobs are pulled | String | Yes |
| tag |None| Job's `MediaInfo` | String |Yes|
| orderByTime | None | `Desc` (default) or `Asc` | String | No |
| nextToken | None | Context token for pagination | String | No |
| size | None | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100. | Integer | No |
| states | None | Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. Valid values: `All` (default), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. | String | No |
| startCreationTime | None | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`, such as `2001-01-01T00:00:00+0800` | String | No |
| endCreationTime | None | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`, such as `2001-01-01T23:59:59+0800`  | String | No |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <JobsDetail>
  </JobsDetail>
  <NextToken></NextToken>
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
| NextToken             | Response | Context token for pagination | String    |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Samples

#### Request

```shell
GET /jobs?queueId=aaaaaaaaaaa&tag=MediaInfo HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
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
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=

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
    <Tag>MediaInfo<Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
  </JobsDetail>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>jabcxxxxfeipplsdfwe</JobId>
    <State>Success</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>MediaInfo<Tag>
    <Input>
        <Object>test.mp4</Object>
    </Input>
    <Operation>
      <MediaInfo>
        <Format>
          <Bitrate>1014.950000</Bitrate>
          <Duration>10.125000</Duration>
          <FormatLongName>QuickTime / MOV</FormatLongName>
          <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
          <NumProgram>0</NumProgram>
          <NumStream>2</NumStream>
          <Size>1284547</Size>
          <StartTime>0.000000</StartTime>
        </Format>
        <Stream>
          <Audio>
            <Bitrate>70.451000</Bitrate>
            <Channel>1</Channel>
            <ChannelLayout>mono</ChannelLayout>
            <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
            <CodecName>aac</CodecName>
            <CodecTag>0x6134706d</CodecTag>
            <CodecTagString>mp4a</CodecTagString>
            <CodecTimeBase>1/44100</CodecTimeBase>
            <Duration>10.125000</Duration>
            <Index>1</Index>
            <Language>und</Language>
            <SampleFmt>fltp</SampleFmt>
            <SampleRate>44100</SampleRate>
            <StartTime>0.000000</StartTime>
            <Timebase>1/44100</Timebase>
          </Audio>
          <Subtitle/>
          <Video>
            <AvgFps>24/1</AvgFps>
            <Bitrate>938.164000</Bitrate>
            <CodecLongName>H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10</CodecLongName>
            <CodecName>H.264</CodecName>
            <CodecTag>0x31637661</CodecTag>
            <CodecTagString>avc1</CodecTagString>
            <CodecTimeBase>1/12288</CodecTimeBase>
            <Dar>40:53</Dar>
            <Duration>10.125000</Duration>
            <Fps>24.500000</Fps>
            <HasBFrame>2</HasBFrame>
            <Height>1280</Height>
            <Index>0</Index>
            <Language>und</Language>
            <Level>32</Level>
            <NumFrames>243</NumFrames>
            <PixFormat>yuv420p</PixFormat>
            <Profile>High</Profile>
            <RefFrames>1</RefFrames>
            <Sar>25600:25599</Sar>
            <StartTime>0.000000</StartTime>
            <Timebase>1/12288</Timebase>
            <Width>966</Width>
          </Video>
        </Stream>
      </MediaInfo>
    </Operation>
  </JobsDetail>
</Response>
```


