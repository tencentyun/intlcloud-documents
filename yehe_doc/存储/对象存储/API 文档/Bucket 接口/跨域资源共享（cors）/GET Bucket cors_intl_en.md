## API description

This API is used to query the cross-origin resource sharing (CORS) access control configuration of a bucket.

## Request

#### Sample request

```plaintext
GET /?cors HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

This API does not use any request parameters.

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful query will return **application/xml** data which includes all information about the CORS configuration on the bucket.

```xml
<?xml version='1.0' encoding='utf-8' ?>
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

The detailed nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| CORSConfiguration | None     | Stores the result of the `GET Bucket cors` request | Container |

**Container node `CORSConfiguration`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| CORSRule | CORSConfiguration | Contains all information on a CORS rule |  Container |

**Container node `CORSRule`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| AllowedOrigin | CORSConfiguration.CORSRule | Allowed access source(s) in a CORS rule; supports `*` or domain names containing `*` | string |
| AllowedMethod | CORSConfiguration.CORSRule | Allowed HTTP method(s) in a CORS rule; corresponds to the Access-Control-Allow-Methods header in a CORS response. Enumerated values: PUT, GET, POST, DELETE, HEAD | enum |
| AllowedHeader | CORSConfiguration.CORSRule | Specifies one or more custom HTTP request headers (case-insensitive) in a CORS rule that the browser is allowed to include in a CORS request. `*` is supported. | string |
| ExposeHeader | CORSConfiguration.CORSRule | CORS response header(s) in a CORS rule that can be exposed to the browser; case-insensitive | string |
| MaxAgeSeconds | CORSConfiguration.CORSRule | Sets only one validity duration in sec of a CORS configuration in a CORS rule. This parameter corresponds to the CORS response header `Access-Control-Max-Age` | integer |
| ID | CORSConfiguration.CORSRule | Sets the single unique ID of a CORS rule. The use of this node depends on whether the ID was specified when using PUT Bucket cors to set a CORS configuration on the bucket | string |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

```plaintext
GET /?cors HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 09 Jul 2020 11:15:12 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1594293312;1594300512&q-key-time=1594293312;1594300512&q-header-list=date;host&q-url-param-list=cors&q-signature=8c00249260b2535056d2ef8fc43ecd675515****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1196
Connection: close
Date: Thu, 09 Jul 2020 11:15:12 GMT
Server: tencent-cos
x-cos-request-id: NWYwNmZjNDBfN2ViMTJhMDlfZDNjOV8xYjdk****

<?xml version='1.0' encoding='utf-8' ?>
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
		<AllowedOrigin>https://example-1.com</AllowedOrigin>
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
