## Overview

This API is used to query the uploaded parts of a specified multipart upload, i.e., listing all successfully uploaded parts of a multipart upload whose `uploadId` is specified.


>?
>Only the root account or sub-accounts granted the permission of the `List Part` API can call this API.
>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=ListParts&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
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
GET /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com, where &lt;BucketName-APPID> is the bucket name followed by the `APPID`, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request fields

| Parameter | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | -------- |
| uploadId | Multipart upload ID obtained from the `Initiate Multipart Upload` API | string | Yes |
| encoding-type | Encoding type for the returned value | string | No |
| max-parts | Maximum number of entries to be returned at a time. Maximum value: `1000`. Default value: `1000`. | int | No |
| part-number-marker | By default, parts are listed in UTF-8 binary order, starting from the part after the marker. | string | No |

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

A successful query returns **application/xml** data, which includes information about the successfully uploaded parts.

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------ | ---------------------------------- | --------- |
| ListPartsResult | None | Stores the response of `List Parts`. | Container |

Content of `ListPartsResult`:

| Node Name (Keyword) | Parent Node | Description | Type |
| -------------------- | --------------- | ------------------------------------------------------------ | --------- |
| Bucket | ListPartsResult | Name of the destination bucket for the multipart upload. It is formed by connecting a user-defined string and the system-generated `APPID` with a hyphen, for example, `examplebucket-1250000000`. | string |
| Encoding-Type | ListPartsResult | Encoding type | string |
| Key | ListPartsResult | Object name | string |
| UploadId | ListPartsResult | ID of the multipart upload | string |
| Initiator | ListPartsResult | Information about the request initiator | Container |
| Owner | ListPartsResult | Information about the part owner | Container |
| StorageClass | ListPartsResult | Storage class of the parts. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`, `DEEP_ARCHIVE`. For more information, please see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | string |
| PartNumberMarker | ListPartsResult | By default, parts are listed in UTF-8 binary order, starting from the part after the marker.  | string |
| NextPartNumberMarker | ListPartsResult | If the returned list is truncated, the `NextMarker` returned will be the starting point of the subsequent list.   | string    |
| MaxParts             | ListPartsResult | Maximum number of entries to be returned at a time                                       | int |
| IsTruncated | ListPartsResult | Indicates whether the returned list is truncated. Valid values: `true`, `false` | boolean |
| Part | ListPartsResult | Metadata | Container |

Content of `Initiator`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------- | -------------------- | ------ |
| ID | ListPartsResult.Initiator | Unique ID of the initiator | string |
| DisplayName | ListPartsResult.Initiator | Username of the initiator | string |

Content of `Owner`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | --------------------- | -------------------- | ------ |
| ID | ListPartsResult.Owner | Unique ID of the owner | string |
| DisplayName | ListPartsResult.Owner | Username of the owner | string |

Content of `Part`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | -------------------- | ----------------------- | ------ |
| PartNumber         | ListPartsResult.Part | Part number                | string |
| LastModified       | ListPartsResult.Part | Last modified time of a part | string |
| ETag               | ListPartsResult.Part | MD5 checksum of a part | string |
| Size               | ListPartsResult.Part | Part size, in bytes | string |

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


## Examples

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

