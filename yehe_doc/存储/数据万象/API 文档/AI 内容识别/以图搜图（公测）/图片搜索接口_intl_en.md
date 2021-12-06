## Overview

This API is used to search for images.

## Request

#### Sample request

```plaintext
GET /<ObjectKey>?ci-process=ImageSearch&action=SearchImage&MatchThreshold=&Offset= HTTP/1.1
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

The nodes are described as follows:

| Node Name (Keyword)  | Description                                                         | Type   | Required |
| :----------------- | :----------------------------------------------------------- | :----- | :--- |
| MatchThreshold     | Only images scoring higher than the value of `MatchThreshold` will be returned. Default value: `0`  | Int    | No |
| Offset             | Starting number. Default value: `0`                                          | Int    | No |
| Limit              | Number of images to return. Default value: `10`. Maximum value: `100`                            | Int    | No  |
| Filter             | Uses image tags to filter images. You can use AND and OR to set multiple conditions (>, >=, <, <=, =, !=). | String | No |



#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body

This request does not have a request body.


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
	<Count>2</Count>
	<ImageInfos>
		<EntityId>apple</EntityId>
		<PicName>ObjectKey1</PicName>
		<Score>99</Score>
		<CustomContent>XXX</CustomContent>
		<Tags>{"key1":"value1","key2":"value2"}</Tags>
	</ImageInfos>
	<ImageInfos>
		<EntityId>apple</EntityId>
		<PicName>ObjectKey2</PicName>
		<Score>90</Score>
		<CustomContent>XXX</CustomContent>
		<Tags>{"key1":"value1","key2":"value2"}</Tags>
	</ImageInfos>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------- | :-------- |
| RequestId          | Response | Unique ID of the request | String    |
| Count              | Response | Number of images returned  | Int       |
| ImageInfos         | Response | Image information  | Container |

`ImageInfos` is an array. Each of its items includes the following nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :--------- | :------------------------- | :----- |
| EntityId           | ImageInfos | Entity ID                     | String |
| CustomContent      | ImageInfos | Custom content set for the image      | String |
| Tags               | ImageInfos | Custom tags. The value is a JSON string. | String |
| PicName            | ImageInfos | Image name       | String |
| Score              | ImageInfos | Similarity score           | Int    |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

```plaintext
GET /<ObjectKey>?ci-process=ImageSearch&action=SearchImage&MatchThreshold=10&Offset=2 HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558699190;1558706390&q-key-time=1558699190;1558706390&q-header-list=date;host&q-url-param-list=&q-signature=89fa1f6a56c34e460f3db4d65f928eaf034a****
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 150
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
	<Count>2</Count>
	<ImageInfos>
		<EntityId>apple</EntityId>
		<PicName>ObjectKey</PicName>
		<Score>99</Score>
		<CustomContent>XXX</CustomContent>
		<Tags>{"key1":"value1","key2":"value2"}</Tags>
	</ImageInfos>
	<ImageInfos>
		<EntityId>apple</EntityId>
		<PicName>ObjectKey2</PicName>
		<Score>90</Score>
		<CustomContent>XXX</CustomContent>
		<Tags>{"key1":"value1","key2":"value2"}</Tags>
	</ImageInfos>
</Response>
```
