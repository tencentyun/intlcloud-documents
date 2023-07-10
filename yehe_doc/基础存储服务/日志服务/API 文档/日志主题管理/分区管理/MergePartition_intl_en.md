## Feature Description

This API is used to merge a topic partition in read/write state. When merging, specify a topic partition ID, and CLS will automatically merge the partition adjacent to the right of the range.

## Request

#### Sample request

```shell
POST /partitions?topic_id=xxxx-xx-xx-xx-xxxx&partition_id=2&action=merge HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ------ | ----- | -------- | ------------------------------------------------------------ |
| topic_id       | string            | query | Yes       | Log topic ID of partition            |
| partition_id | int    | query | Yes       | Number of the topic partition to be merged. CLS will automatically merge the partition adjacent to the right of the range. <br>For example, if 2 and 3 are two adjacent `readwrite` partitions, and `partition_id` is 2, then partitions 2 and 3 will be merged, and their type will become `readonly`. The merged partition type will be `readwrite`, and its `partition_id` will be 4 |
| action       | string | query | Yes       | Operation type. `action` needs to be set to `merge` |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 21

{
    "partitions":[
        {
           "partition_id": 2,
            "status": "readonly",
            "inclusive_begin_key": "000000000000000000000000000000000000",
            "exclusive_end_key": "7fffffffffffffffffffffffffffffffffff",
            "create_time": "2019-01-14 19:25:41"
        },
        {
            "partition_id": 3,
            "status": "readonly",
            "inclusive_begin_key": "7fffffffffffffffffffffffffffffffffff",
            "exclusive_end_key": "ffffffffffffffffffffffffffffffffffff",
            "create_time": "2019-01-14 19:25:41"
        },
        {
            "partition_id": 4,
            "status": "readwrite",
            "inclusive_begin_key": "000000000000000000000000000000000000",
            "exclusive_end_key": "ffffffffffffffffffffffffffffffffffff",
            "create_time": "2019-01-14 19:33:41"
        }
    ]
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Description |
| ------------------- | ------ | --------------------------------------------------- |
| partition_id        | int    | Topic partition number                                        |
| status              | string | Topic partition status: <br><li>readwrite: read/write <br><li>readonly: read-only |
| inclusive_begin_key | string | Starting position of topic partition range                             |
| exclusive_end_key   | string | Ending position of topic partition range                              |
| create_time         | string | Topic partition creation time                                  |



## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
