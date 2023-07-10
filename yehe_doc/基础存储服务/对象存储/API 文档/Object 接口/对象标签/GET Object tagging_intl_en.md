## Overview

This API is used to query the existing tags of an object.

If a sub-account needs to call this API (`GET Object tagging`), ensure that the root account has authorized it to do so.

#### Versioning

If you have enabled versioning for the bucket and want to query the tags of an object of a specified version, include the `VersionId` parameter in the request.

## Request

#### Sample request

```plaintext
GET /<ObjectKey>?tagging&VersionId=VersionId HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

| Parameter | Description | Type | Required |
| :-------- | :----------------------------------------------------------- | :----- | :------- |
| versionId | Version ID of the object (if versioning is enabled). If this parameter is not specified, the latest version will be queried. | string | No |

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The following describes the nodes of the response body returned for this request:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------ | ------------------------------------------------------------ | ---------- | -------- |
| Tagging | None | Tagging configuration | Container | Yes |
| TagSet | Tagging | Tag set | Container | Yes |
| Tag | Tagging.TagSet | A single tag. Up to 10 tags are supported. | Containers | Yes |
| Key | Tagging.TagSet.Tag | Tag key, which can be up to 128 characters. A tag key can contain letters, digits, spaces, plus signs (+), minus signs (−), underscores (_), equals signs (=), dots (.), colons (:), and slashes (/). | String | Yes |
| Value | Tagging.TagSet.Tag | Tag value, which can be up to 256 characters. A tag value can contain letters, digits, spaces, plus signs (+), minus signs (−), underscores (_), equals signs (=), dots (.), colons (:), and slashes (/). | String | Yes |

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

The following example queries the tags of the `exampleobject.txt` object in the `examplebucket-1250000000` bucket. COS parses the request and returns the `{age:18}` and `{name:xiaoming}` tags.

```plaintext
GET /exampleobject.txt?tagging HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: Auth String
Content-Md5: MD5 String
Content-Length: 127
Content-Type: application/xml
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Connection: close
Date: Fri, 19 Jan 2020 11:40:22 GMT
Server: tencent-cos
<Tagging>
    <TagSet>
        <Tag>
            <Key>age</Key>
            <Value>18</Value>
        </Tag>
        <Tag>
            <Key>name</Key>
            <Value>xiaoming</Value>
        </Tag>
    </TagSet>
</Tagging>
```
