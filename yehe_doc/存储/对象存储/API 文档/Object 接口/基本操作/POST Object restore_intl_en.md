## Feature

This API (POST Object restore) is used to restore (unfreeze) an archived object by generating a temp readable replica. You can set “Keep Readable” for the replica object, and used 'Days' to  parameter to specify the expiration time of the temporary object. If the time is exceeded and you haven’t initiated a copy, extension, or any other operation, the temporary object will be automatically deleted. Temporary objects are only copies of the archived objects which always exist. For more information on Archive Storage, see [Storage Type - Archive Storage] (https://intl.cloud.tencent.com/document/product/436/30925).

#### Versioning

When Versioning is enabled, you can specify the `versionId` to restore an object to a specific version. If it's not specified, the object will be restored to the latest version.

## Request

#### Request sample

```shell
POST /<ObjectKey>restore HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Request Body]
```

> Authorization: Auth String (For more information, see [Request Signature] (https://cloud.tencent.com/document/product/436/7778).

#### Request Parameters

This API does not use any request parameter.

#### Request Header

In addition to common request headers, this API also supports the following request headers. For more information about the common request header, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| --- | --- | --- | --- |
| Content-MD5 | Base64-encoded MD5 hash of the request body content as defined in RFC 1864, used for integrity check to verify whether the request body has changed during transfer | string | Yes |

#### Request body

Submits the **application/xml ** request data, including specific parameters of the restore action.

```shell
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
| RestoreRequest | None | Contains all request information for POST Object restore | Container | Yes |

**Content of Container node RestoreRequest:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Days | RestoreRequest | Specifies the valid duration (days) of a restored temporary copy | number | yes |
| CASJobParameters | RestoreRequest | Restore working parameters | Container | Yes |

**Content of Container node CASJobParameters:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| Tier | RestoreRequest.CASJobParameters | This parameter can be specified as one of the three supported restoration modes:<br> <li>`Standard`, where a restoration job can be completed in 3-5 hours,<br> <li>`Expedited`, where a restoration job can be completed in 1-5 minutes, and<br> <li>`Bulk`, where a restoration job can be completed in 5-12 hours. | Enum | Yes |

## Response

#### Response header

This API only returns common response headers. For more information, see [Common Response Headers](https://cloud.tencent.com/document/product/436/7729).

#### Response Body

The response body of this API is empty.

#### Error codes

The special error messages for this API are shown as below. For all error messages, please see [Error Codes](https://cloud.tencent.com/document/product/436/7730).

| Error Code | Description | HTTP Status Code |
| ------------------------ | ---------------------------------- | ------------ |
| RestoreAlreadyInProgress | This object is being restored | 409 Conflict |

## Use Cases

#### Case 1: Basic case (with Versioning not enabled)

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

#### Case 2: Restore a specific version of the object (with Versioning enabled)

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
