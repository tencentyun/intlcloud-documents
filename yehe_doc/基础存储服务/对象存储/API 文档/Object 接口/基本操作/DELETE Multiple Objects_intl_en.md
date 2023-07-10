## Overview

This API is used to delete multiple objects (up to 1,000) from a bucket in a single request. COS provides the following two response modes:

- Quiet: returns only information about objects that failed to delete and the error messages.
- Verbose: returns the deletion results of each object.

To call this API, you need to have permission to write to the bucket.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=DeleteMultipleObjects&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>


#### Versioning

If versioning is enabled, you can specify a version ID for each object to delete so that these objects/delete markers of the specified versions can be deleted permanently. If no version ID is specified, a new delete marker will be created for the object.

If a delete marker is created or deleted in this request, the &lt;DeleteMarker>true&lt;/DeleteMarker&gt; and &lt;DeleteMarkerVersionId&gt; nodes will be returned for this object.

If an object of a specified version (including the delete marker version) is deleted permanently in this request, the &lt;VersionId&gt; node will be returned, indicating the version ID that is deleted in this request.

## Request

#### Sample request

```plaintext
POST /?delete HTTP/1.1
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

This API has no request parameter.

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body contains **application/xml** data that includes information about the objects to delete.

```xml
<Delete>
	<Quiet>boolean</Quiet>
	<Object>
		<Key>string</Key>
	</Object>
	<Object>
		<Key>string</Key>
		<VersionId>string</VersionId>
	</Object>
</Delete>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | ----------------------------------------------- | --------- | -------- |
| Delete | None | Stores information about the `DELETE Multiple Objects` request. | Container | Yes |

**Content of `Delete`**:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | ------------------------------------------------------------ | --------- | -------- |
| Quiet | Delete | Whether to use the Quiet mode for the response <br><li>`true`: yes (returns only information about objects that failed to delete and the error messages) <br><li>`false` (default): no (uses the Verbose mode instead, returning the deletion results of all objects) | boolean | Yes |
| Object | Delete | Information about a single object to delete | Container | Yes |

**Content of `Object`**:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------------------------------------------------ | ------------- | ------------------------------------------------------------ | ------ | -------- |
| Key | Delete.Object | Key of the object to delete | string | Yes |
| VersionId | Delete.Object | Version ID of the object to delete (if versioning is enabled). If versioning is not enabled, or you want to create a delete marker with versioning enabled, you don’t need to specify this node. | string | Yes |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

**application/xml** data that contains the deletion results will be returned for a successful request.

```xml
<DeleteResult>
	<Deleted>
		<Key>string</Key>
		<DeleteMarker>boolean</DeleteMarker>
		<DeleteMarkerVersionId>string</DeleteMarkerVersionId>
	</Deleted>
	<Deleted>
		<Key>string</Key>
		<VersionId>string</VersionId>
	</Deleted>
	<Deleted>
		<Key>string</Key>
		<DeleteMarker>boolean</DeleteMarker>
		<DeleteMarkerVersionId>string</DeleteMarkerVersionId>
		<VersionId>string</VersionId>
	</Deleted>
	<Error>
		<Key>string</Key>
		<VersionId>string</VersionId>
		<Code>string</Code>
		<Message>string</Message>
	</Error>
</DeleteResult>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------ | ------------------------------------------- | --------- |
| DeleteResult | None | Stores the results of `DELETE Multiple Objects` | Container |

**Content of `DeleteResult`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------ | ----------------------------------------------------------- | --------- |
| Deleted | DeleteResult | An object entry that is successfully deleted. This node is returned only in Verbose mode. | Container |
| Error | DeleteResult | An object entry that failed to delete | Container |

**Content of `Deleted`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| --------------------- | -------------------- | ------------------------------------------------------------ | ------- |
| Key | DeleteResult.Deleted | Key of the object that is successfully deleted | string  |
| DeleteMarker | DeleteResult.Deleted | Fixed to `true`. This node is returned when a delete marker is created or deleted for an object. | boolean |
| DeleteMarkerVersionId | DeleteResult.Deleted | ID of the delete marker that is created or deleted. This node is returned only when a delete marker is created or deleted for an object. | string  |
| VersionId | DeleteResult.Deleted | Version ID of the object that is successfully deleted. This node is returned only when a version ID is specified in the request. | string |

**Content of `Error`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------ | ------------------------------------------------------------ | ------ |
| Key | DeleteResult.Error | Key of the object that failed to delete | string |
| VersionId          | DeleteResult.Error | Version ID of the object that failed to delete. This node is returned only when a version ID is specified in the request. | string |
| Code | DeleteResult.Error | Error code for the deletion failure. The error code can be used to locate the error conditions and scenario. | string |
| Message | DeleteResult.Error | Error message for the deletion failure  | string |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Sample 1: simple use case

#### Request

```plaintext
POST /?delete HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 20 Aug 2019 11:59:35 GMT
Content-Type: application/xml
Content-Length: 158
Content-MD5: zUd/xgzNGDrqJMJUOWV2AQ==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1566302375;1566309575&q-key-time=1566302375;1566309575&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=delete&q-signature=82f77c745ca66fe8c5d93274b3fc44fb895c****
Connection: close

