## Overview

This API (`DescribeMediaJobs`) is used to pull jobs that meet specified conditions.

## Request

#### Request example

```shell
GET /jobs?size=&states=&queueId=&startCreationTime=&endCreationTime= HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```

>?Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request does not have a request body.

#### Request parameters
The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
| queueId | None | ID of the queue from which jobs are pulled | String | Yes |
| tag           | None        | Job type: `VideoProcess`       | String    |Yes|
| orderByTime | None | `Desc` (default) or `Asc` | String | No |
| nextToken | None | Context token for pagination | String | No |
| size | None | Maximum number of jobs pulled. Default value: `10`. Maximum value: `100`. | Integer | No |
| states | None | Status of the jobs to pull. If you enter multiple job states, separate them with commas. Valid values: `All` (default), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel` | String | No |
| startCreationTime | None | Start time of the time range for job pulling. Format: `%Y-%m-%dT%H:%m:%S%z`. Example: 2001-01-01T00:00:00+0800 | String | No |
| endCreationTime | None | End time of the time range for job pulling. Format: `%Y-%m-%dT%H:%m:%S%z`. Example: 2001-01-01T23:59:59+0800  | String | No |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
  <JobsDetail>
  </JobsDetail>
  <NextToken></NextToken>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| JobsDetail | Response | Job details. Same as `Response.JobsDetail` in `CreateMediaJobs`. |  Container |
| NextToken             | Response | Context token for pagination | String    |


#### Error codes

No special error message will be returned for this request. For the common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

#### Request

```shell
GET /jobs?queueId=aaaaaaaaaaa&tag=SDRtoHDR HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
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
    <Tag>VideoProcess<Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <TranscodeTemplateId></TranscodeTemplateId>
        <WatermarkTemplateId></WatermarkTemplateId>
        <Output>
            <Region>ap-beijing</Region>
            <Bucket>examplebucket-1250000000</Bucket>
            <Object>test-montage.mp4</Object>
        </Output>
    </Operation>
  </JobsDetail>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>jabcxxxxfeipplsdfwe</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>VideoProcess<Tag>
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
        <Output>
          <Region>ap-beijing</Region>
          <Bucket>examplebucket-1250000000</Bucket>
          <Object>test-montage.gif</Object>
        </Output>
    </Operation>
  </JobsDetail>
</Response>
```

