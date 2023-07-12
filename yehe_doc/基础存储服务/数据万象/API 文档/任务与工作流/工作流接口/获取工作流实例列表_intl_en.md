## Feature Description

This API (`Describe WorkflowExecution`) is used to get the list of workflow instances.

## Request

#### Sample request

```shell
GET /workflowexecution HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

The request body of this request is empty.

#### Request parameters

| Parameter (Keyword) | Description | Type | Required |
| :----------------- | :----------------------------------------------------------- | :----- | :------- |
| workflowId         | Workflow ID                                                    | string | Yes       |
| name               | Filename                                                     | string | No       |
| orderByTime        | `Desc` (default) or `Asc`                                 | string | No       |
| size               | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100.                      | string | No       |
| states             | Workflow instance status. If you enter multiple statuses, separate them by comma.<br> Valid values: All, Success, Failed, Running, Cancel. Default value: All | string | No       |
| startCreationTime  | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`        | String | No       |
| endCreationTime    | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`        | String | No       |
| nextToken          | Context token for pagination                   | String | No       |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <WorkflowExecutionList>
    <RunId>37145b2919714156bd97f91dc03fa2b4</RunId>
    <WorkflowId>we65e4d260e1042debdfb7e4560a19d3d</WorkflowId>
    <State>Success</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreateTime>
    <Object>https://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/mars_white_test.mp4</Object>
  </WorkflowExecutionList>
  <NextToken></NextToken>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :-------------------- | :------- | :----------------- | :-------- |
| WorkflowExecutionList | Response | Workflow instance details | Container |
| NextToken             | Response | Context token for pagination | string    |

`WorkflowExecutionList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------- | :------------- | :----- |
| RunId              | Response.WorkflowExecutionList | Workflow instance ID  | string |
| WorkflowId         | Response.WorkflowExecutionList | Workflow ID      | string |
| State              | Response.WorkflowExecutionList | Workflow instance status | string |
| CreateTime         | Response.WorkflowExecutionList | Creation time       | string |
| Object             | Response.WorkflowExecutionList | COS object address   | string |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
GET /workflowexecution?workflowId=we65e4d260e1042debdfb7e4560a19d3d HTTP/1.1
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
  <WorkflowExecutionList>
    <RunId>37145b2919714156bd97f91dc03fa2b4</RunId>
    <WorkflowId>we65e4d260e1042debdfb7e4560a19d3d</WorkflowId>
    <State>Success</State>
    <CreateTime>2019-07-07T12:12:12+0800</CreateTime>
    <Object>https://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/mars_white_test.mp4</Object>
  </WorkflowExecutionList>
  <WorkflowExecutionList>
    <RunId>47145b2929714156bd97f91dc03fa2b5</RunId>
    <WorkflowId>we65e4d260e1042debdfb7e4560a19d3d</WorkflowId>
    <State>Success</State>
    <CreateTime>2019-07-07T12:12:12+0800</CreateTime>
    <Object>https://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/_test.mp4</Object>
  </WorkflowExecutionList>
  <NextToken>e65e4d260e1042debdfb7e4560a19d3d</NextToken>
</Response>
```
