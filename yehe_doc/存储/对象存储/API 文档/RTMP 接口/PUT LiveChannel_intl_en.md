## Description

This API is used to create a live channel to transfer audio and video streams.

>!
> - Only the owner of the bucket can call this API.
> - If you call this API repeatedly to create the same channel, the previously created channel will be overwritten. When streams are being pushed to this channel, do not call this API to overwrite the channel.

## Request

#### Sample request

```plaintext
PUT /<ChannelName>?live HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Content-Length: Content Size
Content-Md5: Content MD5
Authorization: Auth String

XML Body
```

> ? Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)

#### Request parameters

| Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ------ | :------- |
| ChannelName | Channel name of up to 128 characters. It should comply with the naming conventions of object keys and cannot contain slashes (/). | string | Yes |




#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

```plaintext
<LiveChannelConfiguration>
  <Description>ChannelDescription</Description>
  <Switch>ChannelSwitch</Switch>
  <Target>
     <Type>HLS</Type>
     <FragDuration>FragDuration</FragDuration>
     <FragCount>FragCount</FragCount>
     <PlaylistName>PlaylistName</PlaylistName>
  </Target>
</LiveChannelConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :---------------------- | :---------------------- | :------------------------------------------- | :-------- | ----------------------- |
| LiveChannelConfiguration | No | A container that stores all `LiveChannel` configurations  | Container | Yes |
| Description | LiveChannelConfiguration | User-defined channel description of up to 128 bytes | String | No |
| Switch | LiveChannelConfiguration | Specifies the status of `LiveChannel`. Valid values: `Enabled` (default), `Disabled`. | EnumString | No |
| Target | LiveChannelConfiguration | A container that stores the dump configurations | Container | Yes |
| Type | Target | Specifies the dump type. Valid value: `HLS`. <br/>Note: If the dump type is `HLS`, COS will update the M3U8 file each time after generating a TS file. The M3U8 file can contain up to `FragCount` latest TS files. | EnumString | Yes |
| FragDuration | Target | Specifies the duration of each TS file. Value range: 1-100. Defaults to `5`.<br/>Note: The default values of `FragDuration` and `FragCount` take effect only when neither of them is specified. If you specify one of them, you must also specify the other one. | String | No |
| FragCount | Target | Specifies the number of TS files in the M3U8 file. Value range: 1-100. Defaults to `3`.<br/>Note: The default values of `FragDuration` and `FragCount` take effect only when neither of them is specified. If you specify one of them, you must also specify the other one. | String | No |
| PlaylistName | Target | Specifies the name of the output M3U8 file. The file extension must be `.m3u8`, and the name can contain 6 to 128 characters. The default value is `playlist.m3u8`. <br/>Note: The generated playlist name (object name) is `ChannelName/PlaylistName`. | String | No |

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The following describes the nodes of the response body returned by this request:

| Node Name (Keyword) | Parent Node | Description | Type |
| :---------------------- | :---------------------- | :------------------------------------------- | :-------- |
| CreateLiveChannelResult | No | A container that stores the result of `CreateLiveChannel` | Container |
| PublishUrls | CreateLiveChannelResult | A container that stores the push URLs | Container |
| Url | PublishUrls | Push URL<br> Note: The returned push URL is unsigned. You can call the SDK or refer to [RTMP Request URL and Signature](https://intl.cloud.tencent.com/document/product/436/39052) to obtain the signature. | String |
| PlayUrls | CreateLiveChannelResult | A container that stores the playback URLs | Container |
| Url | PlayUrls | Playback URL | String |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

```plaintext
PUT /test-channel?live HTTP 1.1
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Date: GMT date
Content-Length:Content Size
Content-Md5:Content MD5
Authorization: Auth String

<?xml version="1.0" encoding="utf-8"?>
<LiveChannelConfiguration>
    <Description/>
    <Switch>Enabled</Status>
    <Target>
        <Type>HLS</Type>
        <FragDuration>2</FragDuration>
        <FragCount>3</FragCount>
    </Target>
</LiveChannelConfiguration>
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
<CreateLiveChannelResult>
  <PublishUrls>
    <Url>rtmp://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/live/test-channel</Url>
  </PublishUrls>
  <PlayUrls>
    <Url>http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/test-channel/playlist.m3u8</Url>
  </PlayUrls>
</CreateLiveChannelResult>
```
