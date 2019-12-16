## Description

The `GET Bucket` request is equivalent to the `List Object` request and can be used to list some or all of the objects in a bucket. To make this request, you need to have the permission to read the bucket.

> If you upload an object to the bucket and immediately call the `GET Bucket` API, due to the eventual consistency characteristic of this API, the response may not include the just uploaded object.

## Request

#### Sample Request

```shell
GET / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Parameters

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| prefix | Matching prefix for object keys, which sets that the response will only contain object keys with the specified prefix | string | No |
| delimiter | A character delimiter used to group object keys. The identical paths between `prefix` or, if no `prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a `Prefix` node under `CommonPrefixes`. The grouped object keys will no longer appear in the subsequent object list. For specific scenarios and usage, see the examples below | string | No |
| encoding-type | Specifies the encoding type of the returned value. Valid value: `url`, which means that the returned object keys are URL-encoded (percent-encoded) values. For example, "腾讯云" will be encoded as `%E8%85%BE%E8%AE%AF%E4%BA%91` | string | No |
| marker | Marker for the starting object key. Object key entries will be returned in UTF-8 lexicographical order starting from the first object key after the marker | string | No |
| max-keys | Maximum number of entries returned at a time. Default value: 1,000; maximum value: 1,000 | integer | No |

#### Request Headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request Body

This API does not have a request body.

## Response

#### Response Headers

In addition to common response headers, this API returns the following response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Name | Description | Type |
| --- | --- | --- |
| x-cos-bucket-region | Bucket region such as `ap-beijing`, `ap-hongkong`, and `eu-frankfurt`. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | Enum |

#### Response Body

A successful query returns **application/xml** data which contain information on the objects in the bucket. For response bodies in different scenarios, see the examples below.

```shell
<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
	<Name>string</Name>
	<Prefix>string</Prefix>
	<Marker/>
	<MaxKeys>integer</MaxKeys>
	<Delimiter>string</Delimiter>
	<IsTruncated>boolean</IsTruncated>
	<CommonPrefixes>
		<Prefix>string</Prefix>
	</CommonPrefixes>
	<CommonPrefixes>
		<Prefix>string</Prefix>
	</CommonPrefixes>
	<Contents>
		<Key>string</Key>
		<LastModified>date</LastModified>
		<ETag>string</ETag>
		<Size>integer</Size>
		<Owner>
			<ID>string</ID>
			<DisplayName>string</DisplayName>
		</Owner>
		<StorageClass>Enum</StorageClass>
	</Contents>
	<Contents>
		<Key>string</Key>
		<LastModified>date</LastModified>
		<ETag>string</ETag>
		<Size>integer</Size>
		<Owner>
			<ID>string</ID>
			<DisplayName>string</DisplayName>
		</Owner>
		<StorageClass>Enum</StorageClass>
	</Contents>
</ListBucketResult>
```

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ListBucketResult | None | Stores the result of the `GET Bucket` request | Container |

**Content of the Container node `ListBucketResult`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Name | ListBucketResult | Bucket name in the format of `<BucketName-APPID>`, such as `examplebucket-1250000000` | string |
| EncodingType | ListBucketResult | Encoding format, which corresponds to the `encoding-type` parameter in the request and will be returned only if the `encoding-type` parameter is specified in the request | string |
| Prefix | ListBucketResult | Matching prefix for object keys, which corresponds to the `prefix` parameter in the request | string |
| Marker | ListBucketResult | Marker for the starting object key. Object key entries will be returned in UTF-8 lexicographical order starting from the first object key after the marker. This parameter corresponds to the `marker` parameter in the request | string |
| MaxKeys | ListBucketResult | Maximum number of entries returned in a single response, which corresponds to the `max-keys` parameter in the request | integer |
| Delimiter | ListBucketResult | Delimiter, which corresponds to the `delimiter` parameter in the request and will be returned only if the `delimiter` parameter is specified in the request | string |
| IsTruncated | ListBucketResult | Whether the returned list is truncated, which is a boolean value. Valid values: `true`, `false` | boolean |
| NextMarker | ListBucketResult | This node will be returned only if the returned list is truncated (i.e., the value of `IsTruncated` is `true`). The value of this parameter is the last object key in the current response and will be passed in as the `marker` parameter in the next request if you need to request subsequent entries | string |
| CommonPrefixes | ListBucketResult | The identical paths between `prefix` or, if no `prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix. This node will be returned only if the `delimiter` parameter is specified in the request | Container |
| Contents | ListBucketResult | Object entries | Container |

**Content of the Container node `CommonPrefixes`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Prefix | ListBucketResult.CommonPrefixes | A single common prefix | string |

**Content of the Container node `Contents`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Key | ListBucketResult.Contents | Object key | string |
| LastModified | ListBucketResult.Contents | Last modified time of an object in ISO8601 format, such as `2019-05-24T10:56:40Z` | date |
| ETag | ListBucketResult.Contents | Hash value calculated based on the file content | string |
| Size | ListBucketResult.Contents | Object size in bytes | integer |
| Owner | ListBucketResult.Contents | Bucket owner information | Container |
| StorageClass | ListBucketResult.Contents | Object storage class, such as `STANDARD_IA` and `ARCHIVE`. For enumerated values, see [Storage Type](https://intl.cloud.tencent.com/document/product/436/30925) | Enum |

**Content of the Container node `Contents.Owner`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ID | ListBucketResult.Contents.Owner | Bucket APPID | string |
| DisplayName | ListBucketResult.Contents.Owner | Object owner name | string |

#### Error Codes

There is no special error message for this API. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1. Basic example

#### Request

```shell
GET / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 27 May 2019 11:26:14 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558956374;1558963574&q-key-time=1558956374;1558963574&q-header-list=date;host&q-url-param-list=&q-signature=9a2596f2a4dc0cf5eaa9019959a8275afd4b****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1517
Connection: close
Date: Mon, 27 May 2019 11:26:15 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWNlYmM5NTdfZjI4NWQ2NF81ZmMwX2Q5N2E1****

