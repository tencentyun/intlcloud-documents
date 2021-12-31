## Feature Description

The API (`DescribeMediaJobs`) is used to pull tasks that meet specified conditions.

## Request

#### Sample request

```shell
GET /jobs?size=&states=&queueId=&startCreationTime=&endCreationTime= HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```

>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request does not have a request body.

#### Request parameters
The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
| QueueId | None | ID of the queue from which tasks are pulled | String | Yes |
| Tag | None | Task type: Segment | String | Yes |
| OrderByTime | None | `Desc` (default) or `Asc` | String | No |
| NextToken | None | Context token for pagination | String | No |
| Size | None | Maximum number of tasks pulled. The default value is 10. The maximum value is 100. | Integer | No |
| States | None | Status of the tasks to pull. If you enter multiple task states, separate them with commas (,). Valid values: `All` (default), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel` | String | No |
| StartCreationTime | None | Start time of the time range for task pulling. Format: `%Y-%m-%dT%H:%m:%S%z`. Example: 2001-01-01T00:00:00+0800 | String | No |
| EndCreationTime | None | End time of the time range for task pulling. Format: `%Y-%m-%dT%H:%m:%S%z`. Example: 2001-01-01T23:59:59+0800  | String | No |

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
| JobsDetail | Response | Task details. Same as `Response.JobsDetail` in `CreateMediaJobs`. |  Container |
| NextToken             | Response | Context token for pagination | String    |

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

#### Request

```plaintext
GET /jobs?queueId=aaaaaaaaaaa&tag=Segment HTTP/1.1
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
    <Tag>Segment<Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
      <Segment>
        <Format>mp4</Format>
        <Duration>5</Duration>
      </Segment>
      <Output>
        <Region>ap-beijing</Region>
        <Bucket>abc-1250000000</Bucket>
        <Object>test-trans${Number}</Object>
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
    <Tag>Segment<Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
      <Segment>
        <Format>mp4</Format>
        <Duration>5</Duration>
      </Segment>
      <Output>
        <Region>ap-beijing</Region>
        <Bucket>examplebucket-1250000000</Bucket>
        <Object>test-trans${Number}</Object>
      </Output>
    </Operation>
  </JobsDetail>
</Response>
```

