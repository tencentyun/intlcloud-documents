## Description
This API allows the bucket owner to obtain the cross-origin resource sharing (CORS, a W3C standard) configuration of a bucket. By default, the bucket owner has the permission to use this API and can grant such permission to other users.

## Request
### Sample Request

```
GET /?cors HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

### Request Headers

#### Common Headers
The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Special Headers
This request operation does not use any special request header.

### Request Body
The request body of this request is empty.

## Response

### Response Headers
#### Common Response Headers
This response contains common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response does not use any special response header.

### Response Body
CORS configuration information is obtained successfully.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<CORSConfiguration>
    <CORSRule>
        <ID>bucketid</ID>
        <AllowedOrigin>http://www.qq.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedHeader>x-cos-meta-test</AllowedHeader>
        <ExposeHeader>x-cos-meta-test1</ExposeHeader>
        <MaxAgeSeconds>500</MaxAgeSeconds>
    </CORSRule>
</CORSConfiguration>
```

The data are described in details below:

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
CORSConfiguration| None | Describes all the information on the CORS configuration, which can contain up to 100 `CORSRules` | Container | Yes

Content of the Container node `CORSConfiguration`:

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
CORSRule|CORSConfiguration| Describes all the information on the CORS configuration, which can contain up to 100 `CORSRules` | Container | Yes

Content of the Container node `CORSRule`:

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
ID | CORSConfiguration.CORSRule | ID of the configuration rule; optional | String | Yes
AllowedOrigin|CORSConfiguration.CORSRule| Allowed origin in the format of `protocol://domain name[:port number]`, such as `http://www.qq.com`. Wildcard `*` is supported |strings| Yes
AllowedMethod|CORSConfiguration.CORSRule| Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE |strings| Yes
AllowedHeader|CORSConfiguration.CORSRule| Tells the server side when sending the `OPTIONS` request what user-defined HTTP request headers can be used for subsequent requests. Wildcard `*` is supported |strings| Yes
MaxAgeSeconds|CORSConfiguration.CORSRule| Sets the validity period of the result of the `OPTIONS` request |integer| Yes
ExposeHeader|CORSConfiguration.CORSRule| Sets the user-defined header information from the server side that can be received by the browser |strings| Yes


### Error Codes
The implementation of this operation does not return special error messages. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example

### Request

```
GET /?cors HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484815944;32557711944&q-key-time=1484815944;32557711944&q-header-list=host&q-url-param-list=cors&q-signature=a2d28e1b9023d09f9277982775a4b3b705d0e23e
```

### Response

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 345
Connection: keep-alive
Date: Wed, 28 Oct 2016 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDdlNGZfNDYyMDRlXzM0YWFfZTBh

<CORSConfiguration>
    <CORSRule>
        <ID>bucketid</ID>
        <AllowedOrigin>http://www.qq.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedHeader>x-cos-meta-test</AllowedHeader>
        <ExposeHeader>x-cos-meta-test1</ExposeHeader>
        <MaxAgeSeconds>500</MaxAgeSeconds>
    </CORSRule>
</CORSConfiguration>
```


