## Description

The PUT Bucket referer API is used to set Referer-based whitelist or blacklist for a bucket.

## Request

### Sample Request

```shell
PUT /?referer HTTP 1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date:GMT Date
Authorization: Auth String
Content-Length:length
Content-MD5:MD5
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information). 

### Request Headers

#### Common Headers

The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

**Required headers**

<table>
   <tr>
      <th>Name</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td nowrap="nowrap">Content-Length</td>
      <td>HTTP request length in bytes as defined in RFC 2616</td>
      <td>String</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Content-MD5</td>
      <td>Base64-encoded 128-bit content MD5 checksum as defined in RFC 1864. This header is used to check whether the file content has changed</td>
      <td>String</td>
      <td>Yes</td>
   </tr>
</table>

This request operation has no special request headers.

### Request Body

The specific node content of this request body is:

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

The content is described in details below:

| Name | Parent Node | Description | Type | Required |
| ----------------------- | -------------------- | ------------------------------------------------------------ | --------- | ---- |
| RefererConfiguration | None | Hotlink protection configuration Information | Container | Yes |
| Status | RefererConfiguration | Whether to enable hotlink protection; enumerated values: Eabled, Disabled | String | Yes |
| RefererType | RefererConfiguration | Hotlink protection type; enumerated values: Black-List, White-List | String | Yes |
| DomainList | RefererConfiguration | List of applicable domain names. Multiple domain names are supported and matching is based on prefix. Domain names and IPs with ports are supported. Wildcard `*` is supported for matching all second-level or lower-level domain names | Container | Yes |
| Domain | DomainList | Single applicable domain name, such as `www.qq.com/example`, `192.168.1.2:8080`, or `*.qq.com` | String | Yes |
| EmptyReferConfiguration | RefererConfiguration | Whether to allow empty Refer to access; enumerated values: Allow, Deny; default value: Deny | String | No |


## Response

### Response Headers

#### Common Response Headers

This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers

This response has no special response headers.

### Response Body

This response body is empty.

### Error Codes

There are no special error messages for this request operations. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

### Request

```shell
PUT /?referer HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 25 Feb 2017 04:10:22 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1547105134;32526689134&q-key-time=1547105134;32620001134&q-header-list=content-md5;content-type;host&q-url-param-list=referer&q-signature=0f7fef5b1d2180deaf6f92fa2ee0cf87ae83f0cd\
Content-MD5: kOz7g54LMJZjxKs070V9jQ==
Content-Type: application/xml

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

### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: keep-alive
Date: Fri, 25 Feb 2017 04:10:22 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhfMjIw
```
