## Description

This API is used to list some or all live channels in a specified bucket.

## Request

#### Sample request

```plaintext
GET /?live HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Content-Length: Content Size
Content-Md5: Content MD5
Authorization: Auth String
```

> ? Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)


#### Request parameters

Request parameters of this API are described as follows:

| Parameter | Description | Type | Required |
| :---------------------- | :------------------------------------------- | :-------- | --------- |
| max-keys | Specifies the maximum number of channels that can be listed in a response. Value range: 1-1000. Defaults to `100`. | String | No |
| prefix | Specifies that the returned `LiveChannel` must begin with the `prefix`. Note: If you query with a prefix, the returned key will contain the `prefix`. | String | No |
| marker | Specifies the key to start with in the response. Keys after `marker` are returned in alphabetical order. | String | No |

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body

This request has no request body.

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The following is an example of the response body:

```plaintext
<ListLiveChannelResult>
	<MaxKeys></MaxKeys>
	<Prefix></Prefix>
	<IsTruncated>true</IsTruncated>
	<NextMarker>channel-0</NextMarker>
    <LiveChannel>
        <Name>String</Name>
        <LastModified>String</LastModified>
    </LiveChannel>
    <LiveChannel>
      ...
    </LiveChannel>
</ListSignalingChannelsResult>
```

The following describes the nodes of the response body returned for this request:

| Node Name (Keyword) | Parent Node | Description | Type |
| :---------------------- | :---------------------- | :------------------------------------------- | :-------- |
| ListLiveChannelResult | None | A container that stores the response of `List LiveChannels` | Container |
| MaxKeys | ListLiveChannelResult | The maximum number of channels that can be listed in a response | String |
| Prefix | ListLiveChannelResult | Specifies that the returned live channels must be prefixed with this value. Note that when you use a prefix to query, the returned key will contain the prefix. | String |
| IsTruncated | ListLiveChannelResult | Indicates whether all keys are returned. | String |
| NextMarker | ListLiveChannelResult | Specifies the maximum number of channels. | String |
| LiveChannel | ListLiveChannelResult | Information about the listed channels | Container |
| Name | LiveChannel | Name of the channel | String |
| LastModified | SignalingChannelConfiguration | Last modified time of the `LiveChannel` configuration, in ISO 8601 format  | String |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

```plaintext
GET /?live&max-keys=10&marker=test-channel-0 HTTP 1.1
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
<ListLiveChannelResult>
        <Prefix/>
        <Marker>test-channel-0</Marker>
        <MaxKeys>10</MaxKeys>
        <IsTruncated>true</IsTruncated>
        <NextMarker>test-channel-108</NextMarker>
        <LiveChannel>
                <Name>test-channel-1</Name>
                <LastModified>2020-11-29T02:58:31.000Z</LastModified>
        </LiveChannel>
        <LiveChannel>
                <Name>test-channel-100</Name>
                <LastModified>2020-11-26T03:47:41.000Z</LastModified>
        </LiveChannel>
        <LiveChannel>
                <Name>test-channel-101</Name>
                <LastModified>2020-11-25T12:07:45.000Z</LastModified>
        </LiveChannel>
        <LiveChannel>
                <Name>test-channel-102</Name>
                <LastModified>2020-11-25T12:07:45.000Z</LastModified>
        </LiveChannel>
        <LiveChannel>
                <Name>test-channel-103</Name>
                <LastModified>2020-11-25T12:07:45.000Z</LastModified>
        </LiveChannel>
        <LiveChannel>
                <Name>test-channel-104</Name>
                <LastModified>2020-11-25T12:07:45.000Z</LastModified>
        </LiveChannel>
        <LiveChannel>
                <Name>test-channel-105</Name>
                <LastModified>2020-11-25T12:07:45.000Z</LastModified>
        </LiveChannel>
        <LiveChannel>
                <Name>test-channel-106</Name>
                <LastModified>2020-11-25T12:07:45.000Z</LastModified>
        </LiveChannel>
        <LiveChannel>
                <Name>test-channel-107</Name>
                <LastModified>2020-11-25T12:07:45.000Z</LastModified>
        </LiveChannel>
        <LiveChannel>
                <Name>test-channel-108</Name>
                <LastModified>2020-11-25T12:07:45.000Z</LastModified>
        </LiveChannel>
</ListLiveChannelResult>
```
