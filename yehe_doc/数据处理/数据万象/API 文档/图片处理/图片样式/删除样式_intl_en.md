## Overview
This API is used to delete a specified style.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=DeleteBucketStyle&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
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

```
DELETE /?style HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
<XML File>
```
>?Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request line

```
DELETE /?style HTTP/1.1
```
This API allows DELETE requests.

#### Request headers
#### Common request headers
This API uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Non-common request headers
This API does not use any non-common request header.

#### Request body
```
<?xml version="1.0" encoding="UTF-8" ?>
<DeleteStyle>
  <StyleName>string</StyleName>
</DeleteStyle>
```

## Response
#### Response headers
#### Common response headers
This API uses common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Non-common response headers
This API does not use any non-common response header.
#### Response body
The response body returned is empty.
  
