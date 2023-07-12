## Feature Description

This API is used to get the log cursor under a specified log topic and download.

## Request

#### Sample request

```shell
GET /cursor?topic_id=xxxxxxxx-xxxx-xxxx-xxxx&start=2017-12-28%2014%3A13%3A00 HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request line

```shell
GET /cursor
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| -------- | ------ | ----- | ---- | ---------------------------------------------------- |
| topic_id | string | query | Yes   | Log topic ID                                        |
| start    | string | query | Yes   | Log start time accurate to the minute in the format of `YYYY-mm-dd HH:MM:SS` |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 23

{
    "cursor": "1212ssssxxxxxx"
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
| ------ | ------ | ---- | ---- |
| cursor | string | Yes   | Cursor |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).