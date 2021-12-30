## Overview

Cloud Log Service (CLS) is a platform service integrating log collection, log storage and log search analysis. CLS centralizes logs for storage management and search analysis. It can also collect data and ship it to COS and other cloud products for further analysis.

To get you started, instructions to the following CLS features are described in this document:

- Collecting logs with LogListener
- Searching logs
- Shipping logs

## Directions

### 1. Activate CLS

First, you need to request to activate [CLS](https://intl.cloud.tencent.com/product/cls) on Tencent Cloud.

### 2. Download and install LogListener  

[LogListener](https://intl.cloud.tencent.com/document/product/614/30449) is a client that collects log data and sends it to CLS in a fast and non-intrusive way. The detailed installation procedures are as follows.

#### 2.1 Check the network connection

To install LogListener, the source server network and CLS network must be able to access each other. Tencent Cloud Virtual Machine (CVM) accesses CLS via the private network by default.
You can run the following command to check the network connectivity, where `<region>` is the abbreviation for the CLS region. For more information about regions, please see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).
```shell
telnet <region abbreviation>.cls.tencentyun.com 80
```

#### 2.2 View/Create a key pair

Log in to [CAM console](https://console.cloud.tencent.com/cam/capi) with your Tencent Cloud account, view (or create) a key pair, and make sure that the key is enabled.


#### 2.3 Install LogListener

In this example, the CLS service runs in the CVM CentOS 7.2 (64-bit) environment. To download and install LogListener, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).

### 3. Create a logset and a log topic 

CLS service is differentiated by region. To lower network latency, try to create log resources in a CLS region closest to your business region. For supported regions, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940). Log resource management involves the management of logsets and log topics. A logset represents a project, while a log topic represents a type of service. A single logset may contain multiple log topics.

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Log Topic** and click **Create Log Topic** to start creating a log topic.
3. Select an existing logset and enter the name of the log topic to create, for example, **nginx_access**. Then the created log topic will be displayed on the log topic list.</br>


### 4. Create a machine group 

