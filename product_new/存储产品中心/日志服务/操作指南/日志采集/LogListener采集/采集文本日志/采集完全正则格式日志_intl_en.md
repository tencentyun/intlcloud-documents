## Overview
The Full RegEx mode is a log parsing mode used to extract multiple key-value pairs from a log by RegEx. If no key-value pair needs to be extracted, see Single-Line Full Text Collection or Multi-Line Full Text Collection for configuration. To configure the Full RegEx mode, you need to enter a log sample and then define a regular expression. The system extracts the related key-value pair according to the capturing group in the regular expression. The following describes how to collect full regular logs.

### Sample

Assume that the raw log is as follows:

```shell
10.135.46.111 - - [22/Jan/2019:19:19:30 +0800] "GET /my/course/1 HTTP/1.1" 127.0.0.1 200 782 9703 "http://127.0.0.1/course/explore?filter%5Btype%5D=all&filter%5Bprice%5D=all&filter%5BcurrentLevelId%5D=all&orderBy=studentNum" "Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0"  0.354 0.354
```

The configured custom regular expression is as follows:

```shell
(\S+)[^\[]+(\[[^:]+:\d+:\d+:\d+\s\S+)\s"(\w+)\s(\S+)\s([^"]+)"\s(\S+)\s(\d+)\s(\d+)\s(\d+)\s"([^"]+)"\s"([^"]+)"\s+(\S+)\s(\S+).*
```

The CLS extracts the related key-value pair according to the `()` capturing group. You can define the key name for each group as follows:

```shell
body_bytes_sent: 9703
http_host: 127.0.0.1
http_protocol: HTTP/1.1
http_referer: http://127.0.0.1/course/explore?filter%5Btype%5D=all&filter%5Bprice%5D=all&filter%5BcurrentLevelId%5D=all&orderBy=studentNum
http_user_agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0
remote_addr: 10.135.46.111
request_length: 782
request_method: GET
request_time: 0.354
request_url: /my/course/1
status: 200
time_local: [22/Jan/2019:19:19:30 +0800]
upstream_response_time: 0.354
```

> The Full RegEx mode supports extraction of key-value pairs only from single-line logs. To collect from multi-line logs, see Multi-Line Full Text Collection.

## Collection Configuration

### 1. Logging In to the Console

