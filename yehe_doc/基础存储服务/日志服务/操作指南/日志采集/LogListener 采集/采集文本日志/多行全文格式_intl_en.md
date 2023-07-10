## Overview

In "full text in multi lines" mode, a log spans multiple lines (such as a Java program log), and the line break `\n` cannot be used to mark the end of a log. To help CLS distinguish between logs, a first-line regular expression is used for matching. When a line of a log matches the preset regular expression, it is considered as the beginning of the log, and the log ends before the next matching line.

In "full text in multi lines" mode, a default key `__CONTENT__` is also set, but the log data itself is not structured, and no log fields are extracted. The time attribute of a log is determined by the collection time.

## Prerequisites

Assume the raw data of a multi-line log is:
```plaintext
10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 
Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0 0.310 0.310
```
The log is eventually structured by CLS as follows:
```plaintext
__CONTENT__:10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 \nMozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0  0.310 0.310
```

## Directions

### Logging in to the console

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Log Topic** to go to the log topic management page.

### Creating a log topic

1. Click **Create Log Topic**.
2. In the pop-up dialog box, enter `test-mtext` as **Log Topic Name** and click **Confirm**.

### Managing the machine group

1. After the log topic is created successfully, click its name to go to the log topic management page.
2. Click the **Collection Configuration** tab, click **Add** in **LogListener Collection Configuration**, and select the format in which you need to collect logs.
3. On the **Machine Group Management** page, select the server group to which to bind the current log topic and click **Next** to proceed to collection configuration.
For more information, see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).


### Configuring collection

#### Configuring the log file collection path

On the **Collection Configuration** page, enter the collection rule name and enter the **Collection Path** according to the **log collection path format**.
Log collection path format: `[directory prefix expression]/**/[filename expression]`.

After the log collection path is entered, LogListener will match all common prefix paths that meet the **[directory prefix expression]** rule and listen for all log files in the directories (including subdirectories) that meet the **[filename expression]** rule. The parameters are as detailed below:

| Parameter     | Description       |
| -------- | ------------------------------------------------------------ |
| Directory Prefix | Directory prefix for log files, which supports only the wildcard characters `\*` and `?`.<ul style="margin: 0;"><li>`\*` indicates to match any multiple characters.</li><li>`?` indicates to match any single character.</li></ul> |
| /\*\*/     | Current directory and all its subdirectories.   |
| File Name   | Log file name, which supports only the wildcard characters `\*` and `?`.<ul style="margin: 0;"><li>`\*` indicates to match any multiple characters.</li><li>`?` indicates to match any single character.</li></ul> |

Common configuration modes are as follows:
- [Common directory prefix]/\*\*/[common filename prefix]\*
- [Common directory prefix]/\*\*/\*[common filename suffix]
- [Common directory prefix]/\*\*/[common filename prefix]\*[common filename suffix]
- [Common directory prefix]/\*\*/\*[common string]\*

Below are examples:

| No. | Directory Prefix Expression | Filename Expression | Description                                                         |
| :--- | :------------- | :----------- | :----------------------------------------------------------- |
| 1.   | /var/log/nginx | access.log   | In this example, the log path is configured as `/var/log/nginx/**/access.log`. LogListener will listen for log files named `access.log` in all subdirectories in the `/var/log/nginx` prefix path. |
| 2.   | /var/log/nginx | *.log        | In this example, the log path is configured as `/var/log/nginx/**/*.log`. LogListener will listen for log files suffixed with `.log` in all subdirectories in the `/var/log/nginx` prefix path. |
| 3.   | /var/log/nginx | error*       | In this example, the log path is configured as `/var/log/nginx/**/error*`. LogListener will listen for log files prefixed with `error` in all subdirectories in the `/var/log/nginx` prefix path. |

>!
> - Only LogListener 2.3.9 and later support adding multiple collection paths.
> - The system does not support uploading logs with contents in multiple text formats, which may cause write failures, such as `key:"{"substream":XXX}"`.
> - We recommend you configure the collection path as `log/*.log` and rename the old file after log rotation as `log/*.log.xxxx`.
> - By default, a log file can only be collected by one log topic. If you want to have multiple collection configurations for the same file, add a soft link to the source file and add it to another collection configuration.
> 

#### Configuring the collection policy

- Full collection: When LogListener collects a file, it starts reading data from the beginning of the file.
- Incremental collection: When LogListener collects a file, it collects only the newly added content in the file.

#### Configuring the "full text in multi lines" mode

1. On the **Collection Configuration** page, select **Full text in multi lines** as the **Extraction Mode**.

2. Define a regular expression according to the following rules.
You can choose **Auto-Generate** or **Enter Manually** to define a first-line regular expression, and the system will verify the regular expression based on the sample content.
 - **Auto-Generate**: Enter the sample log in the text box, click **Auto-Generate**, and the system will automatically generate the first-line regular expression in the grayed-out text box.

 - **Enter Manually**: Enter the sample log and first-line regular expression in the text box, click **Verify**, and the system will determine whether the expression has passed verification.



#### Configuring filter rules

Filters are designed to help you extract valuable log data by adding log collection filter rules based on your business needs. If the filter rule is a Perl regular expression, the created filter rule will be used for matching; in other words, only logs that match the regular expression will be collected and reported.

In "full text in multi lines" mode, `__CONTENT__` is used as the key name of a log by default. For example, below is a sample log with full text in multi lines:
```plaintext
10.20.20.10 - - [Tue Jan 22 14:24:03 CST 2019 +0800] GET /online/sample HTTP/1.1 127.0.0.1 200 628 35 http://127.0.0.1/group/1 
Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0 0.310 0.310
```
If you want to collect all logs of the machine `10.20.20.10`, enter `__CONTENT__` in **Key** and `10.20.20.10.*` in **Filter Rule**.

>! The relationship logic between multiple filter rules is "AND". If multiple filter rules are configured for the same key name, previous rules will be overwritten.
>

#### Configuring parsing-failed log upload

We recommend you enable **Upload Parsing-Failed Logs**. After it is enabled, LogListener will upload all types of parsing-failed logs. If it is disabled, such logs will be discarded.

After this feature is enabled, you need to configure the `Key` value for parsing failures (which is `LogParseFailure` by default). All parsing-failed logs are uploaded with the input content as the key name (`Key`) and the raw log content as the key value (`Value`).


### Configuring indexes

1. Click **Next** to enter the **Index Configuration** page.
2. On the **Index Configuration** page, set the following information:

 - Index Status: Select whether to enable it.
>! Index configuration must be enabled before you can perform searches.
>
 - Full-Text Index: Select whether to set it to case-sensitive.
 - Full-Text Delimiter: The default value is `@&()='",;:<>[]{}/ \n\t\r` and can be modified as needed.
 - Key-Value Index: Disabled by default. You can configure the field type, delimiters, and whether to enable statistical analysis according to the key name as needed. To enable key-value index, you can set <img src="https://main.qcloudimg.com/raw/bd22396a4acfbf6d96def87060207a46.png" /> to <img src="https://main.qcloudimg.com/raw/d7ba8412e263386b627369741b457f2e.png" />.
3. Click **Submit**.

## Related Operations

For more information on log search, see [Overview and Syntax Rules](https://intl.cloud.tencent.com/document/product/614/37803).
