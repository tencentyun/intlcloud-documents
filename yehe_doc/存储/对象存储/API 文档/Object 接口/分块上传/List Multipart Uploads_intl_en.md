## Overview
This API is used to query the ongoing multipart uploads. Up to 1,000 multipart uploads can be listed in a single request.

>! 
>The request requires read access to the bucket. Only the root account or sub-accounts granted the permissions of the `List Multipart Upload` API can call this API.
>

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=ListMultipartUploads&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
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

```shell
GET /?uploads HTTP/1.1
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

#### Request parameters

The parameters are as follows: <style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

| Parameter | Description | Type | Required |
| ---------------- | ---------------------------------------- | ------ | ---- |
| delimiter | A symbol. The identical paths between `prefix` and the first occurrence of the `delimiter` are grouped and defined as a common prefix. If `prefix` is not specified, the common prefix starts with the beginning of the path. | String | No |
| encoding-type | Encoding type for the returned value. Valid value: `url` | String | No |
| prefix | A prefix that the returned object keys must start with. </br>Note that if you use this parameter, the returned keys will contain this prefix. | String | No |
| max-uploads | Sets the maximum number of multipart uploads that can be returned at a time. Value range: 1−1000. Defaults to `1000`. | Int | No |
| key-marker | This parameter is used together with `upload-id-marker`: <Br/><li>If `upload-id-marker` is not specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed.<Br/><li>If `upload-id-marker` is specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed, and multipart uploads whose `ObjectName` is lexicographically equal to `key-marker` with `UploadId` greater than `upload-id-marker` will be listed. | String | No |
| upload-id-marker | This parameter is used together with `key-marker`: <Br/><li>If `key-marker` is not specified, `upload-id-marker` will be ignored. <Br/><li>If `key-marker` is specified, multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed, and multipart uploads whose `ObjectName` is lexicographically equal to `key-marker` with `UploadId` greater than `upload-id-marker` will be listed. | String | No |

#### Request body
The request body of this request is empty.

## Response

#### Response headers
This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<ListMultipartUploadsResult>
  <Bucket></Bucket>
  <Encoding-Type></Encoding-Type>
  <KeyMarker></KeyMarker>
  <UploadIdMarker></UploadIdMarker>
  <NextKeyMarker></NextKeyMarker>
  <NextUploadIdMarker></NextUploadIdMarker>
  <MaxUploads></MaxUploads>
  <IsTruncated></IsTruncated>
  <Prefix></Prefix>
  <Delimiter></Delimiter>
  <Upload>
    <Key></Key>
    <UploadId></UploadId>
    <StorageClass></StorageClass>
    <Initiator>
      <ID></ID>
	<DisplayName></DisplayName>
    </Initiator>
    <Owner>
      <ID></ID>
	<DisplayName></DisplayName>
    </Owner>
    <Initiated></Initiated>
  </Upload>
  <CommonPrefixes>
    <Prefix></Prefix>
  </CommonPrefixes>
</ListMultipartUploadsResult>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| ListMultipartUploadsResult | None | Information about all multipart uploads | Container |

Content of `ListMultipartUploadsResult`:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Bucket | ListMultipartUploadsResult | Destination bucket for the multipart upload. It is formed by connecting a user-defined string and the system-generated `APPID` with a hyphen, for example, `examplebucket-1250000000`. | String |
| Encoding-Type | ListMultipartUploadsResult | Encoding type for the returned value. Valid value: `url` | String |
| KeyMarker | ListMultipartUploadsResult | The key where the listing should start |  String |
| UploadIdMarker | ListMultipartUploadsResult| The `UploadId` where the listing should start  | String |
| NextKeyMarker | ListMultipartUploadsResult | If the returned list is truncated, the `NextKeyMarker` returned will be the starting point of the next list. | String |
| NextUploadIdMarker | ListMultipartUploadsResult | If the returned list is truncated, the `UploadId` returned will be the starting point of the next list. | String |
| MaxUploads | ListMultipartUploadsResult | Maximum number of multipart uploads that can be returned at a time. Value range: 0−1000 | int |
| IsTruncated | ListMultipartUploadsResult | Whether the returned list is truncated. Valid values: `TRUE`, `FALSE` | Boolean |
| Prefix | ListMultipartUploadsResult | A prefix that the returned object keys must start with. </br>Note that if you use this parameter, the returned keys will contain this prefix. | String |
| Delimiter | ListMultipartUploadsResult | A symbol. The identical paths between `Prefix` and the first occurrence of the `Delimiter` are grouped and defined as a common prefix. If `Prefix` is not specified, the common prefix starts with the beginning of the path. | String |
| Upload | ListMultipartUploadsResult | Information about each upload | Container |
| CommonPrefixes | ListMultipartUploadsResult | The identical paths between `prefix` and `delimiter` are grouped and defined as a common prefix. | Container |

Content of `Upload`:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Key | ListMultipartUploadsResult.Upload | Name of the object | String |
| UploadID | ListMultipartUploadsResult.Upload | ID of the multipart upload | String |
| StorageClass | ListMultipartUploadsResult.Upload | Storage class of the parts. Enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String |
| Initiator | ListMultipartUploadsResult.Upload | Information about the upload initiator | Container |
| Owner | ListMultipartUploadsResult.Upload | Information about the part owner |  Container |
| Initiated | ListMultipartUploadsResult.Upload | Time when the multipart upload is started |  Date |

Content of `Initiator`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
| ID | ListMultipartUploadsResult.Upload.Initiator | Unique CAM ID of the upload initiator | String  |
| DisplayName | ListMultipartUploadsResult.Upload.Initiator | User ID (UIN) | String  |

Content of `Owner`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
| ID | ListMultipartUploadsResult.Upload.Owner | Unique CAM ID of the part owner | String  |
| DisplayName | ListMultipartUploadsResult.Upload.Owner| User ID (UIN) | String  |

Content of `CommonPrefixes`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
| Prefix | ListMultipartUploadsResult.CommonPrefixes | A common prefix | String |

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Request

```shell
GET /?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 18 Jan 2015 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484727508;32557623508&q-key-time=1484727508;32557623508&q-header-list=host&q-url-param-list=uploads&q-signature=5bd4759a7309f7da9a0550c224d8c61589c9****
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1203
Date: Wed, 18 Jan 2015 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjI0ZGRfNDQyMDRlXzNhZmRf****

