## Description
This API (List Multipart Uploads) is used to query the multipart uploads in progress. Up to 1,000 ones can be listed in one single request operation.

> You need to have read permission to the bucket.

## Request
### Sample Request

```
GET /?uploads HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)

### Request Headers

#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
This request operation has no special request headers.

### Request Parameter

The specific content is as follows: <style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

| Name | Description | Type | Required |
| ---------------- | ---------------------------------------- | ------ | ---- |
| delimiter | The delimiter is a symbol. The specified prefix in the object name before the first delimiter character is defined as a set of elements: common prefix. If there is no prefix, it starts at the beginning of the path | String | No |
| encoding-type    | Specifies the encoding method of the return value; value range: url | String | No |
| prefix | Specifies that the returned object key must be prefixed with the "prefix". </br>Note that when a prefix query is used, the returned key will still contain the prefix | String | No |
| max-uploads | Sets the maximum number of parts returned between 1 and 1,000. Default value: 1,000 | String | No |
| key-marker | Used together with upload-id-marker. <Br>If upload-id-marker is not specified, only the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list; <Br/>otherwise, the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included, and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker | String | No |
| upload-id-marker | Used together with key-marker. <Br>If key-marker is not specified, upload-id-marker will be ignored; <Br/>otherwise, the multipart uploads with ObjectNames lexicographically greater than the specified key-marker will be included in the list, and any multipart uploads with ObjectNames equal to the key-marker will also be included, provided that they have UploadIDs lexicographically greater than the specified upload-id-marker | String | No |

### Request Body
The request body of this request is empty.

## Response

### Response Headers
#### Common Response Headers
This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response has no special response headers.

### Response Body
The return of this response body is **application/xml** data. Below is a sample containing all the node data:

```
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
    <UploadID></UploadID>
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

Detailed data is as shown below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| ListMultipartUploadsResult | None | Represents the information of all parts | Container |

Content of the Container node ListMultipartUploadsResult:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Bucket | InitiateMultipartUploadResult | Destination bucket for the multipart upload, which is formed by connecting the user-defined string and system-generated APPID with a dash, such as examplebucket-1250000000 | String |
| Encoding-Type | ListMultipartUploadsResult | Specifies the encoding method of the return value; value range: url | String |
| KeyMarker | ListMultipartUploadsResult| The entry list starts at this key value                                      | String |
| UploadIdMarker | ListMultipartUploadsResult| The entry list starts at this UploadId value | String |
| NextKeyMarker | ListMultipartUploadsResult | If the returned entries are truncated, then NextKeyMarker is the starting point of the next entry | String |
| NextUploadIdMarker | ListMultipartUploadsResult | If the returned entries are truncated, then UploadId is the starting point of the next entry | String |
| MaxUploads | ListMultipartUploadsResult | Sets the maximum number of parts returned between 0 and 1,000 | String |
| IsTruncated | ListMultipartUploadsResult | Whether returned entries are truncated, which is a boolean value (TRUE or FALSE) |  Boolean |
| Prefix | ListMultipartUploadsResult | Specifies that the returned object key must be prefixed with the "prefix". </br>Note that when a prefix query is used, the returned key will still contain the prefix | String |
| Delimiter | ListMultipartUploadsResult | The delimiter is a symbol. The specified prefix in the object name before the first delimiter character is defined as a set of elements: common prefix. If there is no prefix, it starts at the beginning of the path | String |
| Upload | ListMultipartUploadsResult | Information of each upload | Container |
| CommonPrefixes | ListMultipartUploadsResult | The identical paths between prefix and delimiter are grouped into one class and defined as a common prefix | Container |

Content of the Container node Upload:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Key | ListMultipartUploadsResult.Upload |  Object name |  String |
| UploadID | ListMultipartUploadsResult.Upload | ID of this multipart upload | String |
| StorageClass | ListMultipartUploadsResult.Upload |  Indicates the storage class of the parts; enumerated value: STANDARD, STANDARD_IA, ARCHIVE | String    |
| Initiator | ListMultipartUploadsResult.Upload | Identifies the initiator of this upload                                 | Container |
| Owner | ListMultipartUploadsResult.Upload | Identifies the owner of the parts |  Container |
| Initiated | ListMultipartUploadsResult.Upload |  Start time of the multipart upload |  Date |

Content of the Container node Initiator:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
| ID | ListMultipartUploadsResult.Upload.Initiator | Unique CAM ID of the user | String  |
| DisplayName | ListMultipartUploadsResult.Upload.Initiator | User ID (UIN) | String  |

Content of the Container node Owner:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
| ID | ListMultipartUploadsResult.Upload.Owner | Unique CAM ID of the user | String  |
| DisplayName | ListMultipartUploadsResult.Upload.Owner| User ID (UIN) | String  |

Content of the Container node CommonPrefixes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------ | ------------------------------------- | --------- |:--|
| Prefix | ListMultipartUploadsResult.CommonPrefixes | Displays the specific CommonPrefixes | String |

### Error Analysis
Some frequent special errors that may occur with this request are listed below:

| Error Code | HTTP Status Code | Description |
| ------------- | ------------------------------------ | ------------- |
| InvalidArgument | 400 Bad Request | max-uploads must be an integer between 0 and 1,000; otherwise, InvalidArgument will be returned. <br>The value of encoding-type can only be url; otherwise, InvalidArgument will be returned |

For more common error codes in COS or the complete list of errors, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

### Request

```
GET /?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 18 Jan 2015 21:32:00 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484727508;32557623508&q-key-time=1484727508;32557623508&q-header-list=host&q-url-param-list=uploads&q-signature=5bd4759a7309f7da9a0550c224d8c61589c9dbbf
```

### Response

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 1203
Date: Wed, 18 Jan 2015 21:32:00 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjI0ZGRfNDQyMDRlXzNhZmRfMjRl

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
        <UploadID>1484726657932bcb5b17f7a98a8cad9fc36a340ff204c79bd2f51e7dddf0b6d1da6220520c</UploadID>
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
        <UploadID>1484727158f2b8034e5407d18cbf28e84f754b791ecab607d25a2e52de9fee641e5f60707c</UploadID>
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
        <UploadID>1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e</UploadID>
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