<Delete>
	<Quiet>false</Quiet>
	<Object>
		<Key>example-object-1.jpg</Key>
	</Object>
	<Object>
		<Key>example-object-2.jpg</Key>
	</Object>
</Delete>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 144
Connection: close
Date: Tue, 20 Aug 2019 11:59:35 GMT
Server: tencent-cos
x-cos-request-id: NWQ1YmUwYTdfM2FiMDJhMDlfYzczN18zMGM1****

<DeleteResult>
	<Deleted>
		<Key>example-object-1.jpg</Key>
	</Deleted>
	<Deleted>
		<Key>example-object-2.jpg</Key>
	</Deleted>
</DeleteResult>
```

#### Sample 2: simple use case (using the Quiet mode)

#### Request

```plaintext
POST /?delete HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 20 Aug 2019 12:12:26 GMT
Content-Type: application/xml
Content-Length: 157
Content-MD5: +iI9kJvM2k/y5y3nHcn8BQ==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1566303146;1566310346&q-key-time=1566303146;1566310346&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=delete&q-signature=16581dcc0ae999ce343488de2449436ee182****
Connection: close

<Delete>
	<Quiet>true</Quiet>
	<Object>
		<Key>example-object-1.jpg</Key>
	</Object>
	<Object>
		<Key>example-object-2.jpg</Key>
	</Object>
</Delete>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 15
Connection: close
Date: Tue, 20 Aug 2019 12:12:27 GMT
Server: tencent-cos
x-cos-request-id: NWQ1YmUzYWFfMTljMDJhMDlfNTg3ZV8zNDI0****

<DeleteResult/>
```

#### Sample 3: versioning-enabled (creating a delete marker)

#### Request

```plaintext
POST /?delete HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 21 Aug 2019 12:04:03 GMT
Content-Type: application/xml
Content-Length: 100
Content-MD5: MowFtlG7iwK7Wmk79IVXFA==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1566389043;1566396243&q-key-time=1566389043;1566396243&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=delete&q-signature=b1aee84c567b16e5e6c8634c2760a0e5d348****
Connection: close

<Delete>
	<Quiet>false</Quiet>
	<Object>
		<Key>example-object-1.jpg</Key>
	</Object>
</Delete>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 200
Connection: close
Date: Wed, 21 Aug 2019 12:04:03 GMT
Server: tencent-cos
x-cos-request-id: NWQ1ZDMzMzNfNDhiNDBiMDlfMmIzNzZfMTBh****

<DeleteResult>
	<Deleted>
		<Key>example-object-1.jpg</Key>
		<DeleteMarker>true</DeleteMarker>
		<DeleteMarkerVersionId>MTg0NDUxNzc2ODQ2NjU3ODM4NTc</DeleteMarkerVersionId>
	</Deleted>
</DeleteResult>
```

#### Sample 4: deleting an object of a specified version

#### Request

```plaintext
POST /?delete HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 21 Aug 2019 11:24:43 GMT
Content-Type: application/xml
Content-Length: 154
Content-MD5: EwFydeQSMzaHWi0qMTOGWw==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1566386683;1566393883&q-key-time=1566386683;1566393883&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=delete&q-signature=2b6261e526960a433124b752fd21a7a9a363****
Connection: close

<Delete>
	<Quiet>false</Quiet>
	<Object>
		<Key>example-object-2.jpg</Key>
		<VersionId>MTg0NDUxNzc2ODcwMjYyNjIwMTM</VersionId>
	</Object>
