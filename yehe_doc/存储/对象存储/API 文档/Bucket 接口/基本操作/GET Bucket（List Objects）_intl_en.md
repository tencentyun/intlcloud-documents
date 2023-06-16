## Overview

This API is equivalent to the `List Objects` API and can be used to list some or all objects in a bucket. To call this API, you need to have permission to read the bucket.

>? If you upload an object to the bucket and call the `GET Bucket` API immediately, due to the eventual consistency characteristic of this API, the response may not include the newly uploaded object.
>


<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetBucket&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>


## Requests

#### Request example

```shell
GET / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request fields

| Field |  Description | Type | Required |
| --- | --- | --- | --- |
| prefix | Key prefix to query objects by | String | No   |
| delimiter | Character delimiter used to group object keys. Keys that contain identical paths between the prefix (or, if no prefix is specified, the beginning of the string) and the first delimiter are grouped and defined as a `Prefix` node under `CommonPrefixes`. The grouped object keys will no longer appear in the subsequent object list. For specific scenarios and usage, see the samples below. | String | No |
| encoding-type | Encoding type of the returned value. Valid value: `url`, meaning that the returned object keys are URL-encoded (percent-encoded) values. For example, "Tencent Cloud" will be encoded to `%E8%85%BE%E8%AE%AF%E4%BA%91`. | String | No |
| marker | Marker for the starting object key. Object key entries will be returned in UTF-8 lexicographical order, starting from the first object key after the marker. | string | No |
| max-keys | The maximum number (up to 1,000) of keys returned in the response. Defaults to `1000`. <br>**Note**: This parameter limits the maximum number of keys (the sum of `CommonPrefixes` and `Contents`) COS can return in each `List Objects` response. If not all objects are listed in a single response, COS will return the `NextMarker` node, the value of which can be used to specify `marker` so that the remaining objects can be listed in your next request. | integer | No |

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information about common response headers, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Header | Description | Type |
| --- | --- | --- |
| x-cos-bucket-region | Bucket region, such as `ap-beijing`, `ap-hongkong`, and `eu-frankfurt`. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | Enum |

#### Response body

A successful query returns **application/xml** data, which contains information about objects in the bucket. For the response bodies of different scenarios, see the examples below.

```xml
<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
			<Name>string</Name>
			<EncodingType>string</EncodingType>
			<Prefix>string</Prefix>
			<Marker>string</Marker>
			<MaxKeys>integer</MaxKeys>
			<Delimiter>string</Delimiter>
			<IsTruncated>boolean</IsTruncated>
			<NextMarker>string</NextMarker>
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
				<StorageTier>Enum</StorageTier>
				<RestoreStatus>Enum</RestoreStatus>
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
				<StorageTier>Enum</StorageTier>
				<RestoreStatus>Enum</RestoreStatus>
			</Contents>
</ListBucketResult>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ListBucketResult | None | Stores the result of the `GET Bucket` request. | Container |

**Content of `ListBucketResult`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Name | ListBucketResult | Bucket name, formatted as `<BucketName-APPID>`, such as `examplebucket-1250000000` | string |
| EncodingType | ListBucketResult | Encoding type, which corresponds to the `encoding-type` parameter in the request. This node will be returned only when the `encoding-type` parameter is specified in the request. | string |
| Prefix | ListBucketResult | Matching prefix to filter object keys. This node corresponds to the `Prefix` parameter in the request. | string |
| Marker | ListBucketResult | Marks the object key to start with. Object keys after the marker will be returned in UTF-8 lexicographical order. This node corresponds to the `marker` parameter in the request. | string |
| MaxKeys | ListBucketResult | Maximum number of keys returned in a single response. This node corresponds to the `max-keys` parameter in the request. | integer |
| Delimiter | ListBucketResult | Delimiter, which corresponds to the `delimiter` parameter in the request and will be returned only if the `delimiter` parameter is specified in the request. | string |
| IsTruncated | ListBucketResult | Indicates whether the returned list is truncated. Valid values: `true`, `false` | boolean |
| NextMarker | ListBucketResult | This node will be returned only if the returned list is truncated (i.e., the value of `IsTruncated` is `true`). The value of this node is the last object key in the current response. If you need to request subsequent entries, the value can be passed in as the value of the `marker` parameter in the next request. | string |
| CommonPrefixes | ListBucketResult | The identical paths between the prefix (or, if no prefix is specified, the beginning of the string) and the first delimiter are grouped and defined as a common prefix. This node will be returned only if the `delimiter` parameter is specified in the request | Container |
| Contents | ListBucketResult | Object entries | Container |

**Content of `CommonPrefixes`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Prefix | ListBucketResult.CommonPrefixes | A single common prefix | string |

