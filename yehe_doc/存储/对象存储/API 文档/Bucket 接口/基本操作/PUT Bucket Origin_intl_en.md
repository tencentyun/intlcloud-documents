## Overview

This API is used to set origin-pull for a bucket.

## Request

### Request sample

```http
PUT /?origin HTTP 1.1
Host:<BucketName-APPID>.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

>
>- Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information.)
>- This request should be used with a request body.

### Request headers

#### Common headers

The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special headers

There are no special request headers.

### Request body

The request body of this API request is an origin-pull rule.

```plaintext
<?xml version="1.0" encoding="UTF-8"?>
<OriginConfiguration>
  <OriginRule>
    <OriginType>Redirect</OriginType>
    <OriginInfo>
      <Protocol>HTTP</Protocol>
      <HostName>examplebucket.test.xyz</HostName>
    </OriginInfo>
    <HttpRedirectCode>302</HttpRedirectCode>
  </OriginRule>
</OriginConfiguration>
```

The data are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :------------------ | :----- | :-------------- | :-------- | :--- |
| OriginConfiguration | None     | Origin-pull Configuration | Container | Yes   |

Container node `OriginConfiguration`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------------ | :------------------ | :-------- | :--- |
| OriginRule         | OriginConfiguration | Supports only one OriginRule | Container | Yes   |

Container node `OriginRule`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------- | :----------------------------------------------- | :-------- | :--- |
| OriginType         | OriginConfiguration.OriginRule | Sets origin-pull type. Enumerated value: Redirect                        | Container | Yes   |
| Prefix             | OriginConfiguration.OriginRule | The directory on which the origin-pull acts. Default: root directory; if set, it cannot be null. | String    | No   |
| OriginInfo         | OriginConfiguration.OriginRule | Origin-pull address information                                 | Container | Yes   |
| HttpRedirectCode   | OriginConfiguration.OriginRule | Return code for request redirects; only supports 302 currently.              | String    | No   |

Container node `OriginInfo`:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>Protocol</td>
      <td>OriginConfiguration.OriginRule.OriginInfo</td>
      <td>Origin-pull protocol; only supports HTTP currently.</td>
      <td>String</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>HostName</td>
      <td>OriginConfiguration.OriginRule.OriginInfo</td>
			<td>Origin-pull address. Just enter your domain name or IP address, and no prefix <code>http://</code>, or alternatively, enter your port number using the format <code>:[port]</code>, where <code>:</code> is the English symbol, and no private IP is valid.</td>
      <td>String</td>
      <td>Yes</td>
   </tr>
</table>

## Response

### Response headers

#### Common response headers

This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special response headers

This response has no special response headers.

### Response body

The response body is empty.

### Error codes

| Error/Return Code | Description | HTTP Status Code |
| --------------------- | -------------------------------------- | --------------- |
| InvalidArgument | Invalid provided parameter | 400 Bad Request |
| SignatureDoesNotMatch | Returned if you provide an invalid signature     | 403 Forbidden |
| NoSuchKey             | Returned if the bucket does not exist | 404 Not Found   |

## Use Case

### Request

```plaintext
PUT /?origin= HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Authorization:q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484639384;32557535384&q-key-time=1484639384;32557535384&q-header-list=host&q-url-param-list=&q-signature=5c07b7c67d56497d9aacb1adc19963135b7d00dc
Content-Length: 347

<?xml version="1.0" encoding="UTF-8"?>
<OriginConfiguration>
  <OriginRule>
    <OriginType>Redirect</OriginType>
    <OriginInfo>
      <Protocol>HTTP</Protocol>
      <HostName>examplebucket.test.xyz</HostName>
    </OriginInfo>
    <HttpRedirectCode>302</HttpRedirectCode>
  </OriginRule>
</OriginConfiguration>
```

### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Sun, 28 Apr 2019 12:02:25 GMT
Server: tencent-cos
x-cos-request-id: NWNjNTk2NTFfMmM4OGY3MGFfNTI1X2Y2NmU=
```