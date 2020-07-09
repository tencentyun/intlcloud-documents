## Description

This API is used to query existing tags on a COS bucket.

> ?To call this API using a sub-account, please make sure that you have obtained the permission to use this API from the root account.

## Request

#### Sample request

```http
GET /?tagging HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response Headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body
A successful query will return **application/xml** data which includes existing tags on the bucket.
```shell
<Tagging>
    <TagSet>
        <Tag>
            <Key>string</Key>
            <Value>string</Value>
        </Tag>
        <Tag>
            <Key>string</Key>
            <Value>string</Value>
        </Tag>
    </TagSet>
</Tagging>
```

The nodes are detailed as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------ | ------------------------------------------------------------ | ---------- |
| Tagging | None | Tag set | Container |
| TagSet | Tagging | Tag set | Container |
| Tag | Tagging.TagSet | Tag set, which can contain up to 50 tags | Container |
| Key | Tagging.TagSet.Tag | Tag key, which is up to 128 characters, containing English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String |
| Value | Tagging.TagSet.Tag | Tag value, which is to 256 characters, containing English letters, digits, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

The following request queries the tags from the bucket `examplebucket-1250000000`. COS parses the request and returns two existing bucket tags, {age:18} and {name:xiaoming}.

```shell
GET /?tagging HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDrbAYjEBqqdEconpFi8NPFsOjrnX4****&q-sign-time=1516361923;1517361973&q-key-time=1516361923;1517361973&q-url-param-list=tagging&q-header-list=content-md5;host&q-signature=71251feb4501494edcfbd01747fa87300375****
Content-Length: 127
Content-Type: application/xml
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Connection: close
Date: Fri, 19 Jan 2018 11:40:22 GMT
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
