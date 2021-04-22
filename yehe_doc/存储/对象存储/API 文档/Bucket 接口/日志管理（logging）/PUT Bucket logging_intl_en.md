## API Description
This API is used to enable logging for a source bucket and store access logs in a specified destination bucket.

>!
>- Only the owner of the source bucket can make this request.
>- To enable logging, you need to grant Cloud Log Service (CLS) write permission for COS. For information on the authorization process, see [Enabling Log Management](https://intl.cloud.tencent.com/document/product/436/16920).

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

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body
This request uses a request body. An example request body with all nodes is as follows:
```shell
<BucketLoggingStatus>
  <LoggingEnabled>
    <TargetBucket>examplebucket-1250000000</TargetBucket>
    <TargetPrefix>prefix</TargetPrefix>
  </LoggingEnabled>
</BucketLoggingStatus>
```

The nodes are detailed as follows: <style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

|Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
| BucketLoggingStatus | None | Indicates the status of logging configuration. If there is no child node, logging is disabled | Container | Yes |

Container node `BucketLoggingStatus`:

|Node Name (Keyword) | Parent Node | Description | Type | Required  |
|:---|:-- |:--|:--|:--|
| LoggingEnabled | BucketLoggingStatus | Specifies the logging configuration, mainly for the destination bucket | Container | No |

Container node `LoggingEnabled`:

|Node Name (Keyword) | Parent Node | Description | Type | Required  |
|:---|:-- |:--|:--|:--|
| TargetBucket | LoggingEnabled | The destination bucket used to store logs; this can be the same bucket (not recommended) or a bucket in the same region under the same account | String | No |
| TargetPrefix | LoggingEnabled | The specified path in which logs are stored in the destination bucket | String | No |

>?After you specify the two nodes above, the generated log file name will take the format of `TargetBucket/TargetPrefix {YYYY}/{MM}/{DD}/{time}_{random}_{index}.gz`.

## Response

#### Response headers
This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body
The response body is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

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
