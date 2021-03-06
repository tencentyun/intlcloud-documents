## 描述

获取 agent 对应的采集配置。

## 请求
#### 请求行

```
GET /agent/config
```

#### 请求示例

```
GET /agent/config HTTP/1.1Host: <Region>.cls.myqcloud.comAuthorization: <AuthorizationString>
```

#### 请求头

| Header名            | 含义          |
| ------------------- | ------------- |
| x-cls-agent-version | agent 的版本号 |
| x-cls-agent-ip      | agent 的 IP 地址 |

#### 请求参数

无

## 响应
#### 返回示例

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


#### 响应头

无特殊

#### 返回内容说明

| 字段名       | 类型               | 是否必选 | 含义                              |
| ------------ | ------------------ | -------- | --------------------------------- |
| logconf      | JsonArray(ColInfo) | 是       | 日志的采集信息                    |
| needupdate   | bool               | 是       | agent 是否需要更新                 |
| last_version | string             | 否       | agent 最新的版本号，需要更新时返回 |
| url          | string             | 否       | agent 的下载地址，需要更新时返回   |
| file_md5     | string             | 否       | agent 的 MD5 值，需要更新时返回      |

ColInfo 格式如下：

| 字段名         | 类型   | 是否必选 | 含义                                                         |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| topicid        | string | 是       | 日志主题的 ID                                               |
| path           | string | 否       | 采集的路径（兼容旧版本采集路径，multi_wildpath，wildpath 和 path 只会返回其中一个） |
| wildpath       | string | 否       | 采集的路径（新版本采集路径，multi_wildpath，wildpath 和 path 只会返回其中一个） |
| multi_wildpath | string | 否       | 采集的路径（新版本采集路径，multi_wildpath，wildpath 和 path 只会返回其中一个） |
| log_type       | string | 是       | 日志类型                                                     |
| extract_rule   | object | 是       | 提取规则                                                     |

extract_rule 格式如下：

| 字段名          | 类型          | 是否必选 | 含义                                                 |
| --------------- | ------------- | -------- | ---------------------------------------------------- |
| time_key        | string        | 否       | 日志中时间的 key                                      |
| time_format     | string        | 否       | 时间的格式                                           |
| delimiter       | string        | 否       | 分隔符，`delimiter_log` 类型的日志时返回             |
| log_regex       | string        | 否       | 整个日志的提取规则，`regex_log` 类型的日志时返回     |
| beginning_regex | string        | 否       | 多行日志的首行匹配规则，`regex_log` 类型的日志时返回 |
| keys            | array(string) | 否       | key 名字列表                                          |
| filter_keys     | array(string) | 否       | 过滤的key名字列表                                    |
| filter_regex    | array(string) | 否       | 过滤的正则                                           |

## 错误码

请参见 [错误码](https://intl.cloud.tencent.com/document/product/614/12402) 文档。

