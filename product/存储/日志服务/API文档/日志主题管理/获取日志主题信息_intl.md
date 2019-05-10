## Description

This API is used to get the information on a log topic.

### Request example

```
GET /topic?topic_id=xxxx-xx-xx-xx-yyyyyyyy HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
```

### Request line

```
GET /topic
```

### Request header

No special request header is used except for the common header.

### Request parameters

| Field Name | Type | Location | Required | Description |
| -------- | ------ | ----- | ---- | --------------- |
| topic_id | string | query | Yes | ID of the topic to be queried |

## Response

### Response example

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "logset_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "topic_id": "xxxx-xx-xx-xx-yyyyyyyy",
  "topic_name": "testname",
  "log_path": "/abc/log/test.log",
  "wild_path":"/data/nginx/log/**/access.log",
  "collection": true,
  "index": true,
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
  },
  "create_time": "2017-08-08 12:12:12"
}
```

### Response header

No special response header is used except for the common response header.

### Response parameters

| Field Name | Type | Required | Description |
| ------------- | ---------- | ---- | ------------------------------------------------------------ |
| logset_id | string | Yes | Logset ID |
| topic_id | string | Yes | Log topic ID |
| topic_name | string | Yes | Log topic name |
| path | string | Yes | Log file path of the old version |
| wild_path | string | Yes | The new log file path with wildcards, which separates the file directory and file name with /\*\*/. New and old paths cannot exist at the same time. |
| collection | bool | Yes | Indicates whether to enable collection |
| index | bool | Yes | Indicates whether to enable index |
| log_type | string | Yes | Type of logs to be collected. `json_log`: Logs in JSON format; `delimiter_log`: Logs in separator-based format; `minimalist_log`: Minimalist logs; `regex_log` and `multiline_log`: Multiline logs; `fullregex_log`: Full regular expressions. |
| extract_rule | JsonObject | Yes | Extraction rule |
| machine_group | JsonObject | No | Information of the server group on which logs are collected |
| create_time | string | No | Creation time |

extract_rule is composed as follows:

| Field Name | Type | Required | Description |
| --------------- | ----------------- | -------- | ----------------------------------------------------------- |
| time_key | string | No | Key of the time field |
| time_format | string | No | Format of the time field. For the description of time format, see `strftime` function in C programming language. |
| delimiter | string | No | The separator for separator-based logs |
| log_regex | string | No | The rule of matching the entire log for multiline logs |
| beginning_regex | string | No | The rule of matching the beginning of line for multiline logs |
| keys | JsonArray(string) | No | Key of each extracted field |
| filter_keys | JsonArray(string) | No | The keys used to filter logs |
| filter_regex | JsonArray(string) | No | Values corresponding to the keys specified in filter_keys. The number of values is equal to that of filter_keys. A value corresponds to a key. |

## Error Codes

For more information, see [Error Codes](https://cloud.tencent.com/document/product/614/12402).

