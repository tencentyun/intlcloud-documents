## Feature Description

This API is used to download logs by using a cursor.

## Request

#### Sample request

```json
GET /log?topic_id=xxxxxxxx-xxxx-xxxx-xxxx&cursor=xxxxxx&count=10 HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request line

```json
GET /log
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id     | string | query| Yes     | Log topic ID                                     |
| cursor       | string | query| Yes     | Cursor obtained through the log cursor getting API                 |
| count        | string | query| Yes     | Number of logs to be downloaded. Maximum value: 1000                      |

## Response

#### Sample response

```http
HTTP/1.1 200 OK
Content-Type: application/x-protobuf
Content-Length: 23
x-cls-cursor: xxxxxx
x-cls-count:10

<Packaged content of `LogGroupList` in pb format>
```

#### Response header

| Header Name | Description |
|------------------------|--------------------------------|
| x-cls-cursor           | Current log cursor for use by next download  |
| x-cls-count            | Number of logs downloaded in the current request           |

#### Response parameters

The packaged content of the `LogGroupList` object is returned. For the pb file description, please see [Uploading Structured Logs](https://intl.cloud.tencent.com/document/product/614/16873).

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
