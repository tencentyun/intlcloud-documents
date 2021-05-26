## Overview

A full RegEx log is a full log with key-value pairs extracted using a regular expression (regex). As an alternative, you can also [collect logs with full text in a single line](https://intl.cloud.tencent.com/document/product/614/32287), or [collecting logs with full text in multi-lines](https://intl.cloud.tencent.com/document/product/614/32284). In this collection mode, you need to enter a sample log, and a custom regex based on which CLS extracts key-values with capturing groups. The following samples provide details on how to collect full RegEx logs.

#### Samples

Suppose the raw data of one of your logs is:

```plaintext
10.135.46.111 - - [22/Jan/2019:19:19:30 +0800] "GET /my/course/1 HTTP/1.1" 127.0.0.1 200 782 9703 "http://127.0.0.1/course/explore?filter%5Btype%5D=all&filter%5Bprice%5D=all&filter%5BcurrentLevelId%5D=all&orderBy=studentNum" "Mozilla/5.0 (Windows NT 10.0; WOW64; rv:64.0) Gecko/20100101 Firefox/64.0"  0.354 0.354
```

The custom regex is:

```plaintext
(\S+)[^\[]+(\[[^:]+:\d+:\d+:\d+\s\S+)\s"(\w+)\s(\S+)\s([^"]+)"\s(\S+)\s(\d+)\s(\d+)\s(\d+)\s"([^"]+)"\s"([^"]+)"\s+(\S+)\s(\S+).*
```

Then CLS extracts key-value pairs based on the `()` capturing groups. You can specify the key name of each group as shown below:

```plaintext
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

> !In this mode, you can extract key-values only into single-line logs, but not multi-line logs. To collect multi-line logs, see [Collecting Logs with Full Text in Multi Lines](https://intl.cloud.tencent.com/document/product/614/32284).

## Collection Configuration

### 1. Logging in to the console

Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and click **Logset** in the left sidebar.

### 2. Adding a log topic

Select a logset you want, click **Add Log Topic**, enter log topic name `test-whole`, and click **OK**. 
![](https://main.qcloudimg.com/raw/e566018c591387497d94221d8fcf8fa2.png)

### 3. Configuring LogListener collection

1. Select the log topic you just created to open the management page.
2. Click the **Collection Configuration** tab, and toggle on **Collection Status** to enter Edit mode.
3. Click **Add Configurations** in the **Loglistener Collection** section to enter the agent configuration page.
![](https://main.qcloudimg.com/raw/d90cc9360d42e71253163dd12cce9c5a.png)

### 4. Configuring a log path

A log path to collect logs from takes the form **[directory prefix expression]**/\*\*/**[file name expression]**. LogListener matches all paths with common prefixes that satisfy the **[directory prefix expression]**, and listen on all log files under these directories (including subdirectories) that satisfy the **[file name expression]**. The detailed parameters are as follows:

| Field     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Directory prefix | The directory prefix of a log file supports only the wildcard characters `\*` and `?`. `\*` indicates that one or more characters can be matched, while `?` indicates that any single character can be matched. |
| /**/   | Current directory and all its subdirectories                                  |
| File name   | Name of a log file; supports only the wildcard characters `\*` and `?`. `\*` indicates that one or more characters can be matched, while `?` indicates that any single character can be matched. |

>?Common configuration patterns include:
>- [Common directory prefix]/\*\*/[Common filename prefix]\*
>- [Common directory prefix]/\*\*/*[Common filename suffix]
>- [Common directory prefix]/\*\*/[Common filename prefix]\*[Common filename suffix]
>- [Common directory prefix]/\*\*/\*[Common string]\*

Examples:

| No. | Directory Prefix Expression | Filename Expression | Description                                                         |
| ---- | -------------- | ------------ | ------------------------------------------------------------ |
| 1.   | /var/log/nginx | access.log   | This example configures the log path to `/var/log/nginx/**/access.log`, so that LogListener will listen on all log files named `access.log` in all the sub-directories prefixed with `/var/log/nginx`. |
| 2.   | /var/log/nginx | \*.log   | This example configures the log path to `/var/log/nginx/**/*.log`, so that LogListener will listen on all log files that end with `.log` in all the sub-directories prefixed with `/var/log/nginx`. |
| 3.   | /var/log/nginx | error\*      | This example configures the log path to `/var/log/nginx/**/error*`, so that LogListener will listen on all log files that begin with `error` in all the sub-directories prefixed with `/var/log/nginx`. |

![](https://main.qcloudimg.com/raw/4807b612fc06f4baeca8014a55f86edd.png)


>!
>1. The configuration of hierarchical directories and wildcards is only available for Loglistener version 2.2.2 or above. In order to be compatible with lower versions, you can modify the old path configuration which does not support hierarchical directories.
>2. A log file will only be collected by one log topic.
>3. LogListener does not collect those log files with symbolic links, or in shared file directories of NFS, CIFS, etc.

### 5. Associating a server group

Select a server group from the server groups list, and associate it with the log topic. Note that this server group and log topic should be in the same region. For more information, see [Server Group Management](https://intl.cloud.tencent.com/document/product/614/17412) .
![](https://main.qcloudimg.com/raw/5bb42e4d8501b6a23e1b98cc7135d874.png)

### 6. Configuring the parsing mode

1. Click **Next** to the Log Parsing Mode page.
2.  Select **Full RegEx** for **Extraction Mode**.


#### 6.1 Defining RegEx

In this parsing mode, you can let CLS automatically extract key-value pairs using a predefined regex, or you can manually generate and verify a custom regex.
- Auto method
 a. Enter a sample log.
 b. Select part of the log content as needed, and click **Group**. A grouped part will be highlighted and to be extracted as a key-value pair.
 c. Repeat Step b until you get all the key-value pairs you want.
 d. Click **Auto-Generate** to generate a full RegEx log.

- Manual method
 a. Enter a sample log.
 b. Enter a regex manually.
 c. Click **Verify** to check if the sample log matches the regex.

>Both methods display search results below the regex once it is set correctly. You need to define a key name for each key-value pair for use in future log searches.

### 7. Configuring collection time
- Log time is measured in seconds.
- The time attribute of a log is defined in two ways: collection time and original timestamp.
- Collection time: the time attribute of a log; determined by the time when CLS collects the log.
- Original timestamp: the time attribute of a log; determined by the timestamp in the original log.

#### 7.1 Using the collection time as the time attribute of logs

Simply enable collection time as shown below:


#### 7.2 Using the original timestamp as the time attribute of logs

Disable collection time, and instead, enter the time key and parsing format of the original timestamp. For more information, see [Configuring Time Format](https://intl.cloud.tencent.com/document/product/614/32942).


The examples below show how to specify time parsing formats:  
Example 1: original timestamp: `10/Dec/2017:08:00:00`; parsing format: `%d/%b/%Y:%H:%M:%S`.
Example 2: original timestamp: `2017-12-10 08:00:00`; parsing format: `%Y-%m-%d %H:%M:%S`.
Example 3: original timestamp: `12/10/2017, 08:00:00`; parsing format: `%m/%d/%Y, %H:%M:%S`.

>!Second can be used as the unit of log time. If the time is entered in a wrong format, the collection time is used as the log time.

### 8. Setting filter conditions

The Filter is designed to help you get useful logs by adding filtering rules for log collection as needed. These rules are Perl regexes that must be matched for logs to be collected.

To collect full RegEx logs, you need to set filtering rules based on the custom key-value pairs. For example, to collect all logs with the `status` field as 400 or 500, enter `status` under **Key**, and `400|500` under **Filtering Rule**.

>! The "AND" logic is used for multiple filtering rules; rules will be written if more than one rule is specified for one key.

### 9. Searching logs

Log in to the [CLS console](https://console.cloud.tencent.com/cls), and click **Log Search** in the left sidebar. Select **Logset** and **Log Topic** from their drop-down list, and click **Search Analysis** to begin the search.


> !A log topic must have index configuration enabled to be searchable.
