## Description

This API is used to query the list of all buckets under a requester's account or in a specific region.

## Request

#### Sample Request

**Sample 1**

```shell
GET / HTTP/1.1
Host: service.cos.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

**Sample 2**

```shell
GET / HTTP/1.1
Host: cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> ?
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> - Host: specify this as `service.cos.myqcloud.com` to query the list of all buckets; specify this as `cos.<Region>.myqcloud.com` to query the list of buckets in a specific region.

#### Request Parameters

This API does not use any request parameter.

#### Request Headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request Body

This API does not have a request body.

## Response

#### Response Headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response Body

A successful query returns **application/xml** data which include the list of all buckets or the list of buckets in a specific region.

```shell
<ListAllMyBucketsResult>
	<Owner>
		<ID>string</ID>
		<DisplayName>string</DisplayName>
	</Owner>
	<Buckets>
		<Bucket>
			<Name>string</Name>
			<Location>Enum</Location>
			<CreationDate>date</CreationDate>
		</Bucket>
		<Bucket>
			<Name>string</Name>
			<Location>Enum</Location>
			<CreationDate>date</CreationDate>
		</Bucket>
	</Buckets>
</ListAllMyBucketsResult>
```

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type |
| ---------------------- | ------ | ------------------------------- | --------- |
| ListAllMyBucketsResult | None | Stores the result of the `GET Service` request | Container |

**Content of the Container node `ListAllMyBucketsResult`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ---------------------- | ---------------- | --------- |
| Owner              | ListAllMyBucketsResult | Bucket owner information | Container |
| Buckets            | ListAllMyBucketsResult | Bucket list | Container |

**Content of the Container node `Owner`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ---------------------------- | ------------------------------------------------------------ | ------ |
| ID                 | ListAllMyBucketsResult.Owner | Complete ID of the bucket owner in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001` | string |
| DisplayName        | ListAllMyBucketsResult.Owner | Bucket owner name                                           | string |

**Content of the Container node `Buckets`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------------ | ---------- | --------- |
| Bucket             | ListAllMyBucketsResult.Buckets | Bucket information | Container |

**Content of the Container node `Buckets.Bucket`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------------------- | ------------------------------------------------------------ | ------ |
| Name               | ListAllMyBucketsResult.Buckets.Bucket | Bucket name in the format of `<BucketName-APPID>`, such as `examplebucket-1250000000` | string |
| Location           | ListAllMyBucketsResult.Buckets.Bucket | Bucket region such as `ap-beijing`, `ap-hongkong`, and `eu-frankfurt`. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | Enum |
| CreationDate | ListAllMyBucketsResult.Buckets.Bucket | Bucket creation time in ISO8601 format, such as `2019-05-24T10:56:40Z`    | date   |

#### Error Codes

There is no special error message for this API. For all error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1. Querying the list of all buckets

#### Request

```shell
GET / HTTP/1.1
Host: service.cos.myqcloud.com
Date: Fri, 24 May 2019 11:59:50 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558699190;1558706390&q-key-time=1558699190;1558706390&q-header-list=date;host&q-url-param-list=&q-signature=89fa1f6a56c34e460f3db4d65f928eaf034a****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 805
Connection: close
Date: Fri, 24 May 2019 11:59:51 GMT
Server: tencent-cos
x-cos-request-id: NWNlN2RjYjdfOGFiMjM1MGFfNTVjMl8zMmI1****

<ListAllMyBucketsResult>
	<Owner>
		<ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
	</Owner>
	<Buckets>
		<Bucket>
			<Name>examplebucket1-1250000000</Name>
			<Location>ap-beijing</Location>
			<CreationDate>2019-05-24T11:49:50Z</CreationDate>
		</Bucket>
		<Bucket>
			<Name>examplebucket2-1250000000</Name>
			<Location>ap-beijing</Location>
			<CreationDate>2019-05-24T11:51:50Z</CreationDate>
		</Bucket>
		<Bucket>
			<Name>examplebucket3-1250000000</Name>
			<Location>eu-frankfurt</Location>
			<CreationDate>2019-05-24T11:53:50Z</CreationDate>
		</Bucket>
		<Bucket>
			<Name>examplebucket4-1250000000</Name>
			<Location>eu-frankfurt</Location>
			<CreationDate>2019-05-24T11:55:50Z</CreationDate>
		</Bucket>
	</Buckets>
</ListAllMyBucketsResult>
```

#### Example 2. Querying the list of buckets in a specific region

#### Request

```shell
GET / HTTP/1.1
Host: cos.ap-beijing.myqcloud.com
Date: Fri, 24 May 2019 11:59:51 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558699191;1558706391&q-key-time=1558699191;1558706391&q-header-list=date;host&q-url-param-list=&q-signature=c3f55f4ce2800fb343cf85ff536a9185a0c1****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 495
Connection: close
Date: Fri, 24 May 2019 11:59:51 GMT
Server: tencent-cos
x-cos-request-id: NWNlN2RjYjdfZjhjODBiMDlfOWNlNF9hYzc2****

<ListAllMyBucketsResult>
	<Owner>
		<ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
	</Owner>
	<Buckets>
		<Bucket>
			<Name>examplebucket1-1250000000</Name>
			<Location>ap-beijing</Location>
			<CreationDate>2019-05-24T11:49:50Z</CreationDate>
		</Bucket>
		<Bucket>
			<Name>examplebucket2-1250000000</Name>
			<Location>ap-beijing</Location>
			<CreationDate>2019-05-24T11:51:50Z</CreationDate>
		</Bucket>
	</Buckets>
</ListAllMyBucketsResult>
```
