## Overview

This API is used to set tags for an existing object. It can help you group and manage existing object resources by adding key-value pairs as object tags. For more information, please see [Object Tagging Overview](https://intl.cloud.tencent.com/document/product/436/35665).

If a sub-account needs to call this API (`PUT Object tagging`), ensure that the root account has authorized it to do so.

> !Currently, you can set up to 10 different tags for one object. If you set more, new tags will overwrite the old ones.

#### Versioning

If you have enabled versioning for your bucket and want to add tags to a specific version of object, include the `VersionId` parameter in the request.

## Requests

#### Sample request

```plaintext
PUT /<ObjectKey>?tagging&VersionId=VersionId HTTP 1.1
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
| versionId | Version ID of the object (if versioning is enabled). If this parameter is not specified, tags will be added to the latest version of the object. | string | No |

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

You need to set the following tag set in the request body:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Tagging>
  <TagSet>
    <Tag>
      <Key>string</Key>
      <Value>string</Value>
    </Tag>
  </TagSet>
</Tagging>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------ | ------------------------------------------------------------ | ---------- | -------- |
| Tagging | None | Tagging configuration | Container | Yes |
| TagSet | Tagging | Tag set | Container | Yes |
| Tag | Tagging.TagSet | A single tag. Up to 10 tags are supported. | Containers | Yes |
| Key | Tagging.TagSet.Tag | Tag key, which can be up to 128 characters. A tag key can contain letters, digits, spaces, plus signs (+), minus signs (−), underscores (_), equals signs (=), dots (.), colons (:), and slashes (/). | String | Yes |
| Value | Tagging.TagSet.Tag | Tag value, which can be up to 256 characters. A tag value can contain letters, digits, spaces, plus signs (+), minus signs (−), underscores (_), equals signs (=), dots (.), colons (:), and slashes (/). | String | Yes |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

The following request adds the `{age:18}` and `{name:xiaoming}` tags to the `exampleobject.txt` object in the `examplebucket-1250000000` bucket. COS configures the tags and returns 200 (success).

```plaintext
PUT /exampleobject.txt?tagging HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: Auth String
Content-Length: 127
Content-MD5:MD5 String
Content-Type: application/xml

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

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 19 Jan 2020 11:40:22 GMT
Server: tencent-cos
x-cos-request-id: NWE2MWQ5MjZfMTBhYzM1MGFfMTA5ODVfMTVj****
```
