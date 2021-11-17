## Overview

This API allows you to send a request to restore an ARCHIVED/DEEP ARCHIVED object so that you can read it. The restored readable object is a temporary copy, for which you can set `Keep Readable` and the time at which to delete it at a later point. You can use the `Days` parameter to specify the expiration time of the temporary object. If the time is exceeded and you haven’t initiated a copy, extension, or any other operation, the temporary object will be automatically deleted. Temporary objects are only copies of the archived objects which always exist. For more information about ARCHIVE, please see [Storage Class Overview - ARCHIVE](https://intl.cloud.tencent.com/document/product/436/30925).

>? The QPS of the POST Object restore API is limited to 100.
>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PostObjectRestore&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>


#### Versioning

If versioning is enabled, you can use the `versionId` parameter in your request to specify the ID of the version to restore. If this parameter is not specified, the latest version will be restored.

## Request

#### Sample request

```plaintext
POST /<ObjectKey>?restore HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String



[Request Body]
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

| Parameter | Description | Type | Required |
| ---------------------------- | ------------------------------------------------------------ | ------ | -------- |
| versionId | Specifies the version ID of the versioning-enabled object to restore. If this parameter is not specified, the latest version will be restored. | string | No |

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

Contains the **application/xml** request data, including specific parameters of the restore operation.

```plaintext
<RestoreRequest>
   <Days>number</Days>
   <CASJobParameters>
       <Tier>Enum</Tier>
   </CASJobParameters>
</RestoreRequest>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| RestoreRequest | None | Contains all request information of `POST Object restore`. | Container | Yes |

**Content of `RestoreRequest`**:

| Node Name (Keyword)          | Parent Node | Description                                    | Type        | Required |
| --- | --- | --- | --- | --- |
| Days | RestoreRequest | Specifies the valid duration (in days) for the temporary copy restored. | number | Yes |
| CASJobParameters | RestoreRequest | Restores job parameters. | Container | Yes |

**Content of `CASJobParameters`**:

| Node Name (Keyword)          | Parent Node | Description                                    | Type        | Required |
| --- | --- | --- | --- | --- |
| Tier | RestoreRequest.CASJobParameters | Specifies the restoration mode.<br>The following three restoration modes are available for archived objects:<br><li>Expedited: restores an object within 1-5 minutes. <br> <li>Standard: restores an object within 3-5 hours. <br><li>Bulk: restores an object within 5-12 hours.<br>The following two modes are available for deep archived objects:<br><li>Standard: restores an object within 12-24 hours.<br><li>Bulk: restores an object within 24-48 hours. | Enum | Yes |


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1: simple use case (with versioning disabled)

#### Request

```plaintext
POST /exampleobject?restore HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 27 Dec 2019 08:19:29 GMT
Content-Type: application/xml
Content-Length: 121
Content-MD5: Nr7RAnRMgrplFvD8bt5+0w==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1577434769;1577441969&q-key-time=1577434769;1577441969&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=restore&q-signature=ed3ee8ca63689dbff4be1533fddc17c0b4d8****
Connection: close



<RestoreRequest>
			<Days>1</Days>
			<CASJobParameters>
				<Tier>Expedited</Tier>
			</CASJobParameters>
</RestoreRequest>
```

#### Response

```plaintext
HTTP/1.1 202 Accepted
Content-Length: 0
Connection: close
Date: Fri, 27 Dec 2019 08:19:29 GMT
Server: tencent-cos
x-cos-request-id: NWUwNWJlOTFfMjljOTBiMDlfMTQ2MmNfNzAw****
```

#### Example 2: restoring an object of a specific version (with versioning enabled)

#### Request

```plaintext
POST /exampleobject?restore&versionId=MTg0NDUxNjQ1NjM4OTkzNzY3NDk HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 20 Jan 2020 08:43:40 GMT
Content-Type: application/xml
Content-Length: 121
Content-MD5: Nr7RAnRMgrplFvD8bt5+0w==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1579509820;1579517020&q-key-time=1579509820;1579517020&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=restore;versionid&q-signature=f92b1c6753c452bed9ade49739ddb81a0a47****
Connection: close



<RestoreRequest>
			<Days>1</Days>
			<CASJobParameters>
				<Tier>Expedited</Tier>
			</CASJobParameters>
</RestoreRequest>
```

#### Response

```plaintext
HTTP/1.1 202 Accepted
Content-Length: 0
Connection: close
Date: Mon, 20 Jan 2020 08:43:41 GMT
Server: tencent-cos
x-cos-request-id: NWUyNTY4M2NfZTNjODJhMDlfMWZkM2VfNWZm****
```
