## Feature Description

This API (GET Bucket referer) is used to read the referer whitelist or blacklist of a bucket.

## Request

#### Sample request

```HTTP
GET /?referer HTTP 1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Note:
>
> Authorization: Auth String (for more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request header

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response header

This API only returns common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

application/xml data is returned in the response body, which contains the complete node data as shown below:

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

Detailed data is as shown below:

| Name | Parent Node | Description | Type | Required |
| :---------------------- | :------------------- | :----------------------------------------------------------- | :-------- | :--- |
| RefererConfiguration | None | Hotlink protection configuration information | Container | Yes |
| Status | RefererConfiguration | Whether to enable hotlink protection. Enumerated values: Eabled, Disabled | String | Yes |
| RefererType | RefererConfiguration | Hotlink protection type. Enumerated values: Black-List, White-List | String | Yes |
| DomainList | RefererConfiguration | List of applicable domain names. Supports multiple domain names and prefix matching. Supports domain names and IPs with ports. Supports wildcards `*`. Creates second-level or multi-level domain name wildcards | Container | Yes |
| Domain | DomainList | Single applicable domain name, such as `www.qq.com/example`, `192.168.1.2:8080`, or `*.qq.com` | String | Yes |
| EmptyReferConfiguration | RefererConfiguration | Whether to allow empty Referer access. Enumerated values: Allow, Deny. Default value: Deny | String | No |

#### Error codes

There are no specific error messages for this request operation. For common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use Case

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