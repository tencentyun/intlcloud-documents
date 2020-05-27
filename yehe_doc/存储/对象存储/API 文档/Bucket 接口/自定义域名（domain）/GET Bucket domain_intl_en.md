## Feature

This API (GET Bucket domain) is used to query the custom domain name configuration on a bucket.

>By default, the root account owns the permissions to query the custom domain name of a bucket. For a sub-account to do so, the root account should grant it the access to the `GetBucketDomain` API in the [CAM Console](https://console.cloud.tencent.com/cam/overview).

## Request

#### Request samples

```plaintext
GET /?domain HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request parameters

This API does not use any request parameter.

#### Request headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful query will return **application/xml** data which includes all information on the custom domain name of a bucket.

```xml
<DomainConfiguration>
	<DomainRule>
		<Status>Enum</Status>
		<Name>string</Name>
		<Type>Enum</Type>
	</DomainRule>
	<DomainRule>
		<Status>Enum</Status>
		<Name>string</Name>
		<Type>Enum</Type>
	</DomainRule>
</DomainConfiguration>
```

The detailed nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------- | ------ | ------------------------------------- | --------- |
| DomainConfiguration | None     | Saves all information in the `GET Bucket domain` results | Container |

**Content of the Container node `DomainConfiguration`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------- | -------- | --------- |
| DomainRule         | DomainConfiguration | Domain entry | Container |

**Content of the Container node `DomainRule`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------------ | ------------------------------------------------------------ | ------ |
| Status             | DomainConfiguration.DomainRule | Domain status. Enumerated values:<br><li>`ENABLED`, <li>`DISABLED`    | Enum   |
| Name               | DomainConfiguration.DomainRule | Full domain name                                                     | string |
| Type               | DomainConfiguration.DomainRule | Type of the origin server. Enumerated values: <br><li>REST: default origin server<li>WEBSITE: static website origin server<li>ACCELERATE: global acceleration origin server | Enum   |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use Cases

#### Request

```plaintext
GET /?domain HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 29 Apr 2020 09:16:26 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1588151786;1588158986&q-key-time=1588151786;1588158986&q-header-list=date;host&q-url-param-list=domain&q-signature=b5f4a4b7bd7bca2ade21503b8f64d512ef69****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 277
Connection: close
Date: Wed, 29 Apr 2020 09:16:26 GMT
Server: tencent-cos
x-cos-domain-txt-verification: tencent-cloud-cos-verification=673029e5ff8e4d2b5723d58f73aab232
x-cos-request-id: NWVhOTQ1ZWFfN2ViMTJhMDlfMjU5Zl8xMzQ1****

<DomainConfiguration>
	<DomainRule>
		<Status>ENABLED</Status>
		<Name>cos.cloud.tencent.com</Name>
		<Type>REST</Type>
	</DomainRule>
	<DomainRule>
		<Status>ENABLED</Status>
		<Name>www.cos.cloud.tencent.com</Name>
		<Type>WEBSITE</Type>
	</DomainRule>
</DomainConfiguration>
```