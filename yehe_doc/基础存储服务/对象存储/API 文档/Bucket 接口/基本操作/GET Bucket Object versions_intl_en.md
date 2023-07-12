## Overview

This API is used to get all objects in a bucket and their historical version information. You can also filter certain objects and their version information by specifying relevant parameters. To call this API, you need to have permission to read the bucket.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetBucketObjectVersions&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>

## Request

#### Sample request

```shell
GET /?versions HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

| Header | Description | Type | Required |
| --- | --- | --- | --- |
| prefix | Matching prefix for object keys. The response will contain only object keys with the specified prefix. | string | No |
| delimiter | A character delimiter used to group object keys. Keys that contain identical paths between the prefix (or, if no prefix is specified, the beginning of the string) and the first delimiter are grouped and defined as a `Prefix` node under `CommonPrefixes`. The grouped object keys will no longer appear in the subsequent object list. For specific scenarios and usage, see the examples below | string | No |
| encoding-type | Encoding type of the returned value. Valid value: `url`, meaning that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded to `%E8%85%BE%E8%AE%AF%E4%BA%91`. | string | No |
| key-marker | Marker for the starting object key. Object version entries after this marker will be returned in UTF-8 lexicographical order. | string | No |
| version-id-marker | Marker for the starting version ID. Object version entries after this marker will be returned. If `NextVersionIdMarker` is empty in the last `ListVersionsResult` response, leave this parameter empty. | string | No |
| max-keys | The maximum number (up to 1,000) of keys returned in a response. Defaults to `1000`. <br>**Note**: This parameter limits the maximum number of keys (the sum of `CommonPrefixes`, `Version`, and `DeleteMarker’) COS can return in each `ListVersionsResult` response. If not all objects are listed in a single response, COS will return the `NextKeyMarker` and `NextVersionIdMarker` nodes, the values of which can be used to specify `key-marker` and `version-id-marker`, respectively, so that the remaining versions can be listed in your next request. | integer | No |

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful query returns **application/xml** data, which contains information about object versions in the bucket. For the response bodies of different scenarios, see the examples below.
```xml
<ListVersionsResult>
		<EncodingType>string</EncodingType>
		<Name>string</Name>
		<Prefix>string</Prefix>
		<KeyMarker>string</KeyMarker>
		<VersionIdMarker>string</VersionIdMarker>
		<MaxKeys>integer</MaxKeys>
		<IsTruncated>boolean</IsTruncated>
		<NextKeyMarker>string</NextKeyMarker>
		<NextVersionIdMarker>string</NextVersionIdMarker>
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
			<StorageTier>Enum</StorageTier>
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
		<Version>
			<Key>string</Key>
			<VersionId>string</VersionId>
			<IsLatest>boolean</IsLatest>
			<LastModified>date</LastModified>
			<ETag>string</ETag>
			<Size>integer</Size>
			<StorageClass>Enum</StorageClass>
			<StorageTier>Enum</StorageTier>
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
</ListVersionsResult>
```


The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ListVersionsResult | None | Stores the result of `GET Bucket Object versions`. | Container |

