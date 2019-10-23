## Description

This API (PUT Bucket) is used to create a bucket under the specified account. This API does not support anonymous requests; therefore, to create a bucket, you need to use a request with the Authorization signature. A user who creates a bucket will be the bucket owner by default.

>? When creating a bucket, if no access permission is specified, the private read/write (private) permission will be used by default.

## Request

#### Sample Request

```shell
PUT / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: 0
Authorization: Auth String
```

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request Parameters

This API has no request parameters.

#### Request Header

In addition to common request headers, this API also supports the following request headers. For more information about the common request header, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ------ | -------- |
| x-cos-acl | This defines the access control list (ACL) attribute of the bucket. For the enumerated values such as private and public-read, see the Preset ACL for Buckets section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: private | Enum | No |
| x-cos-grant-read | This grants the grantee permission to read the bucket in the format of id="[OwnerUin]", such as id="100000000001". Multiple grantees can be separated by comma (,), such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-write | This grants the grantee permission to write to the bucket in the format of id="[OwnerUin]", such as id="100000000001". Multiple grantees can be separated by comma (,), such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-read-acp | This grants the grantee permission to read the ACL and policy of the bucket in the format of id="[OwnerUin]", such as id="100000000001". Multiple grantees can be separated by comma (,), such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-write-acp | This grants the grantee permission to write to the ACL and policy of the bucket in the format of id="[OwnerUin]", such as id="100000000001". Multiple grantees can be separated by comma (,), such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-full-control | This grants the grantee full permission to manipulate the bucket in the format of id="[OwnerUin]", such as id="100000000001". Multiple grantees can be separated by comma (,), such as `id="100000000001",id="100000000002"` | String | No |

#### Request Body

This API has no request body.

## Response

#### Response Header

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response Body

The response body of this API is empty.

#### Error Codes

The special error messages for this API are as detailed below. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

| Error Code | Description | HTTP Status Code |
| ----------------------- | ---------------------------------- | ------------ |
| BucketAlreadyExists | The specified bucket already exists. | 409 Conflict |
| BucketAlreadyOwnedByYou | The specified bucket already exists and was created by the current account. | 409 Conflict |

## Samples

#### Sample 1. A Simple Sample

#### Request

```shell
PUT / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sun, 26 May 2019 14:51:38 GMT
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558882298;1558889498&q-key-time=1558882298;1558889498&q-header-list=content-length;date;host&q-url-param-list=&q-signature=c25fd640274a6da2318935ceebfbcfba4598****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Sun, 26 May 2019 14:51:37 GMT
Server: tencent-cos
x-cos-request-id: NWNlYWE3ZjlfZDQyNzVkNjRfMzg1N18yNzFh****
```

#### Sample 2. Specifying Public-read and Granting the Specified User Read/Write Permission

#### Request

```shell
PUT / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 14 Jun 2019 13:48:59 GMT
x-cos-acl: public-read
x-cos-grant-write: id="100000000002"
x-cos-grant-read-acp: id="100000000002"
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1560520139;1560527339&q-key-time=1560520139;1560527339&q-header-list=content-length;date;host;x-cos-acl;x-cos-grant-read-acp;x-cos-grant-write&q-url-param-list=&q-signature=df03e7917270e0bf2b679bc6f99793bd0c63****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 14 Jun 2019 13:49:00 GMT
Server: tencent-cos
x-cos-request-id: NWQwM2E1Y2NfZjBhODBiMDlfOTM1YV83NDRi****
```
