## Description
This API is used to set styles for a bucket. All images uploaded to the bucket later will be added with the specified styles.

>Bucket APIs are subject to frequency control restrictions: up to 1 write request per minute and up to 20 read requests per minute.

## Request
#### Request sample
```plaintext
PUT /?style HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
<XML File>
```

> Authorization: Auth String. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).


#### Request header

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<AddStyle>
  <StyleName>string</StyleName>
  <StyleBody>string</StyleBody>
</AddStyle>
```

The node is described as below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | ---------------- | --------- | -------- |
| AddStyle | None | Information about the style to add | Container | Yes |


Content of container node AddStyle:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | -------- | -------- | ------ | -------- |
| StyleName | AddStyle | Style name | string | Yes |
| StyleBody | AddStyle | Style details | string | Yes |


## Response

#### Response header
This API only uses common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body
Null is returned for the response body.

#### Error codes
This API does not have special error codes. See [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700) for a complete list of error codes.

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
