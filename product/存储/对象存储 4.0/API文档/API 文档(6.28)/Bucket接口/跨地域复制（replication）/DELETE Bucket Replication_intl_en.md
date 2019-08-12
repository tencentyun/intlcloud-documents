## Description
The DELETE Bucket replication API is used to delete the cross-region replication configuration in a bucket. When initiating this request, you need to get the request signature to indicate that the request has been authorized.

## Request
### Sample Request

```shell
DELETE /?replication HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

### Request Headers
#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Special Headers
This request operation has no special request headers.
### Request Body
The request body of this request is empty.

## Response
### Response Headers
#### Common Response Headers
This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response has no special response headers.

### Response Body
This response body is empty.

## Examples

### Request

The following request sample deletes the cross-region replication configuration from the bucket `originBucet-1250000000`.
```shell
DELETE /?replication HTTP/1.1
Date: Fri, 14 Apr 2019 07:47:35 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1503901499;1503901859&q-key-time=1503901499;1503901859&q-header-list=host&q-url-param-list=replication&q-signature=761f3f6449c6a11684464f4b09c6f292f0a4e7e0
Host: originBucet-1250000000.cos.ap-chengdu.myqcloud.com
```

### Response

After the request above is made, COS returns a response of `204 No Content`, indicating that the cross-region replication configuration has been successfully deleted from the bucket. After the configuration is deleted, COS will no longer copy the objects in the source bucket to the destination bucket, and the existing object data in the destination bucket will be retained.
```shell
Content-Length: 0
Connection: keep-alive
Date: Fri, 14 Apr 2019 07:47:35 GMT
Server: tencent-cos
x-cos-request-id: NWQwMzUxMTdfMjBiNDU4NjRfNWZlZF84MjdmZTE=
x-cos-trace-id: OGVmYzZiMmQzYjA2OWNhODk0NTRkMTBiOWVmMDAxODc0OWRkZjk0ZDM1NmI1M2E2MTRlY2MzZDhmNmI5MWI1OWE4OGMxZjNjY2JiNTBmMTVmMWY1MzAzYzkyZGQ2ZWM4MzUyZTg1NGRhNWY0NTJiOGUyNTViYzgyNzgxZTEwOTY=
```
