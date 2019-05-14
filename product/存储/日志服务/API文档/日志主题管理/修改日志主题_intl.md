## Description

This API is used to modify a log topic.

## Request

### Request example

```
PUT /topic HTTP/1.1
Host: <Region>.cls.myqcloud.com
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

### Request line

```
PUT /topic
```

### Request header

No special request header is used except for the common header.

### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ---------- | ---- | ---- | ------------------------------------------------------------ |
| topic_id | string | body | Yes | Log topic ID |
| topic_name | string | body | No | Log topic name |
| path | string | body | No | Path of the log that needs to be collected for the log topic of the old version. |
| wild_path | string | body | No | The new log collection path with wildcards, which separates the file directory and file name with /\*\*/. New and old paths cannot exist at the same time. |
| collection | bool | body | No | Indicates whether to enable collection |
| log_type | string | body | No | Type of logs to be collected. `json_log`: Logs in JSON format; `delimiter_log`: Logs in separator-based format; `minimalist_log`: Minimalist logs; `multiline_log`: Multiline logs; `fullregex_log`: Full regular expressions. |
| extract_rule | JsonObject | body | No | Extraction rule |

>At least one of the following should be provided: topic_name, path, group_id, collection, and (log_type+extract_rule).



extract_rule is composed as follows:

| Field Name | Type | Required | Description |
| --------------- | ----------------- | -------- | ------------------------------------------------------------ |
| time_key | string | No | Key of the time field. time_key and time_format must come in pairs. |
| time_format | string | No | Format of the time field. For the description of time format, see `strftime` function in C programming language. |
| delimiter | string | No | The separator for separator-based logs. This is valid only when `log_type` is `delimiter_log`. |
| log_regex | string | No | The rule of matching the entire log. This is valid only when `log_type` is `fullregex_log`. |
| beginning_regex | string | No | The rule of matching the beginning of line. This is valid only when `log_type` is `multiline_log` or `regex_log`. |
| keys | JsonArray(string) | No | Key of each extracted field. Empty key means discarding the field. This is valid only when `log_type` is `delimiter_log`. JSON key is used for `json_log`. |
| filter_keys | JsonArray(string) | No | The keys used to filter logs. The number of keys is limited to 5. |
| filter_regex | JsonArray(string) | No | Values corresponding to the keys specified in filter_keys. The number of values is equal to that of filter_keys. A value corresponds to a key. Logs that match the rule are collected. |

## Response

### Response example

```
HTTP/1.1 200 OK
Content-Length: 0
```

### Response header

No special response header is used except for the common response header.

### Response parameters

None

## Error Codes

For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

