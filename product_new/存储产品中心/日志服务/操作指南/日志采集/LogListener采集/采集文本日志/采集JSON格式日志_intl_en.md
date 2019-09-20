## Overview
A JSON log automatically extracts the key at the first layer as the field name, and the value at the first layer as the field value, to realize structured processing of the entire log. A complete log ends with a line break `\n`.

### Sample

Assume that the raw log in JSON format is as follows:

```shell
{"remote_ip":"10.135.46.111","time_local":"22/Jan/2019:19:19:34 +0800","body_sent":23,"responsetime":0.232,"upstreamtime":"0.232","upstreamhost":"unix:/tmp/php-cgi.sock","http_host":"127.0.0.1","method":"POST","url":"/event/dispatch","request":"POST /event/dispatch HTTP/1.1","xff":"-","referer":"http://127.0.0.1/my/course/4","agent":"Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0","response_code":"200"}
```

After being structured, the log is changed as follows:

```shell
agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0
body_sent: 23
http_host: 127.0.0.1
method: POST
referer: http://127.0.0.1/my/course/4
remote_ip: 10.135.46.111
request: POST /event/dispatch HTTP/1.1
response_code: 200
responsetime: 0.232
time_local: 22/Jan/2019:19:19:34 +0800
upstreamhost: unix:/tmp/php-cgi.sock
upstreamtime: 0.232
url: /event/dispatch
xff: -
```

## Collection Configuration

### 1. Logging In to the Console

Log in to [CLS Console](https://console.cloud.tencent.com/cls) and choose **Logset Management** in the left sidebar.

### 2. Creating LogListener Collection

Select a target logset, click **Create Log Topic**, enter the log topic name test-json, and click **OK**. 
![](https://main.qcloudimg.com/raw/f1356c2cdfe37a97ca465ea90118943a.png)

### 3. Configuring LogListener Collection

Click the log topic collected by LogListener and click **Edit** in the upper right corner of the **Collection Configuration** page to enter the edit mode. Enable **Collection Status** and **LogListener**.
![](https://main.qcloudimg.com/raw/9348df605381b680da4d31d74dfb2b6e.png)

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
| 2.   | /var/log/nginx | \*.log       | In the sample, the log file path is `/var/log/nginx/**/*.log`. LogListener monitors log files with the file name extension `.log` in all subdirectories in the prefix path `/var/log/nginx`. |
| 3.   | /var/log/nginx | error\*      | In the sample, the log file path is `/var/log/nginx/**/error*`. LogListener monitors log files with the prefix `error` in all subdirectories in the path with the prefix `/var/log/nginx`. |


>1. The configuration methods of multi-level directories and wildcard characters depend on LogListener of version 2.2.2 or later. To be compatible with the path configuration methods of LogListener of earlier versions, you can switch to the earlier configuration for modification. Earlier collection path methods do not support multi-level directory collection.
>2. One log file can only be collected into one log topic.
>3. LogListener cannot monitor log files of the soft link mode or log files in the shared file directories of NFS, CIFS, and others.

### 5. Binding a Server Group

Select the target server group from the server group list, and bind it with the current log topic. Please note that the bound server group and the log topic should be in the same region. For more information, see [How to Create Server Group](https://intl.cloud.tencent.com/document/product/614/17412#.E5.88.9B.E5.BB.BA.E6.9C.BA.E5.99.A8.E7.BB.84).
![](https://main.qcloudimg.com/raw/d728f78b6e4e93586b7c3e9219594e5a.png)

### 6. Selecting a JSON Mode

Set **Key-value Extraction Mode** to **JSON**.
![](https://main.qcloudimg.com/raw/a871ce95aaa7763babb94949bd54d118.png)

### 7. Configuring Collection Time

> - Log time is measured in seconds.
> - The time attribute of a log is defined by the collection time or original timestamp.
> - Collection time: The time attribute of a log is determined by the time when the CLS collects the log.
> - Original timestamp: The time attribute of a log is determined by the timestamp in the raw log.

#### 7.1 Using collection time as the time attribute of logs

Always enable the collection time, as shown below. 
![](https://main.qcloudimg.com/raw/0967a0ec058b11aeced929a546baceb1.png)

#### 7.2 Using original timestamp as the time attribute of logs

If you disable the collection time, enter the time key of the original timestamp and the appropriate time parsing format. The conversion format supports all strftime functions. 
![](https://main.qcloudimg.com/raw/1f8357e0a1f735631b7f7b2981193c71.png)

The following are examples on how to enter the time format parsing rule:
Example 1: Original timestamp: `10/Dec/2017:08:00:00`; Parsing format: `%d/%b/%Y:%H:%M:%S`.
Example 2: Original timestamp: `2017-12-10 08:00:00`; Parsing format: `%Y-%m-%d %H:%M:%S`.
Example 3: Original timestamp: `12/10/2017, 08:00:00`; Parsing format: `%m/%d/%Y, %H:%M:%S`.

> Second can be used as the unit of log time. If the time is entered in a wrong format, the collection time is used as the log time.

### 8. Filter Conditions

The filter is designed to add filtering rules based on your business requirements to help you filter out valuable log data. If the filtering rule is the Perl regular expression and the created filtering rule is the hit rule, the log that matches the regular expression can be collected and reported.

You can configure filtering rules for JSON-formatted logs according to the parsed key-value pairs. For example, if you want all JSON-formatted logs where the value of `response_code` is 400 or 500 to be collected, the key is set to status and the filtering rule is set to 400|500.

> The logical relationship between multiple filtering rules is AND. If you set multiple filtering rules for the same key, the rules are overwritten.

### 9. Search Results

Log in to the [CLS Console](https://console.cloud.tencent.com/cls). In the left sidebar, click **Log Search**, enter the logset and log topic, and click **Search**. The system starts to search for logs.
![](https://main.qcloudimg.com/raw/23780078a38047fc1d1e5554eb3c0e95.png)

> Enable index configuration for searching. Otherwise, you cannot search for logs.
