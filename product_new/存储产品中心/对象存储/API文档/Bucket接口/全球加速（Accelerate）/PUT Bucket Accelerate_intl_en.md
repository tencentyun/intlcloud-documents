## Feature description

This API (PUT Bucket Accelerate) is used to enable or suspend global acceleration for the specified bucket.

**Detail analysis**

1. If you have never enabled global acceleration for the bucket, the request to the GET Bucket Accelerate API will not return global acceleration configuration status.
2. Once enabled, global acceleration can only be suspended but cannot be disabled.
3. Valid values of the global acceleration configuration status are `Enabled` and `Suspended`, indicating that global acceleration is enabled or suspended, respectively.
4. If you are using a sub-account, in order to set the global acceleration feature for the bucket, you should have permission to write the configuration.

## Request

#### Sample request

```shell
PUT /?accelerate HTTP 1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Authorization: Auth String
```

> Authorization: Auth String (for more information, please see [Request Signature](https://cloud.tencent.com/document/product/436/7778)).

#### Request header

This API only uses common request headers. For more information, please see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

#### Request body

```shell
<AccelerateConfiguration xmlns="cos xmlns/"> 
  <Status>Enabled</Status> 
</AccelerateConfiguration>
```

Detailed data is as shown below:

| Node Name (Keyword)      | Parent Node                  | Description                                                 | Type      |
| ----------------------- | ----------------------- | ---------------------------------------------------- | --------- |
| AccelerateConfiguration | None                      | Detailed information of global acceleration                                   | Container |
| Status                  | AccelerateConfiguration | Indicates whether global acceleration is enabled. Enumerated values: Suspended, Enabled | Enum      |


## Response

#### Response header

This API only returns common response headers. For more information, please see [Common Response Headers](https://cloud.tencent.com/document/product/436/7729). 

#### Response body

The response body return is empty.

#### Error codes

The following error messages may be returned for this request operation. For common error messages, please see [Error Codes](https://cloud.tencent.com/document/product/436/7730).

| Error Code | HTTP Status Code | Description |
| --------------- | --------------- | ------------------------------------------------------------ |
| InvalidArgument | 400 Bad Request | 1. If the XML body of the request is empty, `InvalidArgument` will be returned. <br>2. The global acceleration status has only two valid values: `Enabled` and `Suspended`. If any other status value is entered, `InvalidArgument` will be returned. |
| InvalidDigest   | 400 Bad Request | The carried Content-MD5 does not match the request body calculated by the server.        |

## Use cases

#### Request

```shell
PUT /?accelerate HTTP/1.1
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Connection: keep-alive
Authorization: authorization string
Content-Type: text/plain
Content-Length: 83

<AccelerateConfiguration>
    <Status>Enabled</Status>
</AccelerateConfiguration>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Wed, 23 Aug 2019 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0ZThm
```
