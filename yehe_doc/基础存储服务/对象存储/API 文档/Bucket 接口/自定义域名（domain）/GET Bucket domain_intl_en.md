## Overview

This API is used to query the custom domain configuration of a bucket.

> !By default, the root account has permission to query the custom domain configuration of a bucket and can go to the [CAM console](https://console.cloud.tencent.com/cam/overview) to grant such permission to a sub-account by allowing it to call the `GetBucketDomain` API.

## Request

#### Sample request

```plaintext
GET /?domain HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

If the request is successful, **application/xml** data that includes the complete custom domain configuration of the bucket will be returned.

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------- | ------ | ------------------------------------- | --------- |
| DomainConfiguration | None | Stores the result of `GET Bucket domain`. | Container |

**Content of `DomainConfiguration`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------- | -------- | --------- |
| DomainRule         | DomainConfiguration | Domain entry | Container |

**Content of `DomainRule`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------------ | ------------------------------------------------------------ | ------ |
| Status             | DomainConfiguration.DomainRule | Domain status. Enumerated values:<br><li>`ENABLED`, <li>`DISABLED`    | Enum   |
| Name               | DomainConfiguration.DomainRule | Full domain name                                                     | string |
| Type               | DomainConfiguration.DomainRule | Type of the origin server. Enumerated values: <br><li>`REST`: default origin server<li>`WEBSITE`: static website origin server<li>`ACCELERATE`: global acceleration origin server | Enum   |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

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
