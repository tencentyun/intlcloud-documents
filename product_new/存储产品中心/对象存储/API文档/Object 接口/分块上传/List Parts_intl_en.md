## Description

This API is used to query the uploaded parts of a specified multipart upload, i.e., listing all successfully uploaded parts of a multipart upload whose `uploadId` is specified.

## Request

### Sample Request

```
GET /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

### Request Headers

The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request Parameters

| Name | Type | Required | Description |
| ------------------ | ------ | ---- | ------------------------------------------------------------ |
| uploadId | String | Yes | ID of this multipart upload. When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file |
| encoding-type      | string | No | Specifies the encoding type of the returned value |
| max-parts          | string | No   | Maximum number of entries returned at a time. Default value: 1,000                             |
| part-number-marker | string | No   | By default, entries are listed in UTF-8 binary order starting from `marker`  |

### Request Body

The request body of this request is empty.

## Response

### Response Headers

This response contains common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

### Response Body

A successful query returns **application/xml** data which include the information on the successfully uploaded parts.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<ListPartsResult>
    <Bucket>examplebucket-1250000000</Bucket>
    <Encoding-type/>
    <Key>exampleobject</Key>
    <UploadId>14846420620b1f381e5d7b057692e131dd8d72dfa28f2633cfbbe4d0a9e8bd0719933545b0</UploadId>
    <Initiator>
        <ID>1250000000</ID>
        <DisplyName>1250000000</DisplyName>
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

The data are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------ | ---------------------------------- | --------- |
| ListPartsResult | None | Stores the result of the `List Parts` request | Container |

Content of the Container node `ListPartsResult`:

| Node Name (Keyword) | Parent Node | Description | Type |
| -------------------- | --------------- | ------------------------------------------------------------ | --------- |
| Bucket               | ListPartsResult | Name of the destination bucket for the multipart upload, which is formed by connecting a user-defined string and the system-generated APPID with a hyphen, such as `examplebucket-1250000000` | string |
| Encoding-Type | ListPartsResult | Encoding type | string |
| Key                  | ListPartsResult | Object name                                                | string    |
| UploadId             | ListPartsResult | ID which identifies this multipart upload                                        | string    |
| Initiator            | ListPartsResult | Information on the creator of the parts                                 | Container |
| Owner              | ListPartsResult | Information on the owner of the parts                                 | Container |
| StorageClass         | ListPartsResult | Indicates the storage class of the parts; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | string    |
| PartNumberMarker     | ListPartsResult | By default, entries are listed in UTF-8 binary order starting from `marker`  | string    |
| NextPartNumberMarker | ListPartsResult | If the returned list is truncated, the `NextMarker` returned will be the starting point of the subsequent list   | string    |
| MaxParts             | ListPartsResult | Maximum number of entries returned at a time                                       | string    |
| IsTruncated          | ListPartsResult | Whether the returned list is truncated, which is a boolean value. Valid values: `true`, `false`                  | boolean   |
| Part                 | ListPartsResult | Metadata                                                   | Container |

Content of the Container node `Initiator`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------- | -------------------- | ------ |
| ID                 | ListPartsResult.Initiator | Unique ID of the creator | string |
| DisplayName        | ListPartsResult.Initiator | Creator's username   | string |

Content of the Container node `Owner`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | --------------------- | -------------------- | ------ |
| ID                 | ListPartsResult.Owner | Unique ID of the owner | string |
| DisplayName        | ListPartsResult.Owner | Owner's username   | string |

Content of the Container node `Part`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | -------------------- | ----------------------- | ------ |
| PartNumber         | ListPartsResult.Part | Part number                | string |
| LastModified       | ListPartsResult.Part | Last modified time of a part | string |
| ETag               | ListPartsResult.Part | MD5 checksum of a part | string |
| Size               | ListPartsResult.Part | Part size in bytes | string |

## Example

### Request

```
GET /exampleobject?uploadId=1585130821cbb7df1d11846c073ad648e8f33b087cec2381df437acdc833cf654b9ecc6361 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 25 Mar 2020 10:07:25 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1585130845;1585138045&q-key-time=1585130845;1585138045&q-header-list=date;host&q-url-param-list=uploadid&q-signature=ba8d97cefa396d804524a38d7b5412fb0261****
Connection: close
```

### Response

```
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
