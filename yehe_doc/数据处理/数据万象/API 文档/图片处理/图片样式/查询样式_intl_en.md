## Overview
This API is used to query the styles set for a bucket. If the request body is not used, all styles set for the bucket will be queried. If the request body is used, only styles carried in the request body will be queried.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=QueryBucketStyle&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
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
GET /?style HTTP/1.1
Host: <BucketName-APPID>.pic.<Region>.myqcloud.com 
Date: GMT Date
Authorization: Auth String
```
>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request line

```
GET /?style HTTP/1.1
```

This API allows GET requests.

#### Request headers
#### Common request headers
This API uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Non-common request headers
This request does not use any non-common request header.

#### Request body

```
<?xml version="1.0" encoding="UTF-8" ?>
<GetStyle>
  <StyleName>string</StyleName>
</GetStyle>
```

## Response
#### Response headers
#### Common response headers
This API uses common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Non-common response headers
This API does not use any non-common response header.

#### Response body

```
<StyleList>
  <StyleRule>
  <StyleName>string</StyleName>
  <StyleBody>string</StyleBody>
</StyleRule>
  <StyleRule>
  <StyleName>string</StyleName>
  <StyleBody>string</StyleBody>
</StyleRule>
</StyleList>
```
  
