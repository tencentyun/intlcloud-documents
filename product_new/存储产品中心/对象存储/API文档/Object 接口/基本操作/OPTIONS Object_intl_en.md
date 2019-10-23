## Description
This API (OPTIONS Object) is used to implement a pre-request for an cross-origin object access configuration, i.e., an OPTIONS request carrying the specific source origin, HTTP method, and header information is sent to COS for it to determine whether a real cross-origin resource sharing (CORS) request can be made. If no CORS configuration exists, 403 Forbidden will be returned for the request. You can enable the CORS support of a bucket using the PUT Bucket cors API.

## Request
### Sample Request

```
OPTIONS /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Origin: Origin
Access-Control-Request-Method: HTTPMethod
Access-Control-Request-Headers: RequestHeader
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Headers
#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

Name | Type | Description | Required
---|---|---|---
Origin|string| Origin domain name of the simulated cross-origin access request | Yes
Access-Control-Request-Method|string| HTTP method of the simulated cross-origin access request | Yes
Access-Control-Request-Headers|string| Headers of the simulated cross-origin access request | No

### Request Body
The request body of this request is empty.

## Response
### Response Headers
#### Common Response Headers
This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers

Response headers unique to this request operation include:

| Name | Type | Description |
|---|---|---|
|Access-Control-Allow-Origin|string| Origin domain names of the simulated cross-origin access request. This header will not be returned if the origin is not allowed | String |
|Access-Control-Allow-Methods|string| HTTP methods of the simulated cross-origin access request. This header will not be returned if the request method is not allowed |
|Access-Control-Allow-Headers|string| Headers of the simulated cross-origin access request. This request header will not be returned if no simulated headers are allowed |
|Access-Control-Expose-Headers|string| HTTP methods of the simulated cross-origin access request. This header will not be returned if the request method is not allowed |
|Access-Control-Max-Age|string| Sets the validity period of the result of the OPTIONS request |

### Response Body
This response body is empty.

## Samples

### Request

```
OPTIONS /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 12 Jan 2017 17:26:53 GMT
Origin: http://www.qq.com
Access-Control-Request-Method: PUT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDDNMEycgLRPI2axw9xa2Hhx87wZ3MqQCn&q-sign-time=1487070734;32466654734&q-key-time=1487070734;32559966734&q-header-list=host&q-url-param-list=&q-signature=2ac3ada19910f44836ae0df72a0ec1003f34324b
```

### Response

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 16087
Connection: keep-alive
x-cos-request-id: NTg3NzRiZGRfYmRjMzVfM2Y2OF81N2YzNA==
Date: Thu, 12 Jan 2017 17:26:53 GMT
ETag: \"9a4802d5c99dafe1c04da0a8e7e166bf\"
Access-Control-Allow-Origin: http://www.qq.com
Access-Control-Allow-Methods: PUT
Access-Control-Expose-Headers: x-cos-request-id
Server: tencent-cos
```
