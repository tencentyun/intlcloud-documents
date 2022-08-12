## Feature Description

This API (`DescribeInventoryTriggerJob`) is used to query a specified batch data processing job.

## Request

#### Sample request

```shell
GET /inventorytriggerjob/<jobId> HTTP/1.1
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

The request body of this request is empty.


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
  <RequestId><RequestId>
  <JobsDetail>
  </JobsDetail>
  <NonExistJobIds></NonExistJobIds>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:--- |:---|:---|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| RequestId          | Response | Unique ID of the request.                   | String    |
| JobsDetail | Response | Job details. Same as `Response.JobsDetail` in `CreateMediaJobs`. |  Container |
| NonExistJobIds | Response | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |
| NextToken             | Response | Context token for pagination | String    |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Samples

#### Request

```shell
GET /inventorytriggerjob/jabcsdssfeipplsdfwe?size=100 HTTP/1.1
Accept: */*
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
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
  <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzh****</RequestId>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <Name>demo</Name>
    <JobId>be8f65004eb8511eaaed4f377124a303c</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <StartTime>2019-07-07T12:12:12+0800</StartTime>
    <EndTime></EndTime>
    <Input>
      <Manifest></Manifest>
      <UrlFile></UrlFile>
      <Prefix></Prefix>
      <Object></Object>
    </Input>
    <Operation>
      <TimeInterval>
        <Start>0</Start>
        <End>60</End>
      </TimeInterval>
      <WorkflowIds></WorkflowIds>
    </Operation>
  </JobsDetail>
  <NextToken>e8f65004eb8511eaaed4f377124a303c</NextToken>
</Response>
```

