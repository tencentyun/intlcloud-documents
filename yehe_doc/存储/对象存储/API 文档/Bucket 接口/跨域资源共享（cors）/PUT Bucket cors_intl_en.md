## Feature
This API is used to configure the cross-origin resource sharing (CORS) permission for a bucket. You can make the configuration by passing in a configuration file in XML format of up to 64 KB in size. By default, the bucket owner has the permission to use this API and can grant such permission to other users.

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

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

This API does not use any request parameters.
#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).



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


The nodes are described in details below:

|Node Name (Keyword) | Parent Node | Description | Type | Required|
|---|---|---|---|---|
|CORSConfiguration| None | Describes all the information on the CORS configuration, which can contain up to 100 `CORSRules` | Container | Yes |

Container node `CORSConfiguration`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| CORSRule | CORSConfiguration | Describes all the information on the CORS configuration, which can contain up to 100 `CORSRules` | Container | Yes |

Container node `CORSRule`:

|Node Name (Keyword) | Parent Node | Description | Type | Required|
|---|---|---|---|---|
|ID|CORSConfiguration.CORSRule|CORS rule ID; optional |string| No |
|AllowedOrigin|CORSConfiguration.CORSRule| Allowed origin in the format of `protocol://domain name[:port number]`, such as `http://www.qq.com`. Wildcard `*` is supported |strings| Yes |
|AllowedMethod|CORSConfiguration.CORSRule| Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE |strings| Yes |
|AllowedHeader|CORSConfiguration.CORSRule| Tells the server side when sending the `OPTIONS` request what user-defined HTTP request headers can be used for subsequent requests. Wildcard `*` is supported |strings| Yes |
|MaxAgeSeconds|CORSConfiguration.CORSRule| Sets the validity period of the result of the `OPTIONS` request |integer| Yes |
|ExposeHeader|CORSConfiguration.CORSRule| Sets the user-defined headers from the server side that can be received by the browser |strings| Yes |


## Response
#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body
The response body is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

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

