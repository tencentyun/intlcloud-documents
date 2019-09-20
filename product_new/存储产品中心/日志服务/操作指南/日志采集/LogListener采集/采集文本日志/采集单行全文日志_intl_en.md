## Overview

A log in the mode of full text in a single line refers to a complete log in a single line. CLS uses the line break `\n` as the end mark of a log during collection. For unified structured management, each log has a default key `__CONTENT__`. However, the log itself is not structured and no log field is extracted. The time attribute of the log is determined by the collection time.

### Sample

Assume that the raw log is as follows:
```shell
Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64
```

The log is processed by CLS as follows:
```shell
__CONTENT__:Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64
```

## Collection Configuration

### 1. Logging In to the Console

Log in to the [CLS Console](https://console.cloud.tencent.com/cls) and choose **Logset Management** in the left sidebar.

### 2. Creating LogListener Collection

Select a target logset, click **Create Log Topic**, enter the log topic name test-full, and click **OK**.
![](https://main.qcloudimg.com/raw/cc3937823ac7a68534144d54b0719cf9.png)


### 3. Configuring LogListener Collection

Click the log topic collected by LogListener and click **Edit** in the upper right corner of the **Collection Configuration** page to enter the edit mode. Enable **Collection Status** and **LogListener**.
![](https://main.qcloudimg.com/raw/4ee5d39e6a217fabf8f1f71cf762c9d3.png)


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

| No.  | Directory prefix expression   | File name expression    | Description                                      |
| ---- | --------------- | ------------- | ----------------------------------------- |
| 1. | /var/log/nginx | access.log | In the sample, the log file path is `/var/log/nginx/**/access.log`. LogListener monitors log files with the file name `access.log` in all subdirectories in the path with the prefix `/var/log/nginx`. |
| 2. | /var/log/nginx | \*.log | In the sample, the log file path is `/var/log/nginx/**/*.log`. LogListener monitors log files with the file name extension `.log` in all subdirectories in the prefix path `/var/log/nginx`. |
| 3. | /var/log/nginx | error\* | In the sample, the log file path is `/var/log/nginx/**/error*`. LogListener monitors log files with the prefix `error` in all subdirectories in the path with the prefix `/var/log/nginx`. |

>!
>1. The configuration methods of multi-level directories and wildcard characters depend on LogListener of version 2.2.2 or later. To be compatible with the path configuration methods of LogListener of earlier versions, you can switch to the earlier configuration for modification. Earlier collection path methods do not support multi-level directory collection.
>2. One log file can only be collected into one log topic.
>3. LogListener cannot monitor log files of the soft link mode or log files in the shared file directories of NFS, CIFS, and others.

### 5. Binding a Server Group

Select the target server group from the server group list, and bind it with the current log topic. Please note that the bound server group and the log topic should be in the same region. For more information, see [How to Create Server Group](https://intl.cloud.tencent.com/document/product/614/17412#.E5.88.9B.E5.BB.BA.E6.9C.BA.E5.99.A8.E7.BB.84).
![](https://main.qcloudimg.com/raw/67b732e1ae4a099ef247e9e41914986c.png)

### 6. Selecting the Mode of Full Text in a Single Line

Set **Key-value Extraction Mode** to **Full Text in a Single Line**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/5df47173e1921fe3a768299ae35a6767.png)

### 7. Filter Conditions

The filter is designed to add filtering rules based on your business requirements to help you filter out valuable log data. If the filtering rule is the Perl regular expression and the created filtering rule is the hit rule, the log that matches the regular expression can be collected and reported.

In the mode of full text in a single line, use `__CONTENT__` as the key name of the full text by default. For example, the example of a log in the mode of full text in a single line is `Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64`. If you want to collect all logs of January 22, set the key to `__CONTENT__` and set the filtering rule to `Tue Jan 22.*`.

>! The logical relationship between multiple filtering rules is **AND**. If you set multiple filtering rules for the same key, the rules are overwritten.

### 8. Search Results

Log in to the [CLS Console](https://console.cloud.tencent.com/cls). Choose **Log Search** in the left sidebar, select a logset and log topic, and click **Search**. The system starts to search for logs.
![](https://main.qcloudimg.com/raw/c9e348e9b11ecb0c79c58db0da0e139f.png)

>! Enable index configuration for searching. Otherwise, you cannot search for logs.
