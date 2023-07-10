## Feature Description

This API is used to get the log topic information list.

## Request

#### Sample request

```shell
GET /topics?logset_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request line

```shell
GET /topics
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| --------- | ------ | ----- | -------- | ---------------- |
| logset_id | string | query | Yes       | ID of the logset to be queried |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
    "topics": [{
        "logset_id": "xxxx-xx-xx-xx-xxxxxxxx",
        "topic_id": "xxxx-xx-xx-xx-yyyyyyyy",
        "topic_name": "testname",
        "partition_count": "1",
        "path": "/abc/log/test.log",
        "wild_path": "/data/nginx/log/**/access.log",
        "collection": true,
        "index": true,
        "log_type": "delimiter_log",
        "extract_rule": {
            "time_key": "date",
            "time_format": "%Y-%m-%d %H:%M:%S",
            "delimiter": "|",
            "log_regex": ".*",
            "beginning_regex": "^",
            "keys": ["date", "", "content"],
            "filter_keys": [],
            "filter_regex": []
        },
        "assumer_uin": 1000088888,
        "assumer_name": "xxxxxx",
        "topic_modify_acl": 31,
        "topic_show_acl": 31,
        "create_time": "2017-08-08 12:12:12"
    }]
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
| ------ | --------- | -------- | ---------------- |
| topics | JsonArray | Yes       | Log topic information array |

`TopicInfo` is in the following format:

| Field Name | Type | Required | Description |
| ---------------- | ---------- | -------- | ------------------------------------------------------------ |
| logset_id        | string     | Yes       | Logset ID                                                  |
| topic_id         | string     | Yes       | Log topic ID                                                |
| topic_name       | string     | Yes       | Log topic name                                               |
| partition_count  | int        | Yes       | Number of topic partitions                                    |
| path             | string     | Yes       | Path of legacy log file                                             |
| wild_path        | string     | No       | Path of log to be collected by new wildcard log topic. File directory and filename as separated by `/**/`. Either this parameter or the legacy `path` parameter can exist |
| collection       | bool       | Yes       | Whether to enable collection                                                 |
| index            | bool       | Yes       | Whether to enable index                                                 |
| log_type         | string     | Yes       | Type of log to be collected. `json_log`: log in JSON format, `delimiter_log`: log in delimited format, `minimalist_log`: minimalist log, `egex_log` or `multiline_log`: log in multi-line format, `fullregex_log`: log in full regex format |
| extract_rule     | JsonObject | Yes       | Extraction rule                                                     |
| machine_group    | JsonObject | Yes       | Collection server group information                                               |
| assumer_uin      | uint64     | No       | `uin` of the service that creates the topic (this field is present only when a general account views the topics created by a service account) |
| assumer_name     | string     | No       | Name of the service that creates the topic (this field is present only when a general account views the topics created by a service account) |
| topic_modify_acl | int        | No       | General user's permission to modify topics, i.e., `modify_acl` (0B00000: modification prohibited, 0B00001: modification allowed for basic information, 0B00010: modification allowed for collection information, 0B00100: modification allowed for index information, 0B01000: modification allowed for shipping information, 0B10000: modification allowed for consumption information) (this field is present only when a general account views the topics created by a service account) |
| topic_show_acl   | int        | No       | General user's permission to show topics, i.e., `show_acl` (0B00000: show nothing, 0B00001: show basic information, 0B00010: show collection information, 0B00100: show index information, 0B01000: show shipping information, 0B10000: show consumption information) |
| create_time       | string | No   | Creation time                                                     |

`extract_rule` is in the following format:

| Field Name | Type | Required | Description |
| --------------- | ----------------- | -------- | ------------------------------------------------------------ |
| time_key        | string            | No       | Time field key name                                           |
| time_format     | string            | No       | Time field format. For more information, please see the time format description of the `strftime` function in C language |
| delimiter       | string            | No       | Delimiter for delimited log |
| log_regex       | string            | No       | Full log matching rule for multi-line logs                              |
| beginning_regex | string            | No       | Line beginning matching rule for multi-line logs                                   |
| keys            | JsonArray(string) | No       | Key name of each extracted field                                    |
| filter_keys     | JsonArray(string) | No       | Log keys to be filtered                                           |
| filter_regex    | JsonArray(string) | No       | Values corresponding to the above `filter_keys` field. The number of values is the same as that of keys in `filter_keys`. The values are in one-to-one correspondence to the keys |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