**Content of `ListVersionsResult`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| EncodingType | ListVersionsResult | Encoding type, which corresponds to the `encoding-type` parameter in the request. This node will be returned only when the `encoding-type` parameter is specified in the request. | string |
| Name | ListVersionsResult | Bucket name, formatted as `<BucketName-APPID>`, such as `examplebucket-1250000000` | string |
| Prefix | ListVersionsResult | Matching prefix to filter object keys. This node corresponds to the `Prefix` parameter in the request. | string |
| KeyMarker | ListVersionsResult | Marks the object key to start with. Object version entries after the marker will be returned in UTF-8 lexicographical order. This node corresponds to the `key-marker` parameter in the request. | string |
| VersionIdMarker | ListVersionsResult | Marks the version ID to start with. Object version entries after the marker will be returned. This node corresponds to the `version-id-marker` parameter in the request. | string |
| MaxKeys | ListVersionsResult | Maximum number of keys returned in a single response. This node corresponds to the `max-keys` parameter in the request. | integer |
| IsTruncated | ListVersionsResult | Indicates whether the returned list is truncated. Valid values: `true`, `false` | boolean |
| NextKeyMarker | ListVersionsResult | This node will be returned only if the returned list is truncated (i.e., the value of `IsTruncated` is `true`). The value of this node is the last object key in the current response. If you need to request subsequent entries, the value can be passed in as the value of the `key-marker` parameter in the next request. | string |
| NextVersionIdMarker | ListVersionsResult | This node will be returned only if the returned list is truncated (i.e., the value of  `IsTruncated` is `true`). The value of this node is the last version ID in the current response. If you need to request subsequent entries, the value can be passed in as the value of the `version-id-marker` parameter in the next request. If this node is left empty, `version-id-marker` in the next request should also be left empty. | string |
| Delimiter | ListVersionsResult | Delimiter, which corresponds to the `delimiter` parameter in the request and will be returned only if the `delimiter` parameter is specified in the request. | string |
| CommonPrefixes | ListVersionsResult | The identical paths between the prefix (or, if no prefix is specified, the beginning of the string) and the first delimiter are grouped and defined as a common prefix. This node will be returned only if the `delimiter` parameter is specified in the request. | Container |
| Version | ListVersionsResult | Object version entry | Container |
| DeleteMarker | ListVersionsResult | Object delete marker entry | Container |

**Content of `CommonPrefixes`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Prefix | ListVersionsResult.CommonPrefixes | A single common prefix | string |

**Content of `Version`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Key | ListVersionsResult.Version | Object key | string |
| VersionId | ListVersionsResult.Version | Version ID of the object <br><li>If versioning is disabled, the value of this node is an empty string. <li>If versioning is enabled, the value of this node is `null` for an object uploaded before you enable versioning. <li>If versioning is suspended, the value of this node is `null` for an object uploaded after you suspend versioning. Note that each object can have only one object version whose ID is `null`. | string |
| IsLatest | ListVersionsResult.Version | Indicates whether the current version is the latest one of the object. | boolean |
| LastModified | ListVersionsResult.Version | Last modified time of the current version, in ISO 8601 format (for example, 2019-05-24T10:56:40Z) | date |
| ETag | ListBucketResult.Contents | Entity tag of the object. It indicates the content of the object when it is created and can be used to verify whether the object content is changed. <br>Example: "8e0b617ca298a564c3331da28dcb50df"<br>The value of `ETag` is not necessarily the MD5 checksum of the object. The value will be different if the uploaded object is encrypted. | string |
| Size | ListVersionsResult.Version | Object size, in bytes | integer |
| StorageClass | ListVersionsResult.Version | Object storage class, such as `STANDARD_IA` or `ARCHIVE`. For enumerated values, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | Enum |
| StorageTier | ListVersionsResult.Version | Access tier (for INTELLIGENT TIERING) the object is currently stored in. Enumerated values: `FREQUENT`, `INFREQUENT`. This node is returned only when `StorageClass` is set to `INTELLIGENT_TIERING`. | Enum |
| Owner | ListVersionsResult.Version | Information of the object owner | Container |

**Content of `Version.Owner`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ID | ListVersionsResult.Version.Owner | `APPID` of the object owner | string |
| DisplayName | ListVersionsResult.Version.Owner | Name of the object owner | string |

**Content of `DeleteMarker`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Key | ListVersionsResult.DeleteMarker | Object key | string |
| VersionId | ListVersionsResult.DeleteMarker | Version ID of the object delete marker | string |
| IsLatest | ListVersionsResult.DeleteMarker | Indicates whether the current delete marker version is the latest one of the object. | boolean |
| LastModified | ListVersionsResult.DeleteMarker | Last modified time of the current delete marker, in ISO 8601 format (for example, 2019-05-24T10:56:40Z) | date |
| Owner | ListVersionsResult.DeleteMarker | Information of the object owner | Container |

**Content of `DeleteMarker.Owner`**:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ID | ListVersionsResult.DeleteMarker.Owner | `APPID` of the object owner | string |
| DisplayName | ListVersionsResult.DeleteMarker.Owner | Name of the object owner | string |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1: versioning not enabled

#### Request