**Content of `Contents`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| Key | ListBucketResult.Contents | Object key | string |
| LastModified | ListBucketResult.Contents | Time the object was last modified, in ISO 8601 format (for example, `2019-05-24T10:56:40Z`) | date |
| ETag | ListBucketResult.Contents | Entity tag of the object. It indicates the content of the object when it is created and can be used to verify whether the object content is changed. Example: "8e0b617ca298a564c3331da28dcb50df"<br>The value of `ETag` is not necessarily the MD5 checksum of the object. The value will be different if the uploaded object is encrypted. | string |
| Size | ListBucketResult.Contents | Object size, in bytes | integer |
| Owner | ListBucketResult.Contents | Information of the object owner | Container |
| StorageClass | ListBucketResult.Contents | Object storage class, such as `STANDARD_IA` or `ARCHIVE`. For enumerated values, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925) | Enum |
| StorageTier | ListBucketResult.Contents | Access tier (for INTELLIGENT TIERING) the object is currently stored in. Enumerated values: `FREQUENT`, `INFREQUENT`. This node is returned only when `StorageClass` is set to `INTELLIGENT_TIERING`. | Enum |
|RestoreStatus | ListBucketResult.Contents | When the object storage class is `ARCHIVE` or `DEEP ARCHIVE`, this field indicates the restoration status of the object. Valid values: `ONGOING`, `DONE`, `FAILED`. If no restoration request is initiated to the object, this field is null. After a restoration request is initiated, the value is `ONGOING`, `DONE`, and `FAILED` respectively if the restoration is in progress, completed, or failed. This node is returned only when `StorageClass` is `ARCHIVE` or `DEEP_ARCHIVE`. | Enum |

**Content of `Contents.Owner`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| --- | --- | --- | --- |
| ID | ListBucketResult.Contents.Owner | `APPID` of the object owner | string |
| DisplayName | ListBucketResult.Contents.Owner | Name of the object owner | string |

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1: simple use case

#### Request

```shell
GET / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 10 Dec 2020 03:37:41 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607571461;1607578661&q-key-time=1607571461;1607578661&q-header-list=date;host&q-url-param-list=&q-signature=918fd2e0149edf8982bebaab2956ec81ede1****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 2931
Connection: close
Date: Thu, 10 Dec 2020 03:37:41 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWZkMTk4MDVfNjViODJhMDlfNDZkYl8xNzU0****
		
<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
      <Name>examplebucket-1250000000</Name>
      <Prefix/>
      <Marker/>
      <MaxKeys>1000</MaxKeys>
      <IsTruncated>false</IsTruncated>
      <Contents>
          <Key>example-folder-1/example-object-1.jpg</Key>
          <LastModified>2020-12-10T03:37:30.000Z</LastModified>
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
          <LastModified>2020-12-10T03:37:30.000Z</LastModified>
          <ETag>&quot;c9d28698978bb6fef6c1ed1c439a17d3&quot;</ETag>
          <Size>37</Size>
          <Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
          </Owner>
				<StorageClass>INTELLIGENT_TIERING</StorageClass>
				<StorageTier>FREQUENT</StorageTier>
      </Contents>
				...
      <Contents>
          <Key>example-object-2.jpg</Key>
          <LastModified>2020-12-10T03:37:30.000Z</LastModified>
          <ETag>&quot;51370fc64b79d0d3c7c609635be1c41f&quot;</ETag>
          <Size>20</Size>
          <Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
          </Owner>
          <StorageClass>STANDARD_IA</StorageClass>
      </Contents>
      <Contents>
          <Key>example-object-3.jpg</Key>
          <LastModified>2020-12-10T04:37:30.000Z</LastModified>
          <ETag>&quot;51370fc64b79d0d3c7c609635be1c41f&quot;</ETag>
          <Size>20</Size>
          <Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
          </Owner>
          <StorageClass>ARCHIVE</StorageClass>
          <RestoreStatus>DONE</RestoreStatus>
      </Contents>
</ListBucketResult>
```

#### Example 2. Specifying the `encoding-type` parameter (object keys are URL-encoded)

#### Request

