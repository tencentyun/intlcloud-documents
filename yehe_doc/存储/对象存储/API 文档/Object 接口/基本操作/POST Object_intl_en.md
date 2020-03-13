## Feature

This API is used to upload a local object smaller than 5GB to a specified bucket via HTML form. To make this request, you need to have the permission to write to the bucket.

>
>- This API has special requirements for signatures instead of using standard COS request signatures. For more information, see [Signature Protection](#id1) and description of related fields.
>- If versioning is not enabled and you try to upload an object whose name already exists, the newly uploaded object will overwrite the prior one and a response will be returned in the specified way upon success.

#### Versioning

- If versioning is enabled for the bucket, COS will automatically generate a unique version ID for the object to be uploaded and return this ID in the response using the `x-cos-version-id` response header.
- If versioning is suspended for the bucket, COS will always use `null` as the version ID of the object in the bucket and will not return the `x-cos-version-id` response header.

## Request

#### Sample Request

```shell
POST / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: multipart/form-data; boundary=Multipart Boundary
Content-Length: Content Length

[Multipart Form Data]
```


#### Request Form

The request body of this API is encoded with multipart/form-data. When sending requests in HTML with the &lt;form&gt; element, you need to configure the enctype attribute of the &lt;form&gt; element as multipart/form-data, and then use HTML form elements, e.g., &lt;input&gt;, &lt;select&gt;, to add required form fields.

**Form Fields**

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| Cache-Control | Cache directives as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Content-Disposition | File name as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | String | No |
| Content-Type | HTTP content type (MIME) as defined in RFC 2616, which will be stored in the object metadata<br>**Note:** when files are uploaded via forms, the browser will automatically carry the MIME type of the specified file in the request. However, COS will not use the MIME type carried by the browser, so you need to explicitly specify the `Content-Type` field as the object content type | string | No |
| Expires | Cache expiration time as defined in RFC 2616, which will be stored in the object metadata | String | No |
| file | File content. When uploading the file via a form, the browser will automatically configure the field in proper format | file | Yes |
| key | Object key. If you specify the `${filename}` wildcard in the object key, the wildcard in the object key will be replaced with the actual file name. For more information, see [Example 7](#step7) | string | Yes |
| success_action_redirect | Destination address for URL redirect upon a successful upload. If this field is not set, HTTP status code 303（Redirect）and the `Location` response header will be returned. The `Location` response header will include the URL address specified by this field together with the bucket, key, and etag parameters. For more information, see [Example 8](#step8) | string | No |
| success_action_status | HTTP status code returned upon a successful upload. Valid values: 200, 201, 204; default value: 204. If `success_action_redirect` is specified, this field will be ignored. For more information, see [Example 9](#step9) | number | No |
| x-cos-meta-\* | Header suffix and information of user-defined metadata, which will be stored in the object metadata. Maximum size: 2 KB. <br>**Note:** User-defined metadata information can contain underscores (_), whereas header suffixes of user-defined metadata can only contain minus signs (-), not underscores | String | No |
| x-cos-storage-class | Object storage class, such as `STANDARD_IA` and `ARCHIVE`. Default value: `STANDARD`. For enumerated values, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | Enum | No |
| Content-MD5 | MD5 hash value of the Base64-encoded file content used for integrity check, i.e., checking whether the file content has changed during the upload | string | No |

**ACL-related Form Fields**

You can configure access permissions for the object by specifying the following form fields during upload:

| Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| --- | --- | --- | --- |
| x-cos-acl | Defines the access control list (ACL) attribute of the object. For enumerated values such as `default`, `private`, and `public-read`, see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default` <br>**Note:** currently, there can be up to 1,000 entries in one ACL. If you do not need access control for the object, set the field as `default` or simply leave it blank, and the object will inherit the permissions of the bucket | Enum | No |
| x-cos-grant-read | Allows grantee to read the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-read-acp | Allows grantee to read the ACL of the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-write-acp | Allows grantee to write to the ACL of the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |
| x-cos-grant-full-control | Grants a user full permission to operate on the object; format: `id="[OwnerUin]"`, such as `id="100000000001"`. You can use comma (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | String | No |

**Form fields related to server-side encryption**

You can use server-side encryption by specifying the following form fields when uploading the object:

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| x-cos-server-side-encryption | Server-side encryption algorithm supporting AES256, cos/kms | string | This field is required when using SSE-COS or SSE-KMS | | String | This field is required when using SSE-COS or SSE-KMS |
| x-cos-server-side-encryption-customer-algorithm | Server-side encryption algorithm; currently only AES256 is supported | String | Yes |
| x-cos-server-side-encryption-cos-kms-key-id | When x-cos-server-side-encryption value is cos/kms, it is used to specify the user master key of KMS. If not specified, CMK created by COS is used by default. For more details, please refer to [SSE-KMS Encryption](https://intl.cloud.tencent.com/document/product/436/18145) | String | No |
| x-cos-server-side-encryption-context | When the value of x-cos-server-side-encryption is cos/kms, it is used to specify the encryption context, and the value is Base64-encoded string holding JSON with the key-value pairs for the encryption context.<br>For example `eyJhIjoiYXNkZmEiLCJiIjoiMTIzMzIxIn0 =` | String | No |
| x-cos-server-side-encryption-customer-key | Base64-encoded server-side encryption key.<br> For example, `MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=` | String | Yes |
. x-cos-server-side-encryption-customer-key-MD5 | Base64-encoded MD5 hash value of the server-side encryption key.<br> For example, `U5L61r7jcwdNvT7frmUG8g==` | String| Yes |

<span id="id1"></span>
#### Signature Protection

POST Object API requires signature-related fields to be carried in the request. After receiving the message, the COS server performs authentication. If the verification is successful, the request is accepted and executed. Otherwise, an error message is returned and the request is discarded.

The signature is generated as follows:

## 2. Preparations

(2) Log into the CAM Console and get your project's SecretId and SecretKey on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.

### Generating KeyTime

1. Get the Unix timestamp "StartTimestamp" corresponding to the current time, which is the total seconds from January 1, 1970, 00:00:00 UTC (January 1, 1970, 08:00:00 Beijing time) to now.
2. Calculate the Unix timestamp "EndTimestamp" corresponding to the signature expiry time based on the timestamp above and the expected validity period of the signature.
3. Splice the signature validity period in the format of `StartTimestamp;EndTimestamp`, which is the KeyTime.

#### 3. Creating "Policy"

The policy is a JSON text. A typical policy is as follows:

```shell
{
    "expiration": "2019-08-30T09:38:12.414Z",
    "conditions": [
        { "acl": "default" },
        { "bucket": "examplebucket-1250000000" },
        [ "starts-with", "$key", "folder/subfolder/" ],
        [ "starts-with", "$Content-Type", "image/" ],
        [ "starts-with", "$success_action_redirect", "https://my.website/" ],
        [ "eq", "$x-cos-server-side-encryption", "AES256" ],
        { "q-sign-algorithm": "sha1" },
        { "q-ak": "AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q" },
        { "q-sign-time": "1567150692;1567157892" }
    ]
}
```

Notes:
- expiration: Expiration time of the policy, string in ISO8601 format
- conditions: An array of specific conditions for the policy. The specific rules for the conditions are listed below.

| Type | Description |
| --- | --- |
| Exact Match | Use `{" key ":" value "}` or `[" eq "," $ key "," value "]` to express, where key is a specified form field and value is a specified value |
| Prefix Match | Use `[ "starts-with", "$key", "value" ]` to express, where key is a specified form field and value is a specified prefix that can be empty |
| Range Match | Only applies to `[" content-length-range ", minNum, maxNum]`, used to limit the file length to be within minNum and maxNum |

The supported form fields are as follows:

| Field Name | Description | Match Method&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nbsp;nbsp; | Required |
| --- | --- | --- | --- |
| acl | Access control list (ACL) attributes of the object | Exact, prefix | No |
| bucket | Uploaded Bucket | Exact | No |
| key | Object key. If the object key uses the `$ {filename}` wildcard when uploading, the object key will be processed as the final object key before policy verification. At this time, prefix match should be used in the policy instead of `$ {filename} ` wildcard | Exact, Prefix | No |
| content-length-range | File Length | Range | No |
| Cache-Control, Content-Type, Content-Disposition, Content-Encoding, Expires | The relevant headers defined in RFC 2616 will be returned as response headers when downloading the object | Exact, Prefix | No |
| success_action_redirect | URL returned after a successful upload | Exact, prefix | No |
| success_action_status | Status returned after a successful upload | Exact | No |
| x-cos-meta-* | User-defined metadata header fields | Exact, prefix | No |
| x-cos-* | Other COS-related form fields mentioned in this document, such as ACL- and SSE-related fields | Exact | No |
| q-sign-algorithm | Signature hash algorithm, fixed as sha1 | Exact | Yes |
| q-ak | SecretId mentioned above | Exact | Yes |
| q-sign-time | KeyTime generated above | Exact | Yes |

> 
>- Fields other than buckets defined in “Policy” must appear in form fields. For example, if you specify `{" acl ":" default "}`, acl must appear in the form with the default value.
>- For security reasons, we strongly recommend you specify all form fields that can be specified.

#### Generating SignKey

Use HMAC-SHA1 with SecretKey as the key and KeyTime as the message, compute the message digest (hash value), which is the SignKey.

### Generating StringToSign

Use SHA1 to compute the message digest (hash value) of the Policy text constructed above, which is StringToSign.

#### Generating Signature

Use HMAC-SHA1 with SignKey as the key and StringToSign as the message, and compute the message digest, which is the Signature.

#### 7. Attaching a signature to the form

Attach the above policy and signature-related information to the form as described in the following table:

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| policy | 经过 Base64 编码的“策略”（Policy）内容 | string | 是 |
| q-sign-algorithm | Signature hash algorithm, fixed as sha1 | string | Yes |
q-ak | SecretId mentioned above | string | Yes |
| q-key-time | KeyTime generated above | string | yes |
| q-signature | Signature generated above | string | Yes |

** Signature protection use cases**

### Preparations

Log into the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in CAM Console to obatin your APPID, SecretId, and SecretKey. Below is an example:

| APPID | SecretId | SecretKey |
| ---------- | ------------------------------------ | -------------------------------- |
| 1250000000 | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q | BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz |

**Construction Policy**

```shell
{
    "expiration": "2019-08-30T09:38:12.414Z",
    "conditions": [
        { "acl": "default" },
        { "bucket": "examplebucket-1250000000" },
        [ "starts-with", "$key", "folder/subfolder/" ],
        [ "starts-with", "$Content-Type", "image/" ],
        [ "starts-with", "$success_action_redirect", "https://my.website/" ],
        [ "eq", "$x-cos-server-side-encryption", "AES256" ],
        { "q-sign-algorithm": "sha1" },
        { "q-ak": "AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q" },
        { "q-sign-time": "1567150692;1567157892" }
    ]
}
```

**Intermediate Variables**

- KeyTime = `1567150692;1567157892`
- SignKey = `39acc8c9f34ba5b19bce4e965b370cd3f62d2fba`
- StringToSign = `d5d903b8360468bc81c1311f134989bc8c8b5b89`
- Signature = `7758dc9a832e9d301dca704cacbf9d9f8172fdef`

** Signature form fields **

- policy = `ewogICAgImV4cGlyYXRpb24iOiAiMjAxOS0wOC0zMFQwOTozODoxMi40MTRaIiwKICAgICJjb25kaXRpb25zIjogWwogICAgICAgIHsgImFjbCI6ICJkZWZhdWx0IiB9LAogICAgICAgIHsgImJ1Y2tldCI6ICJleGFtcGxlYnVja2V0LTEyNTAwMDAwMDAiIH0sCiAgICAgICAgWyAic3RhcnRzLXdpdGgiLCAiJGtleSIsICJmb2xkZXIvc3ViZm9sZGVyLyIgXSwKICAgICAgICBbICJzdGFydHMtd2l0aCIsICIkQ29udGVudC1UeXBlIiwgImltYWdlLyIgXSwKICAgICAgICBbICJzdGFydHMtd2l0aCIsICIkc3VjY2Vzc19hY3Rpb25fcmVkaXJlY3QiLCAiaHR0cHM6Ly9teS53ZWJzaXRlLyIgXSwKICAgICAgICBbICJlcSIsICIkeC1jb3Mtc2VydmVyLXNpZGUtZW5jcnlwdGlvbiIsICJBRVMyNTYiIF0sCiAgICAgICAgeyAicS1zaWduLWFsZ29yaXRobSI6ICJzaGExIiB9LAogICAgICAgIHsgInEtYWsiOiAiQUtJRFFqejNsdG9tcFZqQm5pNUxpdGtXSEZsRnB3a245VTVxIiB9LAogICAgICAgIHsgInEtc2lnbi10aW1lIjogIjE1NjcxNTA2OTI7MTU2NzE1Nzg5MiIgfQogICAgXQp9`
- q-sign-algorithm = `sha1`
- q-ak = `AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q`
- q-key-time = `1567150692;1567157892`
- q-signature = `7758dc9a832e9d301dca704cacbf9d9f8172fdef`


## Response

#### Response Headers

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Name | Description | Type |
| --- | --- | --- |
Location | <li> When using the success_action_redirect form field, the value of this response header is the URL specified by success_action_redirect, with bucket, key, and etag parameters appended. For related examples, see [Case 8](# step8) in this document <br> <li>If the success_action_redirect form field is not used, the value of this response header is the complete URL address for object access. For related examples, see [Case 1](# step1) | string |

**Versioning-related Headers**

When the object is uploaded to a bucket where versioning is enabled, the following response headers will be returned:

| Name | Description | Type |
| --- | --- | --- |
| x-cos-version-id | Object version ID | string |

**Headers related to server-side encryption (SSE)**

If server-side encryption is used during object upload, this API will return headers used specifically for server-side encryption. For more information, see [Server-side encryption headers](https://cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response Body

The response body of this API is empty.

#### Error Codes

There are no special error messages for this API. For all error messages, see [Error Codes](https://cloud.tencent.com/document/product/436/7730).

## Examples

<span id="step1"></span>
#### Example 1. Simple example (versioning not enabled)

#### Request

```shell
POST / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 29 Aug 2019 07:39:34 GMT
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryZBPbaoYE2gqeB21N
Content-Length: 1119
Connection: close

------WebKitFormBoundaryZBPbaoYE2gqeB21N
Content-Disposition: form-data; name="key"

exampleobject
------WebKitFormBoundaryZBPbaoYE2gqeB21N
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
------WebKitFormBoundaryZBPbaoYE2gqeB21N
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjpbeyJxLXNpZ24tYWxnb3JpdGhtIjoic2hhMSJ9LHsicS1hayI6IkFLSUQ4QTBmQlZ0WUZyTm0wMm9ZMWcxSlFRRjBjM0pPNk5FdSJ9LHsicS1zaWduLXRpbWUiOiIxNTY3MDY0Mzc0OzE1NjcwNzE1NzQifV0sImV4cGlyYXRpb24iOiIyMDE5LTA4LTI5VDA5OjM5OjM0LjQ3MVoifQ==
------WebKitFormBoundaryZBPbaoYE2gqeB21N
Content-Disposition: form-data; name="q-sign-algorithm"

sha1
------WebKitFormBoundaryZBPbaoYE2gqeB21N
Content-Disposition: form-data; name="q-ak"

AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****
------WebKitFormBoundaryZBPbaoYE2gqeB21N
Content-Disposition: form-data; name="q-key-time"

1567064374;1567071574
------WebKitFormBoundaryZBPbaoYE2gqeB21N
Content-Disposition: form-data; name="q-signature"

74ba120129a13d8f0e19479fbdc01bca3bca****
------WebKitFormBoundaryZBPbaoYE2gqeB21N--
```

#### Response

```shell
HTTP/1.1 204 
Content-Length: 0
Connection: close
Date: Thu, 29 Aug 2019 07:39:34 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Location: http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Server: tencent-cos
x-cos-request-id: NWQ2NzgxMzZfMmViMDJhMDlfY2NjOF84NGQz****
```

<span id="step2"></span>
#### Example 2. Specifying metadata and ACL using request headers

#### Request

```shell
POST / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 29 Aug 2019 07:39:34 GMT
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Length: 2146
Connection: close

------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="key"

exampleobject
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="acl"

public-read
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="Cache-Control"

max-age=86400
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="Content-Disposition"

attachment; filename=example.jpg
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="Content-Type"

image/jpeg
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="x-cos-meta-example-field"

example-value
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="Content-MD5"

7o3pGNBWQBRbGPcPTDqmAg==
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjpbeyJhY2wiOiJwdWJsaWMtcmVhZCJ9LHsiYnVja2V0IjoiZXhhbXBsZWJ1Y2tldC0xMjUyMjQ2NTU1In0seyJrZXkiOiJleGFtcGxlb2JqZWN0In0sWyJlcSIsIiRDb250ZW50LURpc3Bvc2l0aW9uIiwiYXR0YWNobWVudDsgZmlsZW5hbWU9ZXhhbXBsZS5qcGciXSxbInN0YXJ0cy13aXRoIiwiJENvbnRlbnQtVHlwZSIsImltYWdlLyJdLFsiZXEiLCIkeC1jb3MtbWV0YS1leGFtcGxlLWZpZWxkIiwiZXhhbXBsZS12YWx1ZSJdLHsicS1zaWduLWFsZ29yaXRobSI6InNoYTEifSx7InEtYWsiOiJBS0lEOEEwZkJWdFlGck5tMDJvWTFnMUpRUUYwYzNKTzZORXUifSx7InEtc2lnbi10aW1lIjoiMTU2NzA2NDM3NDsxNTY3MDcxNTc0In1dLCJleHBpcmF0aW9uIjoiMjAxOS0wOC0yOVQwOTozOTozNC45MzdaIn0=
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="q-sign-algorithm"

sha1
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="q-ak"

AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="q-key-time"

1567064374;1567071574
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="q-signature"

228a89b5f7b8fce7fdfa4a3b36cfb5a5eafb****
------WebKitFormBoundary9JtEhEGHSdx8Patg--
```

#### Response

```shell
HTTP/1.1 204 
Content-Length: 0
Connection: close
Date: Thu, 29 Aug 2019 07:39:35 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Location: http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Server: tencent-cos
x-cos-request-id: NWQ2NzgxMzdfM2NhZjJhMDlfMTQzYV84Nzhh****
```

<span id="step3"></span>
#### Example 3. Using server-side encryption SSE-COS

#### Request

```shell
POST / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 29 Aug 2019 07:39:35 GMT
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryBVaHvBJQJnQrAxKY
Content-Length: 1296
Connection: close

------WebKitFormBoundaryBVaHvBJQJnQrAxKY
Content-Disposition: form-data; name="key"

exampleobject
------WebKitFormBoundaryBVaHvBJQJnQrAxKY
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
------WebKitFormBoundaryBVaHvBJQJnQrAxKY
Content-Disposition: form-data; name="x-cos-server-side-encryption"

AES256
------WebKitFormBoundaryBVaHvBJQJnQrAxKY
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjpbeyJ4LWNvcy1zZXJ2ZXItc2lkZS1lbmNyeXB0aW9uIjoiQUVTMjU2In0seyJxLXNpZ24tYWxnb3JpdGhtIjoic2hhMSJ9LHsicS1hayI6IkFLSUQ4QTBmQlZ0WUZyTm0wMm9ZMWcxSlFRRjBjM0pPNk5FdSJ9LHsicS1zaWduLXRpbWUiOiIxNTY3MDY0Mzc1OzE1NjcwNzE1NzUifV0sImV4cGlyYXRpb24iOiIyMDE5LTA4LTI5VDA5OjM5OjM1LjUyN1oifQ==
------WebKitFormBoundaryBVaHvBJQJnQrAxKY
Content-Disposition: form-data; name="q-sign-algorithm"

sha1
------WebKitFormBoundaryBVaHvBJQJnQrAxKY
Content-Disposition: form-data; name="q-ak"

AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****
------WebKitFormBoundaryBVaHvBJQJnQrAxKY
Content-Disposition: form-data; name="q-key-time"

1567064375;1567071575
------WebKitFormBoundaryBVaHvBJQJnQrAxKY
Content-Disposition: form-data; name="q-signature"

65f3f8864bb1b271e1235d1ec7d1cb508ffa****
------WebKitFormBoundaryBVaHvBJQJnQrAxKY--
```

#### Response

```shell
HTTP/1.1 204 
Content-Length: 0
Connection: close
Date: Thu, 29 Aug 2019 07:39:35 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Location: http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Server: tencent-cos
x-cos-request-id: NWQ2NzgxMzdfMTljMDJhMDlfNTg4ZF84Njgx****
x-cos-server-side-encryption: AES256
```

<span id="step4"></span>
#### Example 4. Using server-side encryption SSE-C

#### Request

```shell
POST / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 29 Aug 2019 07:39:36 GMT
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Length: 1667
Connection: close

------WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Disposition: form-data; name="key"

exampleobject
------WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
------WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Disposition: form-data; name="x-cos-server-side-encryption-customer-algorithm"

AES256
------WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Disposition: form-data; name="x-cos-server-side-encryption-customer-key"

MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=
------WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Disposition: form-data; name="x-cos-server-side-encryption-customer-key-MD5"

U5L61r7jcwdNvT7frmUG8g==
------WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjpbeyJ4LWNvcy1zZXJ2ZXItc2lkZS1lbmNyeXB0aW9uLWN1c3RvbWVyLWFsZ29yaXRobSI6IkFFUzI1NiJ9LHsicS1zaWduLWFsZ29yaXRobSI6InNoYTEifSx7InEtYWsiOiJBS0lEOEEwZkJWdFlGck5tMDJvWTFnMUpRUUYwYzNKTzZORXUifSx7InEtc2lnbi10aW1lIjoiMTU2NzA2NDM3NjsxNTY3MDcxNTc2In1dLCJleHBpcmF0aW9uIjoiMjAxOS0wOC0yOVQwOTozOTozNi4wODdaIn0=
------WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Disposition: form-data; name="q-sign-algorithm"

sha1
------WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Disposition: form-data; name="q-ak"

AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****
------WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Disposition: form-data; name="q-key-time"

1567064376;1567071576
------WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Disposition: form-data; name="q-signature"

0273a4b4ede39d0e5162758e145ea0c3e9ef****
------WebKitFormBoundaryYa6H7Gd4xuhlyfJb--
```

#### Response

```shell
HTTP/1.1 204 
Content-Length: 0
Connection: close
Date: Thu, 29 Aug 2019 07:39:36 GMT
ETag: "582d9105f71525f3c161984bc005efb5"
Location: http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Server: tencent-cos
x-cos-request-id: NWQ2NzgxMzhfMzdiMDJhMDlfNDA4YV84MzQx****
x-cos-server-side-encryption-customer-algorithm: AES256
x-cos-server-side-encryption-customer-key-MD5: U5L61r7jcwdNvT7frmUG8g==
```

<span id="step5"></span>
#### Example 5: Enabling Versioning

#### Request

```shell
POST / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 29 Aug 2019 07:40:07 GMT
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryJspR3QIUhGJLALwf
Content-Length: 1119
Connection: close

------WebKitFormBoundaryJspR3QIUhGJLALwf
Content-Disposition: form-data; name="key"

exampleobject
------WebKitFormBoundaryJspR3QIUhGJLALwf
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
------WebKitFormBoundaryJspR3QIUhGJLALwf
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjpbeyJxLXNpZ24tYWxnb3JpdGhtIjoic2hhMSJ9LHsicS1hayI6IkFLSUQ4QTBmQlZ0WUZyTm0wMm9ZMWcxSlFRRjBjM0pPNk5FdSJ9LHsicS1zaWduLXRpbWUiOiIxNTY3MDY0NDA3OzE1NjcwNzE2MDcifV0sImV4cGlyYXRpb24iOiIyMDE5LTA4LTI5VDA5OjQwOjA3LjQ4OFoifQ==
------WebKitFormBoundaryJspR3QIUhGJLALwf
Content-Disposition: form-data; name="q-sign-algorithm"

sha1
------WebKitFormBoundaryJspR3QIUhGJLALwf
Content-Disposition: form-data; name="q-ak"

AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****
------WebKitFormBoundaryJspR3QIUhGJLALwf
Content-Disposition: form-data; name="q-key-time"

1567064407;1567071607
------WebKitFormBoundaryJspR3QIUhGJLALwf
Content-Disposition: form-data; name="q-signature"

699ad0ce7780eb559b75e88f77e95743d829****
------WebKitFormBoundaryJspR3QIUhGJLALwf--
```

#### Response

```shell
HTTP/1.1 204 
Content-Length: 0
Connection: close
Date: Thu, 29 Aug 2019 07:40:07 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Location: http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Server: tencent-cos
x-cos-request-id: NWQ2NzgxNTdfNzFiNDBiMDlfMmE3ZmJfODQ1****
x-cos-version-id: MTg0NDUxNzcwMDkzMDE3NDQ0MDU
```

<span id="step6"></span>
#### Example 6: Suspending Versioning

#### Request

```shell
POST / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 29 Aug 2019 07:40:38 GMT
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryX8hd2lxTMzIBk5Li
Content-Length: 1119
Connection: close

------WebKitFormBoundaryX8hd2lxTMzIBk5Li
Content-Disposition: form-data; name="key"

exampleobject
------WebKitFormBoundaryX8hd2lxTMzIBk5Li
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
------WebKitFormBoundaryX8hd2lxTMzIBk5Li
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjpbeyJxLXNpZ24tYWxnb3JpdGhtIjoic2hhMSJ9LHsicS1hayI6IkFLSUQ4QTBmQlZ0WUZyTm0wMm9ZMWcxSlFRRjBjM0pPNk5FdSJ9LHsicS1zaWduLXRpbWUiOiIxNTY3MDY0NDM4OzE1NjcwNzE2MzgifV0sImV4cGlyYXRpb24iOiIyMDE5LTA4LTI5VDA5OjQwOjM4LjA5MloifQ==
------WebKitFormBoundaryX8hd2lxTMzIBk5Li
Content-Disposition: form-data; name="q-sign-algorithm"

sha1
------WebKitFormBoundaryX8hd2lxTMzIBk5Li
Content-Disposition: form-data; name="q-ak"

AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****
------WebKitFormBoundaryX8hd2lxTMzIBk5Li
Content-Disposition: form-data; name="q-key-time"

1567064438;1567071638
------WebKitFormBoundaryX8hd2lxTMzIBk5Li
Content-Disposition: form-data; name="q-signature"

bb04222322bfb17f4d1f43833bbbac0a03aa****
------WebKitFormBoundaryX8hd2lxTMzIBk5Li--
```

#### Response

```shell
HTTP/1.1 204 
Content-Length: 0
Connection: close
Date: Thu, 29 Aug 2019 07:40:38 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Location: http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Server: tencent-cos
x-cos-request-id: NWQ2NzgxNzZfMjFjOTBiMDlfMWY3YTFfNjY2****
```

<span id="step7"></span>
#### Example 7: Object key (form field key) uses `$ {filename}` wildcard

#### Request

```shell
POST / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 29 Aug 2019 12:35:07 GMT
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryHrAMWZO4BNyT0rca
Content-Length: 1188
Connection: close

------WebKitFormBoundaryHrAMWZO4BNyT0rca
Content-Disposition: form-data; name="key"

folder/subfolder/${filename}
------WebKitFormBoundaryHrAMWZO4BNyT0rca
Content-Disposition: form-data; name="file"; filename="photo.jpg"
Content-Type: image/jpeg

[Object Content]
------WebKitFormBoundaryHrAMWZO4BNyT0rca
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjpbWyJzdGFydHMtd2l0aCIsIiRrZXkiLCJmb2xkZXIvc3ViZm9sZGVyLyJdLHsicS1zaWduLWFsZ29yaXRobSI6InNoYTEifSx7InEtYWsiOiJBS0lEOEEwZkJWdFlGck5tMDJvWTFnMUpRUUYwYzNKTzZORXUifSx7InEtc2lnbi10aW1lIjoiMTU2NzA4MjEwNzsxNTY3MDg5MzA3In1dLCJleHBpcmF0aW9uIjoiMjAxOS0wOC0yOVQxNDozNTowNy44OTlaIn0=
------WebKitFormBoundaryHrAMWZO4BNyT0rca
Content-Disposition: form-data; name="q-sign-algorithm"

sha1
------WebKitFormBoundaryHrAMWZO4BNyT0rca
Content-Disposition: form-data; name="q-ak"

AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****
------WebKitFormBoundaryHrAMWZO4BNyT0rca
Content-Disposition: form-data; name="q-key-time"

1567082107;1567089307
------WebKitFormBoundaryHrAMWZO4BNyT0rca
Content-Disposition: form-data; name="q-signature"

3cc37f8c81e36f57506efa02d0a3b6c9d551****
------WebKitFormBoundaryHrAMWZO4BNyT0rca--
```

#### Response

```shell
HTTP/1.1 204 
Content-Length: 0
Connection: close
Date: Thu, 29 Aug 2019 12:35:08 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Location: http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/folder/subfolder/photo.jpg
Server: tencent-cos
x-cos-request-id: NWQ2N2M2N2NfNWZhZjJhMDlfNmUzMV84OTg4****
```

<span id="step8"></span>
#### Example 8: Specifying the success_action_redirect form field

#### Request

```shell
POST / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 29 Aug 2019 08:02:29 GMT
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryJ0bRH1MwgMq5eu6H
Content-Length: 1351
Connection: close

------WebKitFormBoundaryJ0bRH1MwgMq5eu6H
Content-Disposition: form-data; name="key"

exampleobject
------WebKitFormBoundaryJ0bRH1MwgMq5eu6H
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
------WebKitFormBoundaryJ0bRH1MwgMq5eu6H
Content-Disposition: form-data; name="success_action_redirect"

https://my.website/upload_success.html
------WebKitFormBoundaryJ0bRH1MwgMq5eu6H
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjpbWyJzdGFydHMtd2l0aCIsIiRzdWNjZXNzX2FjdGlvbl9yZWRpcmVjdCIsImh0dHBzOi8vbXkud2Vic2l0ZS8iXSx7InEtc2lnbi1hbGdvcml0aG0iOiJzaGExIn0seyJxLWFrIjoiQUtJRDhBMGZCVnRZRnJObTAyb1kxZzFKUVFGMGMzSk82TkV1In0seyJxLXNpZ24tdGltZSI6IjE1NjcwNjU3NDk7MTU2NzA3Mjk0OSJ9XSwiZXhwaXJhdGlvbiI6IjIwMTktMDgtMjlUMTA6MDI6MjkuMjcyWiJ9
------WebKitFormBoundaryJ0bRH1MwgMq5eu6H
Content-Disposition: form-data; name="q-sign-algorithm"

sha1
------WebKitFormBoundaryJ0bRH1MwgMq5eu6H
Content-Disposition: form-data; name="q-ak"

AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****
------WebKitFormBoundaryJ0bRH1MwgMq5eu6H
Content-Disposition: form-data; name="q-key-time"

1567065749;1567072949
------WebKitFormBoundaryJ0bRH1MwgMq5eu6H
Content-Disposition: form-data; name="q-signature"

c4a8ae7411687bc3d6ed2ac9b249e87a50b5****
------WebKitFormBoundaryJ0bRH1MwgMq5eu6H--
```

#### Response

```shell
HTTP/1.1 303 Redirect
Content-Length: 0
Connection: close
Date: Thu, 29 Aug 2019 08:02:29 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Location: https://my.website/upload_success.html?bucket=examplebucket-1250000000&key=exampleobject&etag=%22ee8de918d05640145b18f70f4c3aa602%22
Server: tencent-cos
x-cos-request-id: NWQ2Nzg2OTVfMTRiYjI0MDlfZGFkOV85MDA4****
```

<span id="step9"></span>
#### Example 9: Specifying the success_action_status form field

#### Request

```shell
POST / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 29 Aug 2019 08:04:29 GMT
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryST9Mz8AGzCDphgJF
Content-Length: 1270
Connection: close

------WebKitFormBoundaryST9Mz8AGzCDphgJF
Content-Disposition: form-data; name="key"

exampleobject
------WebKitFormBoundaryST9Mz8AGzCDphgJF
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
------WebKitFormBoundaryST9Mz8AGzCDphgJF
Content-Disposition: form-data; name="success_action_status"

200
------WebKitFormBoundaryST9Mz8AGzCDphgJF
Content-Disposition: form-data; name="policy"

eyJjb25kaXRpb25zIjpbeyJzdWNjZXNzX2FjdGlvbl9zdGF0dXMiOiIyMDAifSx7InEtc2lnbi1hbGdvcml0aG0iOiJzaGExIn0seyJxLWFrIjoiQUtJRDhBMGZCVnRZRnJObTAyb1kxZzFKUVFGMGMzSk82TkV1In0seyJxLXNpZ24tdGltZSI6IjE1NjcwNjU4Njk7MTU2NzA3MzA2OSJ9XSwiZXhwaXJhdGlvbiI6IjIwMTktMDgtMjlUMTA6MDQ6MjkuMzI3WiJ9
------WebKitFormBoundaryST9Mz8AGzCDphgJF
Content-Disposition: form-data; name="q-sign-algorithm"

sha1
------WebKitFormBoundaryST9Mz8AGzCDphgJF
Content-Disposition: form-data; name="q-ak"

AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****
------WebKitFormBoundaryST9Mz8AGzCDphgJF
Content-Disposition: form-data; name="q-key-time"

1567065869;1567073069
------WebKitFormBoundaryST9Mz8AGzCDphgJF
Content-Disposition: form-data; name="q-signature"

e46285af04d4fb68e0624fdd0a525b6a07ab****
------WebKitFormBoundaryST9Mz8AGzCDphgJF--
```

#### Response

```shell
HTTP/1.1 200 
Content-Length: 0
Connection: close
Date: Thu, 29 Aug 2019 08:04:29 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Location: http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
Server: tencent-cos
x-cos-request-id: NWQ2Nzg3MGRfZjhjODBiMDlfOGM3N184Nzdl****
```
