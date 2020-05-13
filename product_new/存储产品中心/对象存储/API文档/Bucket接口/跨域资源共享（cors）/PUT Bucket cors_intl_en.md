## Feature Description

This API (PUT Bucket cors) is used to set the cross-origin resource sharing permission of a bucket. You can implement the configuration by passing in a configuration file in XML format of up to 64 KB in size. By default, the bucket owner has direct permission to use this API and can also grant permission to other users.

## Request

#### Sample request

```sh
PUT /?cors HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: length
Content-Type: application/xml
Content-MD5: MD5
Authorization: Auth String
```

> Note:
>
> Authorization: Auth String (for more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request header

In addition to common request headers, this API also supports the following required request headers. For more information on common request headers, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name | Description | Type | Required |
| :---------- | :----------------------------------------------------------- | :----- | :------- |
| Content-MD5 | Base64-encoded MD5 hash of the request body content as defined in RFC 1864, used for performing integrity checks to verify whether the request body has changed during transfer | string | Yes |

#### Request body

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

The detailed data are described as follows:

| Node Name (Keyword) | Parent Node | Description  | Type | Required |
| :----------------- | :----- | :--------------------------------------------------------- | :-------- | :------- |
| CORSConfiguration  | None | Information list of all CORS configurations, can contain up to 100 CORSRules | Container | Yes |

Content of the Container node CORSConfiguration:

| Node Name (Keyword) | Parent Node | Description  | Type | Required |
| :----------------- | :---------------- | :--------------------------------------------------------- | :-------- | :------- |
| CORSRule | CORSConfiguration  | Information list of all CORS configurations, can contain up to 100 CORSRules | Container | Yes |

Content of the Container node CORSRule:

| Node Name (Keyword) | Parent Node | Description  | Type | Required |
| :----------------- | :------------------------- | :----------------------------------------------------------- | :------ | :------- |
| ID                 | CORSConfiguration.CORSRule | ID of the configured rule (optional)                                         | string  | No       |
| AllowedOrigin      | CORSConfiguration.CORSRule | Allowed origin in the format `protocol://domain name[:port number]`, such as `http://www.qq.com`. Wildcard `*` is supported | strings | Yes |
| AllowedMethod      | CORSConfiguration.CORSRule | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE       | strings | Yes       |
| AllowedHeader      | CORSConfiguration.CORSRule | Tells the server when sending `OPTIONS` requests which user-defined HTTP request headers can be used for subsequent requests. Wildcard `*` is supported | strings | Yes       |
| MaxAgeSeconds      | CORSConfiguration.CORSRule | Sets the validity period of the result of the OPTIONS request                            | integer | Yes       |
| ExposeHeader       | CORSConfiguration.CORSRule | Sets custom header information from the server that the browser can receive           | strings | Yes       |

## Response

#### Response header

This API only returns common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this request is empty.

#### Error codes

| Error Code | Description | HTTP Status Code |
| :-------------------- | :--------------------------------------------------- | :----------------------------------------------------------- |
| SignatureDoesNotMatch | If the signature provided does not meet the rules, this error code will be returned  | 403 [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) |
| NoSuchBucket          | If the bucket to which you want to add the rule does not exist, this error code will be returned | 404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) |

## Use Case

#### Request

```sh
PUT /?cors HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Content-MD5: q+xJ56ypmuOSKbkohlpZIg==
Content-Type: application/xml
Authorization: q-sign-algorithm=sha1&q-ak=AKIDVMyLTL4B8rVt52LTozzPZBYffPs9****&q-sign-time=1578385303;1578392503&q-key-time=1578385303;1578392503&q-header-list=content-md5;content-type;host&q-url-param-list=cors&q-signature=730a82c7afed2a6c051870d54895193235e8****
Content-Length: 385

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

#### Response

```sh
HTTP/1.1 200 OK
content-length: 0
connection: close
date: Tue, 07 Jan 2020 08:21:44 GMT
server: tencent-cos
x-cos-request-id: NWUxNDNmOThfNWFiMjU4NjRfMWIxYl9lYWY1****
```