CLS uses a [machine group](https://intl.cloud.tencent.com/document/product/614/30449) to manage a list of log source machines.
Log in to the CLS console(https://console.cloud.tencent.com/cls), and click **Machine Group** on the left sidebar to open the machine group management page. Select the appropriate region at the top of the page, and click **Create Machine Group**. A machine group can contain multiple machine IP addresses (one IP address per line). For CVM, enter the private IP address directly. For more information, see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).

After a machine group is created, click **View** in the machine group list to check the connection between the LogListener client and servers. If the status is normal, the LogListener client is successfully connected to CLS. Otherwise, please see [Machine Group Exception](https://intl.cloud.tencent.com/document/product/614/17424) for troubleshooting.

### 5. Configure LogListener 


Log in to the [CLS console](https://console.cloud.tencent.com/cls) and click **Logset** on the left sidebar. Click the logset name/ID, then click the log topic ID/name to go to the log topic management page. Go to the **Collection Configuration** tab, and click **Add Configurations** to specify a collection path, a parsing mode and a server group to bind for your log topic. Here, we only describe how to use LogListener to collect logs. For more information, see [Collection Methods](https://intl.cloud.tencent.com/document/product/614/12502).

#### 5.1 Configure a collection path

The collection path needs to match the absolute path of the log file on the server. You are required to enter two parameters: the directory prefix and the file name in the format of **[directory prefix expression]//\*\*//[file name expression]**. LogListener matches all paths with common prefixes that satisfy the **[directory prefix expression]**, and monitors all log files under these directories (including subdirectories) that satisfy the **[file name expression]**. The parameters are described as follows:

| Parameter     | Description       |
| -------- | ------------------------------------------------------------ |
| Directory Prefix | Directory prefix for log files, which supports only the wildcard characters `\*` and `?`\*` indicates to match any multiple characters. `?` indicates to match any single character. |
| /\*\*/     | Current directory and all its subdirectories.   |
| File Name   | Log file name, which supports only the wildcard characters `\*` and `?`. `\*` indicates to match any multiple characters. `?` indicates to match any single character. |

For example, if the absolute path of the file to be collected is `/cls/logs/access.log`, then the directory prefix entered for the collection path should be `/cls/logs`, and the file name `access.log`, as shown below:


#### 5.2 Bind a machine group

Select an existing machine group, and associate it with the current log topic. Then, LogListener will monitor the log files in this machine group according to the rules you set. You may bind a log topic to multiple machine groups, but a log file will only be collected into one log topic.

#### 5.3 Configure a parsing mode

CLS supports various log parsing modes such as full text in a single line, separator, JSON, and full regex. The following log sample uses the separator mode (for more information, please see [Separator Format](https://intl.cloud.tencent.com/document/product/614/32285)).
```sh
Tue Jan 22 14:49:45 2019;download;success;194;a31f28ad59434528660c9076517dc23b
```
- Selecting an extraction mode
  Select `Separator` for the **Extraction Mode**, and `Semicolon` for the log separator.
- Inputting a sample log and extracting key-value pairs
  Enter a complete log in the log sample field, and key-value pairs will be automatically extracted. Then, you can define a unique key for each key-value pair.
	In this example, the log is parsed into `Tue Jan 22 14:49:45 2019`, `download`, `success`, `194`, and `a31f28ad59434528660c9076517dc23b`. The keys defined for these 5 fields are `time`, `action`, `status`, `size`, and `hashcode` respectively. LogListener will then use this defined structure to collect data.


### 6. Search for logs

#### 6.1 Configure indexes

CLS offers a log search and analysis feature based on segment indexing. We currently offer two index types: full-text index and key-value index. They can be managed on the index configuration tab on the log topic management page. Both index types can be enabled at the same time. 

| Index Type | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Full-Text | Breaks a full log into segments by delimiter, and executes keyword query based on the segments. |
| Key-Value | Breaks a full log into key-value pairs according to the specifications, and executes field query based on the key-value pairs. |

Here we use key-value indexes as an example to describe how to configure indexes. On the log topic management page, go to the **Index Configuration** tab, click **Edit**, and toggle the key to enable index status. Toggle on **Key-Value Index**. Click **Add** to add keys. Select a field type for each key. Currently, `long`, `double`, and `text` are supported. The `text` type allows you to specify delimiters, which separate a character string into segments. Continuing the above example, enter `time`, `action`, `status`, `size`, and `hashcode` as key-value indexes, and set the field type of `size` to `long`.



Once the index rule is enabled, indexes will be created for new input data accordingly, and stored over a specified period of time depending on your configured storage cycle. Only logs for which indexes have been created can be queried for analysis. **Therefore, modifying an index rule or disabling an index only affects new input data. Unexpired legacy data will still be searchable.**

#### 6.2 Search for logs

Log in to the [CLS console](https://console.cloud.tencent.com/cls), and click **Log Search** on the left sidebar to enter the log search page.
Select the time range and log topic before using the search box. The search syntax supports searching by keyword, fuzzy match, and scope. For more information, see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/16981). Now, click **Search Analysis** to begin searching for logs.

- Sample 1: Querying failure logs
  Search statement: `status:fail`

- Sample 2: Querying logs of downloaded files over 300 KB
  Search statement: `action:download and size>300`


### 7. Ship logs to COS

CLS can ship logs to Cloud Object Storage (COS) for long-term storage at a low cost. This also enables you to perform big data analysis offline.

To enable log shipping, you need to first create a [COS bucket](https://intl.cloud.tencent.com/document/product/436/13309). Next, log in to the [CLS console](https://console.cloud.tencent.com/cls) and navigate through the logset management page. Go to the **Shipping Configuration** tab and click **Add Shipping Task** to create a shipping task.
Currently, CLS supports shipping in [CSV format](https://intl.cloud.tencent.com/document/product/614/31582) and [JSON format](https://intl.cloud.tencent.com/document/product/614/31583). Once you create a shipping task, CLS asynchronously ships data to the destination bucket. You can view the shipping status by clicking **Shipping Task** on the left sidebar of the console.

