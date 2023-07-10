## Feature Description

This API is used to create a consumer group.

## Request

#### Sample request

```shell
POST /consumergroup?topic_id=xxxx-xx-xx-xx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Content-Type: application/json
Authorization: <AuthorizationString>

{"consumer_group": "cls_demo_consumer_group", "timeout": 3600, "order": false}
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| -------------- | ------ | ----- | -------- | ------------------------------------------------------------ |
| topic_id       | string            | query | Yes       | ID of the log topic under which to create consumer group            |
| consumer_group    | string | body  | Yes | Consumer group name which can contain 1–255 characters (allowed characters: a–z, A–Z, 0–9, _, -) |
| timeout        | int    | body  | Yes       | Consumer group timeout period in seconds. If no heartbeat is received in `timeout` seconds, the system will delete the consumer group |
| order          | bool   | body  | Yes       | This configuration item will affect the consumption behavior when topic partitions are split/merged: <br><li>true: consume in sequence <br><li>false: consume out of sequence |



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
