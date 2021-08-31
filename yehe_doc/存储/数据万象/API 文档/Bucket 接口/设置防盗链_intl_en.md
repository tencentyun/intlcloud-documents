## Feature

This API is used to add hotlink protection (set blacklist/whitelist) for a bucket.

## Request
#### Request example

```shell
PUT /?hotlink HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

#### Request headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body

The node content of this request body is as follows:

```shell
<Hotlink>
        <Url>xxxxx</Url>
        <Type>black</Type>
</Hotlink>>
```

The content is described in details below:

| Node Name | Parent Node | Description | Type | Required |
| :--- | :------ | :------------------------------------------------------- | :-------- | :--- |
| Url | Hotlink | Indicates the domain name address. | Container | Yes |
| Type | Hotlink | Indicates the hotlink protection type. The value white indicates whitelist, the value black indicates blacklist, and the value off indicates the hotlink protection is disabled. | String | Yes |

## Response
#### Response headers
This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body
The response body of this response is empty.

## Use Cases

#### Request

```shell
PUT /?hotlink HTTP/1.1
Host: examplebucket-1250000000.pic.ap-chengdu.myqcloud.com
Date: Wed, 18 Mar 2000 06:57:54 GMT
Authorization: XXXXXXXXXXXX

<Hotlink>
        <Url>www.example.com</Url>
        <Type>black</Type>
</Hotlink>
```

#### Response



```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: keep-alive
Date: Fri, 25 Feb 2017 04:10:22 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjFjMmJfOWIxZjRlXzZmNDhf****
```
