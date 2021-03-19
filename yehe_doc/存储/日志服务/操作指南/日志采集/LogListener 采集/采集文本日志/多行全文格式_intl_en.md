## Overview

A log with full text in multi lines spans multiple lines in a log text file (such as Java program logs). In this mode, the line break `\n` cannot be used as the end mark of a log. To help CLS distinguish between the logs, the "first-line regular expression" is used for match. When a log in a line matches the preset regular expression, it is considered as the beginning of a log, and the next matching line will be the end mark of the log.

In the mode of full text in multi lines, a default key `__CONTENT__` is also set, but the log data itself is not structured, and no log fields are extracted. The time attribute of a log is determined by the collection time.

#### Sample

Suppose your raw multi-line log data is:
```plaintext
10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 
Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0 0.310 0.310
```

The log is eventually structured by CLS as:
```plaintext
__CONTENT__:10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 \nMozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0  0.310 0.310
```

## Collection Configuration

### 1. Log in to the console

Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Logset** on the left sidebar.

### 2. Create LogListener collection

Select the target logset, click **Create Log Topic**, enter the log topic name "test-mtext", and click **OK**.

### 3. Configure LogListener collection

1. Select the log topic collected by LogListener to enter the log topic management page.
2. Select the **Collection Configuration** tab and click the collection status switch to enter the collection configuration editing mode.
3. In the **LogListener Collection Configuration** item, click **Add Configuration** to enter the Agent configuration page.


### 4. Configure the log file collection path

The log collection path is in the format of **[directory prefix expression]**/\*\*/**[filename expression]**. LogListener will match all common prefix paths that meet the **[directory prefix expression]** rule and listen on all log files in the directories (including subdirectories) that meet the **[filename expression]** rule. The parameters are as detailed below:

| Field     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Directory prefix | Directory structure of the log file prefix. Only wildcards `\*` and `?` are supported. `\*` indicates to match any number of characters, while `?` indicates to match any single character |
| /**/     | Current directory and all its subdirectories                                   |
| Filename   | Log file name. Only wildcards `\*`  and `?` are supported. `\* indicates to match any number of  characters, while `?` indicates to match any single character |

>? Common configuration modes are as follows:
>- [Common directory prefix]/\*\*/[common filename prefix]\*
>- [Common directory prefix]/\*\*/*[common filename suffix]
>- [Common directory prefix]/\*\*/[common filename prefix]\*[common filename suffix]
>- [Common directory prefix]/\*\*/\*[Common string]\*

Samples:

| No. | Directory Prefix Expression | Filename Expression | Description                                                         |
| ---- | -------------- | ------------ | ------------------------------------------------------------ |
| 1.   | /var/log/nginx | access.log   | In this example, the log path is configured as `/var/log/nginx/**/access.log`. LogListener will listen on log files named `access.log` in all subdirectories in the `/var/log/nginx` prefix path |
| 2.   | /var/log/nginx | \*.log       | In this example, the log path is configured as `/var/log/nginx/**/*.log`. LogListener will listen on log files suffixed with `.log` in all subdirectories in the `/var/log/nginx` prefix path |
| 3.   | /var/log/nginx | error\*      | In this example, the log path is configured as `/var/log/nginx/**/error*`. LogListener will listen on log files prefixed with `error` in all subdirectories in the `/var/log/nginx` prefix path |

>!
> - Only LogListener 2.3.9 or above allows adding multiple collection paths.
> - By default, a log file can only be collected by one log topic. If you want to have multiple collection configurations for the same file, please add a soft link to the source file and add it to another collection configuration.
> 

### 5. Associate a machine group

Select the target machine group from the machine group list and associate it with the current log topic. Please note that the associated machine group must be in the same region as the log topic. For detailed directions, please see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).

### 6. Select the full text in multi lines mode


1. Click **Next** to configure the log parsing mode.
2. Select **Full text in multi lines** as **Extraction Mode** as shown below:

**Auto-generate full text in multi lines**:
a. Select **Full text in multi lines** as the key-value extraction mode.
b. Paste a single multi-line log in the log file into the dialog box, and the system will automatically extract the content of the matched first line and highlight it.
c. Click **Auto-Generate**.
d. The regular expression is populated automatically to complete the configuration.

**Manually enter full text in multi lines**:
a. Select **Full text in multi lines** as the key-value extraction mode.
b. Paste a single multi-line log in the log file into the dialog box, and the system will automatically extract the content of the matched first line and highlight it.
c. Manually enter the first-line regular expression and click **Verify**.
d. After the verification is passed, the configuration is completed.


### 7. Set a filter

Filters are designed to help you extract valuable log data by adding log collection filter rules based on your business needs. If the filter rule is a Perl regular expression, the created filter rule will be a hit rule; in other words, only logs that match the regular expression will be collected and reported.

In the mode of full text in multi lines, `__CONTENT__` is used as the `key` name of the full text by default. For example, below is a sample log with full text in multi lines:
```plaintext
10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 
Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0 0.310 0.310
```
If you want to collect all logs of the machine `10.20.20.10`, enter `__CONTENT__` in the `key` field and configure the filter rule `10.20.20.10.*`.

>! The relationship between multiple filter rules is logic "AND". If multiple filter rules are configured for the same key name, previous rules will be overwritten.
>

### 8. Search for logs

Log in to the [CLS console](https://console.cloud.tencent.com/cls), click **Log Search**, select the target logset and log topic, and click **Search** to search for logs.

>! Index configuration must be enabled first before you can perform searches.
>
