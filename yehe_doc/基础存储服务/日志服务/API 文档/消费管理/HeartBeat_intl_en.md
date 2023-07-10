## Feature Description

This API is used to upload consumer heartbeats.

## Request

#### Sample request

```shell
POST /consumerheartbeat?topic_id=xxxx-xx-xx-xx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Content-Type: application/json
Authorization: <AuthorizationString>

{"consumer_group": "cls_demo_consumer_group", "consumer_id": "consumer_id", "partition_id_list": []}
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| ----------------- | ------ | ----- | -------- | ----------------------- |
| topic_id       | string            | query | Yes       | Log topic ID of consumer group            |
| consumer_group    | string | body  | Yes | Consumer group name |
| consumer_id       | string | body  | Yes       | Consumer name              |
| partition_id_list | array  | body  | Yes       | List of partitions consumed by consumer    |



## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
    "partition_id_list":[
        4,
        5
    ]
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
| ----------------- | ----- | -------- | ------------------------ |
| partition_id_list | array | Yes       | List of partitions consumable by consumer    |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
