## Feature Description

This API is used to get the topic partition information list.

## Request

#### Sample request

```shell
GET /partitions?topic_id=xxxx-xx-xx-xx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Parameter Name | Type | Location | Required | Description |
| -------- | ------ | ----- | -------- | ----------- |
| topic_id       | string            | query | Yes       | Log topic ID            |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 21

{
    "partitions":[
        {
            "partition_id": 1,
            "status": "readwrite",
            "inclusive_begin_key": "000000000000000000000000000000000000",
            "exclusive_end_key": "a00000000000000000000000000000000000",
            "create_time": "2019-01-14 19:19:41"
        },
        {
           "partition_id": 2,
            "status": "readwrite",
            "inclusive_begin_key": "a00000000000000000000000000000000000",
            "exclusive_end_key": "ffffffffffffffffffffffffffffffffffff",
            "create_time": "2019-01-14 19:19:41"
        }
    ]
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
| ------------------- | ------ | -------- | --------------------------------------------------- |
| partition_id        | int    | Yes       | Topic partition number                                        |
| status              | string | Yes       | Topic partition status: <br><li>readwrite: read/write <br><li>readonly: read-only |
| inclusive_begin_key | string | Yes       | Starting position of topic partition range                             |
| exclusive_end_key   | string | Yes       | Ending position of topic partition range                              |
| create_time         | string | Yes       | Topic partition creation time                                  |



## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
