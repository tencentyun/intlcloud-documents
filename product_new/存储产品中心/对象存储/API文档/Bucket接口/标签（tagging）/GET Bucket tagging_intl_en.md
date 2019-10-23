## Description

COS supports setting tags for existing buckets. This API (GET Bucket tagging) is used to get existing tags of the specified bucket.

> ? If you call the `GET Bucket tagging ` API using a sub-account, please make sure that you have obtained the permission to use this API from the root account.

## Request

### Sample Request

```http
GET /?tagging HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Headers

#### Common Headers

The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

This request operation has no special request headers.

### Request Body

The request body of this request is empty.

## Response

### Response Headers

#### Common Response Headers

This response uses a common response header. For more information about common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers

This request operation has no special response headers.

### Response Body

The elements of the response body returned by this request are as detailed below:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------ | ------------------------------------------------------------ | ---------- |
| Tagging | None | Tag set | Container |
| TagSet | Tagging | Tag set | Container |
| Tag | Tagging.TagSet | Tag set, which can contain up to 10 tags | Containers |
| Key | Tagging.TagSet.Tag | Tag key, which can contain up to 128 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes | String |
| Value | Tagging.TagSet.Tag | Tag value, which can contain up to 256 bytes of letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes | String |

### Error Codes

Some frequent special errors that may occur with this request are listed below:

| Error Code | Description | HTTP Status Code |
| --------------------- | ---------------------------------------------------- | ------------------------------------------------------------ |
| SignatureDoesNotMatch | If the provided signature does not conform to the rule, this error code will be returned | 403 [Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3) |
| NoSuchBucket | If the bucket to which you want to add the rule does not exist, this error code will be returned | 404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) |
| NoSuchTagSetError     | No bucket tags have been set for the requested bucket | 404 [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) |

## Samples

### Request

The following request is made to get the tags of the bucket `examplebucket-1250000000`. After COS parses the request, two tags {age:18} and {name:xiaoming} in the bucket will be returned.

```shell
GET /?tagging HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-chengdu.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDrbAYjEBqqdEconpFi8NPFsOjrnX4LYUE&q-sign-time=1516361923;1517361973&q-key-time=1516361923;1517361973&q-url-param-list=tagging&q-header-list=content-md5;host&q-signature=71251feb4501494edcfbd01747fa873003759404
Content-Md5: LIbd5t5HLPhuNWYkP6qHcQ==
Content-Length: 127
Content-Type: application/xml
```

### Response

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
