## Overview

A log with full text in a single line means a line is a full log. When CLS collects logs, it uses `\n` as line break to end a log with. For structural purposes, each log contains a default key value `__CONTENT__`, but the log data itself will not be structured, nor will any log fields be extracted. The log attribute `Time` is determined by the time the log was collected.

#### Samples

Assume a log contains raw data as follows:

```plaintext
Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64
```

CLS outputs it into:

```plaintext
__CONTENT__:Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64
```

## Collection Configuration

### 1. Logging in to the console

Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and click **Logset** in the left sidebar.

### 2. Creating log topic for LogListener

Select a logset, click **Add Log Topic**, enter the log topic name, e.g. `test_full`, and click **OK**.
![](https://main.qcloudimg.com/raw/cc3937823ac7a68534144d54b0719cf9.png)

### 3. Configuring LogListener collection

1. Select the log topic to open the management page.
2. Click the **Collection Configuration** tab, and toggle on **Collection Status** to enter Edit mode.
3. Click **Add Configurations** in the **Loglistener Collection** section to enter the agent configuration page.
![](https://main.qcloudimg.com/raw/4ee5d39e6a217fabf8f1f71cf762c9d3.png)

### 4. Configuring a log path

A path under which to collect logs takes the form **[directory prefix expression]**/\*\*/**[file name expression]**. LogListener matches all paths with common prefixes that satisfy the **[directory prefix expression]**, and listen on all log files under these directories (including subdirectories) that satisfy the **[file name expression]**. The detailed parameters are as follows:

| Field     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Directory prefix | The prefix of a log directory; supports only the wildcard characters `\*` and `?`. `\*` indicates that one or more characters can be matched, while `?` indicates that any single character can be matched. |
| /**/   | Current directory and all its subdirectories                                  |
| File name   | Name of a log file; supports only the wildcard characters `\*` and `?`. `\*` indicates that one or more characters can be matched, while `?` indicates that any single character can be matched. |

>Common configuration patterns include:
> - [Common directory prefix]/\*\*/[Common filename prefix]\*
> - [Common directory prefix]/\*\*/*[Common filename suffix]
> - [Common directory prefix]/\*\*/[Common filename prefix]\*[Common filename suffix]
> - [Common directory prefix]/\*\*/\*[Common string]\*

Examples:

| No. | Directory Prefix Expression | Filename Expression | Description                                                         |
| ---- | -------------- | ------------ | ------------------------------------------------------------ |
| 1.   | /var/log/nginx | access.log   | This example configures the log path to `/var/log/nginx/**/access.log`, so that LogListener will listen on all log files named `access.log` in all the sub-directories prefixed with `/var/log/nginx`. |
| 2.   | /var/log/nginx | \*.log   | This example configures the log path to `/var/log/nginx/**/*.log`, so that LogListener will listen on all log files that end with `.log` in all the sub-directories prefixed with `/var/log/nginx`. |
| 3.   | /var/log/nginx | error\*      | This example configures the log path to `/var/log/nginx/**/error*`, so that LogListener will listen on all log files that begin with `error` in all the sub-directories prefixed with `/var/log/nginx`. |


![](https://main.qcloudimg.com/raw/4807b612fc06f4baeca8014a55f86edd.png)

>
> 1. The configuration of hierarchical directories and wildcards is only available for Loglistener version 2.2.2 or above. In order to be compatible with lower versions, you can modify the old path configuration which does not support hierarchical directories.
> 2. A log file will only be collected by one log topic.
> 3. LogListener cannot listen on log files with symbolic links, or in shared file directories of NFS, CIFS, etc.

### 5. Associating a server group

Select a server group from the server groups list, and associate it with the log topic. Note that this server group and log topic should be in the same region. For more information, see [Creating a Server Group](https://intl.cloud.tencent.com/document/product/614/17412) under Server Group Management.
![](https://main.qcloudimg.com/raw/67b732e1ae4a099ef247e9e41914986c.png)


### 6. Selecting parsing mode

1. Click **Next** to the Log Parsing Mode page.
2. Select **Full text in a single line** for **Extraction Mode**.
Full text in a single line: marks the end of a log with Enter key. Each log will be parsed into a full string line with \_\_CONTENT\_\_ as the key value. When Log Index is enabled, you can search for log content via full-text search. The collection time is the log time.
![](https://main.qcloudimg.com/raw/5df47173e1921fe3a768299ae35a6767.png)

### 7. Filter conditions

The Filter is designed to help you get useful logs by adding log filtering rules as needed. These rules are Perl regexes that must be matched for logs to be collected.

By default, this Full-text-in-a-single-line mode uses `__CONTENT__` as the key of a log. Assume a sample log is `Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64`, and you want to collect all such logs on Jan 22, then enter `Tue Jan 22.*` under **Filtering Rule**.



>The "AND" logic is used for multiple filtering rules; rules will be written if more than one rule is specified for one key.

### 8. Search results

Log in to the [CLS console](https://console.cloud.tencent.com/cls), and click **Log Search** in the left sidebar. Select **Logset** and **Log Topic** from their drop-down list, and click **Search Analysis** to begin the search.
![img](https://main.qcloudimg.com/raw/c9e348e9b11ecb0c79c58db0da0e139f.png)

>A log topic must have index configuration enabled to be searchable.
