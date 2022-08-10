## Feature Description

This API (`Describe WorkflowExecutions`) is used to get the workflow instance list.

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

>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

The request body of this request is empty.

#### Request parameters

| Parameter Name (Keyword) | Description                                                         | Type   | Required |
| :----------------- | :----------------------------------------------------------- | :----- | :------- |
| workflowId         | Workflow ID                                                    | string | Yes       |
| name               | File name                                                     | string | No       |
| orderByTime        | Desc (default) or Asc                                 | string | No       |
| size               | Maximum number of tasks pulled. The default value is 10. The maximum value is 100.                      | string | No       |
| states             | Workflow instance status. If you enter multiple states, separate them with commas (,).<br> Valid values: `All` (default), `Success`, `Failed`, `Running`, `Cancel` | string | No       |
| startCreationTime  | The pulling request creation time must be later than this time. Format: `%Y-%m-%dT%H:%m:%S%z`        | String | No       |
| endCreationTime    | The pulling request creation time must be earlier than this time. Format: `%Y-%m-%dT%H:%m:%S%z`        | String | No       |
| nextToken          | Context token for pagination                   | String | No       |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None | Response container | Container |

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

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

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
