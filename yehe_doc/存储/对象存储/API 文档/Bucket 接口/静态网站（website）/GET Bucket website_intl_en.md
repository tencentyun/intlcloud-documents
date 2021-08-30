## Overview

This API is used to query the configuration of static websites associated with a bucket.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetBucketWebsite&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
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
GET /?website HTTP/1.1
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

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful query will return **application/xml** data that includes all information about the static website configuration of the bucket.

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| WebsiteConfiguration | None | Stores the result of `GET Bucket website`. | Container |

**Content of `WebsiteConfiguration`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| IndexDocument | WebsiteConfiguration | Index document configuration | Container |
| RedirectAllRequestsTo | WebsiteConfiguration | Redirection configuration for all requests | Container |
| ErrorDocument | WebsiteConfiguration | Error document configuration | Container |
| RoutingRules | WebsiteConfiguration | Routing rule configuration | Container |

**Content of `IndexDocument`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Suffix | WebsiteConfiguration.IndexDocument | The object key suffix of index documents. For example, if this parameter is set to `index.html`, `index.html` will be automatically returned when you access the root directory of the bucket, and `article/index.html` will be returned when you access the `article/` directory. | string |

**Content of `RedirectAllRequestsTo`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Protocol | WebsiteConfiguration.RedirectAllRequestsTo | The target protocol to redirect all requests | string |

**Content of `ErrorDocument`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Key | WebsiteConfiguration.ErrorDocument | Object key of the general error document | string |

**Content of `RoutingRules`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| RoutingRule | WebsiteConfiguration.RoutingRules | A single routing rule | Container |

**Content of `RoutingRules.RoutingRule`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Condition | WebsiteConfiguration.RoutingRules.RoutingRule | Condition for the routing rule | Container |
| Redirect | WebsiteConfiguration.RoutingRules.RoutingRule | Configuration of the redirection target | Container |

**Content of `RoutingRules.RoutingRule.Condition`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| HttpErrorCodeReturnedEquals | WebsiteConfiguration.RoutingRules.<br>RoutingRule.Condition | The error code to match the routing rule | integer |
| KeyPrefixEquals | WebsiteConfiguration.RoutingRules.<br>RoutingRule.Condition | The object key prefix to match the routing rule | string |

**Content of `RoutingRules.RoutingRule.Redirect`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Protocol | WebsiteConfiguration.RoutingRules.<br>RoutingRule.Redirect | Target protocol for the routing rule | string |
| ReplaceKeyWith | WebsiteConfiguration.RoutingRules.<br>RoutingRule.Redirect | Target object key to replace the original object key in the request | string |
| ReplaceKeyPrefixWith | WebsiteConfiguration.RoutingRules.<br>RoutingRule.Redirect | Target object key prefix to replace the original object key prefix that is matched in the request | string |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

```plaintext
GET /?website HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 20 May 2020 09:33:49 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1589967229;1589974429&q-key-time=1589967229;1589974429&q-header-list=date;host&q-url-param-list=website&q-signature=50a22a30b02b59e5da4a0820d15a36805ea7****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1163
Connection: close
Date: Wed, 20 May 2020 09:33:49 GMT
Server: tencent-cos
x-cos-request-id: NWVjNGY5N2RfYTdjMjJhMDlfNjZkY18yYWUx****

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
