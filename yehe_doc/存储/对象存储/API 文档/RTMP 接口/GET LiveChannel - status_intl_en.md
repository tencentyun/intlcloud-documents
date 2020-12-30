## Overview

This API (GET LiveChannel - status) is used to obtain the push status of a specified live channel.

## Request

#### Sample request

```plaintext
GET /<ChannelName>?live&comp=status HTTP 1.1
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

The following is an example of the response body:

``` plaintext
<LiveChannelStatus>
  <Status>Live</Status>
  <ConnectedTime>2016-08-25T06:25:15.000Z</ConnectedTime>
  <RemoteAddr>127.0.0.1:47745</RemoteAddr>
  <RequestId>NWZjMzUyM2NfNWNhM2IwYV8xOTYyX2Mz****</RequestId>
  <Video>
    <Width>1280</Width>
    <Height>720</Height>
    <FrameRate>24</FrameRate>
    <Bandwidth>71510</Bandwidth>
    <Codec>H264</Codec>
  </Video>
  <Audio>
    <Bandwidth>13308</Bandwidth>
    <SampleRate>48000</SampleRate>
    <Codec>AAC</Codec>
  </Audio>
</LiveChannelStatus>
```

The following describes the nodes of the response body returned by this request:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ----------------- | ------------------------------------------------------------ | ---------- |
| LiveChannelStatus | None | A container that stores the response of `GetLiveChannelStatus` | Container |
| Status | LiveChannelStatus | Push status of the channel. Valid values: `Live`, `Idle` | EnumString |
| ConnnectedTime | LiveChannelStatus | If the value of `Status` is `Live`, this parameter indicates the client’s push start time (in ISO 8601 format). | EnumString |
| RemoteAddr | LiveChannelStatus | If the value of `Status` is `Live`, this parameter indicates the remote IP address of the push client. | Container |
| RequestId | LiveChannelStatus | If the value of `Status` is `Live`, this parameter indicates the `RequestId` of the current push request. | String |
| Video | LiveChannelStatus | If the value of `Status` is `Live`, this parameter is a container that stores the video stream information.<br/>Note: The `Video` and `Audio` containers will be returned only when the value of `Status` is `Live`. However, if `Status` is `Live`, these two containers are not necessarily returned. For example, if the client has connected to `LiveChannel` but hasn’t sent any video or audio data, these two containers will not be returned. | Container  |
| Width | Video | Width of the video streams, in pixels | String |
| Height | Video | Height of the video streams, in pixels | String |
| FrameRate | Video  | Frame rate of the video streams | String |
| Bandwidth | Video | Bitrate of the video streams, in B/s                               | String |
| Codec | Video | Codec of the video streams | EnumString |
| Audio | LiveChannelStatus | If the value of `Status` is `Live`, this parameter is a container that stores the audio stream information.<br/>Note: The `Video` and `Audio` containers will be returned only when the value of `Status` is `Live`. However, if `Status` is `Live`, these two containers are not necessarily returned. For example, if the client has connected to `LiveChannel` but hasn’t sent any video or audio data, these two containers will not be returned. | Container |
| SampleRate | Audio | Sample rate of the audio streams | String |
| Bandwidth | Audio | Bitrate of the audio streams, in B/s | String |
| Codec | Audio | Codec of the audio streams | String |



#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Case 1: channel in Idle status (without push)

#### Request

```plaintext
GET /test-channel?live&comp=status HTTP 1.1
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
<LiveChannelStat>
  <Status>Idle</Status>
</LiveChannelStat>
```

#### Case 2: channel in Live status (with push)

#### Request

```plaintext
GET /test-channel?live&comp=status HTTP 1.1
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
<LiveChannelStatus>
  <Status>Live</Status>
  <ConnectedTime>2016-08-25T06:25:15.000Z</ConnectedTime>
  <RemoteAddr>127.0.0.1:47745</RemoteAddr>
  <RequestId>NWZjMzUyM2NfNWNhM2IwYV8xOTYyX2Mz****</RequestId>
  <Video>
    <Width>1280</Width>
    <Height>720</Height>
    <FrameRate>24</FrameRate>
    <Bandwidth>71510</Bandwidth>
    <Codec>H264</Codec>
  </Video>
  <Audio>
    <Bandwidth>13308</Bandwidth>
    <SampleRate>48000</SampleRate>
    <Codec>AAC</Codec>
  </Audio>
</LiveChannelStatus>
```

