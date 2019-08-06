## Description
A POST Object API request allows the users to upload a file (object) to the specified bucket through a form. This operation requires that you have WRITE permission to the bucket. All API parameters carried by the HTTP header are requested through form fields.

### Version

If versioning is enabled for the bucket, the POST operation will automatically generate a unique version ID for the object to be uploaded. COS returns this ID in the response using the x-cos-version-id response header.
If you suspend versioning for the bucket, COS will always use "null" as the version ID of the object stored in the bucket.

### Detail Analysis
1. You need to have write permission of the bucket.
2. If a file with the same name as the file to be uploaded already exists in the bucket, it will be overwritten and 200 OK will be returned upon success.

## Request
### Request Example

```shell
POST / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: length
Headers
Form
```

### Request Headers

#### Common Headers

We implement this request with a common request header. For more information about common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Request Headers
The following required headers are needed for this request operation:

| Name | Description | Type | Required |
|:---|:-- |:---|:-- |
| Content-Length | HTTP request length in byte defined in RFC 2616 | String | Yes |

### Form Fields

<table>
   <tr>
      <th>Name</td>
      <th>Description</td>
      <th>Type</td>
      <th>Required</td>
   </tr>
   <tr>
      <td>acl</td>
      <td>It defines the ACL attribute of the object. Value range: private, public-read, and default; default value: default (i.e., inheriting the bucket's permissions); <br>Note: Currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, use "default" for this parameter or simply leave it blank, so that the object will inherit the permissions of the bucket</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>Cache-Control, Content-Type, Content-Disposition, Content-Encoding, Expires</td>
      <td>Header defined in RFC 2616. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/7749">PUT Object</a></td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>file</td>
      <td>File content as the last field in the form</td>
      <td>String</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>key</td>
      <td>The filename after the file is uploaded, which will be changed if ${filename} is used; for example, with a/b/${filename}, if the uploaded file is photo.jpg, then the final path after upload will be a/b/photo.jpg</td>
      <td>String</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>success_action_redirect</td>
      <td>If this is set, it will take precedence to return 303, provide the Location header, and add the bucket={bucket}&key={key}&etag={%22etag%22} at the end of the URL</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>success_action_status</td>
      <td>Value range: 200, 201, and 204. 204 is returned by default. If success_action_redirect is set, this parameter will be ignored</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>x-cos-meta-*</td>
      <td>This includes the suffix and information of the user-defined header, which will be returned as the object metadata of up to 2 KB. Note: User-defined header information can contain underscores, but user-defined header suffixes cannot</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>x-cos-storage-class</td>
      <td>This sets the storage class of the object. Enumerated values: STANDARD, STANDARD_IA, and ARCHIVE. Default value: STANDARD</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>policy</td>
      <td>This should be Base64-encoded and is used for request verification. If the content of the request does not match the conditions specified by the policy, 403 Access Denied will be returned</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>x-cos-server-side-encryption</td>
      <td>This specifies how the server-side encryption is enabled for the object. For encryption with the COS master key, enter AES256</td>
      <td>String</td>
      <td nowrap="nowrap">Yes if encryption is needed</td>
   </tr>
</table>

#### Signature Protection

If signature protection is needed for an HTTP POST request as a form, the form should contain the content of the following form-data:

| Form Field | Description |
| ---------------- | ----------------------------------------- |
| policy | Base64-encrypted policy content, which is used to verify the content of the request. If the request content does not match the conditions specified by the policy, the request will be rejected. |
| q-sign-algorithm | Algorithm for calculating the signature. COS currently supports SHA1. Enter `sha1` (in lowercase) here. |
| q-ak | Your account ID in Tencent Cloud, i.e., SecretId |
| q-key-time | The validity start and end time of the key used to request the signature, described by Unix timestamp in seconds with the format [start-seconds];[end-seconds], such as `1480932292;1481012298` |
| q-signature | Request signature for using the elements above in calculation. COS will verify the form elements against the signature content and reject the request if the signature does not match the signed content |

#### Signature Calculation

The signature "q-signature" can be calculated in three steps:

1. Use the key content to encrypt the time value of q-key-time and calculate the value of SignKey.
2. Create a POST request policy and encrypt its content with sha1 to get the StringToSign.
3. Encrypt the StringToSign with the SignKey to generate the signature.

#### Policy
Below is an example of a complete policy:

```shell
{ "expiration": "2007-12-01T12:00:00.000Z",
  "conditions": [
    {"acl": "public-read" },
    {"bucket": "examplebucket-1250000000" },
    ["starts-with", "$key", "user/eric/"],
    {"q-sign-algorithm": "sha1" },
    {"q-ak": "AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q" },
    {"q-sign-time": "1480932292;1481012298" }
  ]
}
```

**Expiration**
This sets the expiration time for the POST policy in ISO8601 GMT time, such as 2017-12-01T12:00:00.000Z

**Conditions Rules**

| Type | Description |
| ---- | ---------------------------------------- |
| Full match | Expressed with `{"key": "value"}` or `["eq", "$key", "value"]` |
| Prefix match | Expressed with `["starts-with", "$key", "value"]`, where the value can be left blank |
| Range match | Only for `["content-length-range", int1, int2]`. The number of file bytes must be between int1 and int2 |

**Conditions Parameters**
All parameters are optional. If they are not entered, the verification can be skipped.

| Name | Description | Matching Method |
| --------------- | ---------------------- | ----- |
| acl | Permitted scope for the file's ACL attribute. This is optional | Full, prefix |
| bucket | This specifies the bucket to upload to | Full |
| content-length-range | This specifies the upload size range of the file | Range |
| key | Object storage path | Full, prefix |
| success_action_redirect | URL returned after a successful upload | Full, prefix |
| success_action_status | Status returned after a successful upload | Full |
| x-cos-meta-\* | This includes the suffix and information of the user-defined header, which will be returned as the object metadata of up to 2 KB. <br>**Note:** User-defined header information can contain underscores, but user-defined header suffixes cannot | Full, prefix |
| x-cos-\* | Other COS headers that need to be signed | Full |


## Response
### Response Headers
#### Common Response Headers
This response uses a common response header. For more information about common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers
The request may return the following response headers:

| Name | Description | Type |
|:---|:-- |:-- |
| x-cos-version-id | A version of the copied object in the destination bucket. This header will be returned only if versioning is enabled or enabled and then suspended for the bucket | String |
| x-cos-server-side-encryption | If the object is stored with COS-managed server-side encryption, the response will contain the values of this header and the encryption algorithm used (AES256) | string |


### Response Parameters
| Name | Description | Type |
|:---|:-- |:-- |
| ETag | This returns the MD5 checksum of the file. The value of ETag can be used to check whether the object gets corrupted during upload | String |
| Location | If success_action_redirect for upload is specified, the corresponding value will be returned; otherwise, the full path of the object will be returned | String |


### Response Body
application/xml data is returned in the response body, which contains the complete node data as shown below:

```shell
<PostResponse>
        <Location>http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/photo.jpg</Location>
        <Bucket>examplebucket-1250000000</Bucket>
        <Key>photo.jpg</Key>
        <ETag>d41d8cd98f00b204e9800998ecf8427e</ETag>
</PostResponse>
```

The detailed data are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :-------------------------- | :-------- |
| PostResponse | None | Container for storing the POST Object result | Container |


Content of the Container node PostResponse:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------- | :--------------- | :----- |
| Location | PostResponse | Full path of the object | String |
| Bucket | PostResponse | The bucket where the object is stored | String |
| Key | PostResponse | Key name of the object | String |
| ETag | PostResponse | Etag content | String |


### Error Codes
Errors that are frequently seen with the request are listed below. For more common error codes in COS, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

| Error Code | HTTP Status Code | Description |
| ------------------- | --------------------------------------- | ------------------ |
| InvalidDigest | 400 Bad Request | If the Content-MD5 header is carried in the request when the file is uploaded, COS will check whether the MD5 of the body is the same as that carried, and if not, InvalidDigest will be returned |
| KeyTooLong | 400 Bad Request | If a custom header beginning with x-cos-meta is carried in the request when the file is uploaded, the combined size of the key and value of the custom header cannot exceed 4 KB; otherwise, the KeyTooLong error will be returned |
| MissingContentLength | 411 Length Required | If the Content-Length header is not carried in the request when the file is uploaded, this error code will be returned |
| NoSuchBucket | 404 Not Found | If the bucket to which you want to upload the object does not exist, the 404 Not Found error will be returned with the error code NoSuchBucket |
| EntityTooLarge | 400 Bad Request | If the file to be uploaded is larger than 5 GB, the EntityTooLarge error will be returned with the error message `“Your proposed upload exceeds the maximum allowed object size”` |
| InvalidURI | 400 Bad Request | The object key length cannot exceed 850; otherwise, the InvalidURI error will be returned |


## Examples
### Request

```
POST / HTTP/1.1
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 1352
Content-Type: multipart/form-data; boundary=e07f2a7876ae4755ae18d300807ad879

--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="key"

photo.jpg
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="success_action_status"

201
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="Acl"

public-read
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="x-cos-storage-class"

STANDARD
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="Signature"

q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1512983814;1512984814&q-key-time=1512983814;1512984814&q-url-param-list=&q-header-list=host&q-signature=2ffd2ae714e7445a8da000ec5d51771ff5056500
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjogW3siYnVja2V0IjogImtpdG1hbnMzdGVzdDEifSwgWyJjb250ZW50LWxlbmd0aC1yYW5nZSIsIDAsIDEwMDAwMDAwXSwgWyJzdGFydHMtd2l0aCIsICJ4LWNvcy1tZXRhLWJiIiwgIjEyIl1dLCAiZXhwaXJhdGlvbiI6ICIyMDQ3LTEyLTAxVDEyOjAwOjAwLjAwMFoifQ==
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="x-Cos-meta-bb"

124
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="key1"

1
--e07f2a7876ae4755ae18d300807ad879
Content-Disposition: form-data; name="file"; filename="empty:a"


--e07f2a7876ae4755ae18d300807ad879--
```

### Response

```shell
HTTP/1.1 204
Content-Type: application/xml
Content-Length: 232
Connection: keep-alive
Date: Mon, 11 Dec 2017 09:16:56 GMT
ETag: "d41d8cd98f00b204e9800998ecf8427e"
Location: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/photo.jpg
Server: tencent-cos
x-cos-request-id: NWEyZTRkMDZfMjQ4OGY3MGFfNTE4Yl81
```
