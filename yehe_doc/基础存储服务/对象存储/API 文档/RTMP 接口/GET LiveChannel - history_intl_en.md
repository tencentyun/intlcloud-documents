## Overview

This API (GET LiveChannel - history) is used to obtain the push record of a specified live channel. A maximum of 10 push records can be returned.


>!If no streams are pushed to the channel for over 90 days, COS will clear its push records.

## Request

#### Sample request

```plaintext
GET /<ChannelName>?live&comp=history HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Content-Length: Content Size
Content-Md5: Content MD5
Authorization: Auth String

```

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request parameter
This API has no request parameter.

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request has no request body.

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The following describes the nodes of the response body returned by this request:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------ | --------------------------------------- | --------- |
| LiveChannelHistory | None | A container that stores the response of `GetLiveChannelHistory` | Container |
| LiveRecord | LiveChannelHistory | A container that stores the record of a push operation | Container |
| StartTime | LiveRecord | Start time of the push request, in ISO 8601 format | String |
| EndTime | LiveRecord | End time of the push request, in ISO 8601 format | String |
| RemoteAddr | LiveRecord  | IP address of the push client | String |
| RequestId | LiveRecord | `RequestId` of the push request | String |



#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample



#### Request

```plaintext
GET /test-channel?live&comp=history HTTP 1.1
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Date: GMT date
Content-Length:Content Size
Content-Md5:Content MD5
Authorization: Auth String

```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed, 23 Aug 2020 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****
 
<?xml version="1.0" encoding="UTF-8"?>
<LiveChannelHistory>
        <LiveRecord>
                <StartTime>2020-11-27T04:13:19Z</StartTime>
                <EndTime>2020-11-27T04:13:22Z</EndTime>
                <RemoteAddr>127.0.0.1:57126</RemoteAddr>
                <RequestId>NWZjMDdjZGZfODVjMTNiMGFfNmIw****</RequestId>
        </LiveRecord>57126
        <LiveRecord>
                <StartTime>2020-11-27T04:17:12Z</StartTime>
                <EndTime>2020-11-27T04:17:15Z</EndTime>
                <RemoteAddr>127.0.0.1:57126</RemoteAddr>
                <RequestId>NWZjMDdkYzhfODVjMTNiMGFfNmIw****</RequestId>
        </LiveRecord>
        <LiveRecord>
                <StartTime>2020-11-27T07:28:09Z</StartTime>
                <EndTime>2020-11-27T07:28:16Z</EndTime>
                <RemoteAddr>127.0.0.1:57126</RemoteAddr>
                <RequestId>NWZjMGFhODlfODVjMTNiMGFfNmIy****</RequestId>
        </LiveRecord>
        <LiveRecord>
                <StartTime>2020-11-27T07:41:12Z</StartTime>
                <EndTime>2020-11-27T07:41:15Z</EndTime>
                <RemoteAddr>127.0.0.1:57126</RemoteAddr>
                <RequestId>NWZjMGFkOThfODVjMTNiMGFfMjAyNV8y</RequestId>
        </LiveRecord>
        <LiveRecord>
                <StartTime>2020-11-27T07:50:09Z</StartTime>
                <EndTime>2020-11-27T07:50:15Z</EndTime>
                <RemoteAddr>10.59.193.160</RemoteAddr>
                <RequestId>NWZjMGFmYjFfNzhjMTNiMGFfNzdl****</RequestId>
        </LiveRecord>
        <LiveRecord>
                <StartTime>2020-11-27T08:00:17Z</StartTime>
                <EndTime>2020-11-27T08:00:23Z</EndTime>
                <RemoteAddr>10.59.193.160:57126</RemoteAddr>
                <RequestId>NWZjMGIyMTFfNzhjMTNiMGFfMTA5****</RequestId>
        </LiveRecord>
        <LiveRecord>
                <StartTime>2020-11-27T10:55:57Z</StartTime>
                <EndTime>2020-11-27T10:55:59Z</EndTime>
                <RemoteAddr>127.0.0.1:57126</RemoteAddr>
                <RequestId>NWZjMGRiM2RfODVjMTNiMGFfNmIy****</RequestId>
        </LiveRecord>
        <LiveRecord>
                <StartTime>2020-11-28T07:49:00Z</StartTime>
                <EndTime>2020-11-28T07:49:23Z</EndTime>
                <RemoteAddr>127.0.0.1</RemoteAddr>
                <RequestId>NWZjMjAwZWNfODVjMTNiMGFfNmI0****</RequestId>
        </LiveRecord>
        <LiveRecord>
                <StartTime>2020-11-28T08:10:15Z</StartTime>
                <EndTime>2020-11-28T08:10:22Z</EndTime>
                <RemoteAddr>127.0.0.1:57126</RemoteAddr>
                <RequestId>NWZjMjA1ZTdfODVjMTNiMGFfNmI1****</RequestId>
        </LiveRecord>
        <LiveRecord>
                <StartTime>2020-11-28T08:12:11Z</StartTime>
                <EndTime>2020-11-28T08:12:14Z</EndTime>
                <RemoteAddr>127.0.0.1:57126</RemoteAddr>
                <RequestId>NWZjMjA2NWJfODVjMTNiMGFfNmIy****</RequestId>
        </LiveRecord>
</LiveChannelHistory>
```



