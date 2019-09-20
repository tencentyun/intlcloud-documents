## Overview

A separator-based log refers to a log that can be structured using the specified separator. A complete log ends with a line break `\n`. You need to define a unique key for each separate field for CLS to process separator-based logs.

### Sample

Assume that the raw log is as follows:

```shell
10.20.20.10 - ::: [Tue Jan 22 14:49:45 CST 2019 +0800] ::: GET /online/sample HTTP/1.1 ::: 127.0.0.1 ::: 200 ::: 647 ::: 35 ::: http://127.0.0.1/
```

When the specified separator for log parsing is `:::`, the log is divided into eight fields and a unique key is defined for each of the field as follows:

```shell
IP: 10.20.20.10 -
bytes: 35
host: 127.0.0.1
length: 647
referer: http://127.0.0.1/
request: GET /online/sample HTTP/1.1
status: 200
time: [Tue Jan 22 14:49:45 CST 2019 +0800]
```

## Collection Configuration

### 1. Logging In to the Console

Log in to the [CLS Console](https://console.cloud.tencent.com/cls) and choose **Logset Management** in the left sidebar.

### 2. Creating LogListener Collection

Select a target logset, click **Create Log Topic**, enter the log topic name test-separator, and click **OK**.
![](https://main.qcloudimg.com/raw/9ad94a9088f143eaf0987a709f8f6d93.png)

### 3. Configuring LogListener Collection

Click the log topic collected by LogListener and click **Edit** in the upper right corner of the **Collection Configuration** page to enter the edit mode. Enable **Collection Status** and **LogListener**.
![](https://main.qcloudimg.com/raw/e49f2dfe5342010a3e33113b5530362f.png)

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
| 1.   | /var/log/nginx | access.log   | In the sample, the log file path is `/var/log/nginx/**/access.log`. LogListener monitors log files with the file name `access.log` in all subdirectories in the prefix path `/var/log/nginx`. |
| 2.   | /var/log/nginx | \*.log       | In the sample, the log file path is `/var/log/nginx/**/*.log`. LogListener monitors log files with the file name extension `.log` in all subdirectories in the prefix path `/var/log/nginx`. |
| 3.   | /var/log/nginx | error\*      | In the sample, the log file path is `/var/log/nginx/**/error*`. LogListener monitors log files with the prefix `error` in all subdirectories in the prefix path `/var/log/nginx`. |

>!
>1. The configuration methods of multi-level directories and wildcard characters depend on LogListener of version 2.2.2 or later. To be compatible with the path configuration methods of LogListener of earlier versions, you can switch to the earlier configuration for modification. Earlier collection path methods do not support multi-level directory collection.
>2. One log file can only be collected into one log topic.
>3. LogListener cannot monitor log files of the soft link mode or log files in the shared file directories of NFS, CIFS, and others.

### 5. Binding a Server Group

Select the target server group from the server group list, and bind it with the current log topic. Please note that the bound server group and the log topic should be in the same region. For more information, see [How to Create Server Group](https://intl.cloud.tencent.com/document/product/614/17412#.E5.88.9B.E5.BB.BA.E6.9C.BA.E5.99.A8.E7.BB.84).
![](https://main.qcloudimg.com/raw/a6bf012aca0efa7ec40233480c8d93ce.png)

### 6. Selecting the Separator Mode

Set **Key-value Extraction Mode** to **Separator**, as shown in the following figure.

![](https://main.qcloudimg.com/raw/96762c7d10456545c31a29ad25bc8bb5.png)

### 7. Confirming the Separator

First, you need to select a unique separator. The system splits the log sample by using the selected separator and displays it in the parsing result. You need to define a unique key for each field. Log collection supports a variety of separators. Common separators include spaces, tabs, commas (,), semicolons (;), and vertical bars (|). If you use another symbol as the separator of log data, such as `:::`, you can also parse the log by using a custom separator.
![](https://main.qcloudimg.com/raw/1721555739d53fa1dfc7049eb8c86fcd.png)

### 8. Configuring Collection Time

> - Log time is measured in seconds.
> - The time attribute of a log is defined by the collection time or original timestamp.
> - Collection time: The time attribute of a log is determined by the time when the CLS collects the log.
> - Original timestamp: The time attribute of a log is determined by the timestamp in the raw log.

#### 8.1 Using collection time as the time attribute of logs

Always enable **Collection Time**, as shown in the following figure.

![](https://main.qcloudimg.com/raw/5dede85877e54a69a3d4cf8fdaf81893.png)

#### 8.2 Using original timestamp as the time attribute of logs

If you disable the collection time, enter the time key of the original timestamp and the appropriate time parsing format. The conversion format supports all strftime functions.

![](https://main.qcloudimg.com/raw/611e5517422e485362c0c2db75c0426c.png)

The following are examples on how to enter the time format parsing rule:
Example 1: Original timestamp: `10/Dec/2017:08:00:00`; Parsing format: `%d/%b/%Y:%H:%M:%S`.
Example 2: Original timestamp: `2017-12-10 08:00:00`; Parsing format: `%Y-%m-%d %H:%M:%S`.
Example 3: Original timestamp: `12/10/2017, 08:00:00`; Parsing format: `%m/%d/%Y, %H:%M:%S`.

>!Second can be used as the unit of log time. If the time is entered in a wrong format, the collection time is used as the log time.

### 9. Filter Conditions

The filter is designed to add filtering rules based on your business requirements to help you filter out valuable log data. If the filtering rule is the Perl regular expression and the created filtering rule is the hit rule, the log that matches the regular expression can be collected and reported.

For separator-based logs, you can configure filtering rules based on the custom key-value pairs. For example, after a sample log is parsed in separator mode, if you want all logs where the value of `status` is 400 or 500 to be collected, the key is set to status and the filtering rule is set to 400|500.

>! The logical relationship between multiple filtering rules is AND. If you set multiple filtering rules for the same key, the rules are overwritten.

### 10. Search Results

Log in to the [CLS Console](https://console.cloud.tencent.com/cls). Choose **Log Search** in the left sidebar, select a logset and log topic, and click **Search**. The system starts to search for logs.
![](https://main.qcloudimg.com/raw/22dfcc938d8b7e2db37c56e51bd52f47.png)

>! Enable index configuration for searching. Otherwise, you cannot search for logs.
