## Feature Description

This API (POST Object restore) is used to restore (unfreeze) an object in archive storage class so that it can be read. The restored readable object is temporary, and you can make configuration to keep it readable and set the time when you want it to be deleted. You can use the `Days` parameter to specify the expiration time of the temporary object. If the object expires and you have not initiated any operation to copy the object or extend its validity period before the expiration, the temporary object will be automatically deleted. A temporary object is only a copy of the source archived object and the source archived object will exist throughout the period. For more information on archive storage, please see [Storage Class - Archive Storage](https://intl.cloud.tencent.com/zh/document/product/436/30925#.E5.BD.92.E6.A1.A3.E5.AD.98.E5.82.A8).

#### Versioning

If versioning is enabled, this request operation can use the `versionId` request parameter to specify the ID of the version to be restored, and the object will be restored to the specified version; otherwise, the latest version of the specified object will be restored.

## Request

#### Sample request

```shell
POST /<ObjectKey>?restore HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Request Body]
```

>? Authorization: Auth String (for more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request parameters

This API has no request parameters.

#### Request header

In addition to common request headers, this API also supports the following request headers. For more information on the common request headers, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| Content-MD5 | Base64-encoded MD5 hash of the request body content as defined in RFC 1864, which is used for integrity check to verify whether the request body has changed during transfer | string | Yes |

#### Request body

Submit the **application/xml** request data, including the specific parameters for the restoration operation.

```shell
<RestoreRequest>
   <Days>number</Days>
   <CASJobParameters>
       <Tier>Enum</Tier>
   </CASJobParameters>
</RestoreRequest>
```

The specific nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| RestoreRequest | None | Contains all request information of the `POST Object restore` operation | Container | Yes |

**Content of the Container node `RestoreRequest`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Days | RestoreRequest | Specifies the validity period in days of the temporary copy generated during restoration | number | Yes |
| CASJobParameters | RestoreRequest | Restoration job parameter | Container | Yes |

**Content of the Container node `CASJobParameters`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Tier | RestoreRequest.CASJobParameters | During restoration, `Tier` can be specified as one of the following three supported restoration modes: <br> <li>Standard: standard mode where a restoration job can be completed in 3–5 hours <br> <li>Expedited: expedited mode where a restoration job can be completed in 1–5 minutes (only available to objects below 256 MB) <br><li>Bulk: bulk mode where a restoration job can be completed in 5–12 hours | Enum | Yes |

## Response

#### Response header

This API only returns common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

The special error messages for this API are as listed below. For all error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

| Error Code | Description | HTTP Status Code |
| ------------------------ | ---------------------------------- | ------------ |
| RestoreAlreadyInProgress | The specified object is being restored             | 409 Conflict |

## Use Cases

#### Sample 1. Simple sample (with versioning not enabled)

#### Request

```shell
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

```shell
HTTP/1.1 202 Accepted
Content-Length: 0
Connection: close
Date: Fri, 27 Dec 2019 08:19:29 GMT
Server: tencent-cos
x-cos-request-id: NWUwNWJlOTFfMjljOTBiMDlfMTQ2MmNfNzAw****
```

#### Sample 2. Restoring object to specified version (with versioning enabled)

#### Request

```shell
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

```shell
HTTP/1.1 202 Accepted
Content-Length: 0
Connection: close
Date: Mon, 20 Jan 2020 08:43:41 GMT
Server: tencent-cos
x-cos-request-id: NWUyNTY4M2NfZTNjODJhMDlfMWZkM2VfNWZm****
```
