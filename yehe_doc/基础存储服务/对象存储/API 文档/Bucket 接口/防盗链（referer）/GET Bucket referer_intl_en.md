## Overview

This API is used to read the referer allowlist/blocklist of a bucket.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetBucketReferer&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
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

```HTTP
GET /?referer HTTP 1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com`, &lt;BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 


#### Request headers
This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers
This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

This response body returns `application/xml` data. The following contains all the nodes:

```shell
<RefererConfiguration>
	<Status>Enabled</Status>
	<RefererType>White-List</RefererType>
	<DomainList>
		<Domain>*.qq.com</Domain>
		<Domain>*.qcloud.com</Domain>
	</DomainList>
	<EmptyReferConfiguration>Allow</EmptyReferConfiguration>
</RefererConfiguration>
```

The nodes are described as follows:

| Node Name | Parent Node | Description | Type | Required |
| ----------------------- | -------------------- | ------------------------------------------------------------ | --------- | ---- |
| RefererConfiguration | None | Hotlink protection configuration | Container | Yes |
| Status | RefererConfiguration | Whether hotlink protection is enabled. Enumerated values: `Enabled`, `Disabled` | String | Yes |
| RefererType | RefererConfiguration | Hotlink protection type. Enumerated values: `Black-List`, `White-List` | String | Yes |
| DomainList | RefererConfiguration | A list of domain names in the blocklist/allowlist. Using a prefix to specify multiple domains is supported. Domain names and IPs with ports are supported. A wildcard (*) is supported for second-level or multi-level domains. | Container | Yes |
| Domain | DomainList | A single domain in the blocklist/allowlist, such as `www.qq.com/example`, `192.168.1.2:8080`, or `*.qq.com` | String | Yes |
| EmptyReferConfiguration | RefererConfiguration | Whether accessing with an empty referer is allowed. Enumerated values: `Allow`, `Deny` (default) | String | No |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

```shell
GET /?referer HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 25 Feb 2017 04:10:22 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1547105134;32526689134&q-key-time=1547105134;32620001134&q-header-list=content-md5;content-type;host&q-url-param-list=referer&q-signature=0f7fef5b1d2180deaf6f92fa2ee0cf87ae83****
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 260
Connection: keep-alive
Date: Fri, 25 Feb 2017 04:10:22 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhf****

<RefererConfiguration>
	<Status>Enabled</Status>
	<RefererType>White-List</RefererType>
	<DomainList>
		<Domain>*.qq.com</Domain>
		<Domain>*.qcloud.com</Domain>
	</DomainList>
	<EmptyReferConfiguration>Allow</EmptyReferConfiguration>
</RefererConfiguration>
```
