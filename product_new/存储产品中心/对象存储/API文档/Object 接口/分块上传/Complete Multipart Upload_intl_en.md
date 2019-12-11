## Description
This API is used to complete a multipart upload. After all parts are uploaded via the `Upload Part` API, you need to call this API to complete the multipart upload. When using this API, you need to specify the `PartNumber` and `ETag` of each part in the request body for the part information to be verified.
As the parts need to be merged after they are uploaded, and the merge takes several minutes, COS will immediately return status code `200` when the merge starts, and periodically return spaces during the merge to keep the connection active until the merge is complete. After that, COS will return the content of the merged object in the response body.
- If any uploaded part is below 1 MB in size, `400 EntityTooSmall` will be returned when this API is called.
- If the numbers of the uploaded parts are not continuous, `400 InvalidPart` will be returned when this API is called.
- If the part information entries in the request body are not sorted by number in ascending order, `400 InvalidPartOrder` will be returned when this API is called.
- If the `uploadId` does not exist, `404 NoSuchUpload` will be returned when this API is called.

><font color="#0000cc">**Note：** </font>
>It is recommended to either complete or abort a multipart upload as early as possible, as the uploaded parts of an incomplete multipart upload will take up storage capacity and incur storage fees.

### Version
If versioning is enabled, the `GET` operation will return the current version of the object. To obtain a different version, please use the `versionId` parameter.

## Request

Syntax example:
```
POST /ObjectName?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

### Request Line
```
POST /ObjectName?uploadId=UploadId HTTP/1.1
```
This API allows POST requests.
#### Request Parameters <style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

See the details below:

| Parameter Name | Description | Type | Required |
| :------- | :--------------------------------------- | :----- | :--- |
| uploadId | ID of this multipart upload. <br>When the `Initiate Multipart Upload` API is used to initialize a multipart upload, an `uploadId` will be returned. The ID uniquely identifies the data of the part and its position in the entire file | String | Yes |

### Request Headers

#### Common Headers
The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
This request operation does not use any special request header.

### Request Body
The node content of this request body is:
```
<CompleteMultipartUpload>
  <Part>
    <PartNumber></PartNumber>
    <ETag></ETag>
  </Part>
  ...
</CompleteMultipartUpload>
```

The data are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :---------------------- | :--- | :-------------- | :-------- | :--- |
| CompleteMultipartUpload | None | Describes all information on this multipart upload | Container | Yes |

Content of the Container node `CompleteMultipartUpload`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :-------- | :---------------------- | :---------------- | :-------- | :--- |
| Part      | CompleteMultipartUpload | Describes information on each part in this multipart upload | Container | Yes |

Content of the Container node `Part`:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :--------- | :--------------------------- | :--------------- | :------ | :--- |
| PartNumber | CompleteMultipartUpload.Part | Part number              | Integer | Yes    |
| ETag       | CompleteMultipartUpload.Part | MD5 checksum of each part | String | Yes |
## Response

### Response Headers
#### Common Response Headers 
This response uses common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers

| Name | Description | Type |
| ---------------------------- | ---------------------------------------- | ------ |
| x-cos-server-side-encryption | Specifies how the server-side encryption is enabled for the object. <br/>For encryption with a COS master key, pass in `AES256` | String |
|x-cos-version-id| Version ID of the new object if versioning is enabled for the bucket | String |


### Response Body
This response body returns **application/xml** data. The following contains all the node data:
```
<CompleteMultipartUploadResult>
  <Location></Location>
  <Bucket></Bucket>
  <Key></Key>
  <ETag></ETag>
</CompleteMultipartUploadResult>
```
The data are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :---------------------------- | :--- | :------- | :-------- |
| CompleteMultipartUploadResult | None | Describes all the returned information | Container |

Content of the Container node `CompleteMultipartUploadResult`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :-------- | :---------------------------- | :--------------------------------------- | :----- |
| Location  | CompleteMultipartUploadResult | Public network domain name used to access the new object                         | URL    |
| Bucket    | CompleteMultipartUploadResult | Destination bucket for the multipart upload, which is formed by connecting a user-defined string and the system-generated appid with a hyphen, such as `mybucket-1250000000` | String |
| Key       | CompleteMultipartUploadResult | Object name                                | String |
| ETag      | CompleteMultipartUploadResult | The unique tag value of the merged object, which is not the MD5 checksum of the object's content and can only be used to check the object's uniqueness. | String |

## Example

### Request
```
POST /ObjectName?uploadId=1484728886e63106e87d8207536ae8521c89c42a436fe23bb58854a7bb5e87b7d77d4ddc48 HTTP/1.1
Host: arlenhuangtestsgnoversion-1251668577.cos.ap-beijing.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484729794;32557625794&q-key-time=1484729794;32557625794&q-header-list=host&q-url-param-list=uploadId&q-signature=23627c8fddb3823cce4257b33c663fd83f9f820d
Content-Length: 138

<CompleteMultipartUpload><Part><PartNumber>1</PartNumber><ETag>"fc392a65890e447ff4e2d256489a9773"</ETag></Part></CompleteMultipartUpload>
```

### Response
```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 277
Connection: keep-alive
Date: Wed，18 Jan 2017 16:17:03 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjJlMjVfNDYyMDRlXzM0YzRfMjc1

<CompleteMultipartUploadResult>
    <Location>arlenhuangtestsgnoversion-1251668577.cos.ap-beijing.myqcloud.com/ObjectName</Location>
    <Bucket>arlenhuangtestsgnoversion-1251668577</Bucket>
    <Key>ObjectName</Key>
    <ETag>"3a0f1fd698c235af9cf098cb74aa25bc"</ETag>
</CompleteMultipartUploadResult>

```
