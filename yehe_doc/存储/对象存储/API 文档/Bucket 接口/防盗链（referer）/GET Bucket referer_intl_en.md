## Description

This API is used to read a whitelist or blacklist of bucket referers.

## Request

#### Sample request

```HTTP
GET /?referer HTTP 1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).


#### Request headers
This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers
This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

This response body returns `application/xml` data. The following example contains all the node data:

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

The nodes are described in details below:

| Node Name | Parent Node | Description | Type | Required |
| ----------------------- | -------------------- | ------------------------------------------------------------ | --------- | ---- |
| RefererConfiguration | None | Hotlink protection configuration information | Container | Yes |
| Status | RefererConfiguration | Indicates whether to enable hotlink protection. Enumerated value: Enabled and Disabled | String | Yes |
| RefererType | RefererConfiguration | Hotlink protection type. Enumerated value: Black-List and White-List | String | Yes |
| DomainList | RefererConfiguration | Sets a list of domain names used in the blacklist/whitelist. You can configure multiple domain names by using prefix match. Domain names and IPs with ports are supported. Wildcard `*` is supported for second-level and third-level domain names. | Container | Yes |
| Domain | DomainList | A single applicable domain name, such as `www.qq.com/example`, `192.168.1.2:8080`, or `*.qq.com` | String | Yes |
| EmptyReferConfiguration | RefererConfiguration | Indicates whether to allow access with empty Referer. Enumerated values: Allow, Deny. Default value: Deny | String | No |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

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
