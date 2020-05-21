## Feature Description

This API is used to update a consumer group cursor.

## Request

#### Sample request

```shell
PUT /consumergroupcursor?topic_id=xxxx-xx-xx-xx-xxxx&consumer_group=cls_demo_consumer_group&partition_id=1 HTTP/1.1
Host: <Region>.cls.tencentyun.com
Content-Type: application/json
Authorization: <AuthorizationString>

{"consumer_id": "cls_demo_consumer_1", "cursor": "FAjUjMtmELBo"}
```

#### Request line

```shell
PUT  /consumergroupcursor
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| -------------- | ------ | ----- | -------- | ----------------------- |
| topic_id       | string            | query | Yes       | Log topic ID of consumer group            |
| consumer_group | string | query | Yes | Consumer group name |
| partition_id   | int    | query | Yes       | Topic partition number                                        |
| consumer_id    | string | body  | No       | Consumer group name              |
| cursor         | string | body  | Yes       | Cursor value                  |



## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

None.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
