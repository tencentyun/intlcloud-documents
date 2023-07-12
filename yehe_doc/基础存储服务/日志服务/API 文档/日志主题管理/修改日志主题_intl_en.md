## Feature Description

This API is used to modify a log topic.

## Request

#### Sample request

```
PUT /topic HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "topic_id": "xxxxxx-xx-xx-xx-xxxxxxxx",
  "topic_name": "testname",
  "path": "/data/nginx/log/access.log",
  "wild_path":"/data/nginx/log/**/access.log",
  "collection": false,
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

```
PUT /topic
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ---------- | ---- | -------- | ------------------------------------------------------------ |
| topic_id     | string     | body | Yes       | Log topic ID                                                |
| topic_name   | string     | body | No       | Log topic name                                               |
| path         | string     | body | No       | Path of log to be collected by legacy log topic                               |
| wild_path    | string     | body | No       | Path of log to be collected by new wildcard log topic. File directory and filename as separated by `/**/`. Either this parameter or the legacy `path` parameter can exist |
| collection   | bool       | body | No       | Whether to enable collection                                                 |
| log_type     | string     | body | No       | Type of log to be collected: <br><li>`json_log`: log in JSON format<br><li>`delimiter_log`: log in delimited format<br><li>`minimalist_log`: log in single-line format<br><li>`multiline_log`: log in multi-line format<br><li>`fullregex_log`: log in full regex format |
| extract_rule | JsonObject | body | No       | Extraction rule                                                     |

>At least one parameter out of `topic_name`, `path`, `group_id`, `collection`, and (log_type+extract_rule) must be provided.



`extract_rule` is in the following format:

| Field Name | Type | Required | Description |
| --------------- | ----------------- | -------- | ------------------------------------------------------------ |
| time_key        | string            | No       | Time field key name. `time_key` and `time_format` must appear in pairs |
| time_format     | string            | No       | Time field format. For more information, please see the time format description of the `strftime` function in C language |
| delimiter       | string            | No       | Delimiter for delimited log, which is valid only if `log_type` is `delimiter_log` |
| log_regex       | string            | No       | Full log matching rule, which is valid only if `log_type` is `fullregex_log`      |
| beginning_regex | string            | No       | Line beginning matching rule, which is valid only if `log_type` is `fullregex_log` or `multiline_log` |
| keys            | JsonArray(string) | No       | Key name of each extracted field. An empty key indicates to discard the field. This parameter is valid only if `log_type` is `delimiter_log`. `json_log` logs use the key of JSON itself |
| filter_keys     | JsonArray(string) | No       | Log keys to be filtered (up to 5)                                  |
| filter_regex    | JsonArray(string) | No       | Values corresponding to the above `filter_keys` field. The number of values is the same as that of keys in `filter_keys`. The values are in one-to-one correspondence to the collected logs |

## Response

#### Sample response

```
HTTP/1.1 200 OK
Content-Length: 0
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

None.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