<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix/>
	<Marker/>
	<MaxKeys>1000</MaxKeys>
	<IsTruncated>false</IsTruncated>
	<Contents>
		<Key>example-folder-1/example-object-1.jpg</Key>
		<LastModified>2019-05-27T11:26:14.000Z</LastModified>
		<ETag>&quot;f173c1199e3d3b53dd91223cae16fb42&quot;</ETag>
		<Size>37</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
	<Contents>
		<Key>example-folder-1/sub-folder-1/example-object-1.jpg</Key>
		<LastModified>2019-05-27T11:26:14.000Z</LastModified>
		<ETag>&quot;bef7bb344812457ffc72f7bf99dabfdd&quot;</ETag>
		<Size>50</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
	<Contents>
		<Key>example-object-1.jpg</Key>
		<LastModified>2019-05-27T11:26:14.000Z</LastModified>
		<ETag>&quot;0f0cd12c48979d1bf3f95255a36cb861&quot;</ETag>
		<Size>20</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
	<Contents>
		<Key>example-object-2.jpg</Key>
		<LastModified>2019-05-27T11:26:14.000Z</LastModified>
		<ETag>&quot;51370fc64b79d0d3c7c609635be1c41f&quot;</ETag>
		<Size>20</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
</ListBucketResult>
```

#### Example 2. Specifying the `delimiter` parameter (listing objects and subdirectories in the root directory)

#### Request

```shell
GET /?delimiter=%2F HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 27 May 2019 11:26:15 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558956375;1558963575&q-key-time=1558956375;1558963575&q-header-list=date;host&q-url-param-list=delimiter&q-signature=d409a7025e1633c162213ab34fbf7e87ef50****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1008
Connection: close
Date: Mon, 27 May 2019 11:26:15 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWNlYmM5NTdfNzViMDJhMDlfNDkzNF9kMTQ3****

<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix/>
	<Marker/>
	<MaxKeys>1000</MaxKeys>
	<Delimiter>/</Delimiter>
	<IsTruncated>false</IsTruncated>
	<CommonPrefixes>
		<Prefix>example-folder-1/</Prefix>
	</CommonPrefixes>
	<CommonPrefixes>
		<Prefix>example-folder-2/</Prefix>
	</CommonPrefixes>
	<Contents>
		<Key>example-object-1.jpg</Key>
		<LastModified>2019-05-27T11:26:14.000Z</LastModified>
		<ETag>&quot;0f0cd12c48979d1bf3f95255a36cb861&quot;</ETag>
		<Size>20</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
	<Contents>
		<Key>example-object-2.jpg</Key>
		<LastModified>2019-05-27T11:26:14.000Z</LastModified>
		<ETag>&quot;51370fc64b79d0d3c7c609635be1c41f&quot;</ETag>
		<Size>20</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
</ListBucketResult>
```

#### Example 3. Specifying the `prefix` and `delimiter` parameters (listing objects and subdirectories in the specified subdirectory)

#### Request

```shell
GET /?prefix=example-folder-1%2F&delimiter=%2F HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 27 May 2019 11:26:15 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558956375;1558963575&q-key-time=1558956375;1558963575&q-header-list=date;host&q-url-param-list=delimiter;prefix&q-signature=f4a0854aa3a3b9b1699e1989d675297867f3****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1093
Connection: close
Date: Mon, 27 May 2019 11:26:15 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWNlYmM5NTdfNDQyODVkNjRfNTIwYl82ZGQy****

