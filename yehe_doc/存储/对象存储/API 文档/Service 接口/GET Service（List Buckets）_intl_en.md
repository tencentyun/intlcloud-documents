## Overview

This API is used to query the list of all buckets under a requester's account or in a specific region.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                We recommend using Tencent Cloud API Explorer.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetService&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
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

**Sample 1**

```plaintext
GET / HTTP/1.1
Host: service.cos.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

**Sample 2**

```plaintext
GET / HTTP/1.1
Host: cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> ?
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - Host: To query the list of all buckets, set it to `service.cos.myqcloud.com`. To query the list of buckets in a specified region, set it to `cos.&lt;Region>.myqcloud.com`, where &lt;Region> is a COS available region (see [Regions and Access Endpoitns](https://intl.cloud.tencent.com/document/product/436/6224)).

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful query returns **application/xml** data that includes the list of all buckets or the list of buckets in a specific region.

```plaintext
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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ---------------------- | ------ | ------------------------------- | --------- |
| ListAllMyBucketsResult | None | Stores the result of the `GET Service` request | Container |

**Content of `ListAllMyBucketsResult`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ---------------------- | ---------------- | --------- |
| Owner              | ListAllMyBucketsResult | Bucket owner information | Container |
| Buckets            | ListAllMyBucketsResult | Bucket list | Container |

**Content of `Owner`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ---------------------------- | ------------------------------------------------------------ | ------ |
| ID | ListAllMyBucketsResult.Owner | Complete ID of the bucket owner in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`<br>Example: `qcs::cam::uin/100000000001:uin/100000000001` | string |
| DisplayName        | ListAllMyBucketsResult.Owner | Bucket owner name                                           | string |

**Content of `Buckets`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------------ | ---------- | --------- |
| Bucket             | ListAllMyBucketsResult.Buckets | Bucket information | Container |

**Content of `Buckets.Bucket`:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------------------- | ------------------------------------------------------------ | ------ |
| Name  | ListAllMyBucketsResult.Buckets.Bucket | Bucket name in the format of `<BucketName-APPID>`<br>Example: `examplebucket-1250000000` | string |
| Location | ListAllMyBucketsResult.Buckets.Bucket | Region of the bucket. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).<br>Example: `ap-beijing`, `ap-hongkong`, `eu-frankfurt` | Enum   |
| CreationDate | ListAllMyBucketsResult.Buckets.Bucket | Bucket creation time in ISO 8601 format. Example: `2019-05-24T10:56:40Z`    | date   |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Example 1. Querying the list of all buckets

#### Request

```plaintext
GET / HTTP/1.1
Host: service.cos.myqcloud.com
Date: Fri, 24 May 2019 11:59:50 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558699190;1558706390&q-key-time=1558699190;1558706390&q-header-list=date;host&q-url-param-list=&q-signature=89fa1f6a56c34e460f3db4d65f928eaf034a****
Connection: close
```

#### Response

```plaintext
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

```plaintext
GET / HTTP/1.1
Host: cos.ap-beijing.myqcloud.com
Date: Fri, 24 May 2019 11:59:51 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558699191;1558706391&q-key-time=1558699191;1558706391&q-header-list=date;host&q-url-param-list=&q-signature=c3f55f4ce2800fb343cf85ff536a9185a0c1****
Connection: close
```

#### Response

```plaintext
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
