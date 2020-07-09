## Description

This API is used to delete a single object from a COS bucket. To make this request, you need to have the permission to write to the bucket.

#### Versioning

To delete a specified version including delete marker (the same below) of an object, specify the version ID of the object using the `versionId` parameter in your request. Then, the response will return the `x-cos-version-id` header to represent the deleted version ID.

In cases where `versionId` is not specified:
- If versioning is enabled, this DELETE operation will create a delete marker as the latest version of the specified object. Then, the response will return the `x-cos-version-id` header, which represents the version ID of this delete marker.
- If versioning is suspended, this DELETE operation will create a delete marker with a null version ID as the latest version of the specified object, and delete any existing versions with a null version ID (if any).

If this DELETE operation creates or deletes a delete marker, the response will return the `x-cos-delete-marker: true` header, which represents this delete marker.

For more information on versioning state, see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).

## Request

#### Sample request

```shell
DELETE /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request parameters

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| versionId | Specifies the version ID of the object to be deleted | string | No |

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Versioning-related headers**

To delete an object or its specified version from a versioning-enabled bucket will return the following response headers:

| Name | Description | Type |
| --- | --- | --- |
| x-cos-version-id | Version ID of an object’s version or delete marker | string |
| x-cos-delete-marker | <li>Returned with a value `true` to indicate the deleted version ID is for a delete marker if you specified the version ID of a delete marker using the `versionId` request parameter<br><li>Returned with a value `true` to indicate the DELETE request has created a delete marker as the latest version of the object if you didn’t use `versionId` and the object was from a versioning-enabled bucket  | boolean |

#### Response body

This response body is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1. Versioning not enabled

#### Request

```shell
DELETE /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 14 Aug 2019 11:59:40 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565783980;1565791180&q-key-time=1565783980;1565791180&q-header-list=date;host&q-url-param-list=&q-signature=75ae614a90d55054f7dea2b5cdcfdeaa1f85****
Connection: close
```

#### Response

```shell
HTTP/1.1 204 No Content
Content-Length: 0
Connection: close
Date: Wed, 14 Aug 2019 11:59:40 GMT
Server: tencent-cos
x-cos-request-id: NWQ1M2Y3YWNfMzdiMDJhMDlfODA1Yl8xZThj****
```

#### Example 2. Versioning enabled (creating delete marker)

#### Request

```shell
DELETE /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 14 Aug 2019 12:00:21 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565784021;1565791221&q-key-time=1565784021;1565791221&q-header-list=date;host&q-url-param-list=&q-signature=f5ee3ccd55378061f1890b9a2d3dd1af94f6****
Connection: close
```

#### Response

```shell
HTTP/1.1 204 No Content
Content-Length: 0
Connection: close
Date: Wed, 14 Aug 2019 12:00:21 GMT
Server: tencent-cos
x-cos-delete-marker: true
x-cos-request-id: NWQ1M2Y3ZDVfN2RiNDBiMDlfMmMwNmVfMTc4****
x-cos-version-id: MTg0NDUxNzgyODk2ODc1NjY0NzQ
```

#### Example 3. Deleting a specified version permanently

#### Request

```shell
DELETE /exampleobject?versionId=MTg0NDUxNzgyODk3MDgyMzI4NDY HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 14 Aug 2019 12:00:32 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565784032;1565791232&q-key-time=1565784032;1565791232&q-header-list=date;host&q-url-param-list=versionid&q-signature=9553e1210ba22f0725e5ff7f9bb7c8760c58****
Connection: close
```

#### Response

```shell
HTTP/1.1 204 No Content
Content-Length: 0
Connection: close
Date: Wed, 14 Aug 2019 12:00:32 GMT
Server: tencent-cos
x-cos-request-id: NWQ1M2Y3ZTBfODhjMjJhMDlfMWNkOF8xZDZi****
x-cos-version-id: MTg0NDUxNzgyODk3MDgyMzI4NDY
```

#### Example 4. Deleting a delete marker permanently

#### Request

```shell
DELETE /exampleobject?versionId=MTg0NDUxNzgyODk2ODc1NjY0NzQ HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 14 Aug 2019 12:00:42 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565784042;1565791242&q-key-time=1565784042;1565791242&q-header-list=date;host&q-url-param-list=versionid&q-signature=14e18786f25e762fb11560ea788d5e07c375****
Connection: close
```

#### Response

```shell
HTTP/1.1 204 No Content
Content-Length: 0
Connection: close
Date: Wed, 14 Aug 2019 12:00:42 GMT
Server: tencent-cos
x-cos-delete-marker: true
x-cos-request-id: NWQ1M2Y3ZWFfNzljMDBiMDlfMjkyMDJfMWRjNjVm****
x-cos-version-id: MTg0NDUxNzgyODk2ODc1NjY0NzQ
```