<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix>example-folder-1/</Prefix>
	<Marker/>
	<MaxKeys>1000</MaxKeys>
	<Delimiter>/</Delimiter>
	<IsTruncated>false</IsTruncated>
	<CommonPrefixes>
		<Prefix>example-folder-1/sub-folder-1/</Prefix>
	</CommonPrefixes>
	<CommonPrefixes>
		<Prefix>example-folder-1/sub-folder-2/</Prefix>
	</CommonPrefixes>
	<Contents>
		<Key>example-folder-1/example-object-1.jpg</Key>
		<LastModified>2019-05-27T11:26:14.000Z</LastModified>
		<ETag>&quot;f173c1199e3d3b53dd91223cae16fb42&quot;</ETag>
		<Size>37</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
	<Contents>
		<Key>example-folder-1/example-object-2.jpg</Key>
		<LastModified>2019-05-27T11:26:15.000Z</LastModified>
		<ETag>&quot;c9d28698978bb6fef6c1ed1c439a17d3&quot;</ETag>
		<Size>37</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
</ListBucketResult>
```

#### Example 4. Getting the first list of entries when the total number of matching entries exceeds the maximum number of entries allowed for a single response

#### Request

```shell
GET / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 27 May 2019 11:07:30 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558955250;1558962450&q-key-time=1558955250;1558962450&q-header-list=date;host&q-url-param-list=&q-signature=4d515ac9853b6e341cf5432c0d57faebe165****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 321247
Connection: close
Date: Mon, 27 May 2019 11:07:30 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWNlYmM0ZjJfZDcyNzVkNjRfNjQ5OV9lNzdk****

<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix/>
	<Marker/>
	<MaxKeys>1000</MaxKeys>
	<IsTruncated>true</IsTruncated>
	<NextMarker>example-object-1000.jpg</NextMarker>
	<Contents>
		<Key>example-object-0001.jpg</Key>
		<LastModified>2019-05-27T11:07:29.000Z</LastModified>
		<ETag>&quot;f49ffbb2dd542ef6843135d66ec97855&quot;</ETag>
		<Size>23</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
	<Contents>
		<Key>example-object-0002.jpg</Key>
		<LastModified>2019-05-27T11:07:29.000Z</LastModified>
		<ETag>&quot;ab1694353a29f925ca67d2956ca14b37&quot;</ETag>
		<Size>23</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
	...
	<Contents>
		<Key>example-object-1000.jpg</Key>
		<LastModified>2019-05-27T11:07:29.000Z</LastModified>
		<ETag>&quot;b76c104f431e06bbfbbe7a97c87aecde&quot;</ETag>
		<Size>23</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
</ListBucketResult>
```

#### Example 5. Getting the second list of entries when the total number of matching entries exceeds the maximum number of entries allowed for a single response

#### Request

```shell
GET /?marker=example-object-1000.jpg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Mon, 27 May 2019 11:08:36 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558955316;1558962516&q-key-time=1558955316;1558962516&q-header-list=date;host&q-url-param-list=marker&q-signature=f9ed03c3944926d06281c607d3314678909e****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1834
Connection: close
Date: Mon, 27 May 2019 11:08:36 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWNlYmM1MzRfZmVhODBiMDlfMmViNjRfZDQw****

<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
	<Name>examplebucket-1250000000</Name>
	<Prefix/>
	<Marker>example-object-1000.jpg</Marker>
	<MaxKeys>1000</MaxKeys>
	<IsTruncated>false</IsTruncated>
	<Contents>
		<Key>example-object-1001.jpg</Key>
		<LastModified>2019-05-27T11:07:29.000Z</LastModified>
		<ETag>&quot;8256f8fc3eb5b11452aa4915a011aa81&quot;</ETag>
		<Size>23</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
	<Contents>
		<Key>example-object-1002.jpg</Key>
		<LastModified>2019-05-27T11:07:29.000Z</LastModified>
		<ETag>&quot;c7ac76bed75b99a3a7169eb3db00389d&quot;</ETag>
		<Size>23</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
	...
	<Contents>
		<Key>example-object-1005.jpg</Key>
		<LastModified>2019-05-27T11:07:29.000Z</LastModified>
		<ETag>&quot;47176b4ca0078855bfd47e30a9c70a61&quot;</ETag>
		<Size>23</Size>
		<Owner>
			<ID>1250000000</ID>
			<DisplayName>1250000000</DisplayName>
		</Owner>
		<StorageClass>STANDARD</StorageClass>
	</Contents>
</ListBucketResult>
```
