## Feature Description

The `POST Object restore` API allows you to send a request to restore an ARCHIVE/DEEP ARCHIVE object so that you can read it. The restored readable object is a temporary copy, for which you can set the readable status and the time to delete it through the `Days` parameter. If the time has elapsed and you haven't initiated a copy or extension operation, the temporary object will be automatically deleted. Temporary objects are only copies of the archived objects which always exist. For more information on the ARCHIVE storage class, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925).

>? The QPS of the `POST Object restore` API is limited to 100.
>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PostObjectRestore&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>


#### Versioning

If versioning is enabled, you can use the `versionId` parameter in your request to specify the ID of the version to be restored. If this parameter is not specified, the latest version will be restored.

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
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com, where &lt;BucketName-APPID> is the bucket name followed by the `APPID`, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> 

#### Request parameters

| Field |  Description | Type | Required |
| ---------------------------- | ------------------------------------------------------------ | ------ | -------- |
| versionId | Specifies the version ID of the versioning-enabled object to restore. If this parameter is not specified, the latest version will be restored. | string | No |

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

Submit **application/xml** request data, including specific parameters of the restoration operation.

```plaintext
<RestoreRequest>
   <Days>number</Days>
   <CASJobParameters>
       <Tier>Enum</Tier>
   </CASJobParameters>
</RestoreRequest>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| RestoreRequest | None | Contains all the request information of `POST Object restore`. | Container | Yes |

**`RestoreRequest` has the following sub-nodes:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Days | RestoreRequest | Specifies the validity period (in days) of the restored temporary copy. | number | Yes |
| CASJobParameters | RestoreRequest | Restoration job parameter. | Container | Yes |

**`CASJobParameters` has the following sub-nodes:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Tier | RestoreRequest.CASJobParameters | Specifies the restoration mode.<br>The following three restoration modes are available for ARCHIVE objects:<br><li>Expedited: Restores an object within 1–5 minutes. <br> <li>Standard: Restores an object within 3–5 hours. <br><li>Bulk: Restores an object within 5–12 hours.<br>The following two restoration modes are available for DEEP ARCHIVE objects:<br><li>Standard: Restores an object within 12–24 hours.<br><li>Bulk: Restores an object within 24–48 hours. | Enum | Yes |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Sample 1: Simple use case (with versioning disabled)

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

#### Sample 2: Restoring an object on a specific version (with versioning enabled)

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
