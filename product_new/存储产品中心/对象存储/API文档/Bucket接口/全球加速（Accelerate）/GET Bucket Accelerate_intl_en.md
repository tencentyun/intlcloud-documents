## Feature description

This API (GET Bucket Accelerate) is used to query the global acceleration configuration of the specified bucket.

**Detail analysis**

1. If you have never enabled global acceleration for the bucket, the request to the GET Bucket Accelerate API will not return global acceleration configuration status.
2. Valid return values of the global acceleration configuration status are `Enabled` and `Suspended`, indicating that global acceleration is enabled or suspended, respectively.
3. If you are using a sub-account, in order to query the global acceleration configuration information of the bucket, you should have permission to read the configuration.

## Request

#### Sample request

```shell
GET /?accelerate HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Authorization: Auth String
```

> Authorization: Auth String (for more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request header

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response header

This API only returns common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729). 

#### Response body

```shell
<AccelerateConfiguration xmlns="cos xmlns/"> 
  <Status>Enabled</Status> 
  <Type>COS</Type>
</AccelerateConfiguration>
```

Detailed data is as shown below:

| Node Name (Keyword)      | Parent Node                  | Description                                                 | Type      |
| ----------------------- | ----------------------- | ---------------------------------------------------- | --------- |
| AccelerateConfiguration | None                      | Detailed information of global acceleration                                   | Container |
| Status                  | AccelerateConfiguration | Indicates whether global acceleration is enabled. Enumerated values: Suspended, Enabled | Enum      |
| Type                    | AccelerateConfiguration | Global acceleration type. Enumerated value: COS  | Enum      |

#### Error codes

There are no special error messages for this API. For all error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use cases

#### Request

```shell
GET /?accelerate HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Connection: keep-alive
Authorization: authorization string
Content-Type: text/plain
```

#### Response 1 (global acceleration enabled)

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 73
Connection: keep-alive
Date: Wed, 23 Aug 2019 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0ZThm

<AccelerateConfiguration>
  <Status>Enabled</Status>
  <Type>COS</Type>
</AccelerateConfiguration>
```

#### Response 2 (global acceleration suspended)

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 73
Connection: keep-alive
Date: Wed, 23 Aug 2019 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0ZThm

<AccelerateConfiguration>
  <Status>Disabled</Status>
  <Type>COS</Type>
</AccelerateConfiguration>
```

#### Response 3 (global acceleration not enabled)

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 73
Connection: keep-alive
Date: Wed, 23 Aug 2019 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0ZThm

<AccelerateConfiguration/>
```
