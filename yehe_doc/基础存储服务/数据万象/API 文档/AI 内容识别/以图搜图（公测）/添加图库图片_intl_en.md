## Overview

This API is used to add an image to an image library.

## Request

#### Sample request

```plaintext
POST /<ObjectKey>?ci-process=ImageSearch&action=AddImage HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>

#### Request parameters

This API has no request parameter.


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request requires the following request body:

```plaintext
<Request>
	<EntityId>apple</EntityId>
	<CustomContent>myapple</CustomContent>
	<Tags>{"key1":"val1","key2":"val2"}</Tags>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------- | :-------- | :--- |
| Request            | None | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :----------------------------------------------------------- | :----- | :--- |
| EntityId           | Request | Entity ID, which can be up to 64 characters. If the `EntityId` already exists, this request adds the image to it. | String | Yes |
| CustomContent      | Request | Custom content, which can be up to 4,096 characters. The content set will be returned when the image is queried.  | String | No  |
| Tags               | Request | Custom tags. The value is a JSON string containing up to 10 key:value pairs. | String | No   |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

This response has no response body.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

```plaintext
POST /<ObjectKey>?ci-process=ImageSearch&action=AddImage HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558699190;1558706390&q-key-time=1558699190;1558706390&q-header-list=date;host&q-url-param-list=&q-signature=89fa1f6a56c34e460f3db4d65f928eaf034a****
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Content-Length: 100
Content-Type: application/xml

<Request>
	<EntityId>apple</EntityId>
	<CustomContent>myapple</CustomContent>
	<Tags>{"key1":"val1","key2":"val2"}</Tags>
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
