## Description

This API (PUT Bucket website) is used to configure a static website for a Bucket by importing configuration files in XML format. The file size is limited to 64 KB.

## Request

### Request example

```shell
PUT /?website HTTP/1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date: date
Content-Length: length
Content-Type:application/xml
Authorization: Auth String
<XML file>
```

> Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

### Request headers

#### Common headers

Common request headers are used for the implementation of this request operation. For more information, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

#### Special request headers

This request operation does not use any special request header.

### Request body

```shell
<WebsiteConfiguration>
	<IndexDocument>
		<Suffix>index.html</Suffix>
	</IndexDocument>
	<RedirectAllRequestsTo>
		<Protocol>https</Protocol>
	</RedirectAllRequestsTo>
	<ErrorDocument>
		<Key>Error.html</Key>
	</ErrorDocument>
	<RoutingRules>
		<RoutingRule>
			<Condition>
				<HttpErrorCodeReturnedEquals>404</HttpErrorCodeReturnedEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyWith>404.html</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>docs/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyPrefixWith>documents/</ReplaceKeyPrefixWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>img/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyWith>demo.jpg</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
	</RoutingRules>
</WebsiteConfiguration>
```

Details are described below:

| Name | Parent Node | Description | Type | Required |
| --------------------------- | --------------------- | ------------------------------------------------------------ | --------- | ---- |
| WebsiteConfiguration | None | Static website configuration, including index document, error document, protocol conversion and routing rules. | Container | Yes |
| IndexDocument | WebsiteConfiguration | Index document | Container | Yes |
| Suffix | IndexDocument | Specifies the index document | String | Yes |
| ErrorDocument | WebsiteConfiguration | Error document | Container | No |
| Key | ErrorDocument | Specifies the common error page returned | String | No |
| RedirectAllRequestsTo | WebsiteConfiguration | Redirects all requests | Container | No |
| Protocol | RedirectAllRequestsTo | Specifies the routing protocol for the entire website. Only HTTP is supported. | String | No |
| RoutingRules | WebsiteConfiguration | Sets routing rules in batch. A maximum of 100 routing rules can be set. | Container | No |
| RoutingRule | RoutingRules | Sets a single routing rule. You can set a routing rule for the requests with a specified path prefix or for the requests for which a specified error code is returned. | Container | No |
| Condition | RoutingRule | Specifies the condition for the redirection. You cannot specify both prefix match routing condition and error code routing condition. | Container | No |
| HttpErrorCodeReturnedEquals | Condition | Specifies the redirection error code. Only 4XX status codes are supported. It has a higher priority than ErrorDocument. | Integer | No |
| KeyPrefixEquals | Condition | Specifies the prefix of the paths to be redirected. | String | No |
| Redirect | RoutingRule | Specifies the replacement rule when the redirection condition is met. | Container | No |
| ReplaceKeyWith | Redirect | Specifies the content which is used to replace the entire Key. | String | No |
| ReplaceKeyPrefixWith | Redirect | Specifies the content which is used to replace the prefix of Key. This is allowed only when Conditon is KeyPrefixEquals. | String | No |

## Response

### Response headers

#### Common response headers

This response uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special response headers

This response does not use any special response header.

### Response body

The response body is empty.

### Error codes

No special error message is returned for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example

### Request

```shell
PUT /?website HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Date:Thu, 21 Sep 2017 13:05:41 +0000
Content-Type: application/xml
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484814927;32557710927&q-key-time=1484814927;32557710927&q-header-list=host&q-url-param-list=website&q-signature=8b9f05dabce2578f3a79d732386e7cbade9033e3
Content-Length: 646

<WebsiteConfiguration>
	<IndexDocument>
		<Suffix>index.html</Suffix>
	</IndexDocument>
	<RedirectAllRequestsTo>
		<Protocol>https</Protocol>
	</RedirectAllRequestsTo>
	<ErrorDocument>
		<Key>Error.html</Key>
	</ErrorDocument>
	<RoutingRules>
		<RoutingRule>
			<Condition>
				<HttpErrorCodeReturnedEquals>404</HttpErrorCodeReturnedEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyWith>404.html</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>docs/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyPrefixWith>documents/</ReplaceKeyPrefixWith>
			</Redirect>
		</RoutingRule>
		<RoutingRule>
			<Condition>
				<KeyPrefixEquals>img/</KeyPrefixEquals>
			</Condition>
			<Redirect>
				<Protocol>https</Protocol>
				<ReplaceKeyWith>demo.jpg</ReplaceKeyWith>
			</Redirect>
		</RoutingRule>
	</RoutingRules>
</WebsiteConfiguration>
```

### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu, 21 Sep 2017 13:05:54 GMT
Server: tencent-cos
x-cos-request-id: NTljM2I5MzJfMjQ4OGY3MGFfNzk4OV83Zg==
```

