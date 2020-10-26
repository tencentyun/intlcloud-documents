## Feature Description

This API is used to split a topic partition in read/write state.

## Request

#### Sample request

```shell
POST /partitions?topic_id=xxxx-xx-xx-xx-xxxx&partition_id=1&split_key=7fffffffffffffffffffffffffffffffffff&action=split HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ------ | ----- | -------- | -------------------------------------------------- |
| topic_id       | string            | query | Yes       | Log topic ID of partition            |
| partition_id | int    | query | No       | Number of the topic partition to be split                               |
| action       | string | query | Yes       | Operation type. `action` needs to be set to `split` |
| split_key    | string | query | No       |  Split position of the two topic partitions, which is a hexadecimal string of up to 32 bits (excluding the `0x` part). If you need to split partitions into three or more partitions, the average split will be used. In this case, this parameter does not take effect.  |
| number       | int    | query | No       | Number of splits. Default value: 2 |

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
            "status": "readonly",
            "inclusive_begin_key": "000000000000000000000000000000000000",
            "exclusive_end_key": "ffffffffffffffffffffffffffffffffffff",
            "create_time": "2019-01-14 19:19:41"
        },
        {
           "partition_id": 2,
            "status": "readwrite",
            "inclusive_begin_key": "000000000000000000000000000000000000",
            "exclusive_end_key": "7fffffffffffffffffffffffffffffffffff",
            "create_time": "2019-01-14 19:25:41"
        },
        {
            "partition_id": 3,
            "status": "readwrite",
            "inclusive_begin_key": "7fffffffffffffffffffffffffffffffffff",
            "exclusive_end_key": "ffffffffffffffffffffffffffffffffffff",
            "create_time": "2019-01-14 19:25:41"
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