```shell
GET /?versions HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 10 Dec 2020 03:35:34 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607571334;1607578534&q-key-time=1607571334;1607578534&q-header-list=date;host&q-url-param-list=versions&q-signature=1c39a124c84ec844e56cb1031a511568c16f****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 952
Connection: close
Date: Thu, 10 Dec 2020 03:35:34 GMT
Server: tencent-cos
x-cos-request-id: NWZkMTk3ODZfZDUyNzVkNjRfNDgxYl8xNjU5****



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
		        <LastModified>2020-12-10T03:35:24.000Z</LastModified>
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
		        <LastModified>2020-12-10T03:35:24.000Z</LastModified>
		        <ETag>&quot;dcffaafe67632b2bd2dd0b9456eafca7&quot;</ETag>
		        <Size>23</Size>
		        <StorageClass>INTELLIGENT_TIERING</StorageClass>
		        <StorageTier>FREQUENT</StorageTier>
		        <Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
</ListVersionsResult>
```

#### Example 2. Uploading an object and then enabling versioning, making its version ID `null` (a continuity of example 1)

#### Request

```shell
GET /?versions HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 10 Dec 2020 03:36:05 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607571365;1607578565&q-key-time=1607571365;1607578565&q-header-list=date;host&q-url-param-list=versions&q-signature=569318dd515c682db22c704d61314156e790****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 2070
Connection: close
Date: Thu, 10 Dec 2020 03:36:05 GMT
Server: tencent-cos
x-cos-request-id: NWZkMTk3YTVfYjFiODJhMDlfNTg0MDZfMTdj****



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
		        <LastModified>2020-12-10T03:35:24.000Z</LastModified>
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
		        <VersionId>MTg0NDUxMzY1MDIzNjQ3NTcwMDk</VersionId>
		        <IsLatest>true</IsLatest>
		        <LastModified>2020-12-10T03:35:44.000Z</LastModified>
		        <ETag>&quot;51ffadb19b3bf062ecd0c6f044a4d4ce&quot;</ETag>
		        <Size>23</Size>
		        <StorageClass>STANDARD_IA</StorageClass>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
		    <Version>
		        <Key>example-object-2.jpg</Key>
		        <VersionId>null</VersionId>
		        <IsLatest>false</IsLatest>
		        <LastModified>2020-12-10T03:35:24.000Z</LastModified>
		        <ETag>&quot;dcffaafe67632b2bd2dd0b9456eafca7&quot;</ETag>
		        <Size>23</Size>
		        <StorageClass>INTELLIGENT_TIERING</StorageClass>
		        <StorageTier>FREQUENT</StorageTier>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
		    <DeleteMarker>
		        <Key>example-object-3.jpg</Key>
		        <VersionId>MTg0NDUxMzY1MDIzNTQ1ODM2NjE</VersionId>
		        <IsLatest>true</IsLatest>
		        <LastModified>2020-12-10T03:35:54.000Z</LastModified>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </DeleteMarker>
		    <Version>
		        <Key>example-object-3.jpg</Key>
		        <VersionId>MTg0NDUxMzY1MDIzNjQ3NjM2MDY</VersionId>
		        <IsLatest>false</IsLatest>
		        <LastModified>2020-12-10T03:35:44.000Z</LastModified>
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

#### Example 3. Suspending versioning and then uploading an object, making its version ID `null` (each object can have only one object version whose ID is `null`) (a continuity of example 2)

#### Request

```shell
GET /?versions HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 10 Dec 2020 03:36:25 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607571385;1607578585&q-key-time=1607571385;1607578585&q-header-list=date;host&q-url-param-list=versions&q-signature=a42ed543ef094e42c8159d8788c509933f20****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 2396
Connection: close
Date: Thu, 10 Dec 2020 03:36:25 GMT
Server: tencent-cos
x-cos-request-id: NWZkMTk3YjlfNDhhOTBiMDlfMTYzNTZfMTIw****



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
		        <LastModified>2020-12-10T03:35:24.000Z</LastModified>
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
		        <VersionId>null</VersionId>
		        <IsLatest>true</IsLatest>
		        <LastModified>2020-12-10T03:36:15.000Z</LastModified>
		        <ETag>&quot;51ffadb19b3bf062ecd0c6f044a4d4ce&quot;</ETag>
		        <Size>23</Size>
		        <StorageClass>STANDARD</StorageClass>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
		    <Version>
		        <Key>example-object-2.jpg</Key>
		        <VersionId>MTg0NDUxMzY1MDIzNjQ3NTcwMDk</VersionId>
		        <IsLatest>false</IsLatest>
		        <LastModified>2020-12-10T03:35:44.000Z</LastModified>
		        <ETag>&quot;51ffadb19b3bf062ecd0c6f044a4d4ce&quot;</ETag>
		        <Size>23</Size>
		        <StorageClass>STANDARD_IA</StorageClass>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
		    <Version>
		        <Key>example-object-3.jpg</Key>
		        <VersionId>null</VersionId>
		        <IsLatest>true</IsLatest>
		        <LastModified>2020-12-10T03:36:15.000Z</LastModified>
		        <ETag>&quot;b2f1d893c5fde000ee8ea6eca18ed81f&quot;</ETag>
		        <Size>20</Size>
		        <StorageClass>STANDARD</StorageClass>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
		    <DeleteMarker>
		        <Key>example-object-3.jpg</Key>
		        <VersionId>MTg0NDUxMzY1MDIzNTQ1ODM2NjE</VersionId>
		        <IsLatest>false</IsLatest>
		        <LastModified>2020-12-10T03:35:54.000Z</LastModified>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </DeleteMarker>
		    <Version>
		        <Key>example-object-3.jpg</Key>
		        <VersionId>MTg0NDUxMzY1MDIzNjQ3NjM2MDY</VersionId>
		        <IsLatest>false</IsLatest>
		        <LastModified>2020-12-10T03:35:44.000Z</LastModified>
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

