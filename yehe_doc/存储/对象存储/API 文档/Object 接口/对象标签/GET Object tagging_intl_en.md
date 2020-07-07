## Feature

This API is used to query existing tags set on an object.

To call this API using a sub-account, please make sure that you have obtained permissions for this API from the root account.

#### Versioning

If versioning is enabled for your bucket, you can include `VersionId` in your request to query tags on the specific version of an object.

## Request

#### Sample request 

```plaintext
GET /<ObjectKey>tagging&VersionId=VersionId HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)

#### Request parameters

| Name | Description | Type | Required |
| :-------- | :----------------------------------------------------------- | :----- | :------- |
| versionId | Specifies the version ID of the object if versioning is enabled; if this parameter is not specified, tags on the latest version will be queried | string | No |

#### Request headers

This API uses only common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API returns only common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The nodes of response body are explained as below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------ | ------------------------------------------------------------ | ---------- | -------- |
| Tagging | None | Tag set | Container | Yes |
| TagSet | Tagging | Tag set | Container | Yes |
| Tag | Tagging.TagSet | Tag set, which can contain up to 10 tags | Containers | Yes |
| Key | Tagging.TagSet.Tag | Tag key, which can contain up to 128 characters. A tag key can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String | Yes |
| Value | Tagging.TagSet.Tag | Tag value, which can contain up to 256 characters. A tag value can contain English letters, numbers, spaces, plus signs, minus signs, underscores, equals signs, dots, colons, and slashes | String | Yes |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

The following example requests to query the tags on the bucket `examplebucket-1250000000`. COS parses the request and returns `{age:18}` and `{name:xiaoming}`, the two existing tags on the bucket.

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
