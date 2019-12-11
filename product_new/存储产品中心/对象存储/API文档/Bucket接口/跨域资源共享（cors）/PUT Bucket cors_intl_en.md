## Description
This API is used to configure the cross-origin resource sharing (CORS) permission of a bucket. You can make the configuration by passing in a configuration file in XML format of up to 64 KB in size. By default, the bucket owner has the permission to use this API and can grant such permission to other users.

## Request
### Sample Request

```sh
PUT /?cors HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: length
Content-Type: application/xml
Content-MD5: MD5
Authorization: Auth String

```
> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).


### Request Headers

#### Common Headers

The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
This request operation does not use any special request header.

### Request Body
The request body of this request is a CORS rule.

```http
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


The data are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|---|---|---|---|---|
|CORSConfiguration| Noe | Describes all the information on the CORS configuration, which can contain up to 100 `CORSRules` | Container | Yes |

Content of the Container node `CORSConfiguration`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| CORSRule | CORSConfiguration | Describes all the information on the CORS configuration, which can contain up to 100 `CORSRules` | Container | Yes |

Content of the Container node `CORSRule`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|---|---|---|---|---|
|ID|CORSConfiguration.CORSRule|ID of the configuration rule; optional |string| Yes |
|AllowedOrigin|CORSConfiguration.CORSRule| Allowed origin in the format of `protocol://domain name[:port number]`, such as `http://www.qq.com`. Wildcard `*` is supported |strings| Yes |
|AllowedMethod|CORSConfiguration.CORSRule| Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE |strings| Yes |
|AllowedHeader|CORSConfiguration.CORSRule| Tells the server side when sending the `OPTIONS` request what user-defined HTTP request headers can be used for subsequent requests. Wildcard `*` is supported |strings| Yes |
|MaxAgeSeconds|CORSConfiguration.CORSRule| Sets the validity period of the result of the `OPTIONS` request |integer| Yes |
|ExposeHeader|CORSConfiguration.CORSRule| Sets the user-defined header information from the server side that can be received by the browser |strings| Yes |


## Response
### Response Headers

#### Common Response Headers

This response uses common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers
This request operation does not use any special response header.

### Response Body
The response body of this request is empty.

### Error Codes

| Error Code | Description | HTTP Status Code |
|---|---|---|
|SignatureDoesNotMatch| If the provided signature does not conform to the rule, this error code will be returned |403 [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) |
|NoSuchBucket| If the bucket to which you want to add the rule does not exist, this error code will be returned |404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) |

## Example

### Request

```sh
PUT /?cors HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2017 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484814927;32557710927&q-key-time=1484814927;32557710927&q-header-list=host&q-url-param-list=cors&q-signature=8b9f05dabce2578f3a79d732386e7cbade9033e3
Content-Type: application/xml
Content-Length: 280

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

### Response

```sh
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 10 Mar 2017 09:45:46 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDdiZWRfOWExZjRlXzQ2OWVfZGY0
```


