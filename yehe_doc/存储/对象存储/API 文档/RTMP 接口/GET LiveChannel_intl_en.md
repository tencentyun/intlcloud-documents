## Overview

This API (GET LiveChannel) is used to obtain the configurations of a specified live channel.

## Request

#### Sample request

```plaintext
GET /<ChannelName>?live HTTP 1.1
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
| ------------------------ | ------------------------ | ------------------------------------------------------------ | ---------- |
| LiveChannelConfiguration | None | A container that stores the response of `GetLiveChannel` | Container |
| Description | LiveChannelConfiguration | User-defined description of the channel | String |
| Switch | LiveChannelConfiguration | Specifies the switch status of `LiveChannel`. For more information, please see the parameter description in [PUT LiveChannel](https://intl.cloud.tencent.com/document/product/436/39047). | EnumString |
| Target | LiveChannelConfiguration | A container that stores the dump configurations | Container |
| Type | Target | Specifies the dump type. For more information, please see the parameter description in [PUT LiveChannel](https://intl.cloud.tencent.com/document/product/436/39047). | EnumString |
| FragDuration | Target | Specifies the duration of each TS file. For more information, please see the parameter description in [PUT LiveChannel](https://intl.cloud.tencent.com/document/product/436/39047). | String |
| FragCount | Target | Specifies the number of TS files in the M3U8 file. <br/>For more information, please see the parameter description in [PUT LiveChannel](https://intl.cloud.tencent.com/document/product/436/39047). | String |
| PlaylistName | Target | Specifies the name of the output M3U8 file. For more information, please see the parameter description in [PUT LiveChannel](https://intl.cloud.tencent.com/document/product/436/39047). | String |
| PublishUrls | Target | A container that stores the push URLs. For more information, please see the parameter description in [PUT LiveChannel](https://intl.cloud.tencent.com/document/product/436/39047). | String |
| Url | PublishUrls | Push URL. For more information, please see the parameter description in [PUT LiveChannel](https://intl.cloud.tencent.com/document/product/436/39047). | String |
| PlayUrls | Target | A container that stores the playback URLs. For more information, please see the parameter description in [PUT LiveChannel](https://intl.cloud.tencent.com/document/product/436/39047). | String |
| Url | PlayUrls | Playback URL. For more information, please see the parameter description in [PUT LiveChannel](https://intl.cloud.tencent.com/document/product/436/39047). | String |



#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

```plaintext
GET /test-channel?live HTTP 1.1
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
<LiveChannelConfiguration>
        <Description>description</Description>
        <Switch>Enabled</Switch>
        <Target>
                <Type>HLS</Type>
                <FragDuration>3</FragDuration>
                <FragCount>3</FragCount>
                <PlaylistName>playlist.m3u8</PlaylistName>
                <PublishUrls>
                        <Url>rtmp://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/live/test-channel</Url>
                </PublishUrls>
                <PlayUrls>
                        <Url>http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/test-channel/playlist.m3u8</Url>
                </PlayUrls>
        </Target>
</LiveChannelConfiguration>
```
