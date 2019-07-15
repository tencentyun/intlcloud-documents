## Description
An Initiate Multipart Upload API request is used to initialize a multipart upload. After the execution of this request, UploadId will be returned for the subsequent Upload Part requests.

## Request
### Request Example

```shell
POST /<ObjectKey>?uploads HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Headers

#### Common Headers
The implementation of this request operation uses a common request header. For more information about common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Request Headers
**Recommended headers**
The implementation of this request operation uses the following recommended request header information: <style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

| Name | Description | Type | Required |
| :------------------ | :--------------------------------------- | :----- | :--- |
| Cache-Control | Cache policy defined in RFC 2616, which will be stored as the object's metadata | String | No |
| Content-Disposition | File name defined in RFC 2616, which will be stored as the object's metadata | String | No |
| Content-Encoding | Encoding format defined in RFC 2616, which will be stored as the object's metadata | String | No |
| Content-Type | Content type (MIME) defined in RFC 2616, which will be stored as the object's metadata | String | No |
| Expires | File date and time defined in RFC 2616, which will be stored as the object's metadata | String | No |
| x-cos-meta-\* | This includes the suffix and information of the user-defined header, which will be returned as the object metadata of up to 2 KB. <br>**Note:** User-defined header information can contain underscores, but user-defined header suffixes cannot | String | No |
| x-cos-storage-class | This sets the storage class of the object. Enumerated values: STANDARD, STANDARD_IA, and ARCHIVE. Default value: STANDARD | String | No |

**Permission-related headers**

> For more information about request ACL, see [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583).

| Name | Description | Type | Required |
| :----------------------- | :--------------------------------------- | :----- | :--- |
| x-cos-acl | It defines the ACL attribute of the object. Value range: private, public-read, and default; default value: default (i.e., inheriting the bucket's permissions); <br>**Note:** Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, use "default" for this parameter or simply leave it blank, so that the object will inherit the permissions of the bucket | String | No |
| x-cos-grant-read | This grants the grantee the read permission in the format of x-cos-grant-read: id="[OwnerUin]" | String | No |
| x-cos-grant-full-control | This grants the grantee all permissions in the format of x-cos-grant-full-control: id="[OwnerUin]" | String | No |

**Server-side encryption-related headers**

This request operation can specify the data encryption policy when data is uploaded to COS. COS will automatically encrypt the data as it is written to the IDC and automatically decrypt it when you retrieve it. Currently, AES-256 encryption with the COS master key is supported. If you want to enable server-side encryption for your data, you need to pass in the following header:

| Name | Description | Type | Required |
| ---------------------------- | ---------------------------------------- | ------ | ------ |
| x-cos-server-side-encryption | This specifies how the server-side encryption is enabled for the object. <br/>For encryption with the COS master key, enter AES256 | String | Yes if encryption is needed |

### Request Body
The request body of this request is null.

## Response

### Response Headers
#### Common Response Headers 
This response uses a common response header. For more information about the common response header, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
**Server-side encryption-related response**

If it is specified to use server-side encryption when the file is uploaded, the response header will contain the following information:

| Name | Description | Type |
| ---------------------------- | ---------------------------------------- | ------ |
| x-cos-server-side-encryption | If the object is stored with COS-managed server-side encryption, the response will contain the values of this header and the encryption algorithm used (AES256) | string |

### Response Body
The return of this response body is **application/xml** data. Below is an example containing all the node data:
```shell
<InitiateMultipartUploadResult>
    <Bucket>examplebucket-1250000000</Bucket>
    <Key>exampleobject</Key>
    <UploadId>1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e</UploadId>
</InitiateMultipartUploadResult>
```
Detailed data is as shown below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :---------------------------- | :--- | :------- | :-------- |
| InitiateMultipartUploadResult | None | This describes all the returned information | Container |

Content of the Container node InitiateMultipartUploadResult:

| Node Name (Keyword) | Parent Node | Description | Type |
| :-------- | :---------------------------- | :--------------------------------------- | :-------- |
| Bucket | InitiateMultipartUploadResult | Destination bucket for the multipart upload, which is formed by connecting the user-defined string and system-generated APPID with a dash, such as examplebucket-1250000000 | Container |
| Key | InitiateMultipartUploadResult | Object name | Container |
| UploadId | InitiateMultipartUploadResult | ID used in subsequent uploads | Container |

## Examples

### Request
```shell
POST /exampleobject?uploads HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2016 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfGFO&q-sign-time=1484727259;32557623259&q-key-time=1484727259;32557623259&q-header-list=host&q-url-param-list=uploads&q-signature=b5f46c47379aeaee74be7578380b193c01b28045
```

### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Fri, 10 Mar 2016 09:45:46 GMT
Server: tencent-cos
x-cos-request-id: NTg3ZjIzZTZfOWIxZjRlXzZmMzhfMWRj

<InitiateMultipartUploadResult>
    <Bucket>examplebucket-1250000000</Bucket>
    <Key>exampleobject</Key>
    <UploadId>1484727270323ddb949d528c629235314a9ead80f0ba5d993a3d76b460e6a9cceb9633b08e</UploadId>
</InitiateMultipartUploadResult>
```
