## Overview

CLS provides log collection clients that allow you to collect your application logs and import them into CLS through APIs or SDKs. Currently, CLS requires logs to be uploaded in a structured manner as key-value pairs.

## Log Structuring

The structuring of logs is to store your log data on the CLS platform in key-value format. Structured logs can be searched for, analyzed, and shipped based on specified keys. CLS allows you to report structured data directly. For more information, please see the following:

For example, a local raw log is as follows:

```shell
10.20.20.10;[Tue Jan 22 14:49:45 CST 2019 +0800];GET /online/sample HTTP/1.1;127.0.0.1;200;647;35;http://127.0.0.1/
```

Specify that the log is parsed by separator and select semicolon (;) as the separator. Then the log can be parsed into multiple field groups and each group is organized in key-value pairs. A key name is defined for each key as follows:

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

LogListener provides various parsing modes, in which reported logs with full text in a single line and full text in multi lines are both structured. LogListener adds `__CONTENT__` as a key and uses the original text as the value by default. The key-value pair is as follows:

| LogListener Parsing Mode | Key | Description                                              |
| -------------------- | ------------- | ----------------------------------------------------- |
| Full text in a single line/Full text in multi lines        | `__CONTENT__`  | `__CONTENT__` is the key name by default.                              |
| JSON format            | Name in the JSON file | The name and value in the original text of the JSON log are used as a key-value pair.  |
| Separator format           | Custom        | After dividing fields using separators, you need to define a key name for each field group.   |
| Full regular expression             | Custom        | After extracting fields based on a regular expression, you need to define a key name for each field group. |


## Collection Methods

CLS provides multiple methods for data collection:

| Collection Method               | Description                                                         |
| :--------------------- | ------------------------------------------------------------ |
| API           | You can upload structured logs to CLS by calling [CLS APIs](https://intl.cloud.tencent.com/document/product/614/12445). For more information, see [Uploading Structured Logs](https://intl.cloud.tencent.com/document/product/614/16873). |
| SDK           | You can use SDKs to upload structured logs to CLS. For more information, see [here](https://intl.cloud.tencent.com/document/product/614/45006).                                              |
| LogListener client | LogListener is a log collection client provided by CLS. You can quickly access CLS by simply configuring LogListener in the console. For more information, see [LogListener Use Process](https://intl.cloud.tencent.com/document/product/614/31578). |

A comparison of the collection methods is as follows:

| Category  | Collection via LogListener                   | Collection via API                   |
| -------- | ---------------------------------- | ------------------------------ |
| Code modification | Provides a non-intrusive collection method for applications, without code modification. | Reports logs only after modifying application code. |
| Resumable upload | Supports resumable upload of logs.                   | Automatically implemented by code.                   |
| Retransmission upon failure | Provides an inherent retry mechanism.                       | Automatically implemented by code.                   |
| Local cache | Supports local cache, ensuring data integrity during peak hours. | Automatically implemented by code.                   |
| Resource occupation | Occupies resources such as memory and CPU resources.                | Occupies no additional resources.                 |

## Accessing Log Sources

You can access different log sources in different ways. For more information, see the following tables:

**Log source category**

| Log Source Category   | Recommended Access Method |
| ------------ | ------------ |
| Direct program output | API          |
| Local log file | LogListener  |

**Log source environment**

| System Environment    | Recommended Access Method                      |
| ----------- | ----------------------------------- |
| Linux/Unix  | LogListener                       |
| Windows     | API (Currently, LogListener does not support Windows.) |
| iOS/Android | [SDK](https://intl.cloud.tencent.com/document/product/614/45006)         |

**Tencent Cloud service logs**

| Tencent Cloud Service               | Recommended Access Method                                                 |
| ------------------------ | ------------------------------------------------------------ |
| CVM | Install and configure LogListener. For more information, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414). |
| TKE | Configure log collection in the TKE console. For more information, see [here](https://intl.cloud.tencent.com/document/product/457/32419). |
| CDN | Configure log collection in the CDN console. For more information, see [here](https://intl.cloud.tencent.com/document/product/228/35380). |
| CLB | Configure log collection in the CLB console. For more information, see [here](https://intl.cloud.tencent.com/document/product/214/35063). |
| SCF | Configure log collection in the SCF console For more information, see [here](https://intl.cloud.tencent.com/document/product/583/34876). |
| LVB | Configure log collection in the LVB console. For more information, see [here](). |
| Flow Logs | Configure log collection in the Flow Logs console. For more information, see [here](https://intl.cloud.tencent.com/document/product/682/18966). |
| TI-ONE | Configure log collection in the TI-ONE console. For more information, see [here](). |
| MGOBE    | Configure log collection in the MGOBE console. For more information, see [here](). |


