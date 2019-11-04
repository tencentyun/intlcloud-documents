## Description
This API (Complete Multipart Upload) is used to complete the entire multipart upload. After all parts are uploaded using the Upload Parts API, this API must be called to complete the multipart upload of the entire file. When using this API, you must specify the PartNumber and ETag of each part in the request body to verify the accuracy of parts.
As the parts need to be merged after they are uploaded, and the merge takes several minutes, when the merge starts, COS will immediately return status code 200 and periodically return space information during the merge process to keep the connection active until the merge is completed. After that, COS will return the content of the merged parts in the response body.
- If the uploaded part size is below 1 MB, 400 EntityTooSmall will be returned when this API is called.
- If the uploaded part numbers are not continuous, 400 InvalidPart will be returned when this API is called.
- If the part information entries in the request body are not sorted by number in ascending order, 400 InvalidPartOrder will be returned when this API is called.
- If the UploadId does not exist, 404 NoSuchUpload will be returned when this API is called.

>**Note:**
> It is recommended that you either complete or abort the multipart upload in a timely manner, as the parts that have been uploaded but not completed will take up storage space and incur storage fees.

### Version
If versioning is enabled, the GET operation will return the current version of the object. To return a different version, use the versionId parameter.

## Request
### Request Example

```shell
POST /<ObjectKey>?uploadId=UploadId HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).


### Request Headers

This API only returns a common response header. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).



### Request Body
The specific nodes of the request body for this API request are:

```shell
<CompleteMultipartUpload>
  <Part>
    <PartNumber>1</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9773"</ETag>
  </Part>
  <Part>
    <PartNumber>2</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9773"</ETag>
  </Part>
    ...
</CompleteMultipartUpload>
```

Detailed data is as shown below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :---------------------- | :--- | :-------------- | :-------- | :--- |
| CompleteMultipartUpload | None | All information of this multipart upload | Container | Yes |

Content of the Container node CompleteMultipartUpload:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :-------- | :---------------------- | :---------------- | :-------- | :--- |
| Part      | CompleteMultipartUpload | Information of each part in this multipart upload | Container | Yes |

Content of the Container node Part:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :--------- | :--------------------------- | :--------------- | :------ | :--- |
| PartNumber | CompleteMultipartUpload.Part | Part number              | Integer | Yes    |
| ETag       | CompleteMultipartUpload.Part | MD5 checksum of each file part | String | Yes |

## Response

### Response Headers
#### Common Response Headers 
This response uses a common response header. For more information about the common response header, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers

**Server-side encryption related response**

| Name | Description | Type |
| ---------------------------- | ---------------------------------------- | ------ |
| x-cos-server-side-encryption | This specifies how the server-side encryption is enabled for the object. <br/>For encryption with the COS master key, enter AES256 | String |


### Response Body
The return of this response body is **application/xml** data. Below is a sample containing all the node data:

```shell
<CompleteMultipartUploadResult>
    <Location>examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject</Location>
    <Bucket>examplebucket-1250000000</Bucket>
    <Key>exampleobject</Key>
    <ETag>"3a0f1fd698c235af9cf098cb74aa25bc"</ETag>
</CompleteMultipartUploadResult>
```

Detailed data is as shown below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :---------------------------- | :--- | :------- | :-------- |
| CompleteMultipartUploadResult | None | This describes all the returned information | Container |

Content of the Container node CompleteMultipartUploadResult:

| Node Name (Keyword) | Parent Node | Description | Type |
| :-------- | :---------------------------- | :--------------------------------------- | :----- |
| Location  | CompleteMultipartUploadResult | Public network access domain name for the created object                         | URL    |
| Bucket    | CompleteMultipartUploadResult | Destination bucket for the multipart upload, which is formatted as bucketname-appid, such as examplebucket-1250000000 | String |
| Key       | CompleteMultipartUploadResult | Object name                                | String |
| ETag      | CompleteMultipartUploadResult | The unique tag value of the merged object, which is not the MD5 checksum of the object's content and can only be used to check the object's uniqueness. | String |

## Samples

### Request
```shell
POST /exampleobject?uploadId=1484728886e63106e87d8207536ae8521c89c42a436fe23bb58854a7bb5e87b7d77d4ddc48 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed，18 Jan 2017 16:17:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484729794;32557625794&q-key-time=1484729794;32557625794&q-header-list=host&q-url-param-list=uploadId&q-signature=23627c8fddb3823cce4257b33c663fd83f9f****
Content-Length: 138

<CompleteMultipartUpload>
  <Part>
    <PartNumber>1</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9773"</ETag>
  </Part>
  <Part>
    <PartNumber>2</PartNumber>
    <ETag>"fc392a65890e447ff4e2d256489a9774"</ETag>
  </Part>
</CompleteMultipartUpload>
```

### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 277
Connection: keep-alive
Date: Wed，18 Jan 2017 16:17:03 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjJlMjVfNDYyMDRlXzM0YzRfMjc1

<CompleteMultipartUploadResult>
    <Location>examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject</Location>
    <Bucket>examplebucket-1250000000</Bucket>
    <Key>exampleobject</Key>
    <ETag>"3a0f1fd698c235af9cf098cb74aa25bc"</ETag>
</CompleteMultipartUploadResult>
```
