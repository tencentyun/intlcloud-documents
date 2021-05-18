## Overview

In a separator log, the entire log data can be structured according to the specified separator, and each complete log ends with a line break `\n`. When CLS processes separator logs, you need to define a unique key for each separate field.

#### Sample

Suppose your raw log data is:

```plaintext
10.20.20.10 - ::: [Tue Jan 22 14:49:45 CST 2019 +0800] ::: GET /online/sample HTTP/1.1 ::: 127.0.0.1 ::: 200 ::: 647 ::: 35 ::: http://127.0.0.1/
```

If the separator for log parsing is specified as `:::`, the log will be segmented into eight fields, and a unique key will be defined for each of them as shown below:

```plaintext
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

### 1. Log in to the console

Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Logset** on the left sidebar.

### 2. Create LogListener collection

Select the target logset, click **Create Log Topic**, enter the log topic name "test-separator", and click **OK**.

### 3. Configure LogListener collection

1. Select the log topic collected by LogListener to enter the log topic management page.
2. Select the **Collection Configuration** tab and click the collection status switch to enter the collection configuration editing mode.
3. In the **LogListener Collection Configuration** item, click **Add Configuration** to enter the agent configuration page.

### 4. Configure the log file collection path

The log collection path is in the format of **[directory prefix expression]**/\*\*/**[filename expression]**. LogListener will match all common prefix paths that meet the **[directory prefix expression]** rule and listen on all log files in the directories (including subdirectories) that meet the **[filename expression]** rule. The parameters are as detailed below:

| Field     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Directory prefix | Directory structure of the log file prefix. Only wildcards `\*` and `?` are supported. `\*` indicates to match any number of characters, while `?` indicates to match any single character |
| /**/     | Current directory and all its subdirectories                                   |
| Filename   | Log file name. Only wildcards `\*`  and `?` are supported. `\* indicates to match any number of characters, while `?` indicates to match any single character |

>? Common configuration modes are as follows:
> - [Common directory prefix]/\*\*/[common filename prefix]\*
> - [Common directory prefix]/\*\*/*[common filename suffix]
> - [Common directory prefix]/\*\*/[common filename prefix]\*[common filename suffix]
> - [Common directory prefix]/\*\*/\*[Common string]\*

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

Select the target machine group from the machine group list and associate it with the current log topic. Please note that the associated machine group must be in the same region as the log topic. For detailed directions, please see [Server Group Management](https://intl.cloud.tencent.com/document/product/614/17412).

### 6. Select the separator mode

1. Click **Next** to configure the log parsing mode.
2. Select **Separator** as **Extraction Mode** as shown below:


### 7. Select a separator

You need to select a unique separator first. The system segments the sample log according to the selected separator and displays it in the extraction result box. You need to define a unique key for each field. Currently, log collection supports a variety of separators. Common separators include space, tab, comma, semicolon, and vertical bar. If your log data uses other separators such as `:::` , it can also be parsed through custom delimiter.

### 8. Configure the collection time

The time configuration is as described below:

 - Log time is measured in seconds.
 - The time attribute of a log is defined in two ways: collection time and original timestamp.
 - Collection time: the time attribute of a log is determined by the time when CLS collects it.
 - Original timestamp: the time attribute of a log is determined by the timestamp in the raw log.

#### 8.1. Use the collection time as the time attribute of logs

Keep **Collection Time** enabled as shown below:

#### 8.2. Use the original timestamp as the time attribute of logs

Disable **Collection Time** and enter the time key of the original timestamp and the corresponding time parsing format in **Time Key** and **Time Parsing Format** respectively. For more information on the time parsing format, please see [Configuring Time Format](https://intl.cloud.tencent.com/document/product/614/32942).

Below are examples of how to enter a time parsing format:
Example 1: if the original timestamp of the sample log is `10/Dec/2017:08:00:00`, then the parsing format is `%d/%b/%Y:%H:%M:%S`.
Example 2: if the original timestamp of the sample log is `2017-12-10 08:00:00`, then the parsing format is `%Y-%m-%d %H:%M:%S`.
Example 3: if the original timestamp of the sample log is `12/10/2017, 08:00:00`, then the parsing format is `%m/%d/%Y, %H:%M:%S`.

>! You can set "second" as the log time unit. If you enter a log time with incorrect format, the collection time will be used as the log time.
>

### 9. Set a filter

Filters are designed to help you extract valuable log data by adding log collection filter rules based on your business needs. If the filter rule is a Perl regular expression, the created filter rule will be a hit rule; in other words, only logs that match the regular expression will be collected and reported.

You need to configure a filter rule for separator logs according to the defined custom key-value pair. For example, if you want to collect all log data with a `status` field whose value is 400 or 500 after the sample log is parsed in separator mode, you need to configure `key` as `status` and the filter rule as `400|500`.

>! The relationship between multiple filter rules is logic "AND". If multiple filter rules are configured for the same key name, previous rules will be overwritten.
>

### 10. Search for logs

Log in to the [CLS console](https://console.cloud.tencent.com/cls), select **Log Search** on the left sidebar, select the target logset and log topic, and click **Search** to search for logs.

>! Index configuration must be enabled first before you can perform searches.
>
