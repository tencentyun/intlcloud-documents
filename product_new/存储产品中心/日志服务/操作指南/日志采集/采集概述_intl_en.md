## Overview

CLS allows you to collect your application logs and import them into CLS through a collector client (LogListener) or APIs. Currently, CLS requires logs to be uploaded in a structured manner as key-value pairs.

## Log Structuring

The structuring of logs is to store your log data on the CLS platform in key-value format. Structured logs can be searched for, analyzed, and delivered based on the specified key values. The CLS allows reports of structured data. For more information, please see the following:

| Log upload mode     | How to upload structured logs                                             |
| ---------------- | ------------------------------------------------------------ |
| Upload via APIs         | Use the [Upload Structured Logs](https://intl.cloud.tencent.com/document/product/614/16873) API |
| Upload by LogListener | LogListener uploads structured logs through configuration of the parsing mode, which includes separator, JSON, and full RegEx modes. |

For example, a local source log is as follows:

```shell
10.20.20.10;[Tue Jan 22 14:49:45 CST 2019 +0800];GET /online/sample HTTP/1.1;127.0.0.1;200;647;35;http://127.0.0.1/
```

Specify that the log is parsed by separators. Select semicolons `;` as the separator. The log can be parsed into multiple field groups and each group is organized in key-value pairs. A key name is defined for each key as follows:

```shell
IP: 10.20.20.10
time: [Tue Jan 22 14:49:45 CST 2019 +0800]
request: GET /online/sample HTTP/1.1
host: 127.0.0.1
status: 200
length: 647
bytes: 35
referer: http://127.0.0.1/
```

LogListener provides various parsing modes, in which reported logs with single-line and multi-line full text are both structured. LogListener adds `__CONTENT__` as a key by default and uses the original text as the value. The key-value pair is as follows:

| LogListener parsing mode | Key | Description                                              |
| -------------------- | ------------- | ----------------------------------------------------- |
| Full text in single line/multi lines        | `__CONTENT__`  | `__CONTENT__` is the key name by default                              |
| JSON format            | Name in the JSON file | The name and value in the original text of the JSON log are used as a key-value pair  |
| Separator format           | Custom        | After dividing fields using separators, you need to define a key name for each field group.   |
| Full RegEx             | Custom        | After extracting fields based on the regular expression, you need to define a key name for each field group. |
