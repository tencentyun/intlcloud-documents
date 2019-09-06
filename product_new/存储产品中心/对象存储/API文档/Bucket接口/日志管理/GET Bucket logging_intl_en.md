## Description
This API (GET Bucket logging) is used to get the log configuration information of the source bucket.

>Only the source bucket owner can request this operation.

## Request

### Sample Request
```shell
GET /?logging HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Headers
#### Common Headers
The implementation of this request uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Non-common Header
This request operation has no special request headers.
### Request Body
The request body of this request is empty.

## Response

### Response Headers
#### Common Response Headers 
This response uses a common response header. For more information about the common response header, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Header
This response has no special response headers.
### Response Body
The return of this response body is **application/xml** data. Below is an example containing complete node data:
```shell
<BucketLoggingStatus>
  <LoggingEnabled>
    <TargetBucket>logs</TargetBucket>
    <TargetPrefix>logdir</TargetPrefix>
  </LoggingEnabled>
</BucketLoggingStatus>
```
The specific data content is as follows: <style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| BucketLoggingStatus | None | Bucket Log Status Information | Container |

Content of the Container node BucketLoggingStatus:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| LoggingEnabled | BucketLoggingStatus | Bucket Log Configuration Details | Container |

Content of the Container node LoggingEnabled:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| TargetBucket | LoggingEnabled | The destination bucket for storing logs, which can be the same bucket (not recommended) or a bucket in the same region under the same account | String |
| TargetPrefix | LoggingEnabled | Specified path to the destination bucket for storing logs | String |

## Use Cases

### Request
```shell
GET /?logging HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2017 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9&q-sign-time=1484815944;32557711944&q-key-time=1484815944;32557711944&q-header-list=host&q-url-param-list=accelerate&q-signature=a2d28e1b9023d09f9277982775a4b3b705d0e23e
```

### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 142
Connection: keep-alive
Date: Wed, 28 Oct 2017 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDdlNGZfNDYyMDRlXzM0YWFfZT==

<BucketLoggingStatus>
  <LoggingEnabled>
    <TargetBucket>logs</TargetBucket>
    <TargetPrefix>logdir</TargetPrefix>
  </LoggingEnabled>
</BucketLoggingStatus>
```