#### Example 4. Specifying the `encoding-type` parameter (object keys are URL-encoded)

#### Request

```shell
GET /?versions&encoding-type=url HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 10 Dec 2020 04:54:22 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607576062;1607583262&q-key-time=1607576062;1607583262&q-header-list=date;host&q-url-param-list=encoding-type;versions&q-signature=9dd5519032837d42fd3bf89fcdeed3889e7c****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 2167
Connection: close
Date: Thu, 10 Dec 2020 04:54:22 GMT
Server: tencent-cos
x-cos-request-id: NWZkMWE5ZmVfZTdjODJhMDlfMzgxZl8xMzQ1****



<ListVersionsResult>
		    <EncodingType>url</EncodingType>
		    <Name>examplebucket-1250000000</Name>
		    <Prefix/>
		    <KeyMarker/>
		    <VersionIdMarker/>
		    <MaxKeys>1000</MaxKeys>
		    <IsTruncated>false</IsTruncated>
		    <Version>
		        <Key>Tencent%20Cloud.jpg</Key>
		        <VersionId>MTg0NDUxMzY0OTc2NjcxNzE4NjA</VersionId>
		        <IsLatest>true</IsLatest>
		        <LastModified>2020-12-10T04:54:02.000Z</LastModified>
		        <ETag>&quot;ee8de918d05640145b18f70f4c3aa602&quot;</ETag>
		        <Size>16</Size>
		        <StorageClass>STANDARD</StorageClass>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
		    <DeleteMarker>
		        <Key>%E7%85%A7%E7%89%87/2020%E5%B9%B4/IMG0001.jpg</Key>
		        <VersionId>MTg0NDUxMzY0OTc2NTY5MDU3OTc</VersionId>
		        <IsLatest>true</IsLatest>
		        <LastModified>2020-12-10T04:54:12.000Z</LastModified>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </DeleteMarker>
		    <Version>
		        <Key>%E7%85%A7%E7%89%87/2020%E5%B9%B4/IMG0001.jpg</Key>
		        <VersionId>MTg0NDUxMzY0OTc2NjcwNjMwMDQ</VersionId>
		        <IsLatest>false</IsLatest>
		        <LastModified>2020-12-10T04:54:02.000Z</LastModified>
		        <ETag>&quot;ee8de918d05640145b18f70f4c3aa602&quot;</ETag>
		        <Size>16</Size>
		        <StorageClass>STANDARD</StorageClass>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
		    <Version>
		        <Key>%E8%85%BE%E8%AE%AF%E4%BA%91.jpg</Key>
		        <VersionId>MTg0NDUxMzY0OTc2NTY5MDA4NzU</VersionId>
		        <IsLatest>true</IsLatest>
		        <LastModified>2020-12-10T04:54:12.000Z</LastModified>
		        <ETag>&quot;8bb76a43f75d3b96442c470f8ec23b89&quot;</ETag>
		        <Size>16</Size>
		        <StorageClass>STANDARD</StorageClass>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
		    <Version>
		        <Key>%E8%85%BE%E8%AE%AF%E4%BA%91.jpg</Key>
		        <VersionId>MTg0NDUxMzY0OTc2NjcxNzA2ODg</VersionId>
		        <IsLatest>false</IsLatest>
		        <LastModified>2020-12-10T04:54:02.000Z</LastModified>
		        <ETag>&quot;dcc880c5eba9e002bc4567c733b0e63e&quot;</ETag>
		        <Size>13</Size>
		        <StorageClass>STANDARD</StorageClass>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
</ListVersionsResult>
```

