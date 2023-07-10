## Feature Description

This API is used to upload an object within 5 GB to a bucket using an HTML form. To call this API, you need to have permission to write to the bucket.

> !
>- This API requires a signature different from the standard COS request signatures. For more information, see [Signature protection](#id1) and the description of related fields.
> - If you upload an object whose name is the same as another object that is already stored in the bucket with versioning disabled, the old object will be overwritten and the response will be returned normally as specified upon successful upload.
> - To upload an image, see the [PUT Object](https://www.tencentcloud.com/document/product/436/7749) API examples for data filling.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PostObject&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>


#### Versioning

- For a versioning-enabled bucket, COS will automatically generate a unique version ID for the object, and the ID will be returned in the `x-cos-version-id` response header.
- For a versioning-suspended bucket, COS will always use `null` as the version ID of the object and will not return the `x-cos-version-id` response header.

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

>? Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com, where &lt;BucketName-APPID> is the bucket name followed by the `APPID`, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> 

#### Request form

The request body of this API is encoded with multipart/form-data. When sending the request with the HTML &lt;form&gt; element, set the value of the `enctype` attribute to `multipart/form-data`. After this, use HTML elements (such as &lt;input&gt; and &lt;select&gt;) to add form fields as needed.

**Form fields**

| Field | Description | Type | Required |
| ----------------------- | ------------------------------------------------------------ | ------- | -------- |
| key | Object key. If you use the `${filename}` wildcard in the object key, the wildcard will be replaced with the name of the object uploaded (see [Example 7](#step7)). | string | Yes |
| Cache-Control | Cache directives defined in RFC 2616. It will be stored as object metadata. | string | No |
| Content-Disposition | Filename defined in RFC 2616. It will be stored as object metadata. | string | No |
| Content-Encoding | Encoding format defined in RFC 2616. It will be stored as object metadata. | string | No |
| Content-Type | HTTP content type (MIME) defined in RFC 2616. It will be stored as object metadata<br>**Note:** If a file is uploaded via an HTML form, the browser will automatically carry the file's MIME type in the request. However, COS will not use this MIME type carried. Therefore, you need to use the `Content-Type` field to specify the content type of the object. | string | No |
| Expires | Cache expiration time defined in RFC 2616. It will be stored as object metadata. | string | No |
| success_action_redirect | Redirection target URL if the upload succeeds. If this field is set, HTTP status code "303 (Redirect)" and the `Location` response header will be returned. `Location` will include the URL specified in this field as well as the bucket, key, and ETag parameters (see [Example 8](#step8)). | string | No |
| success_action_status | HTTP status code to return for a successful upload. Valid values: `200`, `201`, `204` (default). If `success_action_redirect` is specified, this field will be ignored (see [Example 9](#step9)). | number | No |
| x-cos-meta-\* | User-defined metadata and header suffixes. It will be stored as object metadata. Maximum size: 2 KB. <br>**Note**: User-defined metadata can contain underscores (_), but header suffixes can contain minus signs (−) but not underscores. | string | No |
| x-cos-storage-class | Object storage class. For the enumerated values, such as `STANDARD` (default), `INTELLIGENT_TIERING`, `STANDARD_IA`, `ARCHIVE`, and `DEEP_ARCHIVE`, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | Enum | No |
| x-cos-traffic-limit | Limits the speed (in bit/s) for the current upload for traffic control. Valid range: 819200−838860800 (i.e., 100 KB/s−100 MB/s). If the speed exceeds the limit, a 400 error will be returned. | integer | No |
| Content-MD5 | MD5 checksum of the Base64-encoded file content. It is used for integrity check, i.e., whether the file content has changed during the upload. | string | No |
| file | File information and content. When the file is uploaded via an HTML form, the browser automatically sets the value of this parameter to the correct format. <br>**Note**: This field must be placed at the end of the form. | file | Yes |

**ACL-related form fields**

You can configure access permissions for the object by specifying the following form fields during upload:

| Field &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ | -------- |
| acl | Defines the ACL attribute of the object. For the enumerated values, such as `default` (default), `private`, and `public-read`, see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). <br>**Note**: If you do not need to set an ACL for the object, set this parameter to `default` or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | Enum | No |
| x-cos-grant-read | Grants a user permission to read the object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use comma (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-read-acp | Grants a user permission to read the ACL of an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use comma (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-write-acp | Grants a user permission to write to the ACL of an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use comma (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-full-control | Grants a user full permission to operate on an object in the format: `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use comma (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |

**SSE-related form fields**

You can use server-side encryption by specifying the following form fields during upload:

| Field |  Description | Type | Required |
| ----------------------------------------------- | ------------------------------------------------------------ | ------ | ------------------------------------------ |
| x-cos-server-side-encryption | Server-side encryption algorithm. `AES256` and `cos/kms` are supported. | string | Required if SSE-COS or SSE-KMS is used |
| x-cos-server-side-encryption-customer-algorithm | Server-side encryption algorithm. AES256 is supported. | string | Required if SSE-C is used |
| x-cos-server-side-encryption-cos-kms-key-id | Customer master key (CMK) of KMS if `x-cos-server-side-encryption` is set to `cos/kms`. If this field is not specified, the default CMK created by COS will be used. For more information, see [SSE-KMS Encryption](https://intl.cloud.tencent.com/document/product/436/18145). | string | No |
| x-cos-server-side-encryption-context | Base64-encoded encryption context (key-value pairs in JSON format) if `x-cos-server-side-encryption` is set to `cos/kms`. <br>Example: `eyJhIjoiYXNkZmEiLCJiIjoiMTIzMzIxIn0=` | string | No |
| x-cos-server-side-encryption-customer-key | Base64-encoded server-side encryption key <br/>Example: `MDEyMzQ1Njc4OUFCQ0RFRjAxMjM0NTY3ODlBQkNERUY=` | string | Required if SSE-C is used |
| x-cos-server-side-encryption-customer-key-MD5 | Base64-encoded MD5 checksum of the server-side encryption key <br/>Example: `U5L61r7jcwdNvT7frmUG8g==` | string | Required if SSE-C is used |

<span id="id1"></span>

#### Signature protection

This API requires signature-related fields to be carried in the request. COS authenticates the messages carried, and if the authentication is passed, COS executes the request. If not, COS returns an error message and discards the request.

You can generate a signature as follows:

#### 1. Preparations

Log in to the CAM console and go to [Manage API Key](https://console.cloud.tencent.com/cam/capi) to get the `SecretId` and `SecretKey`.

#### 2. Generate KeyTime

a. Get the Unix `StartTimestamp` of the current time. It is the total number of seconds elapsed from January 1, 1970, 00:00:00 UTC till the current time.
b. Calculate the Unix `EndTimestamp` for the signature to expire according to `StartTimestamp` and the expected validity period of the signature.
c. Generate `KeyTime` by splicing the two timestamps above in `StartTimestamp;EndTimestamp` format.

#### 3. Construct a policy

A policy is a text in JSON format. A typical policy is as follows:

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

On the **Stream Interruption Records** page:

- `expiration`: The policy's expiration time, which is a string in ISO 8601 format.
- `conditions`: An array of conditions for the policy. The conditions are described below.

| Type | Description |
| -------- | ------------------------------------------------------------ |
| Exact Match | Uses `{" key ":" value "}` or `[" eq "," $ key "," value "]`, where `key` is a limited form field and `value` is a limited value. |
| Prefix Match | Uses `[ "starts-with", "$key", "value" ]`, where `key` is a limited form field and `value` is a limited prefix that can be empty. |
| Range Match | Uses `[ "content-length-range", minNum, maxNum ]` to limit the file size to be within `minNum` and `maxNum`. |

Form fields that can be limited are as follows:

| Field | Description | Match Type &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Required |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------------------------------------- | -------- |
| acl | ACL attribute of the object | Exact/Prefix | No |
| bucket | Bucket for upload | Exact | No |
| key | Object key. If you use the `${filename}` wildcard in the object key during upload, the object key will be processed to the final object key before the policy is verified. Therefore, you should use prefix match in the policy and `${filename}` should not appear. | Exact/Prefix | No |
| content-length-range | Range of the file length | Range | No |
| Cache-Control, Content-Type, Content-Disposition, Content-Encoding, Expires | Headers defined in RFC 2616, which will be returned as response headers when the object is downloaded. | Exact/Prefix | No |
| success_action_redirect | Redirection target URL when the upload succeeds | Exact/Prefix | No |
| success_action_status | HTTP status code returned when the upload succeeds | Exact | No |
| x-cos-meta-* | User-defined metadata headers | Exact/Prefix | No |
| x-cos-* | Other COS-related form fields described in this document, such as ACL- or SSE-related fields | Exact | No |
| q-sign-algorithm  | Signature hash algorithm. Fixed at `sha1` | Exact | Yes |
| q-ak | `SecretId` mentioned above | Exact | Yes |
| q-sign-time | `KeyTime` generated above | Exact | Yes |

> ! 
>- Except for `bucket`, fields that are used for limitation in the policy must be used in the form fields. For example, if `{ "acl": "default" }` is used, `acl` must be used and set to `default` in the form.
>- For security reasons, we recommend you use all limitable form fields.

#### 4. Generate SignKey

Use HMAC-SHA1 with `SecretKey` as the key and `KeyTime` as the message to calculate the message digest (hash value, lowercase hexadecimal), that is, the `SignKey` (e.g., `39acc8c9f34ba5b19bce4e965b370cd3f62d2fba`).

#### 5. Generate StringToSign

Use SHA1 with the policy text constructed above to calculate the message digest (hash value, lowercase hexadecimal), that is, the `StringToSign` (e.g., `d5d903b8360468bc81c1311f134989bc8c8b5b89`).

#### 6. Generate Signature

Use HMAC-SHA1 with `SignKey` (string, not binary) as the key and `StringToSign` (string, not binary) as the message to calculate the message digest (hash value, lowercase hexadecimal), that is, the `Signature` (e.g., `7758dc9a832e9d301dca704cacbf9d9f8172fdef`).

#### 7. Attach the signature to the form

Attach the policy and signature-related information above to the form as described in the following table:

| Parameter |  Description | Type |Required |
| -------------------- | ------------------------------------------------------------ | ------ | ------------------------------------------ |
| x-cos-security-token | Security token when a temporary security token is used. For more information, see [Temporary security credentials](https://intl.cloud.tencent.com/document/product/436/30613). | string | No <br>(Required when a temp key is used) |
| policy | Base64-encoded policy | string | Yes |
| q-sign-algorithm | Signature hash algorithm. Fixed at `sha1` | string | Yes |
| q-ak | `SecretId` mentioned above | string | Yes |
| q-key-time | `KeyTime` generated above | string | Yes |
| q-signature | `Signature` generated above | string | Yes |

> !Signature form fields should be placed before the `file` form field.

**Signature protection use cases**

**Preparations**

Log in to the CAM console and go to the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page to obtain your `APPID`, `SecretId`, and `SecretKey`. Below is an example:

| APPID      | SecretId                             | SecretKey                        |
| ---------- | ------------------------------------ | -------------------------------- |
| 1250000000 | AKIDQjz3ltompVjBni5LitkWHFlFpwkn9U5q | BQYIM75p8x0iWVFSIgqEKwFprpRSVHlz |

**Constructing a policy**

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

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information about common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Header | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Location | <li>If `success_action_redirect` is used, the value is the URL specified in `success_action_redirect` as well as the bucket, key, and ETag parameters (see [Example 8](#step8)).<br><li>If `success_action_redirect` is not used, the value is the full access URL of the object (see [Example 1](#step1)). | string |

**Versioning-Related Headers**

If the object is uploaded to a versioning-enabled bucket, the following response headers will be returned:

| Header | Description | Type |
| ---------------- | ------------- | ------ |
| x-cos-version-id | Version ID of the object | string |

**SSE-related headers**

If server-side encryption is used during object upload, this API will return headers used specifically for server-side encryption. For more information, see [Server-Side Encryption Headers](https://intl.cloud.tencent.com/document/product/436/7729#.E6.9C.8D.E5.8A.A1.E7.AB.AF.E5.8A.A0.E5.AF.86.E4.B8.93.E7.94.A8.E5.A4.B4.E9.83.A8).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

<span id="step1"></span>

#### Sample 1: Simple use case (with versioning disabled)

#### Request

<dx-codeblock>
:::  shell
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
:::
</dx-codeblock>

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

#### Sample 2: Specifying metadata and ACL using form fields

#### Request

<dx-codeblock>
:::  shell
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
:::
</dx-codeblock>

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

#### Sample 3: Using server-side encryption SSE-COS

#### Request

<dx-codeblock>
:::  shell
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
:::
</dx-codeblock>

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

#### Sample 4: Using server-side encryption SSE-C

#### Request

<dx-codeblock>
:::  shell
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
:::
</dx-codeblock>

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

#### Sample 5: Versioning-enabled

#### Request

<dx-codeblock>
:::  shell
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
:::
</dx-codeblock>

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

#### Sample 6: Versioning-suspended

#### Request

<dx-codeblock>
:::  shell
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
:::
</dx-codeblock>

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

#### Sample 7: Using the `${filename}` wildcard in the object key (`key` form field)

#### Request

<dx-codeblock>
:::  shell
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
:::
</dx-codeblock>

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

#### Sample 8: Specifying the `success_action_redirect` form field

#### Request

<dx-codeblock>
:::  shell
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
:::
</dx-codeblock>

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

#### Sample 9: Specifying the `success_action_status` form field

#### Request

<dx-codeblock>
:::  shell
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
:::
</dx-codeblock>

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
