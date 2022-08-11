## Feature Description

This API (`CreateInventoryTriggerJob`) is used to submit a batch data processing job.

## Request

#### Sample request

```shell
POST /inventorytriggerjob HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 



#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
  <Name></Name>
  <Input>
    <Manifest></Manifest>
    <UrlFile></UrlFile>
    <Prefix></Prefix>
    <Object></Object>
  </Input>
  <Operation>
    <TimeInterval>
        <Start></Start>
        <End></End>
    </TimeInterval>
    <WorkflowIds></WorkflowIds>  
  </Operation>
</Request>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None     | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Name               | Request | Batch data processing job name, which can contain up to 128 letters, digits, hyphens, and underscores.  | String    | Yes    |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | --------------- | ------ | ---- |
| Manifest           | Request.Input | COS inventory filename | String | No   |
| UrlFile            | Request.Input | URL filename | String | No   |
| Prefix             | Request.Input | Object prefix | String | No   |
| Object             | Request.Input | Media filename | String | No   |


`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| WorkflowIds                   | Request.Operation | ID of the triggered workflow      | String | Yes   |
| TimeInterval                  | Request.Operation | Trigger range filtered by time  | Container | No   |

`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |---| ---- |
| Start                | Request.TimeInterval | Start time | String    | No   | 0  | <li>Upload time of the scanned object <br/><li>%Y-%m-%dT%H:%m:%S%z <br/> |
| End             | Request.TimeInterval | End time | String    | No   | Current time | <li>Upload time of the scanned object <br/><li>%Y-%m-%dT%H:%m:%S%z <br/> |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <RequestId><RequestId>
  <JobsDetail>
    <Code></Code>
    <Message></Message>
    <Name></Name>
    <JobId></JobId>
    <State></State>
    <CreationTime></CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <Input>
      <Manifest></Manifest>
      <UrlFile></UrlFile>
      <Prefix></Prefix>
      <Object></Object>
    </Input>
    <Operation>
      <TimeInterval>
        <Start></Start>
        <End></End>
      </TimeInterval>
      <WorkflowIds></WorkflowIds> 
    </Operation>
  </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :--- | :-- | :-- | :-- |
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| RequestId          | Response | Unique ID of the request.                   | String    |
| JobsDetail | Response | Job details |  Container |


`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:--- |:---|:---|
| Code               | Response.JobsDetail | Error code, which is meaningful only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error description, which is meaningful only if `State` is `Failed`   | String    |
| Name | Response.JobsDetail | Job name | String |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| State | Response.JobsDetail | Job status. Valid values: Submitted, Running, Success, Failed, Pause, Cancel |  String |
| CreationTime | Response.JobsDetail | Job creation time |  String |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation | Response.JobsDetail | Operation rule |  Container |

`Input` has the following sub-nodes:
Same as the `Request.Input` node in the request.

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:--- |:---|:---|
| WorkflowIds                   | Response.JobsDetail.Operation | ID of the triggered workflow      | String |
| TimeInterval                  | Response.JobsDetail.Operation | Trigger range filtered by time, which takes effect only for `Input.Prefix`.  | Container |

`TimeInterval` has the following sub-nodes:
Same as the `Request.Operation.TimeInterval` node in the request.




#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
POST /inventorytriggerjob HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Input>
    <Manifest></Manifest>
    <UrlFile></UrlFile>
    <Prefix></Prefix>
    <Object></Object>
  </Input>
  <Operation>
    <TimeInterval>
        <Start>2022-02-16T10:45:10+0800</Start>
        <End>2022-02-16T10:45:12+0800</End>
    </TimeInterval>
    <WorkflowIds></WorkflowIds>
  </Operation>
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
  <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzh****=</RequestId>
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
        <Start>2022-02-16T10:45:12+0800</Start>
        <End>2022-02-16T10:45:12+0800</End>
      </TimeInterval>
      <WorkflowIds></WorkflowIds>
    </Operation>
  </JobsDetail>
</Response>
```
