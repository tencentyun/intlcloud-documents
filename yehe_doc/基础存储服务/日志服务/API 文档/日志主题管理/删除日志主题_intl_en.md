## Feature Description

This API is used to delete a log topic.

## Request

#### Sample request

```shell
DELETE /topic?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request line

```shell
DELETE /topic
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
|--------------|--------|------|---------|--------------------------------|
| topic_id     | string | query| Yes     | ID of the log topic to be deleted                                     |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Length: 0
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

None.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
