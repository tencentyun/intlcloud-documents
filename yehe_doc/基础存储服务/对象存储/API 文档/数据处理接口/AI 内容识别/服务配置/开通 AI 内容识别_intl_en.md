## Feature Description

This API is used to activate the AI-based content recognition service and generate a queue.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateTranscodeTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>

## Request

#### Sample request

```shell
POST /ai_bucket HTTP/1.1
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

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://www.tencentcloud.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <RequestId>NjJmMzRlZGZfOTBmYTUwNjRfNzI0MV8x</RequestId>
    <AiBucket>
        <BucketId>test-1234567890</BucketId>
        <Name>test-1234567890</Name>
        <Region>ap-chongqing</Region>
        <CreateTime2022-08-09T16:23:11+0800></CreateTime>
    </AiBucket>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| RequestId          | Response | Unique ID of the request                                                | String    |
| AiBucket           | Response | Bucket information                                                  | Container |

`AiBucket` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------- | :---------------------- | :----- |
| BucketId           | Response.AiBucket | Bucket ID.               | String |
| Name               | Response.AiBucket | Bucket name, which is the same as `BucketId`. | String |
| Region             | Response.AiBucket | Region.              | String |
| CreateTime         | Response.AiBucket | Creation time.                | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request

```shell
POST /ai_bucket HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 0
Content-Type: application/xml

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 09 Aug 2022 16:23:12 GMT
Server: tencent-ci
x-ci-request-id: NjJmMzRlZGZfOTBmYTUwNjRfNzI0MV8x

<Response>
    <RequestId>NjJmMzRlZGZfOTBmYTUwNjRfNzI0MV8x</RequestId>
    <AiBucket>
        <BucketId>test-1234567890</BucketId>
        <Name>test-1234567890</Name>
        <Region>ap-chongqing</Region>
        <CreateTime2022-08-09T16:23:11+0800></CreateTime>
    </AiBucket>
</Response>
```
