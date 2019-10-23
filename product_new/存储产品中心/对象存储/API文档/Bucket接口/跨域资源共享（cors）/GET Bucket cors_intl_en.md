## Description
This API (GET Bucket cors) is used by the bucket owner to obtain the cross-origin resource sharing (CORS, a W3C standard) configuration set for the bucket. By default, the bucket owner has the permission to use this API and can grant it to others.

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
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Special Headers
This request operation has no special request headers.

### Request Body
The request body of this request is empty.

## Response

### Response Headers
#### Common Response Headers
This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response has no special response headers.

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

The detailed data are described as follows:

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
CORSConfiguration| Noe | All information of the CORS configuration, which can contain up to 100 CORSRules | Container | Yes

Content of the Container node CORSConfiguration:

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
CORSRule|CORSConfiguration| All information of the CORS configuration, which can contain up to 100 CORSRules | Container | Yes

Content of the Container node CORSRule:

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
ID | CORSConfiguration.CORSRule | ID of the configuration rule (optional) | String | Yes
AllowedOrigin|CORSConfiguration.CORSRule| Allowed origin in the format of protocol://domain name[:port number], such as `http://www.qq.com`. Wildcard `*` is supported |strings| Yes
AllowedMethod|CORSConfiguration.CORSRule| Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE |strings| Yes
AllowedHeader|CORSConfiguration.CORSRule| Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard * is supported |strings| Yes
MaxAgeSeconds|CORSConfiguration.CORSRule| Sets the validity period of the result of the OPTIONS request |integer| Yes
ExposeHeader|CORSConfiguration.CORSRule| Sets custom header information from the server that the browser can receive |strings| Yes


### Error Codes
There are no special error messages for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

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


