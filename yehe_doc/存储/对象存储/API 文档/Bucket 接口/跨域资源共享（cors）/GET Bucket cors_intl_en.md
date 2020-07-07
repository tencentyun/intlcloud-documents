## Feature
This API allows the bucket owner to obtain the cross-origin resource sharing (CORS, a W3C standard) configuration of a bucket. By default, the bucket owner has the permission to use this API and can grant such permission to other users.

## Request
#### Sample request

```shell
GET /?cors HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request headers
This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body
The request body of this request is empty.

## Response

#### Response headers
This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body
CORS configuration information is obtained successfully.

```shell
<?xml version="1.0" encoding="UTF-8" ?>
<CORSConfiguration>
    <CORSRule>
        <ID>1234</ID>
        <AllowedOrigin>http://www.qq.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedHeader>x-cos-meta-test</AllowedHeader>
        <MaxAgeSeconds>500</MaxAgeSeconds>
        <ExposeHeader>x-cos-meta-test1</ExposeHeader>
    </CORSRule>
</CORSConfiguration>
```

The nodes are described in details below:

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|--
|CORSConfiguration| None | Describes all the information on the CORS configuration, which can contain up to 100 `CORSRules` | Container

Container node `CORSConfiguration`:

Node Name (Keyword) | Parent Node | Description | Type |
---|---|---|--
CORSRule | CORSConfiguration  | Describes all the information on the CORS configuration, which can contain up to 100 `CORSRules` | Container

Container node `CORSRule`:

Node Name (Keyword) | Parent Node | Description | Type
---|---|---|---
ID|CORSConfiguration.CORSRule| CORS rule ID that depends on whether the ID field is specified in a PUT Bucket cors request |string
AllowedOrigin      | CORSConfiguration.CORSRule | Allowed origin in the format `protocol://domain name[:port number]`, such as `http://www.qq.com`. Wildcard `*` is supported | strings
AllowedMethod|CORSConfiguration.CORSRule| Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE |strings
AllowedHeader   | CORSConfiguration.CORSRule | Tells the server when sending `OPTIONS` requests which user-defined HTTP request headers can be used for subsequent requests. Wildcard `*` is supported | strings
MaxAgeSeconds|CORSConfiguration.CORSRule| Sets the validity period of the result of the `OPTIONS` request |integer
ExposeHeader|CORSConfiguration.CORSRule| Sets the user-defined headers from the server side that can be received by the browser |strings


#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

```shell
GET /?cors HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2016 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484815944;32557711944&q-key-time=1484815944;32557711944&q-header-list=host&q-url-param-list=cors&q-signature=a2d28e1b9023d09f9277982775a4b3b705d0****
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 345
Connection: keep-alive
Date: Wed, 28 Oct 2016 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDdlNGZfNDYyMDRlXzM0YWFf****

<CORSConfiguration>
    <CORSRule>
        <ID>1234</ID>
        <AllowedOrigin>http://www.qq.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedHeader>x-cos-meta-test</AllowedHeader>
        <MaxAgeSeconds>500</MaxAgeSeconds>
        <ExposeHeader>x-cos-meta-test1</ExposeHeader>
    </CORSRule>
</CORSConfiguration>
```


