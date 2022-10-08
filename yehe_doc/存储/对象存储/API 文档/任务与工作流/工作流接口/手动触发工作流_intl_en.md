## Feature Description

This API (`Trigger Workflow`) is used to manually trigger a workflow.

## Request

#### Sample request

```plaintext
POST /triggerworkflow?workflowId=xxx&object=xxx HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

```

>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request parameters

| Field |  Description | Type | Required |
| :--------- | :------------------ | :----- | :------- |
| workflowId | ID of the workflow to trigger | String | Yes       |
|  object     |     Name of the object that requires workflow processing  | String | Yes       |


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).



#### Request body
The request body of this request is empty.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <RequestId>NjA0MWExNGVfOTBmYTUwNjRfMzc0M****</RequestId>
    <InstanceId>i6fc78ca77d6011eba0ac5254008618d9=</InstanceId>
<Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :--------------- | :----- |
| RequestId          | Response | Unique ID of the request                                                | String    |
| InstanceId          | Response | Instance ID    | String |

### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

### Request

```plaintext
POST /triggerworkflow/?workflowId=xxx&object=xxx HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml

```

### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****



<Response>
         <RequestId>NjA0MWExNGVfOTBmYTUwNjRfMzc0M****</RequestId>
         <InstanceId>i6fc78ca77d6011eba0ac5254008618d9=</InstanceId>
<Response>
```
