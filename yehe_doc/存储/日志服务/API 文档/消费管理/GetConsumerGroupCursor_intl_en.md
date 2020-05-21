## Feature Description

This API is used to get a consumer group cursor.

## Request

#### Sample request

```shell
GET /consumergroupcursor?topic_id=xxxx-xx-xx-xx-xxxx&consumer_group=cls_demo_consumer_group&partition_id=1 HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| -------------- | ------ | ----- | -------- | -------------------------------------------------------- |
| topic_id       | string            | query | Yes       | Log topic ID of consumer group            |
| consumer_group | string | query | Yes | Consumer group name |
| partition_id   | int    | query | No       | Topic partition number (if this parameter is not specified, cursors of all partitions under the topic will be returned)                                        |

## Response

#### Sample response

Response packet if `partition_id` is not specified:

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
    "cursors":[
        {
            "consumer_id":"cls-demo_consumer_id",
            "cursor":"FAjUjMtmELBovQRogYkBuq",
            "partition_id":1,
            "update_time":1573645058
        },
        {
            "consumer_id":"cls-demo_consumer_id",
            "cursor":"FAjUjMtmELBovQRogYkBuqg",
            "partition_id":2,
            "update_time":1573645058
        }
    ]
}
```

Response packet if `partition_id` is specified:

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
    "consumer_id":"cls-demo_consumer_id",
    "cursor":"FAjUjMtmELBovQRog",
    "partition_id":1,
    "update_time":1573645058
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
| ------------ | --------- | -------- | ----------------------- |
| partition_id | string    | Yes       | Topic partition number                                        |
| cursor       | string    | Yes       | Cursor value                  |
| update_time  | long long | Yes       | Cursor update time          |
| consumer_id  | string    | Yes       | Consumer ID assigned to this partition |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
