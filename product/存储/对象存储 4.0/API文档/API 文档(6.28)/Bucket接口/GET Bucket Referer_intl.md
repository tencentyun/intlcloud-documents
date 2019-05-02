## Description

This API (GET Bucket Referer) is used to read the whitelist or the blacklist of Bucket Referer.

## Request

### Request example

```HTTP
GET /?referer HTTP 1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (For more information, see [Request Signature](https://cloud.tencent.com/document/product/436/7778)).

### Request headers

#### Common headers

Common request headers are used for the implementation of this request operation. For more information, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

#### Special request headers

This request operation does not use any special request header.

### Request body

The request body of this request is empty.

## Response

### Response headers

#### Common response headers

This response uses common response headers. For more information, see [Common Response Headers](https://cloud.tencent.com/document/product/436/7729).

#### Special response headers

This response does not use any special response header.

### Response body

Application/xml data is returned in the response body. It contains the complete node data, as shown below:

```shell
<RefererConfiguration>
  <Status></Status>
  <RefererType></RefererType>
  <DomainList>
    <Domain></Domain>
    <Domain></Domain>
  </DomainList>
  <EmptyReferConfiguration></EmptyReferConfiguration>
</RefererConfiguration>
```

Detailed data is shown as below:

| Name | Parent Node | Description | Type | Required |
| ----------------------- | -------------------- | ------------------------------------------------------------ | --------- | ---- |
| RefererConfiguration | None | Hotlink protection configuration | Container | Yes |
| Status | RefererConfiguration | Indicates whether to enable hotlink protection. Enumerated value: Enabled and Disabled | String | Yes |
| RefererType | RefererConfiguration | Hotlink protection type. Enumerated value: Black-List and White-List | String | Yes |
| DomainList | RefererConfiguration | Sets a list of domain names used in the blacklist/whitelist. You can configure multiple domain names by using prefix match. Domain names and IPs with ports are supported. Wildcard "*" is supported for second-level and third-level domain names. | Container | Yes |
| Domain | DomainList | Sets a single domain name used in the blacklist/whitelist, such as `www.qq.com/example`, `192.168.1.2:8080`, and `*.qq.com`. | String | Yes |
| EmptyReferConfiguration | RefererConfiguration | Indicates whether an access request without Referer is allowed. Enumerated value: Allow and Deny. It defaults to Deny. | String | No |

### Error codes

No special error message is returned for this request operation. For common error messages, see [Error Codes](https://cloud.tencent.com/document/product/436/7730).

## Example

### Request

```shell
GET /?referer HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 25 Feb 2017 04:10:22 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1547105134;32526689134&q-key-time=1547105134;32620001134&q-header-list=content-md5;content-type;host&q-url-param-list=referer&q-signature=0f7fef5b1d2180deaf6f92fa2ee0cf87ae83f0cd
```

### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 260
Connection: keep-alive
Date: Fri, 25 Feb 2017 04:10:22 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhfMjIw

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

