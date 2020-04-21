## Feature

This API (PUT Object tagging) is used to set tags on an existing object. It can help you group and manage existing object resources by adding key-value pairs as object tags. For more information, see [Object Tagging Overview] (https://intl.cloud.tencent.com/document/product/436/35665).

If you call the `PUT Object tagging` API using a sub-account, please make sure that you have obtained the permission to use this API from the root account.

> Currently, you can set up to 10 different tags on one object. If you set more, COS will replace the existing tags with new ones.

#### Request

#### Request sample

```http
PUT /<ObjectKey>tagging&VersionId=VersionId HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)
> - When versioning is enabled for your bucket, to add tags to the specified version of an object, you can include `VersionId` in your request.

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

For this request, you need to configure the following set of tags:

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

The data are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------ | ------------------------------------------------------------ | ---------- | -------- |
| Tagging | None | Tag set | Container | Yes |
| TagSet | Tagging | Tag set | Container | Yes |
| Tag | Tagging.TagSet | Tag set, which can contain up to 10 tags | Containers | Yes |
| Key | Tagging.TagSet.Tag | Tag key, which can contain up to 128 characters. A tag key can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String | Yes |
| Value | Tagging.TagSet.Tag | Tag value, which can contain up to 256 characters. A tag value can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String | Yes |

## Response

#### Response headers

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

The following describes some frequent special errors that may occur when you make this request:

| Error Code | Description | HTTP Status Code |
| --------------------- | ------------------------------------------------------------ | --------------- |
| SignatureDoesNotMatch | Returned if you provide an invalid signature     | 403 Forbidden |
| NoSuchObject          | Returned when the object does not exist, and thus you cannot read its tags           | 404 Not Found   |
| MalformedXML          | Invalid XML format. Please cross check it against the Restful API documentation.                | 400 Bad Request |
| BadRequest            | The maximum number of 10 tags for one object is exceeded. | 400 Bad Request |
| InvalidTag            | The tag key or value contains the preset string `cos:` or `Project`. | 400 Bad Request |

## Use Cases

#### Request

The following request writes two tags "{age:18}" and "{name:xiaoming}" to the bucket `examplebucket-1250000000`. COS successfully configured the tags and returns 204 (success).

```shell
PUT /exampleobject.txt?tagging HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: Auth String
Content-Length: 127
Content-MD5: MD5 String
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

```shell
HTTP/1.1 204 No Content
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 19 Jan 2020 11:40:22 GMT
Server: tencent-cos
x-cos-request-id: NWE2MWQ5MjZfMTBhYzM1MGFfMTA5ODVfMTVj****
```