Log in to [CLS Console](https://console.cloud.tencent.com/cls) and choose **Logset Management** in the left sidebar.

### 2. Adding Log Topic

Select a target logset, click **Add Log Topic**, enter the log topic name test-whole, and click **OK**. 
![](https://main.qcloudimg.com/raw/e566018c591387497d94221d8fcf8fa2.png)

### 3. Configuring LogListener Collection

Click the log topic collected by LogListener and click **Edit** in the upper right corner of the **Collection Configuration** page to enter the edit mode. Enable **Collection Status** and **LogListener**.
![](https://main.qcloudimg.com/raw/d90cc9360d42e71253163dd12cce9c5a.png)

### 4. Configuring the Log File Collection Path

The log file collection path is **[Directory prefix expression]**/\*\*/**[File name expression]**. The LogListener matches all common-prefix path that conform to the rules according to **[Directory prefix expression]**, and monitors all log files that conform to **[File name expression]** in the directories (including subdirectories). Parameter descriptions are as follows:

| Field     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Directory prefix | The directory prefix structure of a log file supports only the wildcard characters “\*” and question marks (?). The wildcard character “\*” indicates that any multiple characters can be matched and the question mark (?) indicates that any single character can be matched. |
| /**/     | Current directory and all its subdirectories                                   |
| File name   | A log file name supports only the wildcard characters “\*” and question marks (?). The wildcard character “\*” indicates that any multiple characters can be matched and the question mark (?) indicates that any single character can be matched. |

>Common configuration modes for reference:
>[Common directory prefix]/\*\*/[Common file name prefix]\*
>[Common directory prefix]/\*\*/*[Common file name extension]
>[Common directory prefix]/\*\*/[Common file name prefix]\*[Common file name extension]
>[Common directory prefix]/\*\*/\*[Common character string]\*

Samples:

| No. | Directory prefix expression | File name expression | Description                                                         |
| ---- | -------------- | ------------ | ------------------------------------------------------------ |
| 1.   | /var/log/nginx | access.log   | In the sample, the log file path is `/var/log/nginx/**/access.log`. LogListener monitors log files with the file name `access.log` in all subdirectories in the path with the prefix `/var/log/nginx`. |
| 2.   | /var/log/nginx | \*.log       | In the sample, the log file path is `/var/log/nginx/**/*.log`. LogListener monitors log files with the file name extension `.log` in all subdirectories in the path with the prefix `/var/log/nginx`. |
| 3.   | /var/log/nginx | error\*      | In the sample, the log file path is `/var/log/nginx/**/error*`. LogListener monitors log files with the prefix `error` in all subdirectories in the path with the prefix `/var/log/nginx`. |


>1. The configuration methods of multi-level directories and wildcard characters depend on LogListener of version 2.2.2 or later. To be compatible with the path configuration methods of LogListener of earlier versions, you can switch to the earlier configuration for modification. Earlier collection path methods do not support multi-level directory collection.
>2. One log file can only be collected into one log topic.
>3. LogListener cannot monitor log files of the soft link mode or log files in the shared file directories of NFS, CIFS, and others.

### 5. Binding a Server Group

Select the target server group from the server group list, and bind it with the current log topic. Please note that the bound server group and the log topic should be in the same region. For more information, see [How to Creat Server Group](https://intl.cloud.tencent.com/document/product/614/17412#.E5.88.9B.E5.BB.BA.E6.9C.BA.E5.99.A8.E7.BB.84).
![](https://main.qcloudimg.com/raw/5bb42e4d8501b6a23e1b98cc7135d874.png)

### 6. Configuring the Full RegEx Mode

Set **Key-value Extraction Mode** to **Full RegEx**, as shown in the following figure.

![](https://main.qcloudimg.com/raw/4264c5f0f9262d41ab305d56e5b2f901.png)

#### 6.1 Definition of a regular expression

In the Full RegEx mode, the system extracts key-value pairs according to the defined RegEx. Click **Auto-generate** to complete the RegEx extraction. If automatic generation fails, you can switch to the manual mode for RegEx mode verification.
- Auto mode
 a. Enter a log sample.
 b. Select some logs based on the search analysis requirements, and click **Group** to group them into one. After successful grouping, information is displayed, indicating that the logs will be extracted as a key-value group.
 c. Repeat “step b” until all key-value pairs to be extracted are grouped.
 d. Click **Auto-generate**. The system generates a RegEx extraction mode for log grouping.
![](https://main.qcloudimg.com/raw/211351cc674db3e57dae83b1677702c4.png)
- Manual mode
 a. Enter a log sample.
 b. Manually enter a regular expression.
 c. Click **Verify**. The system determines whether the log sample matches the regular expression.
![](https://main.qcloudimg.com/raw/be9fd5e9f86a23a4cae550f0ace645c4.png)
> When the RegEx extraction mode is defined and verified, the extraction result is displayed no matter in the automatic or manual mode. You need to define a key name for each key-value group. The name will be used for search analysis.

### 7. Configuring of Collection Time
- Log time is measured in seconds.
- The time attribute of a log is defined by the collection time or original timestamp.
- Collection time: The time attribute of a log is determined by the time when the CLS collects the log.
- Original timestamp: The time attribute of a log is determined by the timestamp in the raw log.

#### 7.1 Using collection time as the time attribute of logs

Always enable **Collection Time**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/0caad22ab5444f66243281782114c7c8.png)

#### 7.2 Using original timestamp as the time attribute of logs

If you disable the collection time, enter the time key of the original timestamp and the appropriate time parsing format. The conversion format supports all strftime functions.
![](https://main.qcloudimg.com/raw/d2d869cfa6cb128293e9592b9cfb2f2c.png)

The following are examples of how to enter the time format parsing rule:  
Example 1: Original timestamp: `10/Dec/2017:08:00:00`; Parsing format: `%d/%b/%Y:%H:%M:%S`.
Example 2: Original timestamp: `2017-12-10 08:00:00`; Parsing format: `%Y-%m-%d %H:%M:%S`.
Example 3: Original timestamp: `12/10/2017, 08:00:00`; Parsing format: `%m/%d/%Y, %H:%M:%S`.

> Second can be used as the unit of log time. If the time is entered in a wrong format, the collection time is used as the log time.

### 8. Setting Filter Conditions

The filter is designed to add filtering rules based on your business requirements to help you filter out valuable log data. If the filtering rule is the Perl regular expression and the created filtering rule is the hit rule, the log that matches the regular expression can be collected and reported.

When the full RegEx collects the log, the filtering rule needs to be configured based on the defined key-value pair. For example, after the sample log is parsed in Full RegEx mode, if you want all logs, where the value of status is 400 or 500, to be collected, the key is set to status and the filtering rule is set to 400|500.

> The logical relationship between multiple filtering rules is **AND**. If multiple filtering rules are set for the same key, the rules are overwritten.

### 9. Searching for Logs

Log in to the [CLS Console](https://console.cloud.tencent.com/cls). In the left sidebar, click **Log Search**, enter the logset and log topic, and click **Search**. The system starts to search for logs based on the set search criteria.
![](https://main.qcloudimg.com/raw/f3b2687a67e83a7f116df1143181a0ea.png)

> Enable index configuration for searching. Otherwise, you cannot search for logs.
