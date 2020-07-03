## Feature

This API is used to delete multiple objects from a bucket. You can delete up to 1,000 objects using a single request. COS supports two modes for the response: Verbose and Quiet.

- In Quiet mode, the response includes only information on objects with delete failure errors.
- In Verbose mode, the response includes the result of deletion of each object in your request.

To make this request, you need to have permission to write to the bucket.

#### Versioning

If versioning is enabled, you can specify the version ID of each object in this API request to permanently delete the specified version or delete marker of the object. If the version ID is not specified, COS will create a delete marker as the latest version of the object.

When the delete operation creates or deletes a delete marker for an object, the response returns both elements `&lt;DeleteMarker>true&lt;/DeleteMarker&gt;` and &lt;DeleteMarkerVersionId>.

When the delete operation permanently deletes a specified version (including that of a delete marker) from an object, the response returns the element `&lt;VersionId&gt`.

## Request

#### Request samples

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

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request parameters

This API does not use any request parameter.

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

Submits **application/xml** request data, including objects to be deleted.

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

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | ----------------------------------------------- | --------- | -------- |
| Delete             | None     | Contains all information about the DELETE Multiple Objects request | Container | Yes       |

**Content of the Container node `Delete`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | ------------------------------------------------------------ | --------- | -------- |
| Quiet              | Delete | Boolean. Default: `false`<br><li>`true` indicates Quiet mode where the response includes only information on the objects with delete failure errors.<br><li>`false` indicates Verbose mode where the response includes the result of deletion of each object. | boolean   | Yes       |
| Object             | Delete | A single object to be deleted                                   | Container | Yes       |

**Content of the Container node `Object`:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------------------------------------------------ | ------------- | ------------------------------------------------------------ | ------ | -------- |
| Key&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Delete.Object | Key of the object to be deleted                                     | string | Yes       |
| VersionId                                                    | Delete.Object | Version ID of an object to be deleted. Required if you have enabled versioning and want to delete a specified object version; not required if you haven’t enabled versioning, or want to insert a delete marker when versioning is enabled. | string | Yes       |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful request returns the **application/xml** data, which includes deletion results.

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

The detailed nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------ | ------------------------------------------- | --------- |
| DeleteResult       | None     | Contains all results of the DELETE Multiple Objects operation | Container |

**Content of the Container node `DeleteResult`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------ | ----------------------------------------------------------- | --------- |
| Deleted            | DeleteResult | An entry for a single object deleted successfully; only returned when Verbose mode is used | Container |
| Error              | DeleteResult | An entry for a single object that fails to be deleted                                      | Container |

**Content of the Container node `Deleted`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --------------------- | -------------------- | ------------------------------------------------------------ | ------- |
| Key                   | DeleteResult.Deleted | Key of an object deleted successfully                                       | string  |
| DeleteMarker          | DeleteResult.Deleted | Boolean. Fixed value: `true`. Returned only if the delete operation creates or deletes a delete marker for the object. | boolean |
| DeleteMarkerVersionId | DeleteResult.Deleted | Version ID of a delete marker. Returned only if the delete operation creates or deletes a delete marker for the object. | string  |
| VersionId             | DeleteResult.Deleted | ID of the version deleted successfully. Returned only if the request includes a version ID of the object to be deleted. | string  |

**Content of the Container node `Error`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------ | ------------------------------------------------------------ | ------ |
| Key                | DeleteResult.Error | Key of the object that failed to be deleted                                       | string |
| VersionId             | DeleteResult.Error | ID of the version that fails to be deleted. Returned only if the request includes a version ID of the object to be deleted. | string  |
| Code               | DeleteResult.Error | Error code for a delete failure; used to identify the unique error condition and error scenario       | string |
| Message            | DeleteResult.Error | Message of a delete failure                                       | string |

#### Error codes

There are no special error messages for this API. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1. Simple example

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

#### Example 2. Simple example (Quiet mode)

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

#### Example 3. Enabling versioning (creating delete markers)

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

#### Example 4. Deleting a specified version

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

#### Example 5. Deleting a specified delete marker

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

#### Example 6. Partial deletion success

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
