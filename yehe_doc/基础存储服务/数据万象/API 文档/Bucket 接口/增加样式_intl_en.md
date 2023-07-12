## Description
This API adds a style to a bucket. All images uploaded to the bucket afterwards use the style.

> Bucket APIs are rate limited. Write requests are limited to 1 qps while read requests are limited to 10 qps.

## Request
#### Sample requests
```plaintext
PUT /?style HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
<XML File>
```

> Authorization: Auth String (For details, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)


#### Request header

This API uses only common request headers. For details, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<AddStyle>
  <StyleName>string</StyleName>
  <StyleBody>string</StyleBody>
</AddStyle>
```

Detail node descriptions are as follows:

| Node name (keyword) | Parent node | Description | Type | Required |
| ------------------ | ------ | ---------------- | --------- | -------- |
| AddStyle | None | The style to add | Container | Yes |


Description of container node AddStyle:

| Node name (keyword) | Parent node | Description | Type | Required |
| ------------------ | -------- | -------- | ------ | -------- |
| StyleName | AddStyle | Name of the style | string | Yes |
| StyleBody | AddStyle | Style content | string | Yes |


## Response

#### Response header
This response uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body
The response body is null.

#### Error codes
This API do not have any special error code. For information on all error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Example

#### Request
```plaintext
PUT /?style HTTP/1.1
Host: examplebucket-1250000000.pic.ap-chengdu.myqcloud.com
Date: Tue, 03 Apr 2019 09:06:15 GMT
Authorization:XXXXXXXXXXXX

<?xml version="1.0" encoding="UTF-8" ?>
<AddStyle>
  <StyleName>style_name</StyleName>
  <StyleBody>imageMogr2/thumbnail/!50px</StyleBody>
</AddStyle>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Tue, 03 Apr 2019 09:06:16 GMT
x-cos-request-id: xxxxxxxxxxxxxxxxxx
```