<ListMultipartUploadsResult>
    <Bucket>examplebucket-1250000000</Bucket>
    <Encoding-Type/>
    <KeyMarker/>
    <UploadIdMarker/>
    <MaxUploads>1000</MaxUploads>
    <Prefix/>
    <Delimiter>/</Delimiter>
    <IsTruncated>false</IsTruncated>
    <Upload>
        <Key>Object</Key>
        <UploadId>1484726657932bcb5b17f7a98a8cad9fc36a340ff204c79bd2f51e7dddf0b6d1da6220520c</UploadId>
        <Initiator>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Initiator>
        <Owner>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Owner>
        <StorageClass>Standard</StorageClass>
        <Initiated>Wed Jan 18 16:04:17 2017</Initiated>
    </Upload>
    <Upload>
        <Key>Object</Key>
        <UploadId>1484727158f2b8034e5407d18cbf28e84f754b791ecab607d25a2e52de9fee641e5f60707c</UploadId>
        <Initiator>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Initiator>
        <Owner>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Owner>
        <StorageClass>Standard</StorageClass>
        <Initiated>Wed Jan 18 16:12:38 2017</Initiated>
    </Upload>
    <Upload>
        <Key>exampleobject</Key>
        <UploadId>1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e</UploadId>
        <Initiator>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Initiator>
        <Owner>
           <ID>qcs::cam::uin/100000000001:uin/100000000001</ID>
		<DisplayName>100000000001</DisplayName>
        </Owner>
        <StorageClass>Standard</StorageClass>
        <Initiated>Wed Jan 18 16:14:30 2017</Initiated>
    </Upload>
</ListMultipartUploadsResult>
```
