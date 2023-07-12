## Overview

This API (`UpdateDocProcessQueue`) is used to update a file transcoding queue.

## Request

#### Sample request

```plaintext
PUT /docqueue/p8eb46b8cc1a94bc09512d16c5c4f4d3a HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```plaintext
<Request>
    <Name>Queue Name</Name>
    <QueueID></QueueID>
    <State></State>
    <NotifyConfig>
        <Type></Type>
        <Url></Url>
        <Event></Event>
    </NotifyConfig>
</Request>
```

The nodes are described as follows:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>API Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>Request</td>
      <td>N/A</td>
      <td>Request container</td>
      <td>Container</td>
      <td>Supported</td>
   </tr>
</table>


`Request` has the following sub-nodes:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>API Type</th>
      <th>Required</th>
      <th>Constraints</th>
   </tr>
   <tr>
      <td>Name</td>
      <td>Request</td>
      <td>Queue Name</td>
      <td>String</td>
      <td>Supported</td>
      <td>Length limit: 100 characters</td>
   </tr>
   <tr>
      <td>QueueID</td>
      <td>Request</td>
      <td>Queue ID</td>
      <td>String</td>
      <td>Supported</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td>State</td>
      <td>Request</td>
      <td>Queue status</td>
      <td>String</td>
      <td>Supported</td>
      <td>
        1. Active: Jobs in the queue will be scheduled and executed by the file preview service. <br>2. Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Submitted` status, while jobs being executed will continue without being affected.
      </td>
   </tr>
   <tr>
      <td>NotifyConfig</td>
      <td>Request</td>
      <td>Notification channel</td>
      <td>Container</td>
      <td>Supported</td>
      <td>Third-party callback URL</td>
   </tr>
</table>


`NotifyConfig` has the following sub-nodes:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>API Type</th>
      <th>Required</th>
      <th>Constraints</th>
   </tr>
   <tr>
      <td>Url</td>
      <td>Request.NotifyConfig</td>
      <td>Callback configuration</td>
      <td>String</td>
      <td>No</td>
      <td>Length limit: 100 characters</td>
   </tr>
   <tr>
      <td>Type</td>
      <td>Request.NotifyConfig</td>
      <td>Callback type, normal callback: URL</td>
      <td>String</td>
      <td>No</td>
      <td>Length limit: 100 characters</td>
   </tr>
   <tr>
      <td>Event</td>
      <td>Request.NotifyConfig</td>
      <td>Callback event: The file preview job is completed.</td>
      <td>String</td>
      <td>No</td>
      <td>Length limit: 100 characters</td>
   </tr>
   <tr>
      <td>State</td>
      <td>Request.NotifyConfig</td>
      <td>Callback switch: Off, On</td>
      <td>String</td>
      <td>No</td>
      <td>Length limit: 100 characters</td>
   </tr>
</table>




## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610). 

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <Queue>
        <QueueId></QueueId>
        <Name></Name>
        <State>Active</State>
        <NotifyConfig>
            <Url>mts-topic-1</Url>
            <Type></Type>
            <Event></Event>
        </NotifyConfig>
        <CreateTime></CreateTime>
        <UpdateTime></UpdateTime>
    </Queue>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| RequestId          | Response | Unique ID of the request                                                | String    |
| Queue              | Response | Queue information. For more information, see `Response.QueueList` in [DescribeDocProcessQueues](https://intl.cloud.tencent.com/document/product/1045/47935). | Container |

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Examples

#### Request

```plaintext
PUT /docqueue/p2505d57bdf4c4329804b58a6a5fb1572 HTTP/1.1
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: cos-python-sdk-v5.3.2
Host: examplebucket-1250000000.ci.ap-chongqing.myqcloud.com
Content-Type: application/xml
Content-Length: 279
Authorization: Authorization

<?xml version="1.0" encoding="UTF-8" ?>
<Request>
    <QueueId>p2505d57bdf4c4329804b58a6a5fb1572</QueueId>
    <State>Active</State>
    <Name>markjrzhang4</Name>
    <NotifyConfig>
        <Url>http://google.com/</Url>
    <State>On</State>
        <Type>Url</Type>
        <Event>TransCodingFinish</Event>
    </NotifyConfig>
</Request>[!http]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Date: Mon, 27 Jul 2020 08:22:41 GMT
Content-Type: application/xml
Content-Length: 641
Connection: keep-alive
Server: tencent-ci
x-ci-request-id: NWYxZThlZDBfYzc2OTQzNjRfMzUxYV8x****

<?xml version="1.0" encoding="utf-8"?>
<Response>
        <RequestId>NWYxZThlZDBfYzc2OTQzNjRfMzUxYV8x****</RequestId>
        <Queue>
                <QueueId>p2505d57bdf4c4329804b58a6a5fb1572</QueueId>
                <Name>markjrzhang4</Name>
                <State>Active</State>
                <NotifyConfig>
                        <Url>http://example.com/</Url>
                        <Event>TransCodingFinish</Event>
                        <Type>Url</Type>
                        <State>On</State>
                </NotifyConfig>
                <MaxSize>10000</MaxSize>
                <MaxConcurrent>10</MaxConcurrent>
                <CreateTime>2020-07-24T22:42:27+0800</CreateTime>
                <UpdateTime>2020-07-27T16:22:40+0800</UpdateTime>
                <BucketId>test007-1251704708</BucketId>
                <Category>DocProcessing</Category>
        </Queue>
</Response>
```
