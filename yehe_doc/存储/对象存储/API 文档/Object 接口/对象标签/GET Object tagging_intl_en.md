## Feature

This API (GET Object tagging) is used to query existing tags set on an object.

If you call the `GET Object tagging` API using a sub-account, please make sure that you have obtained the permission to use this API from the root account.

#### Request

#### Request sample

```http
GET /<ObjectKey>tagging&VersionId=VersionId HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> - If versioning is enabled for your bucket, to query tags on the specific version of an object, you can include `VersionId` in your request.

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request has no request body.

## Response

#### Response headers

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The following describes the nodes of response body returned by this request:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------ | ------------------------------------------------------------ | ---------- | -------- |
| Tagging | None | Tag set | Container | Yes |
| TagSet | Tagging | Tag set | Container | Yes |
| Tag | Tagging.TagSet | Tag set, which can contain up to 10 tags | Containers | Yes |
| Key | Tagging.TagSet.Tag | Tag key, which can contain up to 128 characters. A tag key can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String | Yes |
| Value | Tagging.TagSet.Tag | Tag value, which can contain up to 256 characters. A tag value can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String | Yes |

#### Error codes

The following describes some frequent special errors that may occur when you make this request:

| Error Code | Description | HTTP Status Code |
| --------------------- | -------------------------------------------------------- | ------------- |
| SignatureDoesNotMatch | Returned if you provide an invalid signature     | 403 Forbidden |
| NoSuchObject          | Returned when the object does not exist, and thus you cannot read its tags           | 404 Not Found   |
| NoSuchTagSetError     | No object tag is set on the requested object.           | 404 Not Found |

## Use Cases

#### Request

The following request is made to query the tags on the bucket `examplebucket-1250000000`. COS parses the request and returns `{age:18}` and `{name:xiaoming}`, the two existing tags on the bucket.

```shell
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

```shell
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
