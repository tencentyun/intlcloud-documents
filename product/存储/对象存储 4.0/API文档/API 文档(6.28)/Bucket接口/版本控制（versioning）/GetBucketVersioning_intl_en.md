## Description
The GET Bucket versioning API is used to get the versioning information of the specified bucket.
### Detail Analysis
1. To query the versioning status of a bucket, you need to have read permission to the bucket.
2. There are three versioning states: not enabled, enabled, or suspended.
- If you have never enabled or suspended versioning in the bucket, the response is:
```
<VersioningConfiguration>
```

- If you have enabled versioning in the bucket, the response is:
```
<VersioningConfiguration>
  <Status>Enabled</Status>
</VersioningConfiguration>
```
- If you have suspended versioning in the bucket, the response is:
```
<VersioningConfiguration>
    <Status>Suspended</Status>
</VersioningConfiguration>
```


## Request
### Sample Request

```
GET /?versioning HTTP 1.1
Host: <Bucketname>-<APPID>.cos.<Region>.myqcloud.com
Date: GMT date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

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

```
<VersioningConfiguration>
    <Status></Status>
</VersioningConfiguration>
```

Detailed data is as shown below:

| Node Name (Keyword) | Parent Node | Description | Type |
| --------------------------------------- | --------------------- | --------- | ------- |
| VersioningConfiguration | None | Describes the specific information of versioning | Container |
| Status | VersioningConfiguration | Indicates whether versioning is enabled. Enumerated values: Suspended, Enabled | Enum |


## Examples
```
GET /?versioning HTTP/1.1
Host: testbucket-1352548703.cos.cn-north.myqcloud.com
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9SmuG00&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=versioning&q-header-list=host&q-signature=5118a936049f9d44482bbb61309235cf4abe99c2
```

### Response
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 120
Connection: keep-alive
Date: Wed, 23 Aug 2017 08:15:16 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5OTRfZDNhZDM1MGFfMjYyMTFfZmU3NWQ=

<?xml version='1.0' encoding='utf-8' ?>
<VersioningConfiguration>
    <Status>Enabled</Status>
</VersioningConfiguration>
```
