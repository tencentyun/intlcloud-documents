## Feature Description

This API (`List Parts`) is used to query the uploaded parts in a specified multipart upload, i.e., listing all successfully uploaded parts in a multipart upload with the specified `uploadId`.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=ListParts&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>


## Request

#### Sample request

```shell
GET /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com, where &lt;BucketName-APPID> is the bucket name followed by the `APPID`, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request parameters

| Field |  Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | -------- |
| UploadId | Multipart upload ID, which is obtained from the response of the `Initiate Multipart Upload` API. | string | Yes |
| encoding-type | Encoding type of the returned value | string | No |
| max-parts | Maximum number of entries to be returned at a time. Maximum value: `1000`. Default value: `1000`. | string | No |
| part-number-marker | The marker after which the returned list begins. By default, entries are listed in UTF-8 binary order. | string | No |

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful query returns **application/xml** data, which includes the information on the successfully uploaded parts.

```shell
<?xml version="1.0" encoding="UTF-8" ?>
<ListPartsResult>
    <Bucket>examplebucket-1250000000</Bucket>
    <Encoding-type/>
    <Key>exampleobject</Key>
    <UploadId>14846420620b1f381e5d7b057692e131dd8d72dfa28f2633cfbbe4d0a9e8bd0719933545b0</UploadId>
    <Initiator>
        <ID>1250000000</ID>
        <DisplayName>1250000000</DisplayName>
    </Initiator>
    <Owner>
        <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
        <DisplayName>100000000001</DisplayName>
    </Owner>
    <PartNumberMarker>0</PartNumberMarker>
    <Part>
        <PartNumber>1</PartNumber>
        <LastModified>Tue Jan 17 16:43:37 2017</LastModified>
        <ETag>"a1f8e5e4d63ac6970a0062a6277e191fe09a1382"</ETag>
        <Size>5242880</Size>
    </Part>
    <NextPartNumberMarker>1</NextPartNumberMarker>
    <StorageClass>STANDARD</StorageClass>
    <MaxParts>1</MaxParts>
    <IsTruncated>true</IsTruncated>
</ListPartsResult>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------ | ---------------------------------- | --------- |
| ListPartsResult | None | Stores the response of `List Parts` | Container |

`ListPartsResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| -------------------- | --------------- | ------------------------------------------------------------ | --------- |
| Bucket               | ListPartsResult | Destination bucket for the multipart upload in the format of `BucketName-APPID`, such as `examplebucket-1250000000`. | string |
| Encoding-Type        | ListPartsResult | Encoding format                                                    | string    |
| Key                  | ListPartsResult | Object name | string |
| UploadId             | ListPartsResult | ID of the multipart upload | string |
| Initiator            | ListPartsResult | Information about the request initiator | Container |
| Owner                | ListPartsResult | Information of the part owner                                 | Container |
| StorageClass         | ListPartsResult | Storage class of the parts, such as `STANDARD`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925). | string |
| PartNumberMarker     | ListPartsResult | The marker after which the returned list begins. By default, entries are listed in UTF-8 binary order. | string |
| NextPartNumberMarker | ListPartsResult | The `NextMarker` after which the next returned list begins if the list is truncated. | string |
| MaxParts             | ListPartsResult | Maximum number of entries to be returned at a time                                       | string      |
| IsTruncated          | ListPartsResult | Whether the returned list is truncated. Valid values: `true`, `false`. | boolean |
| Part                 | ListPartsResult | Metadata                                                   | Container |

`Initiator` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------- | -------------------- | ------ |
| ID | ListPartsResult.Initiator | Unique ID of the initiator | string |
| DisplayName        | ListPartsResult.Initiator | Username of the initiator | string |

`Owner` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | --------------------- | -------------------- | ------ |
| ID                 | ListPartsResult.Owner | Unique ID of the owner | string |
| DisplayName        | ListPartsResult.Owner | Username of the owner | string |

`Part` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | -------------------- | ----------------------- | ------ |
| PartNumber         | ListPartsResult.Part | Part number                | string |
| LastModified       | ListPartsResult.Part | Last modified time of the part    | string |
| ETag               | ListPartsResult.Part | MD5 checksum of the part     | string |
| Size               | ListPartsResult.Part | Part size in bytes | string |

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


## Samples

#### Request

```shell
GET /exampleobject?uploadId=1585130821cbb7df1d11846c073ad648e8f33b087cec2381df437acdc833cf654b9ecc6361 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 25 Mar 2020 10:07:25 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1585130845;1585138045&q-key-time=1585130845;1585138045&q-header-list=date;host&q-url-param-list=uploadid&q-signature=ba8d97cefa396d804524a38d7b5412fb0261****
Connection: close
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1119
Connection: close
Date: Wed, 25 Mar 2020 10:07:25 GMT
Server: tencent-cos
x-cos-request-id: NWU3YjJkNWRfMjNhZjJhMDlfNWY5Ml8zMmUy****



<ListPartsResult>
			<Bucket>examplebucket-1250000000</Bucket>
			<EncodingType/>
			<Key>exampleobject</Key>
			<UploadId>1585130821cbb7df1d11846c073ad648e8f33b087cec2381df437acdc833cf654b9ecc6361</UploadId>
			<Owner>
				<ID>1250000000</ID>
				<DisplayName>1250000000</DisplayName>
			</Owner>
			<PartNumberMarker>0</PartNumberMarker>
			<Initiator>
				<ID>qcs::cam::uin/100000000001:uin/100000000011</ID>
				<DisplayName>100000000011</DisplayName>
			</Initiator>
			<Part>
				<PartNumber>1</PartNumber>
				<LastModified>2020-03-25T10:07:14.000Z</LastModified>
				<ETag>&quot;39270a968a357d24207e9911162507eb&quot;</ETag>
				<Size>1048576</Size>
			</Part>
			<Part>
				<PartNumber>2</PartNumber>
				<LastModified>2020-03-25T10:07:13.000Z</LastModified>
				<ETag>&quot;d899fbd1e06109ea2e4550f5751c88d6&quot;</ETag>
				<Size>1048576</Size>
			</Part>
			<Part>
				<PartNumber>3</PartNumber>
				<LastModified>2020-03-25T10:07:13.000Z</LastModified>
				<ETag>&quot;762890d6c9a871b7bd136037cb2260cd&quot;</ETag>
				<Size>1048576</Size>
			</Part>
			<StorageClass>Standard</StorageClass>
			<MaxParts>1000</MaxParts>
			<IsTruncated>false</IsTruncated>
</ListPartsResult>
```
