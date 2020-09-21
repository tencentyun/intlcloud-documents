## Feature Description

This API is used to upload a local object of less than 5 GB in size to a specified bucket through an HTML form. To make this request, you need to have the permission to write to the bucket.

> !
> - This API has special requirements for signatures instead of using standard COS request signatures. For more information, please see [Signature protection](#id1) and description of related fields.
> - If versioning is not enabled and you try to upload an object whose name already exists, the newly uploaded object will overwrite the prior one and a response will be returned in the specified way upon success.

#### Versioning

- If versioning is enabled for the bucket, COS will automatically generate a unique version ID for the object to be uploaded. It returns this ID in the response by using the `x-cos-version-id` response header.
- If versioning is suspended for the bucket, COS will always use `null` as the version ID of the object in the bucket and will not return the `x-cos-version-id` response header.

## Request

#### Sample request

```shell
POST / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: multipart/form-data; boundary=Multipart Boundary
Content-Length: Content Length

[Multipart Form Data]
```

#### Request form

The request body of this API is encoded with multipart/form-data. When sending requests in HTML with the &lt;form&gt; element, you need to configure the `enctype` attribute of the &lt;form&gt; element as multipart/form-data, and then use HTML form elements (such as &lt;input&gt; and &lt;select&gt;) to add required form fields.

**Form fields**

| Name | Description | Type | Required |
| ----------------------- | ------------------------------------------------------------ | ------ | -------- |
| key | Object key. If you specify the `${filename}` wildcard in the object key, the wildcard in the object key will be replaced with the actual filename. For more information, please see [Sample 7](#step7) | string | Yes |
| Cache-Control | Cache directives as defined in RFC 2616, which will be stored in the object metadata | string | No |
| Content-Disposition | Filename as defined in RFC 2616, which will be stored in the object metadata | string | No |
| Content-Encoding | Encoding format as defined in RFC 2616, which will be stored in the object metadata | string | No |
| Content-Type | HTTP content type (MIME) as defined in RFC 2616, which will be stored in the object metadata<br>**Note:** when files are uploaded through forms, the browser will automatically carry the MIME type of the specified file in the request. However, COS will not use the MIME type carried by the browser, so you need to explicitly specify the `Content-Type` field as the object content type | string | No |
| Expires | The cache expiration time as defined in RFC 2616, which will be saved in the object metadata | string | No |
| success_action_redirect | Destination address for URL redirect upon a successful upload. If this field is not set, HTTP status code 303 (Redirect) and the `Location` response header will be returned. The `Location` response header will include the URL address specified by this field together with the bucket, key, and etag parameters. For more information, please see [Sample 8](#step8) | string | No |
| success_action_status | HTTP status code returned upon a successful upload. Valid values: 200, 201, 204; default value: 204. If `success_action_redirect` is specified, this field will be ignored. For more information, please see [Sample 9](#step9) | number | No |
| x-cos-meta-\*           | Contains user-defined metadata and header suffixes, which will be stored in the object metadata. Maximum size: 2 KB. <br>**Note:** user-defined metadata can contain underscores (_), while the header suffixes of user-defined metadata can only contain minus signs (-) but not underscores | string | No |
| x-cos-storage-class | Object storage class, such as `MAZ_STANDARD`, `MAZ_STANDARD_IA`, `STANDARD_IA`,`ARCHIVE`, and `DEEP_ARCHIVE`. Default value: STANDARD. For enumerated values, please see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925) | Enum | No |
| x-cos-traffic-limit | Specifies the traffic limit in bit/s on this upload. Value range: 819200-838860800, that is, 100 KB/s-100 MB/s. if this range is exceeded, a 400 error will be returned | integer | No       |
| Content-MD5 | MD5 hash value of the Base64-encoded file content used for integrity check, i.e., checking whether the file content has changed during the upload | string | No |
| file                    | Information and content of the file. When the file is uploaded through the web form, the browser will automatically set the value of this field to the correct format. <br>**Note:** the `file` field must be placed at the end of the entire form. | file | Yes |

**ACL-related form fields**

You can configure access permissions for the object by specifying the following form fields during upload:

| Name | Description | Type | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| x-cos-acl | Defines the access control list (ACL) attribute of the object. For enumerated values such as `default`, `private`, and `public-read`, please see the Preset ACL section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: default <br>**Note:** currently, there can be up to 1,000 entries in one ACL. If you don't need access control for the object, set the field to `default` or simply leave it empty, and the object will inherit the permissions of the bucket | Enum | No |
| x-cos-grant-read | Grants a user read permission for an object in the format of `id="[OwnerUin]"`, such as `id="100000000001"`. You can use commas (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |
| x-cos-grant-read-acp | Grants a user read permission for the ACL of an object in the format of `id="[OwnerUin]"`, such as `id="100000000001"`. You can use commas (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |
| x-cos-grant-write-acp | Grants a user write permission for the ACL of an object in the format of `id="[OwnerUin]"`, such as `id="100000000001"`. You can use commas (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |
| x-cos-grant-full-control | Grants a user full permission to operate on an object in the format of `id="[OwnerUin]"`, such as `id="100000000001"`. You can use commas (,) to separate multiple users, such as `id="100000000001",id="100000000002"` | string | No |

**Form fields related to server-side encryption**

You can use server-side encryption by specifying the following form fields when uploading the object:

| Name | Description | Type | Required |
| ----------------------------------------------- | ------------------------------------------------------------ | ------ | ------------------------------------------ |
| x-cos-server-side-encryption                    | Server-side encrypt algorithm. Valid values: AES256, cos/kms                         | string | Yes if SSE-COS or SSE-KMS is used |
| x-cos-server-side-encryption-customer-algorithm | Server-side encryption algorithm. AES256 is supported | string | Yes if SSE-C is used |
| x-cos-server-side-encryption-cos-kms-key-id | When the value of `x-cos-server-side-encryption` is `cos/kms`, this field is used to specify the CMK of KMS. If it is not specified, the CMK created by COS will be used by default. For more information, please see [SSE-KMS Encryption](https://intl.cloud.tencent.com/document/product/436/18145) | string | No |
| x-cos-server-side-encryption-context | When the value of `x-cos-server-side-encryption` is `cos/kms`, this field is used to specify the encryption context, and its value is a Base64-encoded string of the key-value pair for the encryption context in JSON format, <br>such as `eyJhIjoiYXNkZmEiLCJiIjoiMTIzMzIxIn0=` | string | No |
| x-cos-server-side-encryption-customer-key | Base64-encoded server-side encryption key, <br/>such as `MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=` | string | Yes if SSE-C is used |
| x-cos-server-side-encryption-customer-key-MD5 | Base64-encoded MD5 hash value of the server-side encryption key, <br/>such as `U5L61r7jcwdNvT7frmUG8g==` | string| Yes if SSE-C is used |

<span id="id1"></span>

#### Signature protection

The `POST Object` API requires signature-related fields to be carried in the request. After receiving the message, the COS server will perform authentication. If the authentication is successful, the request will be accepted and executed; otherwise, an error message will be returned, and the request will be discarded.

The signature is generated as follows:

#### 1. Prepare

Log in to the CAM Console and get your project's `SecretId` and `SecretKey` on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page.

#### 2. Generate KeyTime

a. Get the Unix timestamp `StartTimestamp` corresponding to the current time, which is the total seconds from January 1, 1970, 00:00:00 UTC (January 1, 1970, 08:00:00 Beijing time) to now.
b. Calculate the Unix timestamp `EndTimestamp` for the moment the signature will expire based on the timestamp above and the expected valid duration of the signature.
c. Get the signature validity period (i.e., `KeyTime`) by splicing the two timestamps above in the format of `StartTimestamp;EndTimestamp`.

#### 3. Create a policy

A policy is a piece of JSON text. A typical policy is as follows:

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

Here:

- expiration: expiration time of the policy, which is a string in ISO8601 format
- conditions: an array of specific conditions for the policy. The specific rules for the conditions are listed below.

| Type | Description |
| -------- | ------------------------------------------------------------ |
| Exact match | Expressed in the format of `{ "key": "value" }` or `[ "eq", "$key", "value" ]`, where `key` is a specified form field and `value` is a specified value |
| Prefix match | Expressed in the format of `[ "starts-with", "$key", "value" ]`, where `key` is a specified form field and `value` is a specified prefix which can be empty |
| Range match | Only applicable to `[ "content-length-range", minNum, maxNum ]` and used to limit the file length to be within `minNum` and `maxNum` |

The form fields that can be specified are as follows:

| Field Name | Description | Match Mode | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------------------------------------- | -------- |
| acl                                                          | Access control list (ACL) attribute of object                                | Exact, prefix                                         | No       |
| bucket                                                       | Bucket to upload to                                                 | Exact                                               | No       |
| key                                                          | Object key. If the `${filename}` wildcard is used for it during upload, it will be processed as the final object key before the policy is verified. At this time, prefix match should be used in the policy instead of the `${filename}` wildcard | Exact, prefix | No |
| content-length-range                                         | File length range                                                 | Range                                               | No       |
| Cache-Control, Content-Type, Content-Disposition, Content-Encoding, Expires | The relevant headers as defined in RFC 2616 will be returned as response headers when the object is downloaded | Exact, prefix | No |
| success_action_redirect                                      | Destination URL address for redirection upon upload success                              | Exact, prefix                                         | No       |
| success_action_status                                        | HTTP status code returned upon upload success                                 | Exact                                               | No       |
| x-cos-meta-*                                                 | User-defined metadata header field                                   | Exact, prefix                                         | No       |
| x-cos-*                                                      | Other COS-related form fields mentioned in this document, such as fields related to ACL and SSE | Exact                                               | No       |
| q-sign-algorithm                                             | Signature hash algorithm, which is always `sha1`                                    | Exact                                               | Yes       |
| q-ak                                                         | Aforementioned `SecretId`                                          | Exact                                               | Yes       |
| q-sign-time                                                  | `KeyTime` generated above                                        | Exact                                               | Yes       |

> ! 
>
> - Fields other than the buckets defined in the policy must appear in the form fields. For example, if you specify `{ "acl": "default" }`, `acl` must be present in the form with the value `default`.
>- For security reasons, we strongly recommend you specify all the form fields that can be specified.

#### 4. Generate SignKey

Calculate the message digest (hash value in hexadecimal lowercase) by using HMAC-SHA1 with `SecretKey` as the key and `KeyTime` as the message, which is `SignKey`, such as `39acc8c9f34ba5b19bce4e965b370cd3f62d2fba`.

#### 5. Generate StringToSign

Calculate the message digest (hash value in hexadecimal lowercase) by using SHA1 on the policy text constructed above, which is `StringToSign`, such as `d5d903b8360468bc81c1311f134989bc8c8b5b89`.

#### 6. Generate a signature

Calculate the message digest (hash value in hexadecimal lowercase) by using HMAC-SHA1 with `SignKey` (in string form instead of original binary form) as the key and `StringToSign` (in string form instead of original binary form) as the message, which is `Signature`, such as `7758dc9a832e9d301dca704cacbf9d9f8172fdef`.

#### 7. Attach the signature to the form

Attach the above policy and signature-related information to the form as described in the following table:

| Name | Description | Type | Required |
| ---------------- | -------------------------------------- | ------ | -------- |
| x-cos-security-token | Specifies the security token required when using temporary security credentials. For details, see [Temporary security credentials](https://intl.cloud.tencent.com/document/product/436/30613#temporary-security-credentials) | string | Required only if you are<br>using temporary keys |
| policy | Base64-encoded policy content | string | Yes |
| q-sign-algorithm | Signature hash algorithm, which is always `sha1`              | string | Yes       |
| q-ak             | Aforementioned `SecretId`                    | string | Yes       |
| q-key-time       | `KeyTime` generated above                   | string | Yes       |
| q-signature      | `Signature` generated above                 | string | Yes       |

>!The signature form fields need to be before the file form fields.

**Signature protection use case**

**Preparations**

Log in to the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM Console to get your `APPID`, `SecretId`, and `SecretKey`. Below is an example:

| APPID      | SecretId                             | SecretKey                        |
| ---------- | ------------------------------------ | -------------------------------- |
| 1250000000 | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q | BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz |

**Construction policy**

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

**Intermediate variables**

- KeyTime = `1567150692;1567157892`
- SignKey = `39acc8c9f34ba5b19bce4e965b370cd3f62d2fba`
- StringToSign = `d5d903b8360468bc81c1311f134989bc8c8b5b89`
- Signature = `7758dc9a832e9d301dca704cacbf9d9f8172fdef`

**Signature form fields**

- policy = `ewogICAgImV4cGlyYXRpb24iOiAiMjAxOS0wOC0zMFQwOTozODoxMi40MTRaIiwKICAgICJjb25kaXRpb25zIjogWwogICAgICAgIHsgImFjbCI6ICJkZWZhdWx0IiB9LAogICAgICAgIHsgImJ1Y2tldCI6ICJleGFtcGxlYnVja2V0LTEyNTAwMDAwMDAiIH0sCiAgICAgICAgWyAic3RhcnRzLXdpdGgiLCAiJGtleSIsICJmb2xkZXIvc3ViZm9sZGVyLyIgXSwKICAgICAgICBbICJzdGFydHMtd2l0aCIsICIkQ29udGVudC1UeXBlIiwgImltYWdlLyIgXSwKICAgICAgICBbICJzdGFydHMtd2l0aCIsICIkc3VjY2Vzc19hY3Rpb25fcmVkaXJlY3QiLCAiaHR0cHM6Ly9teS53ZWJzaXRlLyIgXSwKICAgICAgICBbICJlcSIsICIkeC1jb3Mtc2VydmVyLXNpZGUtZW5jcnlwdGlvbiIsICJBRVMyNTYiIF0sCiAgICAgICAgeyAicS1zaWduLWFsZ29yaXRobSI6ICJzaGExIiB9LAogICAgICAgIHsgInEtYWsiOiAiQUtJRFFqejNsdG9tcFZqQm5pNUxpdGtXSEZsRnB3a245VTVxIiB9LAogICAgICAgIHsgInEtc2lnbi10aW1lIjogIjE1NjcxNTA2OTI7MTU2NzE1Nzg5MiIgfQogICAgXQp9`
- q-sign-algorithm = `sha1`
- q-ak = `AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q`
- q-key-time = `1567150692;1567157892`
- q-signature = `7758dc9a832e9d301dca704cacbf9d9f8172fdef`

## Response

#### Response header

In addition to common response headers, this API also returns the following response headers. For more information on common response headers, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Location | <li> When the `success_action_redirect` form field is used, the value of this response header will be the URL specified by `success_action_redirect`, with bucket, key, and etag parameters appended. For related samples, please see [Sample 8](#step8) in this document <br> <li>If the `success_action_redirect` form field is not used, the value of this response header will be the complete URL address for object access. For related samples, please see [Sample 1](#step1) | string |

**Versioning-related headers**

If the object is uploaded to a versioning-enabled bucket, the following response headers will be returned:

| Name | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Object version ID | string |

**Headers related to server-side encryption (SSE)**

If server-side encryption is used during object upload, this API will return the headers used specifically for server-side encryption. For more information, please see [Server-Side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

<span id="step1"></span>

#### Sample 1. Simple sample (with versioning not enabled)

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
------WebKitFormBoundaryZBPbaoYE2gqeB21N
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
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

#### Sample 2. Specifying metadata and ACL by using form fields

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
------WebKitFormBoundary9JtEhEGHSdx8Patg
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
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

#### Sample 3. Using server-side encryption SSE-COS

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
------WebKitFormBoundaryBVaHvBJQJnQrAxKY
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
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

#### Sample 4. Using server-side encryption SSE-C

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
------WebKitFormBoundaryYa6H7Gd4xuhlyfJb
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
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

#### Sample 5. Enabling versioning

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
------WebKitFormBoundaryJspR3QIUhGJLALwf
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
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

#### Sample 6. Suspending versioning

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
------WebKitFormBoundaryX8hd2lxTMzIBk5Li
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
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

#### Sample 7. Using `${filename}` wildcard for object key (form field key)

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
------WebKitFormBoundaryHrAMWZO4BNyT0rca
Content-Disposition: form-data; name="file"; filename="photo.jpg"
Content-Type: image/jpeg

[Object Content]
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

#### Sample 8. Specifying the success_action_redirect form field

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
------WebKitFormBoundaryJ0bRH1MwgMq5eu6H
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
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

#### Sample 9. Specifying the success_action_status form field

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
------WebKitFormBoundaryST9Mz8AGzCDphgJF
Content-Disposition: form-data; name="file"; filename="example.jpg"
Content-Type: image/jpeg

[Object Content]
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
