## Description
This API (PUT Bucket Logging) is used to enable logging for the source bucket and store its access logs in the specified destination bucket.

>Only the source bucket owner can request this operation.

## Request

### Sample Request
```shell
PUT /?logging HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date:date
Content-Length: length
Content-Type: application/xml
Content-MD5: MD5
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).


### Request Headers
#### Common Headers

The implementation of this request operation requires the use of the Content-MD5 header to verify the integrity of the message, as shown below. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name | Description | Type | Required |
|:---|:-- |:--|:--|
| Content-MD5 | Base64-encoded 128-bit content MD5 checksum as defined in RFC 1864. This header is used to check whether the file content has changed | String | Yes |

### Request Body
The implementation of this request operation requires a request body. An example of the content of a request body with all nodes is as follows:
```shell
<BucketLoggingStatus>
  <LoggingEnabled>
    <TargetBucket>logbucket</TargetBucket>
    <TargetPrefix>mylogs</TargetPrefix>
  </LoggingEnabled>
</BucketLoggingStatus>
```

The specific data descriptions are as follows: <style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
| BucketLoggingStatus | None | Indicates the status of the logging configuration. If there is no child node information, logging is disabled | Container | Yes |

Content of the Container node BucketLoggingStatus:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
| LoggingEnabled | BucketLoggingStatus | Specific information of the bucket logging setting, which is mainly the destination bucket | Container | No |

Content of the Container node LoggingEnabled:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
| TargetBucket | LoggingEnabled | Destination bucket for storing logs | String | No |
| TargetPrefix | LoggingEnabled | Logs are stored in the specified path in the destination bucket | String | No |

## Response

### Response Headers
#### Common Response Headers
This response uses a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response has no special response headers.

### Response Body
The response body return is empty.

## Use Cases

### Request
```shell
PUT /?logging HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2017 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfABC&q-sign-time=1484814927;32557710927&q-key-time=1484814927;32557710927&q-header-list=host&q-url-param-list=accelerate&q-signature=8b9f05dabce2578f3a79d732386e7cbade9033e3
Content-Type: application/xml
Content-Length: 147

<BucketLoggingStatus>
  <LoggingEnabled>
    <TargetBucket>logbucket</TargetBucket>
    <TargetPrefix>mylogs</TargetPrefix>
  </LoggingEnabled>
</BucketLoggingStatus>
```

### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 10 Mar 2017 09:45:46 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDdiZWRfOWExZjRlXzQ2OWVfZG==
```
