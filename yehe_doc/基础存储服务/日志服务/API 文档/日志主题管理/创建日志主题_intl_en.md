## Feature Description

This API is used to create a log topic and return its ID.

## Request

#### Sample request

```shell
POST /topic HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "logset_id": "xxxxxx-xx-xx-xx-xxxxxxxx",
  "topic_name": "testname",
  "partition_count": "1",
  "path": "/data/nginx/log/access.log",
  "wild_path":"/data/nginx/log/**/access.log",
  "log_type": "delimiter_log",
  "extract_rule": {
      "time_key": "date",
      "time_format": "%Y-%m-%d %H:%M:%S",
      "delimiter": "|",
      "log_regex": ".*",
      "beginning_regex": "^",
      "keys": ["date","","content"],
      "filter_keys": [],
      "filter_regex": []
  }
}
```

#### Request line

```shell
POST /topic
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ---------- | ---- | ---- | ------------------------------------------------------------ |
| logset_id    | string     | body | Yes   | Logset ID of log topic                                    |
| topic_name   | string     | body | Yes       | Log topic name                                               |
|     partition_count               |    int           |   body      |  No      |      Number of topic partitions. If this parameter is not passed in, one partition will be created by default. Maximum value: 10. Split/merge operations will change the number of partitions. Up to 50 partitions in total are allowed                                                                  |
| path         | string     | body | No       | Path of log to be collected by legacy log topic. If collection is not performed, there is no need to set this parameter                              |
| wild_path    | string     | body | No       | Path of log to be collected by new wildcard log topic. File directory and filename as separated by `/\*\*/`. Either this parameter or the legacy `path` parameter can exist |
| log_type     | string     | body | No   | Type of log to be collected. `json_log`: log in JSON format, `delimiter_log`: log in delimited format, `minimalist_log`: log in single-line format, `multiline_log`: log in multi-line format, `fullregex_log`: log in full regex format. Default value: `minimalist_log` |
| extract_rule | JsonObject | body | No       | Extraction rule. If `extract_rule` is set, `log_type` must be set                                                      |

`extract_rule` is in the following format:

| Field Name | Type | Required | Description |
| --------------- | ----------------- | -------- | ------------------------------------------------------------ |
| time_key        | string            | No       | Time field key name. `time_key` and `time_format` must appear in pairs |
| time_format     | string            | No       | Time field format. For more information, please see the time format description of the `strftime` function in C language |
| delimiter       | string            | No       | Delimiter for delimited log, which is valid only if `log_type` is `delimiter_log` |
| log_regex       | string            | No       | Full log matching rule, which is valid only if `log_type` is `fullregex_log`      |
| beginning_regex | string            | No       | Line beginning matching rule, which is valid only if `log_type` is `multiline_log` |
| keys            | JsonArray(string) | No       | Key name of each extracted field. An empty key indicates to discard the field. This parameter is valid only if `log_type` is `delimiter_log`. `json_log` logs use the key of JSON itself |
| filter_keys     | JsonArray(string) | No       | Log keys to be filtered (up to 5)                                  |
| filter_regex    | JsonArray(string) | No       | Values corresponding to the above `filter_keys` field. The number of values is the same as that of keys in `filter_keys`. The values are in one-to-one correspondence to the collected logs |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{"topic_id": "xxxx-xx-xx-xx-xxxxxxxx"}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
| -------- | ------ | ---- | ------------- |
| topic_id         | string     | Yes       | Log topic ID                                                |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