#### Example 5. Specifying the `delimiter` parameter (listing object versions and subdirectories in the root directory)

#### Request

```shell
GET /?versions&delimiter=%2F HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 10 Dec 2020 07:04:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607583843;1607591043&q-key-time=1607583843;1607591043&q-header-list=date;host&q-url-param-list=delimiter;versions&q-signature=9eaea1e6072c7175cb593e08b69223521217****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1893
Connection: close
Date: Thu, 10 Dec 2020 07:04:03 GMT
Server: tencent-cos
x-cos-request-id: NWZkMWM4NjNfNzFjODJhMDlfMjlhZTRfMTg5****



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
		    <DeleteMarker>
		        <Key>example-object-1.jpg</Key>
		        <VersionId>MTg0NDUxMzY0ODk4NzYzNTE4Nzk</VersionId>
		        <IsLatest>true</IsLatest>
		        <LastModified>2020-12-10T07:03:53.000Z</LastModified>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </DeleteMarker>
		    <Version>
		        <Key>example-object-1.jpg</Key>
		        <VersionId>MTg0NDUxMzY0ODk4ODY2NTcxMzY</VersionId>
		        <IsLatest>false</IsLatest>
		        <LastModified>2020-12-10T07:03:42.000Z</LastModified>
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
		        <VersionId>MTg0NDUxMzY0ODk4NzYzODYyODA</VersionId>
		        <IsLatest>true</IsLatest>
		        <LastModified>2020-12-10T07:03:53.000Z</LastModified>
		        <ETag>&quot;51ffadb19b3bf062ecd0c6f044a4d4ce&quot;</ETag>
		        <Size>23</Size>
		        <StorageClass>INTELLIGENT_TIERING</StorageClass>
		        <StorageTier>FREQUENT</StorageTier>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
		    <Version>
		        <Key>example-object-2.jpg</Key>
		        <VersionId>MTg0NDUxMzY0ODk4ODY2NTA0Mjk</VersionId>
		        <IsLatest>false</IsLatest>
		        <LastModified>2020-12-10T07:03:42.000Z</LastModified>
		        <ETag>&quot;dcffaafe67632b2bd2dd0b9456eafca7&quot;</ETag>
		        <Size>23</Size>
		        <StorageClass>STANDARD_IA</StorageClass>
		        <Owner>
		        	<ID>1250000000</ID>
		        	<DisplayName>1250000000</DisplayName>
		        </Owner>
		    </Version>
</ListVersionsResult>
```

#### Example 6. Specifying the `prefix` and `delimiter` parameters (listing object versions and subdirectories in a specified subdirectory)

#### Request

