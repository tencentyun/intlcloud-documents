## Feature Description

This API is used to get the consumer group list of a log topic.

## Request

#### Sample request

```shell
GET /consumergroups?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| -------- | ------ | ----- | -------- | ----------------- |
| topic_id       | string            | query | Yes       | ID of the log topic to be queried            |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
    "consumer_groups":[
        {
            "consumer_group":"cls-demo_consumer_group",
            "order":true,
            "timeout":3600
        }
    ]
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| consumer_group | string | Yes | Consumer group name |
| timeout        | int    | Yes       | Consumer group timeout period. If no heartbeat is received in `timeout` seconds, the system will delete the consumer group |
| order          | bool   | Yes       | Whether to consume sequentially                                               |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
