## Overview

This example shows you how to get the collection configuration of the Agent.

## Request
#### Request line

```
GET /agent/config
```

#### Sample request 

```
GET /agent/config HTTP/1.1Host: <Region>.cls.myqcloud.comAuthorization: <AuthorizationString>
```

#### Request headers

| Header | Description |
| ------------------- | ------------- |
| x-cls-agent-version | Agent version |
| x-cls-agent-ip      | Agent IP address |

#### Request parameters

N/A

## Response
#### Sample response

```
HTTP / 1.1 200 OKContent - Type: application / jsonContent - Length: 123 {
			"logconf": [{
				"topicid": "xxxx-xx-xx-xx-yyyyyyyy",
				"path": "/abc/log/test.log",
				"wildpath": "/abc/log/test.log",
				"multi_wildpath": ["abc/test.log", "acb/test.log"],
				"log_type": "delimiter_log",
				"extract_rule": {
					"time_key": "data",
					"time_format": "%t",
					"delimiter": "|",
					"keys": ["data", "", "content"],
					"filter_keys": [],
					"filter_regex": [],
				}
			}, {
				"topicid": "xxxx-xx-xx-xx-yyyyzzzz",
				"path": "/abc/log/test1.log",
				"wildpath": "/abc/log/test.log",
				"multi_wildpath": ["abc/test.log", "acb/test.log"],
				"log_type": "regex_log",
				"extract_rule": {
					"log_regex": "(.*)",
					"beginning_regex": "^abc",
					"keys": ["content"],
					"filter_keys": [],
					"filter_regex": [],
				}
			}],
			"needupdate": true,
			"last_version": "1.0.1",
			"url": "http://test-11101.cossh.myqcloud.com/xxx.so",
			"file_md5": "aee24235afdscrt4safewf"
}
```


#### Response headers

No special response headers

#### Response parameters

| Parameter | Type | Required | Description |
| ------------ | ------------------ | -------- | --------------------------------- |
| logconf      | JsonArray(ColInfo) | Yes       | Collected log information                   |
| needupdate   | bool               | Yes       | Whether the Agent needs update                |
| last_version | string             | No       | Agent latest version, which will be returned if update is needed |
| url | string             | No       | Agent download URL, which will be returned if update is needed |
| file_md5     | string             | No       | Agent’s MD5 value, which will be returned if update is needed      |

Parameters in `ColInfo`:

| Parameter | Type | Required | Description |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| topic_id | string | Yes | Log topic ID |
| path           | string | No       | Legacy-version collection path. Only one parameter among `multi_wildpath`, `wildpath`, and `path` will be returned.|
| wildpath       | string | No       | New-version collection path. Only one parameter among `multi_wildpath`, `wildpath`, and `path` will be returned. |
| multi_wildpath       | string | No       | New-version collection path. Only one parameter among `multi_wildpath`, `wildpath`, and `path` will be returned. |
| log_type       | string | Yes       | Log type                                                    |
| extract_rule | object | Yes | Extraction rule                 |

Parameters in `extract_rule`:

| Parameter | Type | Required | Description |
| --------------- | ------------- | -------- | ---------------------------------------------------- |
| time_key | string | No | Key name of the log time |
| time_format     | string        | No       | Time format                                         |
| delimiter       | string        | No       | Separator, which will be returned for logs of the `delimiter_log` type |
| log_regex       | string        | No       | Extraction rule of the entire log, which will be returned for logs of the `regex_log` type      |
| beginning_regex | string        | No       | First-line matching rule for multi-line logs, which will be returned for logs of the `regex_log` type  |
| keys | array(string) | No | List of key names |
| filter_keys     | array(string) | No       | List of key names found                                |
| filter_regex    | array(string) | No      | Regular expression for filtering           |

## Error Codes

For details, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