```shell
GET /?versions&prefix=example-folder-1%2F&delimiter=%2F HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 10 Dec 2020 07:04:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607583843;1607591043&q-key-time=1607583843;1607591043&q-header-list=date;host&q-url-param-list=delimiter;prefix;versions&q-signature=c09ffca0377304f9a12cb2d8e223ede35569****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1960
Connection: close
Date: Thu, 10 Dec 2020 07:04:03 GMT
Server: tencent-cos
x-cos-request-id: NWZkMWM4NjNfZWVjODJhMDlfNTNmN18xNWNj****



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
		    <DeleteMarker>
		    	<Key>example-folder-1/example-object-1.jpg</Key>
		    	<VersionId>MTg0NDUxMzY0ODk4NzYzNjE4NzA</VersionId>
		    	<IsLatest>true</IsLatest>
		    	<LastModified>2020-12-10T07:03:53.000Z</LastModified>
		    	<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
		    	</Owner>
		    </DeleteMarker>
		    <Version>
		    	<Key>example-folder-1/example-object-1.jpg</Key>
		    	<VersionId>MTg0NDUxMzY0ODk4ODY2NTAzOTY</VersionId>
		    	<IsLatest>false</IsLatest>
		    	<LastModified>2020-12-10T07:03:42.000Z</LastModified>
		    	<ETag>&quot;f173c1199e3d3b53dd91223cae16fb42&quot;</ETag>
		    	<Size>37</Size>
		    	<StorageClass>STANDARD</StorageClass>
		    	<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
		    	</Owner>
		    </Version>
		    <Version>
		    	<Key>example-folder-1/example-object-2.jpg</Key>
		    	<VersionId>MTg0NDUxMzY0ODk4NzYzNzc2ODY</VersionId>
		    	<IsLatest>true</IsLatest>
		    	<LastModified>2020-12-10T07:03:53.000Z</LastModified>
		    	<ETag>&quot;f52cc0bc2042d201b852385927bcab95&quot;</ETag>
		    	<Size>40</Size>
		    	<StorageClass>STANDARD</StorageClass>
		    	<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
		    	</Owner>
		    </Version>
		    <Version>
		    	<Key>example-folder-1/example-object-2.jpg</Key>
		    	<VersionId>MTg0NDUxMzY0ODk4ODY2NjQ2NDc</VersionId>
		    	<IsLatest>false</IsLatest>
		    	<LastModified>2020-12-10T07:03:42.000Z</LastModified>
		    	<ETag>&quot;7b3be6c39746a970d628e6ab9f250342&quot;</ETag>
		    	<Size>40</Size>
		    	<StorageClass>STANDARD</StorageClass>
		    	<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
		    	</Owner>
		    </Version>
</ListVersionsResult>
```

#### Example 7. Obtaining the first page of keys when there are more than one page (this example specifies `max-keys`. If not specified, the value `1000` is used by default. The sum of `Version` and `DeleteMarker` cannot exceed the value of `max-keys`)

#### Request

```shell
GET /?versions&max-keys=3 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 08 Dec 2020 12:46:40 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607431600;1607438800&q-key-time=1607431600;1607438800&q-header-list=date;host&q-url-param-list=max-keys;versions&q-signature=eddd43e98a9001e92f52896de6f8ce88bff5****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1390
Connection: close
Date: Tue, 08 Dec 2020 12:46:40 GMT
Server: tencent-cos
x-cos-request-id: NWZjZjc1YjBfYjBhODBiMDlfZDU5Yl9jYjBl****



<ListVersionsResult>
		    <Name>examplebucket-1250000000</Name>
		    <Prefix/>
		    <KeyMarker/>
		    <VersionIdMarker/>
		    <MaxKeys>3</MaxKeys>
		    <IsTruncated>true</IsTruncated>
		    <NextKeyMarker>example-object-2.jpg</NextKeyMarker>
		    <NextVersionIdMarker>MTg0NDUxMzY2NDIxMjk3MzMwOTM</NextVersionIdMarker>
		    <Version>
		    	<Key>example-object-1.jpg</Key>
		    	<VersionId>MTg0NDUxMzY2NDIxNTAwOTk4NzA</VersionId>
		    	<IsLatest>true</IsLatest>
		    	<LastModified>2020-12-08T12:45:59.000Z</LastModified>
		    	<ETag>&quot;15f0f671f04af108023b5603bea2bfda&quot;</ETag>
		    	<Size>23</Size>
		    	<StorageClass>STANDARD</StorageClass>
		    	<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
		    	</Owner>
		    </Version>
		    <Version>
		    	<Key>example-object-1.jpg</Key>
		    	<VersionId>MTg0NDUxMzY2NDIxNjAyODcyNzk</VersionId>
		    	<IsLatest>false</IsLatest>
		    	<LastModified>2020-12-08T12:45:49.000Z</LastModified>
		    	<ETag>&quot;601389434817e2781d8efb35c0e44717&quot;</ETag>
		    	<Size>23</Size>
		    	<StorageClass>STANDARD</StorageClass>
		    	<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
		    	</Owner>
		    </Version>
		    <DeleteMarker>
		    	<Key>example-object-2.jpg</Key>
		    	<VersionId>MTg0NDUxMzY2NDIxMjk3MzMwOTM</VersionId>
		    	<IsLatest>true</IsLatest>
		    	<LastModified>2020-12-08T12:46:19.000Z</LastModified>
		    	<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
		    	</Owner>
		    </DeleteMarker>
</ListVersionsResult>
```