```shell
GET /?encoding-type=url HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 08 Dec 2020 13:54:16 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607435656;1607442856&q-key-time=1607435656;1607442856&q-header-list=date;host&q-url-param-list=encoding-type&q-signature=ccbffb70b38430c4b6bc2d1b16ec9c1c8b6f****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1220
Connection: close
Date: Wed, 09 Dec 2020 15:28:29 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWZkMGVkMWRfZjdjNzJhMDlfMjJhYTlfYmJk****
		
<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
      <Name>examplebucket-1250000000</Name>
      <EncodingType>url</EncodingType>
      <Prefix/>
      <Marker/>
      <MaxKeys>1000</MaxKeys>
      <IsTruncated>false</IsTruncated>
      <Contents>
				<Key>Tencent%20Cloud.jpg</Key>
				<LastModified>2020-12-09T15:28:19.000Z</LastModified>
				<ETag>&quot;ee8de918d05640145b18f70f4c3aa602&quot;</ETag>
				<Size>16</Size>
				<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
				</Owner>
				<StorageClass>STANDARD</StorageClass>
      </Contents>
      <Contents>
				<Key>%E7%85%A7%E7%89%87/2020%E5%B9%B4/IMG0001.jpg</Key>
				<LastModified>2020-12-09T15:28:19.000Z</LastModified>
				<ETag>&quot;ee8de918d05640145b18f70f4c3aa602&quot;</ETag>
				<Size>16</Size>
				<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
				</Owner>
				<StorageClass>STANDARD</StorageClass>
      </Contents>
      <Contents>
				<Key>%E8%85%BE%E8%AE%AF%E4%BA%91.jpg</Key>
				<LastModified>2020-12-09T15:28:19.000Z</LastModified>
				<ETag>&quot;ee8de918d05640145b18f70f4c3aa602&quot;</ETag>
				<Size>16</Size>
				<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
				</Owner>
				<StorageClass>STANDARD</StorageClass>
			</Contents>
</ListBucketResult>
```

#### Example 3. Specifying the `delimiter` parameter (listing objects and subdirectories in the root directory)

#### Request

```shell
GET /?delimiter=%2F HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 10 Dec 2020 03:37:41 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607571461;1607578661&q-key-time=1607571461;1607578661&q-header-list=date;host&q-url-param-list=delimiter&q-signature=5984c14f29df90235f4c507e7fbf68ad775e****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1011
Connection: close
Date: Thu, 10 Dec 2020 03:37:41 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWZkMTk4MDVfNjRiMDJhMDlfOTZjZV8xOTgw****
		
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
				<LastModified>2020-12-10T03:37:30.000Z</LastModified>
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
				<LastModified>2020-12-10T03:37:30.000Z</LastModified>
				<ETag>&quot;51370fc64b79d0d3c7c609635be1c41f&quot;</ETag>
				<Size>20</Size>
				<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
				</Owner>
				<StorageClass>STANDARD_IA</StorageClass>
			</Contents>
</ListBucketResult>
```

#### Example 4. Specifying the `prefix` and `delimiter` parameters (listing objects and subdirectories in a specified subdirectory)

#### Request

```shell
GET /?prefix=example-folder-1%2F&delimiter=%2F HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 10 Dec 2020 03:37:41 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607571461;1607578661&q-key-time=1607571461;1607578661&q-header-list=date;host&q-url-param-list=delimiter;prefix&q-signature=96b4c558ed02a6e6652427fb91b8d22f2107****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1142
Connection: close
Date: Thu, 10 Dec 2020 03:37:41 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWZkMTk4MDVfZGZjNzJhMDlfMzJiMjRfMTY0****
		
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
				<LastModified>2020-12-10T03:37:30.000Z</LastModified>
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
				<LastModified>2020-12-10T03:37:30.000Z</LastModified>
				<ETag>&quot;c9d28698978bb6fef6c1ed1c439a17d3&quot;</ETag>
				<Size>37</Size>
				<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
				</Owner>
				<StorageClass>INTELLIGENT_TIERING</StorageClass>
				<StorageTier>FREQUENT</StorageTier>
			</Contents>
</ListBucketResult>
```

#### Example 5. Obtaining the first page of keys when there are more than one page (this example specifies the value of `max-keys`. If not specified, the value `1000` is used by default)

#### Request

```shell
GET /?max-keys=3 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 08 Dec 2020 12:05:10 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607429110;1607436310&q-key-time=1607429110;1607436310&q-header-list=date;host&q-url-param-list=max-keys&q-signature=a08797232c663110139c878400339bc5b4f4****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1195
Connection: close
Date: Tue, 08 Dec 2020 12:05:10 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWZjZjZiZjZfZGRjODJhMDlfMWFjZDVfMTlmZTY5****
		
<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
			<Name>examplebucket-1250000000</Name>
			<Prefix/>
			<Marker/>
			<MaxKeys>3</MaxKeys>
			<IsTruncated>true</IsTruncated>
			<NextMarker>example-object-3.jpg</NextMarker>
			<Contents>
				<Key>example-object-1.jpg</Key>
				<LastModified>2020-12-08T12:05:00.000Z</LastModified>
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
				<LastModified>2020-12-08T12:05:00.000Z</LastModified>
				<ETag>&quot;51370fc64b79d0d3c7c609635be1c41f&quot;</ETag>
				<Size>20</Size>
				<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
				</Owner>
				<StorageClass>STANDARD</StorageClass>
			</Contents>
			<Contents>
				<Key>example-object-3.jpg</Key>
				<LastModified>2020-12-08T12:05:00.000Z</LastModified>
				<ETag>&quot;b2f1d893c5fde000ee8ea6eca18ed81f&quot;</ETag>
				<Size>20</Size>
				<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
				</Owner>
				<StorageClass>STANDARD</StorageClass>
			</Contents>
</ListBucketResult>
```

