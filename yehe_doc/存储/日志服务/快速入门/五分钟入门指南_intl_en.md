## Overview

Cloud Log Service (CLS) is a platform service integrating log collection, log storage and log search analysis. CLS collects separate logs for central storage management and search analysis. It can also collect data and ship it to COS and other cloud products for further analysis.

To help you get started, this document will describe how to use the primary features of CLS, including:

- How to collect logs with LogListener
- How to search logs
- How to ship logs

## Directions

### 1. Activating CLS

First, you need to apply for activation of [CLS](https:/intl.cloud.tencent.com/product/cls) on the official website of Tencent Cloud.

### 2. Downloading and installing LogListener  

[LogListener](https://intl.cloud.tencent.com/document/product/614/30449) is a client that collects log data and sends it to CLS in a fast and non-intrusive way. The detailed installation procedures are as follows.

#### 2.1 Determining if the networks are reachable

Installing LogListener requires the network of the log source server and the available region network of CLS to be inter-reachable. Tencent Cloud Virtual Machine (CVM) accesses CLS via the private network by default.
You may execute the following command to check the network connectivity, among which `<region>` is the short form for CLS region. For detailed region information, please see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).
```shell
telnet <region>.cls.myqcloud.com 80
```

#### 2.2 Viewing (or Creating) a key pair

Log in to [CAM Console](https://console.cloud.tencent.com/cam/capi) with your Tencent Cloud account, view (or create) a key pair, and make sure that the key is enabled.
![](https://main.qcloudimg.com/raw/5da40a4e08e052ea6935038960ee563e.png)

#### 2.3 Installing LogListener

In this example, the CLS service runs in the CVM CentOS 7.2 (64-bit) environment. To download and install LogListener, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).

### 3. Creating a logset and a log topic 

CLS is managed by regions. To lower network latency, try to create log resources in a CLS region closest to your business region. For supported regions, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940). Log resource management involves management of logsets and log topics. A logset represents a project, while a log topic represents a type of service. A single logset may contain multiple log topics.

#### 3.1 Creating a logset

