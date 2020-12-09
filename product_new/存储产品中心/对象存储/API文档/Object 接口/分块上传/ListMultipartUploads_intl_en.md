## Description
This API is used to query the ongoing multipart uploads. A single request operation can list up to 1,000 multipart uploads.

> To make the request, you need to have the permission to read the bucket.

## Request
####  Sample Request

```shell
GET /?uploads HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)

####  Request Headers

The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


####  Request Parameters
The content is described in details below: <style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

| Name | Description | Type | Required |
| ---------------- | ---------------------------------------- | ------ | ---- |
| delimiter | The delimiter is a symbol. The delimiter is a symbol. The identical paths between `prefix` or, if no `prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix  | String | No |
| encoding-type    | Specifies the encoding type of the returned value; valid value: `url` | String | No |
| prefix | Sets that the response will only contain object keys with the specified prefix. </br>When you make a query with `prefix` specified, the returned keys will still contain `Prefix` | String | No |
| max-uploads | Sets the maximum number of multipart uploads returned. Value range: [1, 1,000]. Default value: 1,000 | String | No |
| key-marker | Used together with `upload-id-marker`. <Br>If `upload-id-marker` is not specified, only the multipart uploads whose `ObjectName` is lexicographically greater than `key-marker` will be listed; <Br/>If `upload-id-marker` is specified, the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed, and any multipart upload whose `ObjectName` lexicographically equals `key-marker` and whose `UploadId` is greater than `upload-id-marker` will also be listed | String | No |
| upload-id-marker | Used together with `key-marker`. <Br>If `key-marker` is not specified, `upload-id-marker` will be ignored; <Br/>If `key-marker` is specified, the multipart uploads whose `ObjectName` is lexicographically greater than the specified `key-marker` will be listed, and any multipart upload whose `ObjectName` lexicographically equals `key-marker` and whose `UploadId` is greater than `upload-id-marker` will also be listed | String | No |

####  Request Body
The request body of this request is empty.

## Response

####  Response Headers
This API only returns common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

### Response Body
This response body returns **application/xml** data. The following contains all the node data:

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

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| ListMultipartUploadsResult | None | Information on all multipart uploads | Container |

Content of the Container node `ListMultipartUploadsResult`:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Bucket | InitiateMultipartUploadResult | Destination bucket for a multipart upload, which is formed by connecting a user-defined string and the system-generated APPID with a hyphen, such as `examplebucket-1250000000` | String |
| Encoding-Type | ListMultipartUploadsResult | Specifies the encoding type of the returned value; valid value: `url` | String |
| KeyMarker | ListMultipartUploadsResult| The key value where the entry list starts                                      | String |
| UploadIdMarker | ListMultipartUploadsResult| The `uploadId` value where the entry list starts  | String |
| NextKeyMarker | ListMultipartUploadsResult | If the returned list is truncated, the `NextKeyMarker` returned will be the starting point of the subsequent list | String |
| NextUploadIdMarker | ListMultipartUploadsResult | If the returned list is truncated, the `UploadId` returned will be the starting point of the subsequent list | String |
| MaxUploads | ListMultipartUploadsResult | Sets the maximum number of multipart uploads returned. Value range: [0, 1,000] | String |
| IsTruncated | ListMultipartUploadsResult | Whether the returned list is truncated, which is a boolean value. Valid values: `TRUE`, `FALSE` |  Boolean |
| Prefix | ListMultipartUploadsResult | Sets that the response will only contain object keys with the specified `Prefix`. </br>When you make a query with `prefix` specified, the returned keys will still contain `Prefix` | String |
| Delimiter | ListMultipartUploadsResult | The delimiter is a symbol. The identical paths between `prefix` or, if no `prefix` is specified, the beginning and the first `delimiter` are grouped and defined as a common prefix | String |
| Upload | ListMultipartUploadsResult | Information on each upload | Container |
| CommonPrefixes | ListMultipartUploadsResult | The identical paths between `prefix` and `delimiter` are grouped and defined as a common prefix | Container |

Content of the Container node `Upload`:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Key | ListMultipartUploadsResult.Upload |  Object name |  String |
| UploadID | ListMultipartUploadsResult.Upload | ID of a multipart upload | String |
| StorageClass | ListMultipartUploadsResult.Upload |  Indicates the storage class of the parts; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE` | String    |
| Initiator | ListMultipartUploadsResult.Upload | Information on the initiator of an upload                                 | Container |
| Owner | ListMultipartUploadsResult.Upload | Information on the owner of the parts |  Container |
| Initiated | ListMultipartUploadsResult.Upload |  Starting time of a multipart upload |  Date |

Content of the Container node `Initiator`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
| ID | ListMultipartUploadsResult.Upload.Initiator | Unique CAM ID of the user | String  |
| DisplayName | ListMultipartUploadsResult.Upload.Initiator | User ID (UIN) | String  |

Content of the Container node `Owner`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
| ID | ListMultipartUploadsResult.Upload.Owner | Unique CAM ID of the user | String  |
| DisplayName | ListMultipartUploadsResult.Upload.Owner| User ID (UIN) | String  |

Content of the Container node `CommonPrefixes`:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
| Prefix | ListMultipartUploadsResult.CommonPrefixes | Displays a specific common prefix | String |

### Error Codes

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Example

### Request

```shell
GET /?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 18 Jan 2015 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484727508;32557623508&q-key-time=1484727508;32557623508&q-header-list=host&q-url-param-list=uploads&q-signature=5bd4759a7309f7da9a0550c224d8c61589c9****
```

### Response

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
