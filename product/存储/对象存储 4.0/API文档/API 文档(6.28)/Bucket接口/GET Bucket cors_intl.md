## Description
This API (GET Bucket cors) is used by the Bucket owner to obtain the cross-origin resource sharing (CORS, a W3C standard) configuration set for the Bucket. By default, the Bucket owner has the permission to use this API and can grant it to others.

## Request
### Request example

```
GET /?cors HTTP/1.1
Host: <Bucketname-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

### Request headers

#### Common headers
Common request headers are used for the implementation of this request operation. For more information, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).
#### Special request headers
This request operation does not use any special request header.

### Request body
The request body of this request is empty.

## Response

### Response headers
#### Common response headers
This response uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special response headers
This response does not use any special response header.

### Response body
CORS configuration information is obtained successfully.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<CORSConfiguration>
    <CORSRule>
        <ID>bucketid</ID>
        <AllowedOrigin>http: //www.qq.com</AllowedOrigin>
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
CORSConfiguration | None | All CORS configuration information, containing up to 100 CORSRule elements. | Container | Yes

Content of Container node CORSConfiguration:

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
CORSRule | CORSConfiguration | All CORS configuration information, containing up to 100 CORSRule elements. | Container | Yes

Content of Container node CORSRule:

Node Name (Keyword) | Parent Node | Description | Type | Required
---|---|---|---|---
ID | CORSConfiguration.CORSRule | ID of the configuration rule (Optional) | String | Yes
AllowedOrigin | CORSConfiguration.CORSRule | Allowed access source. Wildcard `*` is supported. Format: protocol://domain name[:port], for example, `http://www.qq.com` | strings | Yes |
AllowedMethod | CORSConfiguration.CORSRule | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, and DELETE | strings | Yes
AllowedHeader | CORSConfiguration.CORSRule | Notifies the server about which custom HTTP request headers are allowed for subsequent requests when an OPTIONS request is sent. Wildcard "*" is supported. | strings | Yes
MaxAgeSeconds | CORSConfiguration.CORSRule | Configures the valid period for the results obtained by OPTIONS request. | integer | Yes
ExposeHeader | CORSConfiguration.CORSRule | Configures the custom header information that can be received by the browser from the server end. | strings | Yes


### Error codes
No special error message is returned for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

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
        <AllowedOrigin>http: //www.qq.com</AllowedOrigin>
        <AllowedMethod>PUT</AllowedMethod>
        <AllowedHeader>x-cos-meta-test</AllowedHeader>
        <ExposeHeader>x-cos-meta-test1</ExposeHeader>
        <MaxAgeSeconds>500</MaxAgeSeconds>
    </CORSRule>
</CORSConfiguration>
```



