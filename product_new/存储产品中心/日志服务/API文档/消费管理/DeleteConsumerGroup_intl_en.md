## Feature Description

This API is used to delete a consumer group.

## Request

#### Sample request

```shell
DELETE /consumergroup?topic_id=xxxx-xx-xx-xx-xxxx&consumer_group=cls_demo_consumer_group HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| -------------- | ------ | ----- | -------- | ------------------------- |
| topic_id       | string            | query | Yes       | Log topic ID of consumer group            |
| consumer_group | string | query | Yes | Consumer group name |

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
