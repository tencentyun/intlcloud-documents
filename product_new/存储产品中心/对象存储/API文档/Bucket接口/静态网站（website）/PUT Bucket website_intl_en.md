## Feature

This API is used to configure a static website for a bucket by importing configuration files in XML format. The file size is limited to 64 KB.

## Request

#### Request samples

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

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

This API does not use any request parameter.

#### Request headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request body submits the **application/xml** request data which includes all information about the static website configuration on the bucket.

```xml
<WebsiteConfiguration>
	<IndexDocument>
		<Suffix>string</Suffix>
	</IndexDocument>
	<RedirectAllRequestsTo>
		<Protocol>string</Protocol>
	</RedirectAllRequestsTo>
	<ErrorDocument>
		<Key>string</Key>
	</ErrorDocument>
	<RoutingRules>
		<RoutingRule>
			<Condition>
				<HttpErrorCodeReturnedEquals>integer</HttpErrorCodeReturnedEquals>
			</Condition>
			<Redirect>
				<Protocol>string</Protocol>
				<ReplaceKeyWith>string</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>string</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>string</Protocol>
				<ReplaceKeyPrefixWith>string</ReplaceKeyPrefixWith>
			</Redirect>
		</RoutingRule>
	</RoutingRules>
</WebsiteConfiguration>
```

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| WebsiteConfiguration | None | Contains all the request information about PUT Bucket website | Container | No |

**Content of the Container node `WebsiteConfiguration`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| IndexDocument | WebsiteConfiguration | Index document | Container | Yes |
| RedirectAllRequestsTo | WebsiteConfiguration | Redirects all requests | Container | No |
| ErrorDocument | WebsiteConfiguration | Error document | Container | No |
| RoutingRules | WebsiteConfiguration | Sets routing rules in batch. A maximum of 100 routing rules can be set. | Container | No |

**Content of the Container node `IndexDocument`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Suffix | WebsiteConfiguration.IndexDocument | Specifies the object key suffix for index documents. For example, if it is specified as `index.html`, the request automatically returns `index.html` when you access the root directory of the bucket, or `article/index.html` when you access the directory `article/`. | string | Yes |

**Content of the Container node `RedirectAllRequestsTo`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Protocol | WebsiteConfiguration.RedirectAllRequestsTo | Specifies the destination protocol for all redirect requests, currently supporting only HTTPS | string | Yes |

**Content of the Container node `ErrorDocument`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Key | WebsiteConfiguration.ErrorDocument | Specifies the object key of a general error document. It is returned if an error occurs and does not hit the error code in the redirect rule. | string | Yes |

**Content of the Container node `RoutingRules`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| RoutingRule | WebsiteConfiguration.RoutingRules | Sets a single redirect rule. | Container | Yes |

**Content of the Container node `RoutingRules.RoutingRule`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Condition | WebsiteConfiguration.RoutingRules.RoutingRule | Sets the condition for the redirect rule | Container | Yes |
| Redirect | WebsiteConfiguration.RoutingRules.RoutingRule | Sets the redirect destination for the redirect rule | Container | Yes |

**Content of the Container node `RoutingRules.RoutingRule.Condition`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| HttpErrorCodeRetu<br>rnedEquals | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Condition | Specifies the error code as match condition for the redirect rule. Valid values: only 4XX return codes, such as 403 or 404. | integer | Either this parameter or `KeyPrefixEquals` must be specified. |
| KeyPrefixEquals | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Condition | Specifies the object key prefix as match condition for the redirect rule | string | Either this parameter or `HttpErrorCodeReturnedEquals` must be specified. |

**Content of the Container node `RoutingRules.RoutingRule.Redirect`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Protocol | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Redirect | Specifies the destination protocol for the redirect rule, supporting only HTTPS | string | No |
| ReplaceKeyWith | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Redirect | Specifies the object key of redirect destination in the redirect rule to replace the entire object key included in the original request | string | Either this parameter or `ReplaceKeyPrefixWith` must be specified. |
| ReplaceKeyPrefixWith | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Redirect | Specifies the object key prefix of redirect destination in the redirect rule to replace the prefix which the original request used for match. It is set only if the Condition is `KeyPrefixEquals`. | string | Either this value or `ReplaceKeyWith` must be specified.|

## Response

#### Response headers

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use Cases

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
