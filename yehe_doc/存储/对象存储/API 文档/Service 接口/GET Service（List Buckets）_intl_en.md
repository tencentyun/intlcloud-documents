## Overview

This API is used to query the list of all buckets under a requester's account or in a specific region.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetService&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
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
> - Host: To query the list of all buckets, set it to `service.cos.myqcloud.com`. To query the list of buckets in a specified region, set it to `cos.&lt;Region>.myqcloud.com`, where &lt;Region> is a COS available region (see [Regions and Access Endpoitns](https://www.tencentcloud.com/document/product/436/6224)).

#### Request parameters

GET Service can filter buckets by bucket tag, region, and creation time based on request parameters. If buckets are to be filtered by bucket tag, only one bucket tag is allowed. If a bucket contains multiple bucket tags, the bucket is returned as long as any of them is the bucket tag specified by users.

| Field |  Description | Type | Required |
| --- | --- | --- | --- |
|tagkey | Bucket tag based on which buckets are to be filtered. Only one bucket tag is allowed. `tagkey` is used to pass in a tag key. | string | No |
|tagvalue | Bucket tag based on which buckets are to be filtered. Only one bucket tag is allowed. `tagvalue` is used to pass in a tag value. | string | No |
|region | Region based on which buckets are to be filtered, for example, `region=ap-beijing`. For more information on regions supported by COS, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).| string | No |
|create-time | GMT timestamp, which is used together with the `range` parameter. This parameter specifies the creation time based on which buckets are to be filtered, for example, `create-time=1642662645`. |Timestamp | No |
|range | Used together with the `create-time` parameter. This parameter specifies the creation time based on which buckets are to be filtered. Valid values: `lt` (creation time earlier than `create-time`), `gt` (creation time later than `create-time`), `lte` (creation time earlier than or equal to `create-time`), `gte` (creation time later than or equal to `create-time`) | string | No |


If bucket tag-based authorization is different from GET Service authorization, the authentication and responses of GET Service requests are as follows. For information on the tag authorization method, see [Authorizing Sub-Account to Get Buckets by Tag] (https://intl.cloud.tencent.com/document/product/436/30931).

<table>
    <tr>
        <th>Bucket Tag-based Authorization</th>
        <th>GET Service Authorization</th>
        <th>GET Service Request</th>
        <th>Response</th>
    </tr>
    <tr>
        <td rowspan="4">The root account is authorized through the bucket tag-based authorization, and the sub-account is authorized to perform operations on resources of the bucket tag `tagA`.</td>
        <td rowspan="2">GET Service permission is not granted.</td>
        <td>Carries the bucket tag `tagA`</td>
        <td>List of buckets containing the bucket tag `tagA`</td>
    </tr>
    <tr>
        <td>Not carry the bucket tag</td>
        <td>Access Denied</td>
    </tr>
    <tr>
        <td rowspan="2">GET Service permission is granted.</td>
        <td>Carries the bucket tag `tagA`</td>
        <td>List of buckets containing the bucket tag `tagA`</td>
    </tr>
    <tr>
        <td>Not carry the bucket tag</td>
        <td>List of all buckets</td>
    </tr>
    <tr>
        <td rowspan="4">The root account is not authorized through the bucket tag-based authorization, and the sub-account is not authorized to perform operations on resources of the bucket tag `tagA`.</td>
        <td rowspan="2">GET Service permission is not granted.</td>
        <td>Carries the bucket tag `tagA`</td>
        <td>Access Denied</td>
    </tr>
    <tr>
        <td>Not carry the bucket tag</td>
        <td>Access Denied</td>
    </tr>
    <tr>
        <td rowspan="2">GET Service permission is granted.</td>
        <td>Carries the bucket tag `tagA`</td>
        <td>List of buckets containing the bucket tag `tagA`</td>
    </tr>
    <tr>
        <td>Not carry the bucket tag</td>
        <td>List of all buckets</td>
    </tr>
</table>

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

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
| Location | ListAllMyBucketsResult.Buckets.Bucket | Region of the bucket. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).<br>Example: `ap-beijing`, `ap-hongkong`, `eu-frankfurt` | Enum   |
| CreationDate | ListAllMyBucketsResult.Buckets.Bucket | Bucket creation time in ISO 8601 format. Example: `2019-05-24T10:56:40Z`    | date   |

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

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

#### Example 2. Querying the list of buckets in a specified region (filtering based on region)

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


#### Example 3. Querying the list of buckets in a specified region (filtering based on request parameters)


#### Request

```plaintext
GET /?region=ap-beijing HTTP/1.1
Host: service.cos.myqcloud.com
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
			<Name>examplebucket1-</Name>
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


#### Example 4. Filtering the list of buckets based on a specified tag


The tag of the bucket examplebucket-1250000000 is `<key1, value1>`, and the tags of the bucket examplebucket1-1250000000 are `<key1, value1>` and `<key2, value2>`.

#### Request

```plaintext
GET /?tagkey=key1&tagvalue=value1 HTTP/1.1
Host: service.cos.myqcloud.com
Date: Fri, 24 May 2019 11:59:51 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558699191;1558706391&q-key-time=1558699191;1558706391&q-header-list=date;host&q-url-param-list=&q-signature=c3f55f4ce2800fb343cf85ff536a9185a0c1****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 378
Content-Type: application/xml
Server: tencent-cos
Connection: keep-alive
Date: Thu, 20 Oct 2022 07:29:40 GMT
x-cos-request-id: NjM1MGY4ZTRfMWViMjM1MGFfYjg3MV8xNjdk****

<ListAllMyBucketsResult>
	<Owner>
		<ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
	</Owner>
	<Buckets>
		<Bucket>
			<Name>examplebucket-1250000000 </Name>
			<Location>ap-guangzhou</Location>
			<CreationDate>2022-04-11T03:01:49Z</CreationDate>
			<BucketType>cos</BucketType>
		</Bucket>
	</Buckets>
	<Buckets>
		<Bucket>
			<Name>examplebucket1-1250000000 </Name>
			<Location>ap-guangzhou</Location>
			<CreationDate>2022-04-12T03:01:49Z</CreationDate>
			<BucketType>cos</BucketType>
		</Bucket>
	</Buckets>
</ListAllMyBucketsResult>
```


#### Example 5. Filtering the list of buckets based on creation time

List buckets whose creation time is earlier than `2022-1-20 15:10:45`. 

#### Request

```plaintext
GET /?range=lt&create-time=1642662645 HTTP/1.1
Host: service.cos.myqcloud.com
User-Agent: curl/7.64.1
Accept: */*
Authorization: q-sign-algorithm=sha1&q-ak=AKIDYv3vWrwkHXVDfqk*****&q-sign-time=1667448802;1668448852&q-key-time=1667448802;1668448852&q-url-param-list=create-time;range&q-header-list=host&q-signature=a043c0593c8c4cd1caf570******
```


#### Response


```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 5566
Connection: keep-alive
Date: Thu, 03 Nov 2022 04:14:23 GMT
Server: tencent-cos
x-cos-request-id: NjM2MzQwMWZfMmJiMjM1MGFfYTc******

<ListAllMyBucketsResult>
	<Owner>
		<ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
	</Owner>
	<Buckets>
		<Bucket>
			<Name>examplebucket-1250000000</Name>
			<Location>ap-beijing</Location>
			<CreationDate>2021-11-23T03:02:12Z</CreationDate>
			<BucketType>cos</BucketType>
		</Bucket>
	</Buckets>
</ListAllMyBucketsResult>
```

