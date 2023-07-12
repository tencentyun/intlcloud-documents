## Overview

This API is used to create a bucket under a specified account. A signature needs to be carried in `Authorization` and anonymous calls are not supported. By default, the bucket creator is the bucket owner.

>?
>- If no access permission is specified for a bucket when it is created, `private` (private read/write) will be used by default.
>- To create an MAZ bucket, you should indicate the bucket configuration through the request body; otherwise, you don't need to pass in the request body.
>


<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutBucket&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>


## Request

#### Sample request

**Sample 1**
```plaintext
PUT / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: 0
Authorization: Auth String
```

**Sample 2**
```plaintext
PUT / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Type: application/xml
Content-Length: Content Length
Content-MD5: MD5
Authorization: Auth String

[Request Body]
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

This API has no request parameter.

#### Request headers

In addition to common request headers, this API also supports the following request headers. For more information about common request headers, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

| Header | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ------- | -------- |
| x-cos-tagging      | Adds up to 50 tags to a bucket during bucket creation, such as `key1=value1&key2=value2`. | string | No |


**ACL-related headers**

You can configure an access control list (ACL) for a bucket by specifying the following request headers during bucket creation:

| Header | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ------ | -------- |
| x-cos-acl | Defines the access control list (ACL) attribute of the bucket. For the enumerated values such as `private` (default) and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). | Enum | No |
| x-cos-grant-read | Grants a user permission to read the bucket in the format of `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use a comma (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-write | Grants a user permission to write to the bucket in the format of `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use a comma (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-read-acp | Grants a user permission to read the ACL and policies of the bucket in the format of `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use a comma (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-write-acp | Grants a user permission to write to the ACL and policies of a bucket in the format of `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use a comma (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |
| x-cos-grant-full-control | Grants a user full permission to operate on the bucket in the format of `id="[OwnerUin]"` (e.g., `id="100000000001"`). You can use a comma (,) to separate multiple users, for example, `id="100000000001",id="100000000002"`. | string | No |

#### Request body

Submit the **application/xml** request data only when you need to create an MAZ bucket, which includes the configuration information for bucket creation; otherwise, you don't need to pass in the request body.

```xml
<CreateBucketConfiguration>
	<BucketAZConfig>string</BucketAZConfig>
</CreateBucketConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| CreateBucketConfiguration | None | All configurations of the `PUT Bucket` request | Container | No |

**`CreateBucketConfiguration` has the following sub-nodes:**

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| --- | --- | --- | --- | --- |
| BucketAZConfig | CreateBucketConfiguration | AZ configuration of the bucket. To create an MAZ bucket, specify `MAZ`. | string | Yes |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1: simple use case (OAZ bucket)

#### Request

```plaintext
PUT / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Sun, 26 May 2019 14:51:38 GMT
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1558882298;1558889498&q-key-time=1558882298;1558889498&q-header-list=content-length;date;host&q-url-param-list=&q-signature=c25fd640274a6da2318935ceebfbcfba4598****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Sun, 26 May 2019 14:51:37 GMT
Server: tencent-cos
x-cos-request-id: NWNlYWE3ZjlfZDQyNzVkNjRfMzg1N18yNzFh****
```

#### Example 2: setting `public-read` and granting a user permissions to write to the bucket and read the bucket ACL and policies

#### Request

```plaintext
PUT / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 14 Jun 2019 13:48:59 GMT
x-cos-acl: public-read
x-cos-grant-write: id="100000000002"
x-cos-grant-read-acp: id="100000000002"
Content-Length: 0
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1560520139;1560527339&q-key-time=1560520139;1560527339&q-header-list=content-length;date;host;x-cos-acl;x-cos-grant-read-acp;x-cos-grant-write&q-url-param-list=&q-signature=df03e7917270e0bf2b679bc6f99793bd0c63****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Fri, 14 Jun 2019 13:49:00 GMT
Server: tencent-cos
x-cos-request-id: NWQwM2E1Y2NfZjBhODBiMDlfOTM1YV83NDRi****
```

#### Sample 3: Creating an MAZ bucket

#### Request

```plaintext
PUT / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 04 Jun 2020 06:06:09 GMT
Content-Type: application/xml
Content-Length: 96
Content-MD5: R1ES/YbddhKJK/wcN+f4yg==
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1591250769;1591257969&q-key-time=1591250769;1591257969&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=28db662452fcdf8f004fc578f1c3fccbfedd****
Connection: close

<CreateBucketConfiguration>
	<BucketAZConfig>MAZ</BucketAZConfig>
</CreateBucketConfiguration>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Date: Thu, 04 Jun 2020 06:06:10 GMT
Server: tencent-cos
x-cos-request-id: NWVkODhmNTFfM2JiODJhMDlfMjg4NmFfMzA5ZmE2****
```

#### Sample 4: Creating a bucket and adding tags

The following sample request is used to create the bucket `examplebucket-1250000000` in Beijing region and add two tags `<a,a>` and `<b,b>` to the bucket.

#### Request

```plaintext
PUT / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
x-cos-tagging: a=a&b=b
Authorization: q-sign-algorithm=sha1&q-ak=AKIDYv3vWrwkHXVDf******&q-sign-time=1667446950;1668447000&q-key-time=1667446950;1668447000&q-url-param-list=&q-header-list=host;x-cos-tagging&q-signature=6d0ef3446f29aca9f28f66a031******
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: keep-alive
Date: Thu, 03 Nov 2022 03:43:30 GMT
Server: tencent-cos
x-cos-request-id: NjM2MzM4ZTJfZDRiNTE0M********
```

