## Description

COS supports setting tags for existing buckets. This API is used to set key-value pairs for a bucket as tags, helping you manage existing bucket resources and costs.

>  Currently, up to 30 different tags can be set for one bucket.

## Request

#### Sample Request

```http
PUT /?tagging HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request Headers

#### Common Headers

This API only uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

This request operation does not use any special request header.

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

The data are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------ | ------------------------------------------------------------ | ---------- | ---- |
| Tagging | None | Tag set | Container | Yes |
| TagSet | Tagging | Tag set | Container | Yes |
| Tag | Tagging.TagSet | Tag set, which can contain up to 50 tags | Containers | Yes |
| Key | Tagging.TagSet.Tag | Tag key, which can contain up to 128 characters. A tag key can contain English letters, digits, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String | Yes |
| Value | Tagging.TagSet.Tag | Tag value, which can contain up to 256 characters. A tag value can contain English letters, digits, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String | Yes |

## Response

#### Response Headers

#### Common Response Headers

This response uses common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers

This request operation does not use any special response header.

#### Response Body

The response body of this request is empty.

#### Error Codes

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Example

#### Request

The following request writes two tags "{age:18}" and "{name:xiaoming}" to the bucket `examplebucket-1250000000`. COS successfully configured the tags and returns 204 (success).

```shell
PUT /?tagging HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDrbAYjEBqqdEconpFi8NPFsOjrnX4****&q-sign-time=1516361923;1517361973&q-key-time=1516361923;1517361973&q-url-param-list=tagging&q-header-list=content-md5;host&q-signature=71251feb4501494edcfbd01747fa87300375****
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
x-cos-request-id: NWE2MWQ5MjZfMTBhYzM1MGFfMTA5ODVfMTVj****
```
