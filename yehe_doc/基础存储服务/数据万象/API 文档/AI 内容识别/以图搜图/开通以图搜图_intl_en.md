## Overview

This API is used to enable the search by image feature for a bucket.

## Request

#### Sample request

```plaintext
POST /ImageSearchBucket HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request parameters

This API has no request parameter.


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request requires the following request body:

```plaintext
<Request>
	<MaxCapacity>10000</MaxCapacity>
	<MaxQps>10</MaxQps>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------- | :-------- | :--- |
| Request            | None     | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :------------------- | :--- | :--- |
| MaxCapacity        | Request | Maximum capacity of the image library  | Int  | Yes |
| MaxQps             | Request | Maximum QPS of the image library. Default value: `10` | Int  | No   |

>? The capacity of the image library cannot be modified after being set.


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

This response has no response body.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Request

```plaintext
POST /ImageSearchBucket HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558699190;1558706390&q-key-time=1558699190;1558706390&q-header-list=date;host&q-url-param-list=&q-signature=89fa1f6a56c34e460f3db4d65f928eaf034a****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 50
Content-Type: application/xml

<Request>
	<MaxCapacity>10000</MaxCapacity>
	<MaxQps>10</MaxQps>
</Request>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****
```
