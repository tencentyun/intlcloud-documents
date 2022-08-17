## Feature Description

This API (`UpdateSpeechQueue`) is used to update a speech recognition queue.

## Request

#### Sample request

```plaintext
PUT /asrqueue/p8eb46b8cc1a94bc09512d16c5c4f4d3a HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

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
      <th>Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>Request</td>
      <td>None</td>
      <td>Request container</td>
      <td>Container</td>
      <td>Yes</td>
   </tr>
</table>

`Request` has the following sub-nodes:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
      <th>Constraints</th>
   </tr>
   <tr>
      <td>Name</td>
      <td>Request</td>
      <td>Template name</td>
      <td>String</td>
      <td>Yes</td>
      <td>Length limit: 100 characters</td>
   </tr>
   <tr>
      <td>QueueID</td>
      <td>Request</td>
      <td>Channel ID</td>
      <td>String</td>
      <td>Yes</td>
      <td>-</td>
   </tr>
   <tr>
      <td>State</td>
      <td>Request</td>
      <td>Channel status</td>
      <td>String</td>
      <td>Yes</td>
      <td>
        1. Active: Jobs in the channel will be scheduled and executed by the speech recognition service. <br>2. Paused: The channel is paused, and jobs in it will no longer be scheduled and executed. All jobs in the channel will remain in the `Submitted` status, while jobs being executed will continue without being affected.
      </td>
   </tr>
   <tr>
      <td>NotifyConfig</td>
      <td>Request</td>
      <td>Notification channel</td>
      <td>Container</td>
      <td>Yes</td>
      <td>Third-party callback URL</td>
   </tr>
</table>

`NotifyConfig` has the following sub-nodes:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>Type</th>
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
      <td>Callback type. General callback: Url</td>
      <td>String</td>
      <td>No</td>
      <td>Length limit: 100 characters</td>
   </tr>
   <tr>
      <td>Event</td>
      <td>Request.NotifyConfig</td>
      <td>Callback event</td>
      <td>String</td>
      <td>No</td>
      <td>Length limit: 100 characters</td>
   </tr>
   <tr>
      <td>State</td>
      <td>Request.NotifyConfig</td>
      <td>Callback switch: `Off` or `On`</td>
      <td>String</td>
      <td>No</td>
      <td>Length limit: 100 characters</td>
   </tr>
</table>



## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610). 

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

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------------------------------------ | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| Queue              | Response | Queue information. Same as `Response.QueueList` in [DescribeSpeechQueues].  | Container |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

