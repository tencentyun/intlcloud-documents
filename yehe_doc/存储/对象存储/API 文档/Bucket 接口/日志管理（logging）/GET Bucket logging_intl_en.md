## Description
This API is used to get the logging configuration of a bucket.

>!Only the bucket owner can make this request.

## Request

#### Sample request
```shell
GET /?logging HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body
The request body of this request is empty.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body
This response body returns **application/xml** data. The following example contains all the node data:
```shell
<BucketLoggingStatus>
  <LoggingEnabled>
    <TargetBucket>examplebucket-1250000000</TargetBucket>
    <TargetPrefix>prefix</TargetPrefix>
  </LoggingEnabled>
</BucketLoggingStatus>
```
The nodes are detailed as follows:<style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| BucketLoggingStatus | None | Bucket logging status | Container |

Container node `BucketLoggingStatus`:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| LoggingEnabled | BucketLoggingStatus | Bucket logging configuration details | Container |

Container node `LoggingEnabled`:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| TargetBucket | LoggingEnabled | The destination bucket for storing logs, which can be the same as the source bucket (not recommended), or a bucket in the same region or under the same account | String |
| TargetPrefix | LoggingEnabled | The specified path in which logs are stored in the destination bucket | String |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request
```shell
GET /?logging HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 28 Oct 2017 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5O****&q-sign-time=1484815944;32557711944&q-key-time=1484815944;32557711944&q-header-list=host&q-url-param-list=accelerate&q-signature=a2d28e1b9023d09f9277982775a4b3b705d0****
```

#### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 142
Connection: keep-alive
Date: Wed, 28 Oct 2017 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDdlNGZfNDYyMDRlXzM0YWFf****

<BucketLoggingStatus>
  <LoggingEnabled>
    <TargetBucket>examplebucket-1250000000</TargetBucket>
    <TargetPrefix>prefix</TargetPrefix>
  </LoggingEnabled>
</BucketLoggingStatus>
```
