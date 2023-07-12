## Feature Description

This API is used to modify a consumer group.

## Request

#### Sample request

```shell
PUT /consumergroup?topic_id=xxxx-xx-xx-xx-xxxxxxxx&consumer_group=xxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Content-Type: application/json
Authorization: <AuthorizationString>

{"timeout": 3600, "order": true}
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| -------------- | ------ | ----- | -------- | ------------------------------------------------------------ |
| topic_id       | string            | query | Yes       | Log topic ID of consumer group            |
| consumer_group | string | query | Yes | Consumer group name |
| timeout        | int    | body  | No       | Consumer group timeout period. If no heartbeat is received in `timeout` seconds, the system will delete the consumer group |
| order          | bool   | body  | No       | Whether to consume sequentially                                               |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

None.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
