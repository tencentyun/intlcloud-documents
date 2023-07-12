## Overview

A log with full text in a single line means a line is a full log. When CLS collects logs, it uses the line break `\n` to mark the end of a log. For easier structural management, a default key value `__CONTENT__` is given to each log, but the log data itself will no longer be structured, nor will the log field be extracted. The time attribute of a log is determined by the collection time.

## Prerequisites

Suppose your raw log data is:
```plaintext
Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64
```
The log is eventually structured by CLS as follows:
```plaintext
__CONTENT__:Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64
```

## Directions

### Logging in to the console

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Log Topic** to go to the log topic management page.

### Creating a log topic

1. Click **Create Log Topic**.
2. In the pop-up dialog box, enter `test_full` as **Log Topic Name** and click **Confirm**.

### Managing the machine group

1. After the log topic is created successfully, click its name to go to the log topic management page.
2. Click the **Collection Configuration** tab and click the format in which you need to collect logs.
3. On the **Machine Group Management** page, select the server group to which to bind the current log topic and click **Next** to proceed to collection configuration.
For more information, see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).


### Configuring collection

#### Configuring the log file collection path

On the **Collection Configuration** page, set **Collection Path** according to the log collection path format.
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
| ---- | -------------- | ------------ | ------------------------------------------------------------ |
| 1.   | /var/log/nginx | access.log   | In this example, the log path is configured as `/var/log/nginx/**/access.log`. LogListener will listen for log files named `access.log` in all subdirectories in the `/var/log/nginx` prefix path. |
| 2.   | /var/log/nginx | \*.log       | In this example, the log path is configured as `/var/log/nginx/**/*.log`. LogListener will listen for log files suffixed with `.log` in all subdirectories in the `/var/log/nginx` prefix path. |
| 3.   | /var/log/nginx | error\*      | In this example, the log path is configured as `/var/log/nginx/**/error*`. LogListener will listen for log files prefixed with `error` in all subdirectories in the `/var/log/nginx` prefix path. |


>!
> - Only LogListener 2.3.9 and later support adding multiple collection paths.
> - The system does not support uploading logs with contents in multiple text formats, which may cause write failures, such as `key:"{"substream":XXX}"`.
> - We recommend you configure the collection path as `log/*.log` and rename the old file after log rotation as `log/*.log.xxxx`.
> - By default, a log file can only be collected by one log topic. If you want to have multiple collection configurations for the same file, add a soft link to the source file and add it to another collection configuration.
> 

#### Configuring the "full text in a single line" mode

In the **Collection Configuration** page, select **Full text in a single line** as the **Extraction Mode**.

#### Configuring the collection policy

- Full collection: When LogListener collects a file, it starts reading data from the beginning of the file.
- Incremental collection: When LogListener collects a file, it collects only the newly added content in the file.


#### Configuring filter rules

Filters are designed to help you extract valuable log data by adding log collection filter rules based on your business needs. If the filter rule is a Perl regular expression, the created filter rule will be used for matching; in other words, only logs that match the regular expression will be collected and reported.

By default, this "full text in a single line" mode uses `__CONTENT__` as the key name of a log. Assume that a sample log is `Tue Jan 22 12:08:15 CST 2019 Installed: libjpeg-turbo-static-1.2.90-6.el7.x86_64`, and you want to collect all logs on Jan 22, then enter `__CONTENT__` in **Key** and `Tue Jan 22.*` in **Filter Rule**.

>! The relationship logic between multiple filter rules is "AND". If multiple filter rules are configured for the same key name, previous rules will be overwritten.
>

### Configuring indexes

1. Click **Next** to enter the **Index Configuration** page.
2. On the **Index Configuration** page, set the following information:

 - Index Status: Select whether to enable it.
 - Full-Text Index: Select whether to set it to case-sensitive.
 - Full-Text Delimiter: The default value is `@&()='",;:<>[]{}/ \n\t\r` and can be modified as needed.
 - Key-Value Index: Disabled by default. You can configure the field type, delimiters, and whether to enable statistical analysis according to the key name as needed. To enable key-value index, you can set <img src="https://main.qcloudimg.com/raw/bd22396a4acfbf6d96def87060207a46.png" /> to <img src="https://main.qcloudimg.com/raw/d7ba8412e263386b627369741b457f2e.png" />.
>! Index configuration must be enabled before you can perform searches.
>
3. Click **Submit**.

## Related Operations
### Log search
1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Search and Analysis** to go to the search and analysis page.
3. Select the region, logset, and log topic as needed, and click **Search and Analysis** to search for logs according to the set query rules.



