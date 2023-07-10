## Overview
This API is used to query the logging configuration of a source bucket.

>!Only the owner of the source bucket has permission to call this API.

## Request

#### Sample request
```shell
GET /?logging HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body
The request body of this request is empty.

## Response

#### Response headers

This API only uses [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body
The response body returns **application/xml** data. The following contains all the nodes:
```shell
<BucketLoggingStatus>
  <LoggingEnabled>
    <TargetBucket>examplebucket-1250000000</TargetBucket>
    <TargetPrefix>prefix</TargetPrefix>
  </LoggingEnabled>
</BucketLoggingStatus>
```
The nodes are as follows: <style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| BucketLoggingStatus | None | Logging status of the bucket | Container |

Content of `BucketLoggingStatus`:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| LoggingEnabled | BucketLoggingStatus | Detailed configuration of bucket logging |  Container |

Content of `LoggingEnabled`:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| TargetBucket | LoggingEnabled | Destination bucket that stores logs. It can be a bucket under the same account or in the same region as the source bucket, or the source bucket itself (not recommended). | String |
| TargetPrefix | LoggingEnabled | Path in the destination bucket that stores logs |  String |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

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