Log in to the [CLS Console](https://console.cloud.tencent.com/cls). Click **Logset** in the left sidebar to enter the logset management page. Select a region you see fit at the top, and click **Create Logset**.
For example, if you created a logset named `cls_project`, it will appear in the logset list as shown below:
![](https://main.qcloudimg.com/raw/f1a918059ef2da5868fabbaa4e199a26.png)

#### 3.2 Creating a log topic

Click the logset name to open the log topic management page. Click **Add Log Topic** to start creating a log topic, e.g. a log topic named `nginx_access`. Once completed, the new log topic can appear in the log topic list.
![](https://main.qcloudimg.com/raw/012e53bd7b979c7e250c067cc175e04c.png)

### 4. Creating a server group 

CLS uses a [server group](https://intl.cloud.tencent.com/document/product/614/30449) to manage a list of log source servers.
Log in to the CLS Console(https://console.cloud.tencent.com/cls), and click **Server Group** in the left sidebar to open the server group management page. Select the appropriate region at the top of the page, and click **Create Server Group**. A server group can contain multiple server IP addresses (one IP address per line). For CVM, enter the private IP address directly. For more information, see [Server Group Management](https://intl.cloud.tencent.com/document/product/614/17412).

Once created, click **View** in the server group list to check the status of LogListener connection to the CLB service. If the status is normal, the client LogListener has been connected to CLS successfully. Otherwise, please see [Server Group Exception](https://intl.cloud.tencent.com/document/product/614/17424) for troubleshooting.
![image](https://main.qcloudimg.com/raw/3a3e3eca80cfb7e86b787e4800db3708.png)

### 5. Configuring LogListener 


Log in to the [CLS Console](https://console.cloud.tencent.com/cls), click **Logset** in the left sidebar, and open your logset and log topic management pages in sequence. In the log topic management page, select the **Collection Configuration** tab, and specify a collection path, a parsing mode and a server group to bind for your log topic. Here, we only describe how to use LogListener to collect logs. For more information, see [Collection Methods](https://intl.cloud.tencent.com/document/product/614/12502).

#### 5.1 Configuring a collection path

The collection path needs to match the absolute path of the log file on the server. You are required to enter two parameters: directory prefix and file name in the format of **[directory prefix expression]//\*\*//[file name expression]**. LogListener matches all paths with common prefixes that satisfy the **[directory prefix expression]**, and monitors all log files under these directories (including subdirectories) that satisfy the **[file name expression]**. The detailed parameter description is as follows:

| Field     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Directory prefix | The directory prefix of a log file supports only the wildcard characters `\*` and `?`. `\*` indicates that one or more characters can be matched, while `?` indicates that any single character can be matched. |
| /\*\*/     | Current directory and all its subdirectories                                  |
| File name   | A log file name supports only the wildcard characters `\*` and `?`. `\*` indicates that one or more characters can be matched, while `?` indicates that any single character can be matched. |

For example, if the absolute path of the file to be collected is `/cls/logs/access.log`, then the directory prefix entered for the collection path should be `/cls/logs`, and the file name `access.log`, as shown below:
![image](https://main.qcloudimg.com/raw/20d2f44e3e1b8b60c02ebb772dba1f59.png)

#### 5.2 Binding a server group

Select an existing server group, and associate it with the current log topic. Then, LogListener will monitor the log files in this server group by the rules you set. You may bind a log topic to multiple server groups, but report a log file to only one log topic.

#### 5.3 Configuring a parsing mode

CLS provides various log parsing modes, e.g. full text in a single line, separator, JSON, complete regex, etc. Take the separator mode as an example (For more information, see [separator format](https://intl.cloud.tencent.com/document/product/614/32285)), and the sample log will be like:
```sh
Tue Jan 22 14:49:45 2019;download;success;194;a31f28ad59434528660c9076517dc23b
```
- Selecting an extraction mode
  Take separator-formatted logs as an example: select Separator for **Key-Value Extraction Mode**, and Semicolon for log separator.
- Inputting a sample log and extracting key-value pairs
  Enter a full log in the sample log field, and key-value pairs will be automatically extracted. Then, you can define a unique key for each key-value pair.
	In this example, the log is parsed into `Tue Jan 22 14:49:45 2019`, `download`, `success`, `194`, and `a31f28ad59434528660c9076517dc23b`. The keys defined for these 5 fields are `time`, `action`, `status`, `size`, and `hashcode` in sequence. LogListener will then use this defined structure to collect data.
![](https://main.qcloudimg.com/raw/9d498fdbb6d3e9773cac3bd8e6a3c273.png)

### 6. Searching logs

#### 6.1 Configuring indexes

CLS offers a log search and analysis feature that mainly depends on segment indexing. Currently, there are two types, full-text index and key-value index. You can enable both indexes and manage them from the index configuration page under a log topic.

| Index Type | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Full-Text | Divides a full log into segments by delimiter, and executes keyword query based on the segments |
| Key-Value | Divides a full log into key-value pairs by the specified mode, and executes field query based on the key-value pairs |

This section uses key-value index as an example to describe how to configure indexes. In the log topic management page, select the **Index Configuration** tab, click Edit, and toggle on **Key-Value Index**. Next, enter the fields (keys) you want to search, and for each field (key), select a field type, which currently supports `long`, `double`, and `text`. The `text` type allows you to specify delimiters, which separate a character string into segments.) Continuing to use the above example, enter `time`, `action`, `status`, `size`, and `hashcode` as key-value indexes, and set the field type of `size` to `long`.
![](https://main.qcloudimg.com/raw/17412e632d973788dc12a482a51c61fc.png)


Once the index rule is enabled, indexes will be created for new input data by the rule, and stored over a certain period of time (depending on the storage cycle you configure). Only logs for which indexes have been created can be queried for analysis. **Therefore, modifying an index rule or disabling an index only affects new input data, while some old data may also be searched.**

#### 6.2 Searching logs

Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and click **Log Search** in the left sidebar to enter the log search page.
Select the time range and log topic to search, then enter the search syntax in the input box. The syntax supports search by keyword, fuzzy match, and scope. For more information, see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439). Now, click **Search** to begin searching for logs.

- Sample 1: Querying failure logs
  Search statement: `status:fail`
![](https://main.qcloudimg.com/raw/2030b7b0b6cdd506a45ae3c16cc582c7.png)
- Sample 2: Querying logs of downloaded files over 300 KB
  Search statement: `action:download and size>300`
![](https://main.qcloudimg.com/raw/dca434bd2571fc77aa1f3ecff610e05d.png)

### 7. Shipping logs to COS

CLS can ship logs to Cloud Object Storage (COS) to store for a long time at a low cost while performing offline big data analysis.

To enable log shipping, you need to create a [COS bucket](https://intl.cloud.tencent.com/document/product/436/13309), and log in to the [CLS Console](https://console.cloud.tencent.com/cls). Then, navigate through the logset management page to the **Shipping Configuration** tab, and click **Add Shipping Task** to create a shipping task.
Currently, CLS supports shipping in [CSV format](https://intl.cloud.tencent.com/document/product/614/31582) and [JSON format](https://intl.cloud.tencent.com/document/product/614/31583). Once you created a shipping task, CLS asynchronously ships data to the destination bucket. You can view the shipping status in **Shipping Task Management** in the left sidebar of the console.
![](https://main.qcloudimg.com/raw/c9e92b7a0a5f2e0423c60c285ea16d93.png)
