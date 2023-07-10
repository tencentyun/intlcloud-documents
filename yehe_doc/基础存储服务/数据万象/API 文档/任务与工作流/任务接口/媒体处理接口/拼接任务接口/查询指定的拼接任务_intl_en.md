## Feature Description
This API (`DescribeMediaJob`) is used to query a specified job.

## Request

#### Sample request

```plaintext
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

#### Common request headers
This API uses [common request headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Non-common request headers
This request operation does not use any non-common request headers.

#### Request body
This request does not have a request body.


## Response

#### Response headers

#### Common response headers
This response contains common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Non-common response headers
This response does not use any non-common response header.

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
| JobsDetail | Response | Job details. Same as `Response.JobsDetail` in `PostJobs`. |  Container |
| NonExistJobIds | Response | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |

#### Error codes
The following error may be returned for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Samples

#### Request

```shell
GET /jobs/jabcsdssfeipplsdfwe HTTP/1.1
Accept: */*
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98****-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com

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
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>Concat<Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
        <ConcatTemplate>
            <ConcatFragment>
                <Mode>Start</Mode>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/start.mp4</Url>
            </ConcatFragment>
            <ConcatFragment>
                <Mode>End</Mode>
                <Url>http://bucket-1250000000.cos.ap-beijing.myqcloud.com/end.mp4</Url>
            </ConcatFragment>
            <Audio>
                <Codec>mp3</Codec>
                <Samplerate></Samplerate>
                <Bitrate></Bitrate>
                <Channels></Channels>
            </Audio>
            <Video>
                <Codec>H.264</Codec>
                <Bitrate>1000</Bitrate>
                <Width>1280</Width>
                <Height></Height>
                <Fps>30</Fps>
            </Video>
            <Container>
                <Format>mp4</Format>
            </Container>
        </ConcatTemplate>
        <Output>
            <Region>ap-beijing</Region>
            <Bucket>aabc-1250000000</Bucket>
            <Object>concat.mp4</Object>
        </Output>
    </Operation>
  </JobsDetail>
</Response>
```

