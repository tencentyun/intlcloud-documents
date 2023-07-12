## Description

This API is used to switch the status (enabled or disabled) of a specified live channel.

>!
> - Only the owner of the bucket can call this API.
> - If you push streams to a `disabled` channel, the request will fail.
> - This API can be called during a push.
> - If you call this API to switch the status of a channel from `enabled` to `disabled` during a push, COS will forcibly disconnect the push URL (there may be a delay of about 10 seconds).

## Request

#### Sample request

```plaintext
PUT /<ChannelName>?live&switch=<NewSwitch> HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Content-Length: Content Size
Content-Md5: Content MD5
Authorization: Auth String

XML Body
```

> ? Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)


#### Request parameters

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ---------- | :------- |
| NewSwitch | Sets the status of the channel. Valid values: `enabled` `disabled`.<br/>Note: `enabled` and `disabled` should be in lowercase. | EnumString | Yes |




#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request has no request body.

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.
#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

```plaintext
PUT /test-channel?live&switch=enabled HTTP 1.1
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
```
