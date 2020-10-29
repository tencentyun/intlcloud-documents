## Feature

This API is used to restore an object from the ARCHIVE or DEEP ARCHIVE storage class so that you can read it. The restored object is a temporary copy, for which you can set “Keep Readable”. You can also specify “Days” for which the copy stays active before expiry. If you haven’t initiated a copy, extension, or any other operation during the "Days", an expired temporary object will be automatically deleted. Temporary objects are only copies of ARCHIVE or DEEP ARCHIVE objects which always exist. For more information on storage classes, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925).

#### Versioning

With versioning enabled, you can specify the `versionId` request parameter to restore a specific version of the object. If no version ID is specified, the latest version will be restored.

## Request

#### Sample request 

```plaintext
POST /<ObjectKey>restore HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Request Body]
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request parameters

| Name | Description | Type | Required |
| ---------------------------- | ------------------------------------------------------------ | ------ | -------- |
| versionId | Specifies the version ID of the object if versioning is enabled; if this parameter is not specified, the latest version will be restored | string | No |

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

Contains **application/xml ** request data, including specific parameters of the restore action.

```plaintext
<RestoreRequest>
   <Days>number</Days>
   <CASJobParameters>
       <Tier>Enum</Tier>
   </CASJobParameters>
</RestoreRequest>
```

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| RestoreRequest | None | All information in a POST Object restore request | Container | Yes |

**Container node `RestoreRequest`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Days | RestoreRequest | Specifies the number of days a restored temporary copy remains in COS | number | Yes |
| CASJobParameters | RestoreRequest | Restore job parameters | Container | Yes |

**Container node `CASJobParameters`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Tier | RestoreRequest.CASJobParameters | Specifies the restoration mode.<br>There are three restoration modes available for ARCHIVE:<br><li>`Expedited`, where a restoration job can be completed in 1-5 minutes for up to 256 MB of objects.<br><li>`Standard`, where a restoration job can be completed in 3-5 hours.<br><li>`Bulk`, where a restoration job can be completed in 5-12 hours.<br>There are two restoration modes available for DEEP ARCHIVE:<br><li>`Standard`, where a restoration job can be completed in 12-24 hours.<br><li>`Bulk`, where a restoration job can be completed in 24-48 hours. | Enum | Yes |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1. Simple example (versioning not enabled)

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

#### Example 2. Restoring a specific version of an object (with versioning enabled)

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
