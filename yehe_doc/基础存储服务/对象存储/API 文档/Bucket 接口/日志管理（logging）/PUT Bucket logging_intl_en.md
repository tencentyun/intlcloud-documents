## Overview
This API is used to enable logging for a source bucket and store access logs in a specified destination bucket.

>!
> Only the owner of the source bucket has permission to call this API.
> To enable logging, you need to grant Cloud Log Service (CLS) permission to write to COS. For detailed directions, please see [Enabling Log Management](https://intl.cloud.tencent.com/document/product/436/16920).

## Request

#### Sample request
```shell
PUT /?logging HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date:date
Content-Length: length
Content-Type: application/xml
Content-MD5: MD5
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body
This request requires a request body. A request body with all nodes is as follows:
```shell
<BucketLoggingStatus>
  <LoggingEnabled>
    <TargetBucket>examplebucket-1250000000</TargetBucket>
    <TargetPrefix>prefix</TargetPrefix>
  </LoggingEnabled>
</BucketLoggingStatus>
```

The nodes are as follows: <style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
| BucketLoggingStatus | None | Logging status. If there is no child node information, logging is disabled. | Container | Yes |

Content of `BucketLoggingStatus`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
| LoggingEnabled | BucketLoggingStatus | Specific logging configuration, mainly for the destination bucket | Container | No |

Content of `LoggingEnabled`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
| TargetBucket | LoggingEnabled | Destination bucket to store logs. It can be a bucket under the same account or in the same region as the source bucket, or the source bucket itself (not recommended). | String | No |
| TargetPrefix | LoggingEnabled | Path in the destination bucket used to store logs |  String | No |

>?After you specify the two nodes above, names of the generated logs will be in the format of `TargetBucket/TargetPrefix{YYYY}/{MM}/{DD}/{time}_{random}_{index}.gz`.

## Response

#### Response headers
This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body
The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Example

#### Request
```shell
PUT /?logging HTTP 1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2017 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484814927;32557710927&q-key-time=1484814927;32557710927&q-header-list=host&q-url-param-list=accelerate&q-signature=8b9f05dabce2578f3a79d732386e7cbade90****
Content-Type: application/xml
Content-Length: 147

<BucketLoggingStatus>
  <LoggingEnabled>
    <TargetBucket>examplebucket-1250000000</TargetBucket>
    <TargetPrefix>prefix</TargetPrefix>
  </LoggingEnabled>
</BucketLoggingStatus>
```

#### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 10 Mar 2017 09:45:46 GMT
Server: tencent-cos
x-cos-request-id: NTg4MDdiZWRfOWExZjRlXzQ2OWVf****
```
