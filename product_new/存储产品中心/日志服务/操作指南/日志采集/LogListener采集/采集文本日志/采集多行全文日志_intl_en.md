## Overview
A log in the mode of full text in multi lines refers to a complete log that occupies multiple lines (such as a Java program log). In this mode, the line break `\n` cannot be used as the end mark of a log. To help the CLS system distinguish among the logs, "First Line Regular Expression" is used for matching. When a line of log matches the preset regular expression, the line is considered as the beginning of a log, and the next matching line will be the end mark of the log.

In the mode of full text in multi lines, a default key `__CONTENT__` is also set. However, the log data itself is not structured and no log field is extracted. The time attribute of a log is determined by the collection time.

### Sample

Assume that the raw data of a multi-line log is as follows:
```
10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 
Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0 0.310 0.310
```

The log is structured by the CLS as follows:
```
__CONTENT__:10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 \nMozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0  0.310 0.310
```

## Collection Configuration

### 1. Logging In to the Console

Log in to [CLS Console](https://console.cloud.tencent.com/cls) and choose **Logset Management** in the left sidebar.

### 2. Creating LogListener Collection

Select a target logset, click **Create Log Topic**, enter the log topic name test-mtext, and click **OK**.
![](https://main.qcloudimg.com/raw/68647c620fa31674511f347ca7778746.png)

### 3. Configuring LogListener Collection

Click the log topic collected by LogListener and click **Edit** in the upper right corner of the **Collection Configuration** page to enter the edit mode. Enable **Collection Status** and **LogListener**.
![](https://main.qcloudimg.com/raw/3cc5995a557329ff9daec1ed9234fa41.png)

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


> 1. The configuration methods of multi-level directories and wildcard characters depend on LogListener of version 2.2.2 or later. To be compatible with the path configuration methods of LogListener of earlier versions, you can switch to the earlier configuration for modification. Earlier collection path methods do not support multi-level directory collection.
> 2. One log file can only be collected into one log topic.
> 3. LogListener cannot monitor log files of the soft link mode or log files in the shared file directories of NFS, CIFS, and others.

### 5. Binding a Server Group

Select the target server group from the server group list, and bind it with the current log topic. Please note that the bound server group and the log topic should be in the same region. For more information, see [How to Create Server Group](https://intl.cloud.tencent.com/document/product/614/17412#.E5.88.9B.E5.BB.BA.E6.9C.BA.E5.99.A8.E7.BB.84).
![](https://main.qcloudimg.com/raw/489e42e99ff02c2e4c32a9ca56263967.png)

### 6. Selecting the Mode of Full Text in Multi Lines

Set **Key-value Extraction Mode** to **Full Text in Multi Lines**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/063e469d8eb284c215eb6fe2bd6d664c.png)

**Automatic generation of logs in the mode of full text in multi lines**:
a. Set **Key-value Extraction Mode** to **Full Text in Multi Lines**.
b. Copy a single multi-line log from the log file to the dialog box. The system automatically highlights the first line.
c. Click **Auto-generate**.
d. Ensure that the regular expression is automatically generated to complete the configuration.
![](https://main.qcloudimg.com/raw/4ae4805d159a8bc9d88d68129a811a9f.png)

**Manually enter logs in the mode of full text in multi lines**:
a. Set **Key-value Extraction Mode** to **Full Text in Multi Lines**.
b. Copy a single multi-line log from the log file to the dialog box. The system automatically highlights the first line.
c. Manually enter the regular expression and click **Verify**.
d. Ensure that the verification is successful to complete the configuration.
![](https://main.qcloudimg.com/raw/28a1f37f66a36271f9f6b3ef052eb0cc.png)

### 7. Filter Conditions

The filter is designed to add filtering rules based on your business requirements to help you filter out valuable log data. If the filtering rule is the Perl regular expression and the created filtering rule is the hit rule, the log that matches the regular expression can be collected and reported.

In the mode of full text in multi lines, use `__CONTENT__` as the key name of the full text by default. A sample of a log in the mode of full text in multi lines is as follows:
```
10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 
Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0 0.310 0.310
```
If you want to collect all logs on the server whose IP address is `10.20.20.10`, set the key to `__CONTENT__` and then set the filtering rule to `10.20.20.10.*`.

> The logical relationship between multiple filtering rules is **AND**. If you set multiple filtering rules for the same key, the rules are overwritten.

### 8. Search Results

Log in to the [CLS Console](https://console.cloud.tencent.com/cls). Choose **Log Search** in the left sidebar, select a logset and log topic, and click **Search**. The system starts to search for logs.
![](https://main.qcloudimg.com/raw/c0926f11a9c185b699139bdc2d50c439.png)

> Enable index configuration for searching. Otherwise, you cannot search for logs.
