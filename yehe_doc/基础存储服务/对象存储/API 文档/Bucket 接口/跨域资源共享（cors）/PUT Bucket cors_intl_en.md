## Overview

This API is used to configure CORS for a bucket. You need to pass in an XML configuration file within 64 KB.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutBucketCors&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>


## Request

#### Sample request

```plaintext
PUT /?cors HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Request Body]
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body submits **application/xml** data, which contains all CORS configurations of the bucket.

```plaintext
<CORSConfiguration>
	<CORSRule>
		<AllowedOrigin>string</AllowedOrigin>
		<AllowedMethod>enum</AllowedMethod>
		<AllowedMethod>enum</AllowedMethod>
		<AllowedHeader>string</AllowedHeader>
		<AllowedHeader>string</AllowedHeader>
		<ExposeHeader>string</ExposeHeader>
		<ExposeHeader>string</ExposeHeader>
		<MaxAgeSeconds>integer</MaxAgeSeconds>
	</CORSRule>
	<CORSRule>
		<ID>string</ID>
		<AllowedOrigin>string</AllowedOrigin>
		<AllowedOrigin>string</AllowedOrigin>
		<AllowedMethod>enum</AllowedMethod>
		<AllowedMethod>enum</AllowedMethod>
		<AllowedHeader>string</AllowedHeader>
		<ExposeHeader>string</ExposeHeader>
		<ExposeHeader>string</ExposeHeader>
		<MaxAgeSeconds>integer</MaxAgeSeconds>
	</CORSRule>
</CORSConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| CORSConfiguration | None  | All configurations of the `PUT Bucket cors` request | Container | No |

**Content of `CORSConfiguration`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| CORSRule | CORSConfiguration | A single CORS rule. You can configure up to 100 `CORSRule`. | Container | Yes |

**Content of `CORSRule`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| AllowedOrigin | CORSConfiguration.CORSRule | An origin allowed. More than one `AllowedOrigin` can be configured for a single `CORSRule`.<br><li>You can set it to `*` to allow all domains (not recommended). <br><li>You can set it to a single domain such as `http://www.example.com`.<br><li>`*` can be placed in any positions, including the protocol, domain name, or port to match 0 or more characters. There can only be one `*`. Note that if you use `*`, unexpected origins might be matched.<br><li>Do not omit “http” or “https”, and if the port number is not the default port (HTTP: 80; HTTPS: 443), also include the port (e.g., `https://example.com:8443`). | string | Yes |
| AllowedMethod | CORSConfiguration.CORSRule | An HTTP method allowed, which corresponds to the `Access-Control-Allow-Methods` header in the response to a CORS request. More than one `AllowedMethod` can be configured for a single `CORSRule`. Enumerated values: `PUT`, `GET`, `POST`, `DELETE`, `HEAD` | enum | Yes |
| AllowedHeader | CORSConfiguration.CORSRule | A custom HTTP header (case-insensitive) that the browser is allowed to send in a CORS request. When an `OPTIONS` request is sent, the browser will let the server know what custom HTTP headers will be used in the actual request. More than one `AllowedHeader` can be configured for a single `CORSRule`.<br><li>You can set it to `*` to allow all headers. To avoid missing headers, `*` is recommended. <br><li>If you don’t set it to `*`, every header specified in `Access-Control-Request-Headers` in the `OPTIONS` request must have a corresponding one in `AllowedHeader`. | string | Yes |
| ExposeHeader | CORSConfiguration.CORSRule | A CORS response header (case-insensitive) that can be exposed to the browser. More than one `ExposeHeader` can be configured for a single `CORSRule`. <br><li>If this parameter is not specified, the browser can only access simple response headers (`Cache-Control`, `Content-Type`, `Expires`, and `Last-Modified`) by default. Therefore, if you want the browser to access more response headers, specify them using this parameter. <br><li>You cannot set this parameter to `*`, meaning you must set it to a specific header.<br><li>You are advised to set this parameter according to the needs of your browser. `ETag` is recommended. For more information, please see the response header parts in API Documentation and [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729). | string | Yes |
| MaxAgeSeconds | CORSConfiguration.CORSRule | Validity period of the CORS configuration, in seconds. This parameter corresponds to the `Access-Control-Max-Age` header in the response to the CORS request. During the validity period, the browser does not have to issue more `OPTIONS` requests for the same request. Only one `MaxAgeSeconds` can be configured for a single `CORSRule`. | integer | Yes |
| ID | CORSConfiguration.CORSRule | ID of the `CORSRule`. It can be used to specify a specific `CORSRule` when you call `GET Bucket cors`. You can configure only one ID for a single `CORSRule` at most. | string | No |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

```plaintext
PUT /?cors HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 09 Jul 2020 11:15:01 GMT
Content-Type: application/xml
Content-Length: 1185
Content-MD5: ZNkhBxyjkaZcs1j7/cIE2A==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1594293301;1594300501&q-key-time=1594293301;1594300501&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=cors&q-signature=2ec71624468abfbd5c8ea2679e1365b29f3a****
Connection: close

<CORSConfiguration>
	<CORSRule>
		<AllowedOrigin>*</AllowedOrigin>
		<AllowedMethod>GET</AllowedMethod>
		<AllowedMethod>HEAD</AllowedMethod>
		<AllowedHeader>Range</AllowedHeader>
		<AllowedHeader>x-cos-server-side-encryption-customer-algorithm</AllowedHeader>
		<AllowedHeader>x-cos-server-side-encryption-customer-key</AllowedHeader>
		<AllowedHeader>x-cos-server-side-encryption-customer-key-MD5</AllowedHeader>
		<ExposeHeader>Content-Length</ExposeHeader>
		<ExposeHeader>ETag</ExposeHeader>
		<ExposeHeader>x-cos-meta-author</ExposeHeader>
		<MaxAgeSeconds>600</MaxAgeSeconds>
	</CORSRule>
	<CORSRule>
		<ID>example-id</ID>
		<AllowedOrigin>https://example.com</AllowedOrigin>
		<AllowedOrigin>https://example.net</AllowedOrigin>
		<AllowedMethod>PUT</AllowedMethod>
		<AllowedMethod>GET</AllowedMethod>
		...
		<AllowedMethod>HEAD</AllowedMethod>
		<AllowedHeader>*</AllowedHeader>
		<ExposeHeader>Content-Length</ExposeHeader>
		<ExposeHeader>ETag</ExposeHeader>
		<ExposeHeader>x-cos-meta-author</ExposeHeader>
		<MaxAgeSeconds>600</MaxAgeSeconds>
	</CORSRule>
</CORSConfiguration>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Thu, 09 Jul 2020 11:15:01 GMT
Server: tencent-cos
x-cos-request-id: NWYwNmZjMzVfMzFiYjBiMDlfZjgzYV8xZDky****
```
