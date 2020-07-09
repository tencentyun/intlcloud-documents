## Description

This API is used to retrieve versions of all objects in a bucket. You can also get versions of only part of objects by using parameters. Requests to this API require write permission on the bucket.

## Request

#### Sample request

```shell
GET /?versions HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request parameters

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| prefix | Prefix to be matched for object keys; indicates the response only contains object keys with the specified prefix | string | No |
| delimiter | A character delimiter used to group object keys. Keys that contain identical paths between the prefix (or, if no prefix is specified, the beginning of the string) and the first delimiter are grouped and defined as a `Prefix` node under `CommonPrefixes`. The grouped object keys will no longer appear in the subsequent object list. For specific scenarios and usage, see the examples below | string | No |
| encoding-type | Specifies the encoding type of the returned value. Valid value: `url`, which means that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded as `%E8%85%BE%E8%AE%AF%E4%BA%91` | string | No |
| key-marker | Marks the starting object key. Object key entries will be returned in UTF-8 lexicographical order starting from the first object key after this marker | string | No |
| version-id-marker | Marks the starting version ID. Object version entries will be returned after this marker (excluded) | string | No |
| max-keys | Maximum number of entries returned at a time. Default value: 1,000; maximum value: 1,000 | integer | No |

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful query returns **application/xml** data which contains object versions in the bucket. For the response bodies of different scenarios, see the examples below.

```shell
<ListVersionsResult>
	<Name>string</Name>
	<Prefix>string</Prefix>
	<KeyMarker>string</KeyMarker>
	<VersionIdMarker>string</VersionIdMarker>
	<MaxKeys>integer</MaxKeys>
	<IsTruncated>boolean</IsTruncated>
	<Delimiter>string</Delimiter>
	<CommonPrefixes>
		<Prefix>string</Prefix>
	</CommonPrefixes>
	<CommonPrefixes>
		<Prefix>string</Prefix>
	</CommonPrefixes>
	<Version>
		<Key>string</Key>
		<VersionId>string</VersionId>
		<IsLatest>boolean</IsLatest>
		<LastModified>date</LastModified>
		<ETag>string</ETag>
		<Size>integer</Size>
		<StorageClass>Enum</StorageClass>
		<Owner>
			<ID>string</ID>
			<DisplayName>string</DisplayName>
		</Owner>
	</Version>
	<DeleteMarker>
		<Key>string</Key>
		<VersionId>string</VersionId>
		<IsLatest>boolean</IsLatest>
		<LastModified>date</LastModified>
		<Owner>
			<ID>string</ID>
			<DisplayName>string</DisplayName>
		</Owner>
	</DeleteMarker>
	<DeleteMarker>
		<Key>string</Key>
		<VersionId>string</VersionId>
		<IsLatest>boolean</IsLatest>
		<LastModified>date</LastModified>
		<Owner>
			<ID>string</ID>
			<DisplayName>string</DisplayName>
		</Owner>
	</DeleteMarker>
	<Version>
		<Key>string</Key>
		<VersionId>string</VersionId>
		<IsLatest>boolean</IsLatest>
		<LastModified>date</LastModified>
		<ETag>string</ETag>
		<Size>integer</Size>
		<StorageClass>Enum</StorageClass>
		<Owner>
			<ID>string</ID>
			<DisplayName>string</DisplayName>
		</Owner>
	</Version>
