## Overview

This API is used to query the CORS configuration set for a bucket.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetBucketCors&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
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
GET /?cors HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
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

This API does not have a request body.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful query returns **application/xml** data, which contains all information about the CORS configuration of the bucket.

```plaintext
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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| CORSConfiguration | None | Stores the result of `GET Bucket cors`. | Container |

**Content of `CORSConfiguration`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| CORSRule | CORSConfiguration | A single CORS rule | Container |

**Content of `CORSRule`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| AllowedOrigin | CORSConfiguration.CORSRule | An origin allowed, which can contain or be `*`. More than one `AllowedOrigin` can be configured for a single `CORSRule`. | string |
| AllowedMethod | CORSConfiguration.CORSRule | An HTTP method allowed, which corresponds to the `Access-Control-Allow-Methods` header in the response to a CORS request. More than one `AllowedMethod` can be configured for a single `CORSRule`. Enumerated values: `PUT`, `GET`, `POST`, `DELETE`, `HEAD` | enum |
| AllowedHeader | CORSConfiguration.CORSRule | A custom HTTP request header (case-insensitive) that the browser is allowed to include in a CORS request. It can be `*`. More than one `AllowedHeader` can be configured for a single `CORSRule`. | string |
| ExposeHeader | CORSConfiguration.CORSRule | A CORS response header (case-insensitive) that can be exposed to the browser. More than one `ExposeHeader` can be configured for a single `CORSRule`. | string |
| MaxAgeSeconds | CORSConfiguration.CORSRule | Validity period of the CORS configuration, in seconds. This parameter corresponds to the `Access-Control-Max-Age` header in the response to the CORS request. Only one `MaxAgeSeconds` can be configured for a single `CORSRule`. | integer |
| ID | CORSConfiguration.CORSRule | ID of a single `CORSRule`. If this node exists, `PUT Bucket cors` has set an ID for the CORS rule. Only one ID can be set for a single `CORSRule` at most. | string |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

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
