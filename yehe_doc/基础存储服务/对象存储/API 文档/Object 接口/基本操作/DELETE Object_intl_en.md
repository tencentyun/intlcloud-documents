## Overview

This API is used to delete a specified object. To call this API, you need to have permission to write to the object.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=DeleteObject&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>

#### Versioning

To delete a specified version of object/delete marker, use the `versionId` request parameter to specify the ID of the object version/delete marker. In this way, the `x-cos-version-id` response header will be returned, indicating the version ID deleted.

If `versionId` is not specified:
- When versioning is enabled, the `DELETE` operation will create the latest version of delete marker for this object, and the `x-cos-version-id ` response header will be returned to indicate the version ID of the delete marker created in this request.
- When versioning is suspended, the `DELETE` operation will create a delete marker whose ID is `null` as the latest version of the object, and all other versions whose ID is `null` (if any) will be deleted.

If the `DELETE` operation has successfully created/deleted a delete marker, the `x-cos-delete-marker: true` response header will be returned.

For more information about the status (enabled/suspended) of versioning, please see [Versioning Overview](https://intl.cloud.tencent.com/document/product/436/19883).

## Request

#### Sample request

```shell
DELETE /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```
>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

| Parameter | Description | Type | Required |
| --- | --- | --- | --- |
| versionId | ID of an object version to delete | string | No |

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information about common response headers, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Versioning-related headers**

If you delete an object or a specified version of object from a versioning-enabled bucket, the following response headers will be returned:

| Parameter | Description | Type |
| --- | --- | --- |
| x-cos-version-id | ID of the object version/delete marker | string |
| x-cos-delete-marker | <li>If `versionId` is specified, the value of this parameter will be `true`, indicating that the deleted version of object corresponds to a delete marker.<br><li>If `versionId` is not specified, and the specified object resides in a versioning-enabled bucket, the value of this parameter will be `true`, indicating that this request has created the latest version of delete marker for this object. | boolean |

#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Sample 1: versioning not enabled

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

#### Sample 2: versioning-enabled (creating a delete marker)

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

#### Sample 3: deleting an object of a specified version permanently

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

#### Sample 4: deleting a specified delete marker permanently

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
