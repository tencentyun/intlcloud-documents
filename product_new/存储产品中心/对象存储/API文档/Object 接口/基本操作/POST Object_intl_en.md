## Description
This API is used to upload a file (object) to a specified bucket using forms. To make this request, you need to have the permission to write to the bucket. All the API parameters carried by HTTP headers are requested using form fields.

#### Version

If versioning is enabled for the bucket, the `POST` operation will automatically generate a unique version ID for the object to be uploaded. COS will return this ID in the response using the `x-cos-version-id` response header.
If you suspend versioning for the bucket, COS will always use `null` as the version ID of the objects in the bucket.

### Notes
1. You need to have the permission to write to the bucket.
2. If there is an object in the bucket with the same name as the object to be uploaded, the old object will be overwritten by the new one and the request will return success upon a successful upload.

## Request
#### Sample Request

```shell
POST / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: length
Headers
Form
```

#### Request Headers

##### Common Headers

The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

##### Special Headers
The following request headers are required for the implementation of this operation:

| Name | Description | Type | Required |
|:---|:-- |:---|:-- |
| Content-Length | HTTP request length in bytes as defined in RFC 2616 | String | Yes |

#### Form Fields

<table>
   <tr>
      <th>Name</td>
      <th>Description</td>
      <th>Type</td>
      <th>Required</td>
   </tr>
   <tr>
      <td>acl</td>
      <td>Defines the ACL attribute of the object. Valid values: `private`, `public-read`, and `default`. Default value: `default` (i.e., inheriting the bucket's permission). Note: currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, set `default` for this parameter or simply leave it blank, and the object will inherit the permissions of the bucket</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>Cache-Control, Content-Type, Content-Disposition, Content-Encoding, Expires&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</td>
      <td>Headers as defined in RFC 2616. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/7749">PUT Object</a></td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>file</td>
      <td>File content, as the last field in the form</td>
      <td>String</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>key</td>
      <td>Filename after the file is uploaded, which will be changed if you use <code>${filename}</code>; for example, if you use <code>a/b/${filename}</code> and upload a file named `photo.jpg`, then the final path to the file will be <code>a/b/photo.jpg</code></td>
      <td>String</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>success_action_redirect</td>
      <td>If this field is specified, it will take the priority; `303` and the `Location` header will be returned, and <code>bucket={bucket}&key={key}&etag={%22etag%22}</code> parameter will be added to the end of the URL</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>success_action_status</td>
      <td>Valid values: `200`, `201`, and `204`. `204` is returned by default. If `success_action_redirect` is set, this field will be ignored</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>x-cos-meta-*</td>
      <td>Suffix and information of the user-defined header, which will be returned as the object metadata; maximum size: 2 KB. <br>Note: user-defined header information can contain underscores, whereas user-defined header suffixes cannot</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>x-cos-storage-class</td>
      <td>Specifies the storage class of the object. Enumerated values: `STANDARD`, `STANDARD_IA`, and `ARCHIVE`. Default value: `STANDARD`</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>policy</td>
      <td>Base64-encoded and used for request verification. If the request content does not match the conditions specified by the field, `403 Access Denied` will be returned</td>
      <td>String</td>
      <td>No</td>
   </tr>
   <tr>
      <td>x-cos-server-side-encryption</td>
      <td>Specifies how the server-side encryption is enabled for the object. For encryption with a COS master key, enter AES256</td>
      <td>String</td>
      <td nowrap="nowrap">Yes if encryption is needed</td>
   </tr>
</table>

#### Signature Protection

If signature protection is needed for a `POST` request to upload an object using forms, the forms must contain the content of the following form-data:

| Form Field | Description |
| ---------------- | ----------------------------------------- |
| policy | Base64-encoded policy content, which is used to verify the request content. If the request content does not match the conditions specified by the policy, the request will be denied. |
| q-sign-algorithm | Algorithm for signature calculation. COS currently supports SHA1. Enter `sha1` (in lowercase) for this field. |
| q-ak | Your SecretId in Tencent Cloud |
| q-key-time | Start and end of the validity period of the key used to request the signature, which are described in Unix timestamps; unit: second <br>Format: `[start-seconds];[end-seconds]`, such as `1480932292;1481012298` |
| q-signature | Request signature calculated using the fields above. COS will verify the signature against the form fields. If they do not match, the request will be denied |

#### Signature Calculation

The signature `q-signature` is calculated in three steps:

1. Use the key content to encrypt `q-key-time` to get `SignKey`.
2. Create a `POST` request policy and encrypt its content with sha1 to get `StringToSign`.
3. Encrypt `StringToSign` with `SignKey` to generate the signature.

#### Policy
Below is a sample of a complete policy:

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
Sets the expiration time of the `POST` policy in ISO8601 GMT time, such as `2017-12-01T12:00:00.000Z`

**Conditions Rules**

| Type | Description |
| ---- | ---------------------------------------- |
| Full match | Format: `{"key": "value"}` or `["eq", "$key", "value"]` |
| Prefix match | Format: `["starts-with", "$key", "value"]`, where `value` can be left empty |
| Range match | Format: `["content-length-range", int1, int2]`, which means that the number of file bytes must be between `int1` and `int2` |

**Conditions Parameters**
All parameters are optional. If they are left empty, the verification can be skipped.

| Name | Description | Matching Method |
| --------------- | ---------------------- | ----- |
| acl | Allowed range of the file's ACL attribute; optional | Full, prefix |
| bucket | Specifies the destination bucket | Full |
| content-length-range | Specifies the size range of the file to be uploaded | Range |
| key | Object storage path | Full, prefix |
| success_action_redirect | URL returned after a successful upload | Full, prefix |
| success_action_status | Status returned after a successful upload | Full |
| x-cos-meta-\* | Suffix and information of the user-defined header, which will be returned as the object metadata; maximum size: 2 KB. <br>Note: user-defined header information can contain underscores, whereas user-defined header suffixes cannot | Full, prefix |
| x-cos-\* | Other COS headers that need to be signed | Full |


## Response
#### Response Headers
#### Common Response Headers
This response uses common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers
This request may return the following response headers:

| Name | Description | Type |
|:---|:-- |:-- |
| x-cos-version-id | Version of the copied object in the destination bucket. This header will be returned only if versioning is enabled or enabled and then suspended for the bucket | String |
| x-cos-server-side-encryption | If the object is stored with COS-managed server-side encryption, the response will contain this header and the value of the encryption algorithm used (AES256) | string |


#### Response Parameters
| Name | Description | Type |
|:---|:-- |:-- |
| ETag | Returns the MD5 checksum of the file. The value of `ETag` can be used to check whether the object gets corrupted during the upload | String |
| Location | If `success_action_redirect` is specified, the corresponding value will be returned; otherwise, the full path to the object will be returned | String |


#### Response Body
This response body returns `application/xml` data. The following contains all the node data:

```shell
<PostResponse>
        <Location>http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/photo.jpg</Location>
        <Bucket>examplebucket-1250000000</Bucket>
        <Key>photo.jpg</Key>
        <ETag>d41d8cd98f00b204e9800998ecf8427e</ETag>
</PostResponse>
```

Below are the details:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :-------------------------- | :-------- |
| PostResponse | None | Container storing the response of the `POST Object` request | Container |


Content of the Container node `PostResponse`:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------- | :--------------- | :----- |
| Location | PostResponse | Full path to the object | String |
| Bucket | PostResponse | Bucket where the object is stored | String |
| Key | PostResponse | Object key name | String |
| ETag | PostResponse | Etag content | String |


#### Error Codes
The following describes some frequent special errors that may occur when you make this request. For more COS error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

| Error Code | HTTP Status Code | Description |
| ------------------- | --------------------------------------- | ------------------ |
| InvalidDigest | 400 Bad Request | If the request carries the `Content-MD5` header when the file is uploaded, COS will check whether the MD5 of the body is the same as the one carried, and if not, `InvalidDigest` will be returned |
| KeyTooLong | 400 Bad Request | If a user-defined header beginning with `x-cos-meta` is carried in the request when the file is uploaded, the total size of the key and value of the header cannot exceed 4 KB; otherwise, the `KeyTooLong` error will be returned |
| MissingContentLength | 411 Length Required | If the `Content-Length` header is not carried in the request when the file is uploaded, this error code will be returned |
| NoSuchBucket | 404 Not Found | If the bucket to which you want to upload the object does not exist, the `NoSuchBucket` (404 Not Found) error will be returned |
| EntityTooLarge | 400 Bad Request | If the file to be uploaded is larger than 5 GB, the `EntityTooLarge` error will be returned with the error message `Your proposed upload exceeds the maximum allowed object size` |
| InvalidURI | 400 Bad Request | The object key cannot exceed 850 bytes in length; otherwise, the `InvalidURI` error will be returned |


## Example
#### Request

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

#### Response

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
