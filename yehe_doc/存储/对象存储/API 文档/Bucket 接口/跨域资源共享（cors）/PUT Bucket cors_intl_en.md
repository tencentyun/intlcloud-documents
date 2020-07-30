## API Description

This API is used to configure the cross-origin resource sharing (CORS) access control configuration for a bucket. To do so, you need to pass in a configuration file in XML format of up to 64 KB in size.

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

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

This API does not use any request parameters.

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request body submits the **application/xml** request data which includes all information about the CORS configuration on the bucket.

```xml
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

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| CORSConfiguration  | None     | Contains all information on a PUT Bucket cors request | Container | No       |

**Container node `CORSConfiguration`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| CORSRule | CORSConfiguration  | Contains all information on a CORS rule. You can specify up to 100 CORS rules | Container | Yes |

**Container node `CORSRule`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| AllowedOrigin | CORSConfiguration.CORSRule | Allowed access source(s) in a CORS rule.<br><li>`*` is supported, indicating all domain names are allowed (not recommended).<br><li>A single domain name is supported, e.g. `http://www.example.com`.<br><li>The use of only one `*` wildcard in a domain name is supported. It can appear in any position, including protocol, domain name, and port, indicating matching 0 or more characters. Please use this option with caution, as it may accidentally match unexpected sources.<br><li>Remember to specify http or https, and also port, except the default port 80(http) or 443(https), e.g. `https://example.com:8443`. | string | Yes |
| AllowedMethod | CORSConfiguration.CORSRule | Allowed HTTP method(s) in a CORS rule; corresponds to the Access-Control-Allow-Methods header in a CORS response. Enumerated values: PUT, GET, POST, DELETE, HEAD. | enum | Yes |
| AllowedHeader | CORSConfiguration.CORSRule | Specifies one or more custom HTTP request headers (case-insensitive) in a CORS rule that the browser is allowed to include in a CORS request.<br><li>`*` is supported, indicating allowing all headers (recommended).<br><li>Alternatively, specify headers the same as those in the `Access-Control-Request-Headers` of the OPTIONS preflight request. | string | Yes |
| ExposeHeader | CORSConfiguration.CORSRule | CORS response header(s) in a CORS rule that can be exposed to the browser; cast-insensitive.<br><li>If this parameter is not specified, the browser can access only simple response headers Cache-Control, Content-Type, Expires, and Last-Modified by default.<br><li>Headers must be specified, with `*` not supported.<br><li>Depending on your browser needs, it is recommended to use ETag by default. For more information, see the API-specific documentation about response headers and [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729). | string | Yes |
| MaxAgeSeconds | CORSConfiguration.CORSRule | Sets only one validity duration in sec of a CORS configuration in a CORS rule. Within this duration, the browser need not send another OPTIONS preflight request for the same request. This parameter corresponds to the CORS response header `Access-Control-Max-Age`. | integer | Yes |
| ID | CORSConfiguration.CORSRule | ID of a CORS rule used to search for a specified CORS rule for a GET Bucket cors action. | string | No |

## Response

#### Response headers

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

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
