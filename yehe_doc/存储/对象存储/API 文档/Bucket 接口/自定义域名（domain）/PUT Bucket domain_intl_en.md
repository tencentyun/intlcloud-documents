## Feature description

This API is used to configure a custom domain name for a bucket.

>
> - Currently, you are allowed to add 20 custom domain names. To add more, please contact our technical services team by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).
> - The custom domain name supports 3 types of origin servers, default, static website, and global acceleration. To use a static website origin server, you need to [enable a static website](https://intl.cloud.tencent.com/document/product/436/14984). To use a global acceleration origin server, you need to [enable global acceleration](https://intl.cloud.tencent.com/document/product/436/33406).
> - By default, the root account has the permission to add a custom domain name to a bucket and can grand such permission to a sub-account by granting it permission on the `PutBucketDomain` API in the [CAM Console](https://console.cloud.tencent.com/cam/overview).

## Request

#### Sample request

```plaintext
PUT /?domain HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Request Body]
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request parameters

This API does not use any request parameters.

#### Request headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request body submits the **application/xml** request data which includes all the information on the custom domain name of a bucket.

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

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------- | ------ | ----------------------------------------- | --------- | -------- |
| DomainConfiguration | None     | Contains all the request information for PUT Bucket domain | Container | No       |

**Content of the Container node `DomainConfiguration`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------- | -------- | --------- | -------- |
| DomainRule         | DomainConfiguration | Domain entry | Container | Yes       |

**Content of the Container node `DomainRule`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| Status             | DomainConfiguration.DomainRule | Domain status. Enumerated values:<br><li>`ENABLED`, <li>`DISABLED`    | Enum   | Yes       |
| Name               | DomainConfiguration.DomainRule | Full domain name                                                     | string | Yes       |
| Type               | DomainConfiguration.DomainRule | Type of the origin server. Enumerated values: <br><li>REST: default<li>WEBSITE: static website<li>ACCELERATE: global acceleration | Enum   |
| ForcedReplacement  | DomainConfiguration.DomainRule | If the specified domain name has been used for another bucket, you can specify the element to force the domain name to be a custom domain name for the current bucket. With only CNAME currently supported, this API can set up the custom domain name only after you point its CNAME to the current bucket’s origin domain name, which is associated with a default origin server, static website origin server, or global acceleration origin server, depending on the `Type` element value. | Enum   | No       |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use cases

#### Request

```plaintext
PUT /?domain HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 29 Apr 2020 09:16:14 GMT
Content-Type: application/xml
Content-Length: 288
Content-MD5: WHjVNjOz7lW82VThLKf4Lg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1588151774;1588158974&q-key-time=1588151774;1588158974&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=domain&q-signature=5cd58e4c68125ee6c78d626089d12c41376a****
Connection: close

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

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Wed, 29 Apr 2020 09:16:15 GMT
Server: tencent-cos
x-cos-request-id: NWVhOTQ1ZGVfZTViOTJhMDlfMzA0MjJfMTEwMmJi****
```