## Description

COS supports setting tags for existing buckets. This API (PUT Bucket tagging) is used to set key-value pairs for a bucket as tags, helping you manage existing bucket resources and costs.

>  Currently, up to 30 different tags can be set for one bucket.

## Request

#### Sample Request

```http
PUT /?tagging HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

>? Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request Header

#### Common Headers

The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

This request operation has no special request headers.

#### Request Body

For this request, you need to configure the following set of tags:

```http
<?xml version="1.0" encoding="UTF-8" ?>
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

The detailed data are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------ | ------------------------------------------------------------ | ---------- | ---- |
| Tagging | None | Tag set | Container | Yes |
| TagSet | Tagging | Tag set | Container | Yes |
| Tag | Tagging.TagSet | Tag set, which can contain up to 10 tags | Containers | Yes |
| Key | Tagging.TagSet.Tag | Tag key, which can contain up to 128 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes | String | Yes |
| Value | Tagging.TagSet.Tag | Tag value, which can contain up to 256 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes | String | Yes |

## Response

#### Response Header

#### Common Response Headers

This response uses a common response header. For more information about common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers

This request operation has no special response headers.

#### Response Body

The response body of this request is empty.

#### Error Codes

Some frequent special errors that may occur with this request are listed below:

| Error Code | Description | HTTP Status Code |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| SignatureDoesNotMatch | If the provided signature does not conform to the rule, this error code will be returned | 403 [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) |
| NoSuchBucket | If the bucket to which you want to add the rule does not exist, this error code will be returned | 404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) |
| MalformedXML          | Invalid XML format. Please check against the Restful API documentation                | 400 [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) |
| BadRequest            | The maximum number of tags allowed for one bucket is exceeded. Currently, up to 10 tags can be set | 400 [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) |
| InvalidTag | Tag key or value contains the reserved string "cos:" or "Project" | 400 [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) |

## Samples

#### Request

The following request writes two tags "{age:18}" and "{name:xiaoming}" to the bucket `examplebucket-1250000000`. The COS tag configuration succeeds and 204 success will be returned.

```shell
PUT /?tagging HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDrbAYjEBqqdEconpFi8NPFsOjrnX4LYUE&q-sign-time=1516361923;1517361973&q-key-time=1516361923;1517361973&q-url-param-list=tagging&q-header-list=content-md5;host&q-signature=71251feb4501494edcfbd01747fa873003759404
Content-Md5: LIbd5t5HLPhuNWYkP6qHcQ==
Content-Length: 127
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
Date: Fri, 19 Jan 2018 11:40:22 GMT
Server: tencent-cos
x-cos-request-id: NWE2MWQ5MjZfMTBhYzM1MGFfMTA5ODVfMTVjNDM=
```