</Delete>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 140
Connection: close
Date: Wed, 21 Aug 2019 11:24:44 GMT
Server: tencent-cos
x-cos-request-id: NWQ1ZDI5ZmJfNDhiNDBiMDlfMmIzODNfMTA0****

<DeleteResult>
	<Deleted>
		<Key>example-object-2.jpg</Key>
		<VersionId>MTg0NDUxNzc2ODcwMjYyNjIwMTM</VersionId>
	</Deleted>
</DeleteResult>
```

#### Sample 5: deleting a delete marker

#### Request

```plaintext
POST /?delete HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 21 Aug 2019 12:04:04 GMT
Content-Type: application/xml
Content-Length: 154
Content-MD5: EKphCPpHcKiVqJtMqE+DmA==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1566389044;1566396244&q-key-time=1566389044;1566396244&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=delete&q-signature=f6b49a9b98386632b9545a4cc087449f789f****
Connection: close

<Delete>
	<Quiet>false</Quiet>
	<Object>
		<Key>example-object-1.jpg</Key>
		<VersionId>MTg0NDUxNzc2ODQ2NjU3ODM4NTc</VersionId>
	</Object>
</Delete>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 253
Connection: close
Date: Wed, 21 Aug 2019 12:04:04 GMT
Server: tencent-cos
x-cos-request-id: NWQ1ZDMzMzRfYmIwMmEwOV83YTQzXzEyM2Ri****

<DeleteResult>
	<Deleted>
		<Key>example-object-1.jpg</Key>
		<DeleteMarker>true</DeleteMarker>
		<DeleteMarkerVersionId>MTg0NDUxNzc2ODQ2NjU3ODM4NTc</DeleteMarkerVersionId>
		<VersionId>MTg0NDUxNzc2ODQ2NjU3ODM4NTc</VersionId>
	</Deleted>
</DeleteResult>
```

#### Sample 6: failed to delete some objects

#### Request

```plaintext
POST /?delete HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 21 Aug 2019 12:04:05 GMT
Content-Type: application/xml
Content-Length: 436
Content-MD5: ZAbgvje31aO+0j7pkEkYvQ==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1566389045;1566396245&q-key-time=1566389045;1566396245&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=delete&q-signature=543a9f9f65c45e533a415afe5d014cdc9c73****
Connection: close

<Delete>
	<Quiet>false</Quiet>
	<Object>
		<Key>example-object-1.jpg</Key>
	</Object>
	<Object>
		<Key>example-object-2.jpg</Key>
		<VersionId>MTg0NDUxNzc2ODQ2NjQ1MjM5MTk</VersionId>
	</Object>
	<Object>
		<Key>example-object-3.jpg</Key>
		<VersionId>MTg0NDUxNzc2ODQ2NjQwMTIwMDI</VersionId>
	</Object>
	<Object>
		<Key>example-object-4.jpg</Key>
		<VersionId>MTg0NDUxNzc2ODQ2NjQ0NjI0MDQ</VersionId>
	</Object>
</Delete>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 703
Connection: close
Date: Wed, 21 Aug 2019 12:04:06 GMT
Server: tencent-cos
x-cos-request-id: NWQ1ZDMzMzVfOTNjMjJhMDlfMzhiM18xMWY3****

<DeleteResult>
	<Deleted>
		<Key>example-object-1.jpg</Key>
		<DeleteMarker>true</DeleteMarker>
		<DeleteMarkerVersionId>MTg0NDUxNzc2ODQ2NjM1NTI2NDY</DeleteMarkerVersionId>
	</Deleted>
	<Deleted>
		<Key>example-object-2.jpg</Key>
		<VersionId>MTg0NDUxNzc2ODQ2NjQ1MjM5MTk</VersionId>
	</Deleted>
	<Deleted>
		<Key>example-object-3.jpg</Key>
		<DeleteMarker>true</DeleteMarker>
		<DeleteMarkerVersionId>MTg0NDUxNzc2ODQ2NjQwMTIwMDI</DeleteMarkerVersionId>
		<VersionId>MTg0NDUxNzc2ODQ2NjQwMTIwMDI</VersionId>
	</Deleted>
	<Error>
		<Key>example-object-4.jpg</Key>
		<VersionId>MTg0NDUxNzc2ODQ2NjQ0NjI0MDQ</VersionId>
		<Code>PathConflict</Code>
		<Message>Path conflict.</Message>
	</Error>
</DeleteResult>
```
