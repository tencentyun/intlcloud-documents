In simple Ops scenarios, logs are directly output to local files on the server, and then you can run the `grep` command in Linux to search for logs. In complex service systems, logs are scattered on different servers, CLI operations are not intuitive, and server permission management is restricted. As a result, it is difficult to find logs, which seriously affects Ops efficiency. It's even more difficult if you need to do some statistical analysis or monitor alarms based on logs.

This document describes how to quickly migrate the local logs searched by the `grep` command to CLS to obtain the following advantages:

- Data is stored and searched centrally, and you don't need to log in to multiple servers to query it individually, which is critical in load balancing, microservice, and other architectures.
- You can quickly search for logs with a few clicks, eliminating command lines and tedious server permission management.
- You can perform statistical analysis based on logs to obtain key business metrics such as PV, API response time, and API error rate.
- You can detect exceptional logs in real time and receive notifications through various methods such as SMS, email, and WeChat.

>? If your logs have been collected to CLS, you can skip the steps of log collection and index configuration and go to [Step 3. Searching for logs](#RetrievalLog).
>

## Step 1. Collect Logs

For server local logs, you can use LogListener to collect raw logs to CLS. For how to install LogListener, please see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).
If you are using Tencent Cloud CVMs, you can also use the automatic installation feature provided by the console to install LogListener. For more information, please see [Deploying LogListener on CVMs in Batches](https://intl.cloud.tencent.com/document/product/614/42133).

Different from storing logs locally on servers, collecting logs to CLS makes log search and statistical analysis easier. When collecting logs, you can convert non-formatted raw logs to formatted data. Assume that the raw log is as follows:
```
10.20.20.10 ::: [Tue Jan 22 14:49:45 CST 2019 +0800] ::: GET /online/sample HTTP/1.1 ::: 127.0.0.1 ::: 200 ::: 647 ::: 35 ::: http://127.0.0.1/
```
You can use the separator `:::` to split the log into eight fields and name each field as follows:
```
IP: 10.20.20.10
bytes: 35
host: 127.0.0.1
length: 647
referer: http://127.0.0.1/
request: GET /online/sample HTTP/1.1
status: 200
time: [Tue Jan 22 14:49:45 CST 2019 +0800]
```
For operation details, please see [Separator Format](https://intl.cloud.tencent.com/document/product/614/32285). In addition to using separators to split logs, you can use regular expression, JSON, and full-text log splitting methods. For more information, please see [Collecting Text Logs](https://intl.cloud.tencent.com/document/product/614/32282).

## Step 2. Configure Indexes

The purpose of configuring indexes is to define searchable fields and their types to facilitate future log search. For most scenarios, you can use the automatic index configuration feature to complete the configuration with a few clicks. For more information, please see [Configuring Indexes](https://intl.cloud.tencent.com/document/product/614/39594).


<span id="RetrievalLog"></span>
## Step 3. Search for Logs

The following uses the commonly used `grep` command as an example to describe how to achieve a similar log search feature in CLS.

Assume the raw log is as follows:
```
10.20.20.10 ::: [Tue Jan 22 14:49:45 CST 2019 +0800] ::: GET /online/sample HTTP/1.1 ::: 127.0.0.1 ::: 200 ::: 647 ::: 35 ::: http://127.0.0.1/
```

The corresponding formatted log in CLS is as follows:
```
IP: 10.20.20.10
bytes: 35
host: 127.0.0.1
length: 647
referer: http://127.0.0.1/
request: GET /online/sample HTTP/1.1
status: 200
time: [Tue Jan 22 14:49:45 CST 2019 +0800]
```

#### Example 1

Search for logs where `request` is `/online/sample`.
- Use the `grep` command
```
# grep "/online/sample" test.log
```
- Use the CLS search mode
```
request:"/online/sample"
```


#### Example 2

Search for logs where `status` (status code) is not `200`.
- Use the `grep` command
```
# grep -v "200" test.log
```
In fact, this mode may exclude certain logs where the number 200 exists but `status` is not `200`.
- Use the CLS search mode
```
NOT status:200
```
CLS also supports other more flexible search methods. For example, you can search for logs where `status` is greater than or equal to 500 as follows:
```
status:>=500
```


#### Example 3

Count the number of logs where `status` is not `200`.
- Use the `grep` command
```
# grep -c -v "200" test.log
```
- Use the CLS search mode
```
NOT status:200 | select count(*) as errorLogCounts
```


#### Example 4

Search for logs where `status` is `200` and `request` is `/online/sample`.
- Use the `grep` command
```
# grep "200" test.log | grep "/online/sample"
```
- Use the CLS search mode
```
status:200 AND request:"/online/sample"
```

#### Example 5

Search for logs where `request` is `/online/sample` or `/offline/sample`.
- Use the `grep` command
```
# grep -E "/online/sample|/offline/sample" test.log
```
- Use the CLS search mode
```
request:"/online/sample" OR request:"/offline/sample"
```

#### Example 6

Search for logs where `request` is `/online/sample` but the log file is not `test.log`.
- Use the `grep` command
```
# grep -rn "/online/sample" --exclude=test.log
```
- Use the CLS search mode
```
request:"/online/sample" AND NOT __FILENAME__:"test.log"
```

#### Example 7

Search for the first 10 lines in logs where `time` is `[Tue Jan 22 14:49:45 CST 2019 +0800]`.
- Use the `grep` command
```
# grep "[Tue Jan 22 14:49:45 CST 2019 +0800]" -B 10 test.log
```
- Use the CLS search mode
```
time:"[Tue Jan 22 14:49:45 CST 2019 +0800]"
```
If a matching log is found, you can click **Context Search** in the console to view logs near the log found.