</ListVersionsResult>
```

The detailed nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ListVersionsResult | None | Contains all the results for the GET Bucket Object versions request  | Container |

**Container node `ListVersionsResult`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Name | ListVersionsResult | Bucket name in the format of `<BucketName-APPID>`, such as `examplebucket-1250000000` | string |
| EncodingType | ListVersionsResult | Encoding format, which corresponds to the `encoding-type` parameter in the request and will be returned only if the `encoding-type` parameter is specified in the request | string |
| Prefix | ListVersionsResult | Prefix to be matched for object keys, which corresponds to the `prefix` parameter in the request | string |
| KeyMarker | ListVersionsResult | Marker for the starting object key. Object version entries will be returned in UTF-8 lexicographical order starting from the first object version after this marker. This parameter corresponds to the `marker` parameter in the request | string |
| VersionIdMarker | ListVersionsResult | Marker for the starting version ID. Object version entries will be returned starting from the first object version after this marker. This parameter corresponds to the `version-id-marker` parameter in the request | string |
| MaxKeys | ListVersionsResult | Maximum number of entries returned in a single response, which corresponds to the `max-keys` parameter in the request | integer |
| Delimiter | ListVersionsResult | Delimiter, which corresponds to the `delimiter` parameter in the request and will be returned only if the `delimiter` parameter is specified in the request | string |
| IsTruncated | ListVersionsResult | Indicates whether the returned entry list is truncated. Boolean value: `true`, `false` | boolean |
| NextKeyMarker | ListVersionsResult | This node will be returned only if the returned list is truncated (i.e., the value of `IsTruncated` is `true`). The value of this parameter is the last object key in the current response and will be passed in as the `key-marker` parameter in the next request for subsequent entries | string |
| NextVersionIdMarker | ListVersionsResult | This node will be returned only if the returned list is truncated (i.e., the value of `IsTruncated` is `true`). The value of this parameter is the last object key in the current response and will be passed in as the `version-id-marker` parameter in the next request for subsequent entries | string |
| CommonPrefixes | ListVersionsResult | The identical paths between `prefix` (or, if no `prefix` is specified, the beginning) and the first `delimiter` are grouped and defined as a common prefix. This node will be returned only if the `delimiter` parameter is specified in the request | Container |
| Version | ListVersionsResult | An entry of object version | Container |
| DeleteMarker | ListVersionsResult | An entry of object delete marker | Container |

**Container node `ListVersionsResult.CommonPrefixes`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Prefix | ListVersionsResult.CommonPrefixes | A single common prefix | string |

**Container node `ListVersionsResult.Version`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Key | ListVersionsResult.Version | Object key | string |
| VersionId | ListVersionsResult.Version | Object version ID | string |
| IsLatest | ListVersionsResult.Version | Indicates whether the current version is the latest version of the object | boolean |
| LastModified | ListVersionsResult.Version | The last modified time in ISO8601 format of the current version, e.g. 2019-05-24T10:56:40Z | date |
| ETag | ListVersionsResult.Version | Entity tag of an object, which identifies the content of the object when it is created, and can be used to check whether the object content has changed during transit, e.g. `8e0b617ca298a564c3331da28dcb50df`. It does not necessarily return the MD5 value of the object, but varies depending on how the object is uploaded and encrypted | string |
| Size | ListVersionsResult.Version | Object size in byte | integer |
| StorageClass | ListVersionsResult.Version | Object storage class, such as `STANDARD_IA` and `ARCHIVE`. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | Enum |
| Owner | ListVersionsResult.Version | Object owner | Container |

**Container node `ListVersionsResult.Version.Owner`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ID | ListVersionsResult.Version.Owner | APPID of the object owner | string |
| DisplayName | ListVersionsResult.Version.Owner | Name of the object owner | string |

**Container node `ListVersionsResult.DeleteMarker`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Key | ListVersionsResult.DeleteMarker | Object key | string |
| VersionId | ListVersionsResult.DeleteMarker | Version ID of the object’s delete marker | string |
| IsLatest | ListVersionsResult.DeleteMarker | Indicates whether the deleted delete marker is the latest version of the object | boolean |
| LastModified | ListVersionsResult.DeleteMarker | The time in ISO8601 format that the delete marker is deleted, e.g. 2019-05-24T10:56:40Z | date |
| Owner | ListVersionsResult.DeleteMarker | Object owner | Container |

**Container node `ListVersionsResult.DeleteMarker.Owner`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ID | ListVersionsResult.DeleteMarker.Owner | APPID of the object owner | string |
| DisplayName | ListVersionsResult.DeleteMarker.Owner | Name of the object owner | string |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1. Versioning not enabled

#### Request

```shell
GET /?versions HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 15 Aug 2019 12:03:09 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565870589;1565877789&q-key-time=1565870589;1565877789&q-header-list=date;host&q-url-param-list=versions&q-signature=1d8fcb8522df7be9fa52d94cd79462f92eb3****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1262
Connection: close
Date: Thu, 15 Aug 2019 12:03:10 GMT
Server: tencent-cos
x-cos-request-id: NWQ1NTQ5ZmVfYjliYjBiMDlfMmFhNGZfY2Jm****

<ListVersionsResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix/>
	<KeyMarker/>
	<VersionIdMarker/>
	<MaxKeys>1000</MaxKeys>
	<IsTruncated>false</IsTruncated>
	<Version>
		<Key>example-object-1.jpg</Key>
		<VersionId/>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-15T12:03:10.000Z</LastModified>
		<ETag>&quot;0f0cd12c48979d1bf3f95255a36cb861&quot;</ETag>
		<Size>20</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<Version>
		<Key>example-object-2.jpg</Key>
		<VersionId/>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-15T12:03:09.000Z</LastModified>
		<ETag>&quot;51370fc64b79d0d3c7c609635be1c41f&quot;</ETag>
		<Size>20</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<Version>
		<Key>example-object-3.jpg</Key>
		<VersionId/>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-15T12:03:08.000Z</LastModified>
		<ETag>&quot;b2f1d893c5fde000ee8ea6eca18ed81f&quot;</ETag>
		<Size>20</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
</ListVersionsResult>
```

#### Example 2. Versioning enabled

#### Request

```shell
GET /?versions HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 15 Aug 2019 12:03:41 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565870621;1565877821&q-key-time=1565870621;1565877821&q-header-list=date;host&q-url-param-list=versions&q-signature=36400914186e87b3e88cc8049a79da5e3d79****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 3477
Connection: close
Date: Thu, 15 Aug 2019 12:03:41 GMT
Server: tencent-cos
x-cos-request-id: NWQ1NTRhMWRfODhjMjJhMDlfMWNkOF8xZTRm****

<ListVersionsResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix/>
	<KeyMarker/>
	<VersionIdMarker/>
	<MaxKeys>1000</MaxKeys>
	<IsTruncated>false</IsTruncated>
	<Version>
		<Key>example-object-1.jpg</Key>
		<VersionId>null</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-15T12:03:10.000Z</LastModified>
		<ETag>&quot;0f0cd12c48979d1bf3f95255a36cb861&quot;</ETag>
		<Size>20</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<DeleteMarker>
		<Key>example-object-2.jpg</Key>
		<VersionId>MTg0NDUxNzgyMDMwODg0NzI0Njc</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-15T12:03:41.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	<Version>
		<Key>example-object-2.jpg</Key>
		<VersionId>null</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-15T12:03:09.000Z</LastModified>
		<ETag>&quot;51370fc64b79d0d3c7c609635be1c41f&quot;</ETag>
		<Size>20</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<DeleteMarker>
		<Key>example-object-3.jpg</Key>
		<VersionId>MTg0NDUxNzgyMDMwODg0NzA1NzM</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-15T12:03:41.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	<Version>
		<Key>example-object-3.jpg</Key>
		<VersionId>MTg0NDUxNzgyMDMwODk5NTUxNzU</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-15T12:03:39.000Z</LastModified>
		<ETag>&quot;e5c7403f4ac3ace73477eb8b1fd183f7&quot;</ETag>
		<Size>30</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<Version>
		<Key>example-object-3.jpg</Key>
		<VersionId>null</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-15T12:03:08.000Z</LastModified>
		<ETag>&quot;b2f1d893c5fde000ee8ea6eca18ed81f&quot;</ETag>
		<Size>20</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<Version>
		<Key>example-object-4.jpg</Key>
		<VersionId>MTg0NDUxNzgyMDMwODg4OTI0MDc</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-15T12:03:41.000Z</LastModified>
		<ETag>&quot;c5c4d52f90ec328890953bbe4ae08230&quot;</ETag>
		<Size>30</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<Version>
		<Key>example-object-4.jpg</Key>
		<VersionId>MTg0NDUxNzgyMDMwODkyMTg2NjI</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-15T12:03:40.000Z</LastModified>
		<ETag>&quot;e9ec8bcb980d2e4d8526c346eb3b2585&quot;</ETag>
		<Size>20</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<Version>
		<Key>example-object-5.jpg</Key>
		<VersionId>MTg0NDUxNzgyMDMwODk4NTkzMzM</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-15T12:03:39.000Z</LastModified>
		<ETag>&quot;201669a14bdf051d8a9d6f9828d3f4c4&quot;</ETag>
		<Size>20</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
