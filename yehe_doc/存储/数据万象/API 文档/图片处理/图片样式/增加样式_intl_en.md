## Overview
This API is used to set a style for a bucket to process images in the same way.

>? Currently, the QPS for bucket writes is limited to 1, and bucket reads to 10.
>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=AddBucketStyle&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>


## Request
#### Sample request
```plaintext
PUT /?style HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
<XML File>
```

>? Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)


#### Request headers

This API uses only common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<AddStyle>
    <StyleName>string</StyleName>
    <StyleBody>string</StyleBody>
</AddStyle>
```

Nodes are described as follows:

| Node Name (Keyword)          | Parent Node | Description                                    | Type        | Required |
| ------------------ | ------ | ---------------- | --------- | -------- |
| AddStyle           | None  | The style to be added | Container | Yes  |


Content of `AddStyle`:

| Node Name (Keyword)          | Parent Node | Description                                    | Type        | Required |
| ------------------ | -------- | -------- | ------ | -------- |
| StyleName   | AddStyle | Style name | string | Yes |
| StyleBody   | AddStyle | Style details | string | Yes |


## Response

#### Response headers
This API uses only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body
The response body returned is empty.

#### Error codes
This API does not have any special error codes. For more information about all error codes, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

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
