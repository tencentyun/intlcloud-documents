## Feature Description

This API (`GetPrivateM3U8`) is used to get the download authorization for M3U8 and TS resources (requests are forwarded to CI by COS).

## Request

#### Sample request

```plaintext
GET /<ObjectKey>?ci-process=pm3u8&expires= HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>

```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> - <ObjectKey> is the bucket object.
> 

#### Request parameters

The parameters are as described below:

| Parameter | Description | Type | Required |
|:--- | :--- | :--- | :--- |
| ci-process | Operation type, which is fixed at `pm3u8`. | String | Yes |
| expires | Relative validity period of the download credential for the private TS resource URL in seconds. Value range: [3600, 43200]. | String | Yes |


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/49351).


#### Request body
This request does not have a request body.


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body
The response body is the screenshot file content.

#### Error codes
There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).


## Samples

#### Request

```plaintext
GET /for-test.pm3u8?ci-process=pm3u8&expires=3600 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2016 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfG****-sign-time=1484213027;32557109027&q-key-time=1484213027;32557109027&q-header-list=host&q-url-param-list=acl&q-signature=dcc1eb2022b79cb2a780bf062d3a40e120b4****
Content-Length: 0
```
#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/x-mpegURL
Content-Length: 266005
Connection: keep-alive
Date: Fri, 10 Mar 2016 09:45:46 GMT
Server: tencent-ci
x-cos-request-id: NTg3NzRiMjVfYmRjMzVfMTViMl82ZGZm****

<M3U8 file content>
```
