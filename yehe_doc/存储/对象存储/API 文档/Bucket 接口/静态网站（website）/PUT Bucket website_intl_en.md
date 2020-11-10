## Overview

This API is used to configure a static website for a bucket by importing configuration files in XML format. The file size is limited to 64 KB.

## Request

#### Sample request

```plaintext
PUT /?website HTTP/1.1
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

This request body submits the **application/xml** request data which includes all information about the static website configuration on the bucket.

```xml
<WebsiteConfiguration>
	<IndexDocument>
		<Suffix>String</Suffix>
	</IndexDocument>
	<RedirectAllRequestsTo>
		<Protocol>String</Protocol>
	</RedirectAllRequestsTo>
    <AutoAddressing>
        <Status>Enabled|Disabled</Status>
    </AutoAddressing>
	<ErrorDocument>
		<Key>String</Key>
		<OriginalHttpStatus>Enabled|Disabled</OriginalHttpStatus>
	</ErrorDocument>
	<RoutingRules>
		<RoutingRule>
			<Condition>
				<HttpErrorCodeReturnedEquals>Integer</HttpErrorCodeReturnedEquals>
			</Condition>
			<Redirect>
				<Protocol>String</Protocol>
				<ReplaceKeyWith>String</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>String</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>String</Protocol>
				<ReplaceKeyPrefixWith>String</ReplaceKeyPrefixWith>
			</Redirect>
		</RoutingRule>
	</RoutingRules>
</WebsiteConfiguration>
```

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| WebsiteConfiguration | None | Contains all information on the PUT Bucket website request | Container | No |

**Container node `WebsiteConfiguration`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| IndexDocument | WebsiteConfiguration | Configures the index document | Container | Yes |
| RedirectAllRequestsTo | WebsiteConfiguration | Configures the redirect for all requests | Container | No |
| AutoAddressing     |   WebsiteConfiguration | Specifies whether to ignore the file extension  | Container | No |
| ErrorDocument | WebsiteConfiguration | Configures the error document | Container | No |
| RoutingRules | WebsiteConfiguration | Configures the routing rule.  A `RoutingRules` container can contain up to 100 `RoutingRule` elements | Container | No |

**Container node `IndexDocument`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Suffix | WebsiteConfiguration.IndexDocument | Specifies the object key suffix for the index document. For example, if it is specified as `index.html`, the request automatically returns `index.html` when you access the root directory of the bucket, or `article/index.html` when you access the directory `article/`. | String | Yes |

**Container node `RedirectAllRequestsTo`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Protocol | WebsiteConfiguration.RedirectAllRequestsTo | Specifies the destination protocol for redirecting all requests. Currently, only HTTPS is supported | String | Yes |

**Container node `AutoAddressing`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Status  |  WebsiteConfiguration.AutoAddressing   | Specifies whether to ignore HTML file extension. Valid values: Enabled, Disabled (default) | String | No |

**Container node `ErrorDocument`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Key | WebsiteConfiguration.ErrorDocument | Specifies the object key to return for the error document if an error occurs and does not match the error code in the routing rule | String | Yes |
|  OriginalHttpStatus   |  WebsiteConfiguration.ErrorDocument  | Specifies the HTTP status code to match in the error document. Valid values: Enabled (default), Disabled  |  String  |  No  |

**Container node `RoutingRules`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| RoutingRule | WebsiteConfiguration.RoutingRules | Specifies a routing rule | Container | Yes |

**Container node `RoutingRules.RoutingRule`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Condition | WebsiteConfiguration.RoutingRules.RoutingRule | Sets the condition in the routing rule | Container | Yes |
| Redirect | WebsiteConfiguration.RoutingRules.RoutingRule | Sets the redirect destination in the routing rule | Container | Yes |

**Container node `RoutingRules.RoutingRule.Condition`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| HttpErrorCodeRetu<br>rnedEquals | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Condition | Specifies the error code to match in the routing rule. Only 4XX response codes are allowed, such as 403 or 404 | Integer | Either or both of this parameter and `KeyPrefixEquals` must be specified |
| KeyPrefixEquals | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Condition | Specifies the object key prefix to match in the routing rule | String | Either or both of this parameter and `HttpErrorCodeReturnedEquals` must be specified |

**Container node `RoutingRules.RoutingRule.Redirect`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Protocol | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Redirect | Specifies the destination protocol in the routing rule. Only HTTPS is allowed | String | No |
| ReplaceKeyWith | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Redirect | Specifies the object key to redirect to in the routing rule. It replaces the entire object key included in the request | String | Either or both of this parameter and `ReplaceKeyPrefixWith` must be specified |
| ReplaceKeyPrefixWith | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Redirect | Specifies the object key prefix to redirect to in the routing rule. It replaces the prefix matched in the request. It is set only if `Condition` is set to `KeyPrefixEquals`. | String | Either or both of this parameter and `ReplaceKeyWith` must be specified |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

```plaintext
PUT /?website HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 20 May 2020 09:33:38 GMT
Content-Type: application/xml
Content-Length: 1209
Content-MD5: VHzj4Uwb++HLyCJp7jUzWg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1589967218;1589974418&q-key-time=1589967218;1589974418&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=website&q-signature=4666493555640e834a879c78afaa4fd9b16a****
Connection: close

<WebsiteConfiguration>
	<IndexDocument>
		<Suffix>index.html</Suffix>
	</IndexDocument>
	<RedirectAllRequestsTo>
		<Protocol>https</Protocol>
	</RedirectAllRequestsTo>
	<ErrorDocument>
		<Key>pages/error.html</Key>
	</ErrorDocument>
	<RoutingRules>
		<RoutingRule>
			<Condition>
				<HttpErrorCodeReturnedEquals>403</HttpErrorCodeReturnedEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyWith>pages/403.html</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<HttpErrorCodeReturnedEquals>404</HttpErrorCodeReturnedEquals>
			</Condition>
			<Redirect>
				<ReplaceKeyWith>pages/404.html</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>assets/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<ReplaceKeyWith>index.html</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>article/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyPrefixWith>archived/</ReplaceKeyPrefixWith>
			</Redirect>
		</RoutingRule>
	</RoutingRules>
</WebsiteConfiguration>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Wed, 20 May 2020 09:33:38 GMT
Server: tencent-cos
x-cos-request-id: NWVjNGY5NzJfOThjMjJhMDlfMjg5Ml8yYzNi****
```
