## Overview

This API is used to configure a static website for a bucket by importing configuration files in XML format. The file size is limited to 64 KB.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutBucketWebsite&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>


## Requests

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

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request body submits the **application/xml** data that includes all information about the static website configuration of the bucket.

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| WebsiteConfiguration | None | Contains all the request information about PUT Bucket website | Container | No |

**Content of `WebsiteConfiguration`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| IndexDocument | WebsiteConfiguration | Index document configuration | Container | Yes |
| RedirectAllRequestsTo | WebsiteConfiguration | Configures redirection for all requests | Container | No |
| AutoAddressing     |   WebsiteConfiguration | Whether to ignore all file extensions  | Container | No |
| ErrorDocument | WebsiteConfiguration | Error document configuration | Container | No  |
| RoutingRules | WebsiteConfiguration | Routing rule configuration. A `RoutingRules` container can contain up to 100 `RoutingRule` elements. | Container | No |

**Content of `IndexDocument`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Suffix | WebsiteConfiguration.IndexDocument | Specifies the object key suffix for index documents. For example, if it is specified as `index.html`, the request automatically returns `index.html` when you access the root directory of the bucket, or `article/index.html` when you access the directory `article/`. | String | Yes |

**Content of `RedirectAllRequestsTo`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Protocol | WebsiteConfiguration.RedirectAllRequestsTo | Specifies the target protocol to redirect all requests. Only HTTPS is supported. | String | Yes |

**Content of `AutoAddressing`**:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Status  |  WebsiteConfiguration.AutoAddressing   | Whether to ignore the HTML file extension. Valid values: `Enabled`, `Disabled` (default) | String | No |

**Content of `ErrorDocument`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Key | WebsiteConfiguration.ErrorDocument | Specifies the object key to return for the error document if an error occurs and does not match the error code in the routing rule | String | Yes |
| OriginalHttpStatus | WebsiteConfiguration.ErrorDocument  | Configures whether to return the corresponding HTTPS status code if the error documents are hit. Valid values: `Enabled` (default), `Disabled` |  String  |  No  |

**Content of `RoutingRules`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| RoutingRule | WebsiteConfiguration.RoutingRules | A single routing rule | Container | Yes |

**Content of `RoutingRules.RoutingRule`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Condition | WebsiteConfiguration.RoutingRules.RoutingRule | Condition for the routing rule | Container | Yes |
| Redirect | WebsiteConfiguration.RoutingRules.RoutingRule | Configuration of the redirection target | Container | Yes |

**Content of `RoutingRules.RoutingRule.Condition`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| HttpErrorCodeRetu<br>rnedEquals | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Condition | Specifies the error code as the match condition for the routing rule. Valid values: only 4xx return codes, such as 403 or 404. | Integer | Either this parameter or `KeyPrefixEquals` must be specified. |
| KeyPrefixEquals | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Condition | Specifies the object key prefix as the match condition for the routing rule | String | Either this parameter or `HttpErrorCodeReturnedEquals` must be specified. |

**Content of `RoutingRules.RoutingRule.Redirect`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Protocol | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Redirect | Specifies the target protocol for the routing rule. Only HTTPS is supported. | String | No |
| ReplaceKeyWith | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Redirect | Specifies the target object key to replace the original object key in the request. | String | Either this parameter or `ReplaceKeyPrefixWith` must be specified. |
| ReplaceKeyPrefixWith | WebsiteConfigura<br>tion.RoutingRules.<br>RoutingRule.Redirect | Specifies the object key prefix to replace the original prefix in the request. You can set this parameter only if the condition is `KeyPrefixEquals`. | String | Either this parameter or `ReplaceKeyWith` must be specified.|

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