#### Example 6. Obtaining the subsequent pages (a continuity of example 5)

#### Request

```shell
GET /?max-keys=3&marker=example-object-3.jpg HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 08 Dec 2020 12:05:11 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607429111;1607436311&q-key-time=1607429111;1607436311&q-header-list=date;host&q-url-param-list=marker;max-keys&q-signature=b9613747aa1047ec4d72e63123340e88e1c0****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 859
Connection: close
Date: Tue, 08 Dec 2020 12:05:11 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWZjZjZiZjdfMjRhZjJhMDlfMjc2NV8xYmE2****
			
<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
			<Name>examplebucket-1250000000</Name>
			<Prefix/>
			<Marker>example-object-3.jpg</Marker>
			<MaxKeys>3</MaxKeys>
			<IsTruncated>false</IsTruncated>
			<Contents>
				<Key>example-object-4.jpg</Key>
				<LastModified>2020-12-08T12:05:00.000Z</LastModified>
				<ETag>&quot;e9ec8bcb980d2e4d8526c346eb3b2585&quot;</ETag>
				<Size>20</Size>
				<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
				</Owner>
				<StorageClass>STANDARD</StorageClass>
			</Contents>
			<Contents>
				<Key>example-object-5.jpg</Key>
				<LastModified>2020-12-08T12:05:00.000Z</LastModified>
				<ETag>&quot;201669a14bdf051d8a9d6f9828d3f4c4&quot;</ETag>
				<Size>20</Size>
				<Owner>
					<ID>1250000000</ID>
					<DisplayName>1250000000</DisplayName>
				</Owner>
				<StorageClass>STANDARD</StorageClass>
			</Contents>
</ListBucketResult>
```

#### Example 7. Obtaining the first page of keys when there are more than one page (with `delimiter` specified and the sum of `CommonPrefixes` and `Contents` not exceeding the value of `max-keys`)

#### Request

```shell
GET /?delimiter=%2F&max-keys=3 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 09 Dec 2020 03:22:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607484158;1607491358&q-key-time=1607484158;1607491358&q-header-list=date;host&q-url-param-list=delimiter;max-keys&q-signature=42f6307ea77293c7a507760430bcad255991****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 486
Connection: close
Date: Wed, 09 Dec 2020 03:22:38 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWZkMDQyZmVfYTJjMjJhMDlfYmQwOF8xYjkw****
		
<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
			<Name>examplebucket-1250000000</Name>
			<Prefix/>
			<Marker/>
			<MaxKeys>3</MaxKeys>
			<Delimiter>/</Delimiter>
			<IsTruncated>true</IsTruncated>
			<NextMarker>example-folder-3/</NextMarker>
			<CommonPrefixes>
				<Prefix>example-folder-1/</Prefix>
			</CommonPrefixes>
			<CommonPrefixes>
				<Prefix>example-folder-2/</Prefix>
			</CommonPrefixes>
			<CommonPrefixes>
				<Prefix>example-folder-3/</Prefix>
			</CommonPrefixes>
</ListBucketResult>
```

#### Example 8. Obtaining subsequent pages with `delimiter` specified (a continuity of example 7)

#### Request

```shell
GET /?delimiter=%2F&max-keys=3&marker=example-folder-3%2F HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 09 Dec 2020 03:22:39 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1607484159;1607491359&q-key-time=1607484159;1607491359&q-header-list=date;host&q-url-param-list=delimiter;marker;max-keys&q-signature=921a0e42ac17b3d95c7bf7e68696a489c9e0****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 956
Connection: close
Date: Wed, 09 Dec 2020 03:22:39 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWZkMDQyZmZfZmNhODBiMDlfZmM4N19jYmQz****
		
<?xml version='1.0' encoding='utf-8' ?>
<ListBucketResult>
			<Name>examplebucket-1250000000</Name>
			<Prefix/>
			<Marker>example-folder-3/</Marker>
			<MaxKeys>3</MaxKeys>
			<Delimiter>/</Delimiter>
			<IsTruncated>false</IsTruncated>
			<CommonPrefixes>
				<Prefix>example-folder-4/</Prefix>
			</CommonPrefixes>
			<Contents>
				<Key>example-object-1.jpg</Key>
				<LastModified>2020-12-09T03:22:28.000Z</LastModified>
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
				<LastModified>2020-12-09T03:22:28.000Z</LastModified>
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