</ListVersionsResult>
```

#### Example 3. Specifying the `delimiter` parameter (listing objects and subdirectories in the root directory)

#### Request

```shell
GET /?versions&delimiter=%2F HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 16 Aug 2019 10:45:53 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565952353;1565959553&q-key-time=1565952353;1565959553&q-header-list=date;host&q-url-param-list=delimiter;versions&q-signature=c3130139bcac870247d1a070dbc8ee1c7ad5****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 2529
Connection: close
Date: Fri, 16 Aug 2019 10:45:53 GMT
Server: tencent-cos
x-cos-request-id: NWQ1Njg5NjFfNjFiMDJhMDlfMWE5ZV8yMDY4****

<ListVersionsResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix/>
	<KeyMarker/>
	<VersionIdMarker/>
	<MaxKeys>1000</MaxKeys>
	<IsTruncated>false</IsTruncated>
	<Delimiter>/</Delimiter>
	<CommonPrefixes>
		<Prefix>example-folder-1/</Prefix>
	</CommonPrefixes>
	<CommonPrefixes>
		<Prefix>example-folder-2/</Prefix>
	</CommonPrefixes>
	<Version>
		<Key>example-object-1.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNTU3NTk1Mjg</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-16T10:45:53.000Z</LastModified>
		<ETag>&quot;5d1143df07a17b23320d0da161e2819e&quot;</ETag>
		<Size>30</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<DeleteMarker>
		<Key>example-object-1.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNjE1OTcxMzM</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-16T10:45:47.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	<Version>
		<Key>example-object-1.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNjYzNzU0MjE</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-16T10:45:43.000Z</LastModified>
		<ETag>&quot;0f0cd12c48979d1bf3f95255a36cb861&quot;</ETag>
		<Size>20</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<DeleteMarker>
		<Key>example-object-2.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNTYzMDY3NzY</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-16T10:45:53.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	<Version>
		<Key>example-object-2.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNjI5OTc5OTU</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-16T10:45:46.000Z</LastModified>
		<ETag>&quot;574c289a7906c7d8fecef028216afeca&quot;</ETag>
		<Size>30</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<Version>
		<Key>example-object-2.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNjgyODc1OTY</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-16T10:45:41.000Z</LastModified>
		<ETag>&quot;51370fc64b79d0d3c7c609635be1c41f&quot;</ETag>
		<Size>20</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
</ListVersionsResult>
```

#### Example 4. Specifying the `prefix` and `delimiter` parameters (listing objects and subdirectories in the specified subdirectory)

#### Request

```shell
GET /?versions&prefix=example-folder-1%2F&delimiter=%2F HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 16 Aug 2019 10:45:53 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1565952353;1565959553&q-key-time=1565952353;1565959553&q-header-list=date;host&q-url-param-list=delimiter;prefix;versions&q-signature=6d7b99a4b379b5fefb8b903ee491bae63590****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 2682
Connection: close
Date: Fri, 16 Aug 2019 10:45:53 GMT
Server: tencent-cos
x-cos-request-id: NWQ1Njg5NjFfMzdiMDJhMDlfODA1NV8yMDI2****

<ListVersionsResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix>example-folder-1/</Prefix>
	<KeyMarker/>
	<VersionIdMarker/>
	<MaxKeys>1000</MaxKeys>
	<IsTruncated>false</IsTruncated>
	<Delimiter>/</Delimiter>
	<CommonPrefixes>
		<Prefix>example-folder-1/sub-folder-1/</Prefix>
	</CommonPrefixes>
	<CommonPrefixes>
		<Prefix>example-folder-1/sub-folder-2/</Prefix>
	</CommonPrefixes>
	<Version>
		<Key>example-folder-1/example-object-1.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNTY0MzYyNzE</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-16T10:45:53.000Z</LastModified>
		<ETag>&quot;1a54e134fda29e15d225cd226c4b49a3&quot;</ETag>
		<Size>47</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<DeleteMarker>
		<Key>example-folder-1/example-object-1.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNjE2MTE1NTI</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-16T10:45:47.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	<Version>
		<Key>example-folder-1/example-object-1.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNjcwNjI2MTU</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-16T10:45:42.000Z</LastModified>
		<ETag>&quot;f173c1199e3d3b53dd91223cae16fb42&quot;</ETag>
		<Size>37</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<DeleteMarker>
		<Key>example-folder-1/example-object-2.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNTYyOTQ1MDY</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-16T10:45:53.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	<Version>
		<Key>example-folder-1/example-object-2.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNjI3NTcyNzU</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-16T10:45:46.000Z</LastModified>
		<ETag>&quot;f43741c189c2142b257767bed5b4ce3a&quot;</ETag>
		<Size>47</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<Version>
		<Key>example-folder-1/example-object-2.jpg</Key>
		<VersionId>MTg0NDUxNzgxMjEzNjgwNjgwNDk</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-16T10:45:41.000Z</LastModified>
		<ETag>&quot;c9d28698978bb6fef6c1ed1c439a17d3&quot;</ETag>
		<Size>37</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
</ListVersionsResult>
```

#### Example 5. Getting the first list of entries in case of pagination

#### Request

```shell
GET /?versions HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 23 Aug 2019 11:31:31 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1566559891;1566567091&q-key-time=1566559891;1566567091&q-header-list=date;host&q-url-param-list=versions&q-signature=2b146233465c2164c60e0e0b2385f5386a61****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 372125
Connection: close
Date: Fri, 23 Aug 2019 11:31:32 GMT
Server: tencent-cos
x-cos-request-id: NWQ1ZmNlOTRfMTljMDJhMDlfNTg5OV8yZWYz****

<ListVersionsResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix/>
	<KeyMarker/>
	<VersionIdMarker/>
	<MaxKeys>1000</MaxKeys>
	<IsTruncated>true</IsTruncated>
	<NextKeyMarker>example-object-0135.jpg</NextKeyMarker>
	<NextVersionIdMarker>MTg0NDUxNzc1MTM4MjM0ODYyNjQ</NextVersionIdMarker>
	<Version>
		<Key>example-object-0001.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4Mjg1NzI5Mjc</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-23T11:31:20.000Z</LastModified>
		<ETag>&quot;3dd9c0ec8b6669abec786e52b64e0497&quot;</ETag>
		<Size>36</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<DeleteMarker>
		<Key>example-object-0002.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MjY5NDY2MzQ</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-23T11:31:22.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	<Version>
		<Key>example-object-0002.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MjgzMDg3OTE</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:21.000Z</LastModified>
		<ETag>&quot;626f60ee8f3eb987342554379d63259f&quot;</ETag>
		<Size>36</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	...
	<DeleteMarker>
		<Key>example-object-0004.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MjcwNjg2Mzc</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:22.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	...
	<DeleteMarker>
		<Key>example-object-0135.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MjA2NTk1MTc</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:28.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	...
	<Version>
		<Key>example-object-0135.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MjM0ODYyNjQ</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:26.000Z</LastModified>
		<ETag>&quot;56d3a714c81ba76baa6a0004126a2718&quot;</ETag>
		<Size>36</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
</ListVersionsResult>
```

#### Example 6. Getting subsequent entry lists in case of pagination (by using the `key-marker` and `version-id-marker` request parameters)

#### Request

```shell
GET /?versions&key-marker=example-object-0135.jpg&version-id-marker=MTg0NDUxNzc1MTM4MjM0ODYyNjQ HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 23 Aug 2019 11:32:56 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1566559976;1566567176&q-key-time=1566559976;1566567176&q-header-list=date;host&q-url-param-list=key-marker;version-id-marker;versions&q-signature=5b0787a354752f3161c75d014b75d9f2bd68****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 8358
Connection: close
Date: Fri, 23 Aug 2019 11:32:56 GMT
Server: tencent-cos
x-cos-request-id: NWQ1ZmNlZThfNjFiMDJhMDlfYTgwOF8yZjIw****

<ListVersionsResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix/>
	<KeyMarker>example-object-0135.jpg</KeyMarker>
	<VersionIdMarker>MTg0NDUxNzc1MTM4MjM0ODYyNjQ</VersionIdMarker>
	<MaxKeys>1000</MaxKeys>
	<IsTruncated>false</IsTruncated>
	<Version>
		<Key>example-object-0135.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MjQ4MDkyNjk</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:24.000Z</LastModified>
		<ETag>&quot;5dd4f1fb98a2a6d74c8482f2856ece6b&quot;</ETag>
		<Size>36</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<Version>
		<Key>example-object-0135.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MjYwOTQ5MTk</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:23.000Z</LastModified>
		<ETag>&quot;91e59eed612971f0e00ac483bf5c7329&quot;</ETag>
		<Size>36</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	...
	<DeleteMarker>
		<Key>example-object-0136.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MTg1MjA4MDA</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-23T11:31:31.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	...
	<DeleteMarker>
		<Key>example-object-0136.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MjA2OTA5MDg</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:28.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	...
	<DeleteMarker>
		<Key>example-object-0137.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MjA2OTQ0MzA</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:28.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	...
	<Version>
		<Key>example-object-0137.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4Mjc1MjQ3OTY</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:22.000Z</LastModified>
		<ETag>&quot;9022b9bf1b1503902d46cbe976c94eea&quot;</ETag>
		<Size>36</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
</ListVersionsResult>
```

#### Example 7. Specifying the starting object using `key-marker`

#### Request

```shell
GET /?versions&key-marker=example-object-0135.jpg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 23 Aug 2019 11:32:56 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1566559976;1566567176&q-key-time=1566559976;1566567176&q-header-list=date;host&q-url-param-list=key-marker;versions&q-signature=8b601589aae7ffdb2211694dde4ad73c9634****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 7111
Connection: close
Date: Fri, 23 Aug 2019 11:32:56 GMT
Server: tencent-cos
x-cos-request-id: NWQ1ZmNlZThfNjFiMDJhMDlfYTgwY18yZjRi****

<ListVersionsResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix/>
	<KeyMarker>example-object-0135.jpg</KeyMarker>
	<VersionIdMarker/>
	<MaxKeys>1000</MaxKeys>
	<IsTruncated>false</IsTruncated>
	<DeleteMarker>
		<Key>example-object-0136.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MTg1MjA4MDA</VersionId>
		<IsLatest>true</IsLatest>
		<LastModified>2019-08-23T11:31:31.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	<Version>
		<Key>example-object-0136.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MTg5NjQzNDQ</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:30.000Z</LastModified>
		<ETag>&quot;20f730cd4cab72c0edcbf37c40f9dabe&quot;</ETag>
		<Size>36</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<Version>
		<Key>example-object-0136.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MTk3MDAwMDY</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:29.000Z</LastModified>
		<ETag>&quot;339baa9b8d4450e71fc268aaa5fa250e&quot;</ETag>
		<Size>36</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
	<DeleteMarker>
		<Key>example-object-0136.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MjA2OTA5MDg</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:28.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	...
	<DeleteMarker>
		<Key>example-object-0137.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4MjA2OTQ0MzA</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:28.000Z</LastModified>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</DeleteMarker>
	...
	<Version>
		<Key>example-object-0137.jpg</Key>
		<VersionId>MTg0NDUxNzc1MTM4Mjc1MjQ3OTY</VersionId>
		<IsLatest>false</IsLatest>
		<LastModified>2019-08-23T11:31:22.000Z</LastModified>
		<ETag>&quot;9022b9bf1b1503902d46cbe976c94eea&quot;</ETag>
		<Size>36</Size>
		<StorageClass>STANDARD</StorageClass>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
	</Version>
</ListVersionsResult>
```