#### Example 8: Obtaining the subsequent pages with `key-marker` and `version-id-marker` specified (a continuity of example 7)

#### Request

```shell
GET /?versions&max-keys=3&key-marker=example-object-2.jpg&version-id-marker=MTg0NDUxMzY2NDIxMjk3MzMwOTM HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 08 Dec 2020 12:46:41 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607431601;1607438801&q-key-time=1607431601;1607438801&q-header-list=date;host&q-url-param-list=key-marker;max-keys;version-id-marker;versions&q-signature=ad52682a1febcc068b6420432017daee8145****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1052
Connection: close
Date: Tue, 08 Dec 2020 12:46:41 GMT
Server: tencent-cos
x-cos-request-id: NWZjZjc1YjFfNjljMDBiMDlfNjQwOV8xYjM2****



<ListVersionsResult>
		    <Name>examplebucket-1250000000</Name>
		    <Prefix/>
		    <KeyMarker>example-object-2.jpg</KeyMarker>
		    <VersionIdMarker>MTg0NDUxMzY2NDIxMjk3MzMwOTM</VersionIdMarker>
		    <MaxKeys>3</MaxKeys>
		    <IsTruncated>false</IsTruncated>
		    <Version>
		    	<Key>example-object-2.jpg</Key>
		    	<VersionId>MTg0NDUxMzY2NDIxMzk5MDk1NzU</VersionId>
		    	<IsLatest>false</IsLatest>
		    	<LastModified>2020-12-08T12:46:09.000Z</LastModified>
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
		    	<VersionId>MTg0NDUxMzY2NDIxMTk1NTEyNDI</VersionId>
		    	<IsLatest>true</IsLatest>
		    	<LastModified>2020-12-08T12:46:30.000Z</LastModified>
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

#### Example 9. Specifying the object to start with using the `key-marker` parameter but not the `version-id-marker` parameter (a continuity of example 7)

#### Request

```shell
GET /?versions&max-keys=3&key-marker=example-object-2.jpg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 08 Dec 2020 12:46:41 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607431601;1607438801&q-key-time=1607431601;1607438801&q-header-list=date;host&q-url-param-list=key-marker;max-keys;versions&q-signature=0ed7ce0e8402e35b0ffd2fac429a638a56ea****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 610
Connection: close
Date: Tue, 08 Dec 2020 12:46:42 GMT
Server: tencent-cos
x-cos-request-id: NWZjZjc1YjJfZGZjMTBiMDlfNzAyYl8xMzkx****



<ListVersionsResult>
			<Name>examplebucket-1250000000</Name>
			<Prefix/>
			<KeyMarker>example-object-2.jpg</KeyMarker>
			<VersionIdMarker/>
			<MaxKeys>3</MaxKeys>
			<IsTruncated>false</IsTruncated>
			<Version>
		    	<Key>example-object-3.jpg</Key>
		    	<VersionId>MTg0NDUxMzY2NDIxMTk1NTEyNDI</VersionId>
		    	<IsLatest>true</IsLatest>
		    	<LastModified>2020-12-08T12:46:30.000Z</LastModified>
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

#### Example 10. Obtaining the first page of keys when there are more than one page (with `delimiter` specified and the sum of `CommonPrefixes`, `Version`, and `DeleteMarker` not exceeding the value of `max-keys`)

#### Request

```shell
GET /?versions&delimiter=%2F&max-keys=3 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 09 Dec 2020 13:40:24 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607521224;1607528424&q-key-time=1607521224;1607528424&q-header-list=date;host&q-url-param-list=delimiter;max-keys;versions&q-signature=fdd9031684c544bca32fae81da75b9216079****
Connection: close

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 503
Connection: close
Date: Wed, 09 Dec 2020 13:40:24 GMT
Server: tencent-cos
x-cos-request-id: NWZkMGQzYzhfYmIwMmEwOV83OGU4XzZj****

<ListVersionsResult>
		    <Name>examplebucket-1250000000</Name>
		    <Prefix/>
		    <KeyMarker/>
		    <VersionIdMarker/>
		    <MaxKeys>3</MaxKeys>
		    <IsTruncated>true</IsTruncated>
		    <NextKeyMarker>example-folder-3/</NextKeyMarker>
		    <NextVersionIdMarker/>
		    <Delimiter>/</Delimiter>
		    <CommonPrefixes>
		    	<Prefix>example-folder-1/</Prefix>
		    </CommonPrefixes>
		    <CommonPrefixes>
		    	<Prefix>example-folder-2/</Prefix>
		    </CommonPrefixes>
		    <CommonPrefixes>
		    	<Prefix>example-folder-3/</Prefix>
		    </CommonPrefixes>
</ListVersionsResult>
```

#### Example 11. Obtaining the subsequent pages with `delimiter` specified and `version-id-marker` left empty (as the value of `NextVersionIdMarker` is empty on the first page) (a continuity of example 10)

#### Request

```shell
GET /?versions&delimiter=%2F&max-keys=3&key-marker=example-folder-3%2F&version-id-marker= HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 09 Dec 2020 14:02:32 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607522552;1607529752&q-key-time=1607522552;1607529752&q-header-list=date;host&q-url-param-list=delimiter;key-marker;max-keys;version-id-marker;versions&q-signature=fd4b2ab426e4531be2e52c02d5bd0e747ee7****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1115
Connection: close
Date: Wed, 09 Dec 2020 14:02:32 GMT
Server: tencent-cos
x-cos-request-id: NWZkMGQ4ZjhfZmVhODBiMDlfMTI3NzVfMTBj****



<ListVersionsResult>
		    <Name>examplebucket-1250000000</Name>
		    <Prefix/>
		    <KeyMarker>example-folder-3/</KeyMarker>
		    <VersionIdMarker/>
		    <MaxKeys>3</MaxKeys>
		    <IsTruncated>true</IsTruncated>
		    <NextKeyMarker>example-object.jpg</NextKeyMarker>
		    <NextVersionIdMarker>MTg0NDUxMzY1NTExNzc4NTYzMTk</NextVersionIdMarker>
		    <Delimiter>/</Delimiter>
		    <CommonPrefixes>
		    	<Prefix>example-folder-4/</Prefix>
		    </CommonPrefixes>
		    <Version>
		    	<Key>example-object.jpg</Key>
		    	<VersionId>MTg0NDUxMzY1NTExNjc2OTk4MjE</VersionId>
		    	<IsLatest>true</IsLatest>
		    	<LastModified>2020-12-09T14:02:21.000Z</LastModified>
		    	<ETag>&quot;3979f6bb23f827d258be64cc0d8df5fb&quot;</ETag>
		    	<Size>21</Size>
		    	<StorageClass>STANDARD</StorageClass>
		    	<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
		    	</Owner>
		    </Version>
		    <DeleteMarker>
		    	<Key>example-object.jpg</Key>
		    	<VersionId>MTg0NDUxMzY1NTExNzc4NTYzMTk</VersionId>
		    	<IsLatest>false</IsLatest>
		    	<LastModified>2020-12-09T14:02:11.000Z</LastModified>
		    	<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
		    	</Owner>
		    </DeleteMarker>
</ListVersionsResult>
```

