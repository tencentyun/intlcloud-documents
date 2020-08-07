## Overview

Cloud Log Service (CLS) is a platform service integrating log collection, log storage and log search analysis. CLS centralizes logs for storage management and search analysis. It can also collect data and ship it to COS and other cloud products for further analysis.

To help you get started, this document will describe how to use the primary features of CLS, including:

- How to collect logs with LogListener
- How to search logs
- How to ship logs

## Directions

### 1. Activating CLS

First, you need to request to activate [CLS](https:/intl.cloud.tencent.com/product/cls) on Tencent Cloud.

### 2. Downloading and installing LogListener  

[LogListener](https://intl.cloud.tencent.com/document/product/614/30449) is a client that collects log data and sends it to CLS in a fast and non-intrusive way. The detailed installation procedures are as follows.

#### 2.1 Determining if the networks can access each other

To install LogListener, the source server network and CLS network must be able to access each other. Tencent Cloud Virtual Machine (CVM) accesses CLS via the private network by default.
Execute the following command to check the network connectivity. `<region>` uses the abbreviation for CLS region. For detailed region information, please see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).
```shell
telnet <region>.cls.myqcloud.com 80
```

#### 2.2 Viewing (or Creating) a key pair

Log in to [CAM Console](https://console.cloud.tencent.com/cam/capi) with your Tencent Cloud account, view (or create) a key pair, and make sure that the key is enabled.
![](https://main.qcloudimg.com/raw/5da40a4e08e052ea6935038960ee563e.png)

#### 2.3 Installing LogListener

In this example, the CLS service runs in the CVM CentOS 7.2 (64-bit) environment. To download and install LogListener, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).

### 3. Creating a logset and a log topic 

CLS service is differentiated by regions. To lower network latency, try to create log resources in a CLS region closest to your business region. For supported regions, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940). Log resource management involves management of logsets and log topics. A logset represents a project, while a log topic represents a type of service. A single logset may contain multiple log topics.

#### 3.1 Creating a logset

Log in to the [CLS Console](https://console.cloud.tencent.com/cls). Click **Logset** in the left sidebar to enter the logset management page. Select a suitable region from the top, and click **Create Logset**.
For example, if you created a logset named `cls_project`, it will appear in the logset list as shown below:
![](https://main.qcloudimg.com/raw/f1a918059ef2da5868fabbaa4e199a26.png)

#### 3.2 Creating a log topic

Click the logset name to open the log topic management page. Click **Add Log Topic** to start creating a log topic, e.g. a log topic named `nginx_access`. Once completed, the new log topic will appear in the log topic list.
![](https://main.qcloudimg.com/raw/012e53bd7b979c7e250c067cc175e04c.png)

### 4. Creating a server group 

CLS uses a [server group](https://intl.cloud.tencent.com/document/product/614/30449) to manage a list of log source servers.
Log in to the CLS Console(https://console.cloud.tencent.com/cls), and click **Server Group** in the left sidebar to open the server group management page. Select the appropriate region at the top of the page, and click **Create Server Group**. A server group can contain multiple server IP addresses (one IP address per line). For CVM, enter the private IP address directly. For more information, see [Server Group Management](https://intl.cloud.tencent.com/document/product/614/17412).

Once created, click **View** to check the status of LogListener connection to the CLB service. If the status is normal, the LogListener client has connected to CLS successfully. Otherwise, please see [Server Group Exception](https://intl.cloud.tencent.com/document/product/614/17424) for troubleshooting.
![image](https://main.qcloudimg.com/raw/3a3e3eca80cfb7e86b787e4800db3708.png)

### 5. Configuring LogListener 


Log in to the [CLS Console](https://console.cloud.tencent.com/cls) and click **Logset** in the left sidebar. Click the logset name/ID, then click the log topic ID/name to go to the log topic management page. Go to the **Collection Configuration** tab, and click **Add Configurations** to specify a collection path, a parsing mode and a server group to bind for your log topic. Here, we only describe how to use LogListener to collect logs. For more information, see [Collection Methods](https://intl.cloud.tencent.com/document/product/614/12502).

#### 5.1 Configuring a collection path

The collection path needs to match the absolute path of the log file on the server. You are required to enter two parameters: the directory prefix and the file name in the format of **[directory prefix expression]//\*\*//[file name expression]**. LogListener matches all paths with common prefixes that satisfy the **[directory prefix expression]**, and monitors all log files under these directories (including subdirectories) that satisfy the **[file name expression]**. The detailed parameter description is as follows:

| Field     | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Directory prefix | The directory prefix of a log file supports only the wildcard characters `\*` and `?`. `\*` indicates that one or more characters can be matched, while `?` indicates that any single character can be matched. |
| /\*\*/     | Current directory and all its subdirectories                                  |
| File name   | A log file name supports only the wildcard characters `\*` and `?`. `\*` indicates that one or more characters can be matched, while `?` indicates that any single character can be matched. |

For example, if the absolute path of the file to be collected is `/cls/logs/access.log`, then the directory prefix entered for the collection path should be `/cls/logs`, and the file name `access.log`.

#### 5.2 Binding a server group

Select an existing server group, and associate it with the current log topic. Then, LogListener will monitor the log files in this server group according to the rules you set. You may bind a log topic to multiple server groups, but a log file will only be collected into one log topic.

#### 5.3 Configuring a parsing mode

CLS provides various log parsing modes, e.g. full text in a single line, separator, JSON, complete regex, etc. Here we use the separator mode as an example. See below for the sample log. For more information, see [Collecting CSV Logs](https://intl.cloud.tencent.com/document/product/614/32285).
```sh
Tue Jan 22 14:49:45 2019;download;success;194;a31f28ad59434528660c9076517dc23b
```
- Selecting an extraction mode
  Select `Separator` for the **Extraction Mode**, and `Semicolon` for the log separator.
- Inputting a sample log and extracting key-value pairs
  Enter a complete log in the log sample field, and key-value pairs will be automatically extracted. Then, you can define a unique key for each key-value pair.
	In this example, the log is parsed into `Tue Jan 22 14:49:45 2019`, `download`, `success`, `194`, and `a31f28ad59434528660c9076517dc23b`. The keys defined for these 5 fields are `time`, `action`, `status`, `size`, and `hashcode` respectively. LogListener will then use this defined structure to collect data.
![](https://main.qcloudimg.com/raw/9d498fdbb6d3e9773cac3bd8e6a3c273.png)

### 6. Searching logs

#### 6.1 Configuring indexes

CLS offers a log search and analysis feature based on segment indexing. We currently offer two index types, full-text index and key-value index. They can be managed on the index configuration tab in the log topic management page. Both indexes can be enabled at the same time. 

| Index Type | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Full-Text | Breaks a full log into segments by delimiter, and executes keyword query based on the segments |
| Key-Value | Breaks a full log into key-value pairs according to the specifications, and executes field query based on the key-value pairs |

Here we use key-value index as an example to describe how to configure indexes. In the log topic management page, go to the **Index Configuration** tab, click **Edit**, and toggle the key to enable index status. Toggle on **Key-Value Index**. Click **Add** to add keys. Select a field type for each key, currently `long`, `double`, and `text` are supported. `text` type allows you to specify delimiters, which separate a character string into segments. Continuing the above example, enter `time`, `action`, `status`, `size`, and `hashcode` as key-value indexes, and set the field type of `size` to `long`.
![](https://main.qcloudimg.com/raw/17412e632d973788dc12a482a51c61fc.png)


Once the index rule is enabled, indexes will be created for new input data accordingly, and stored over a specified period of time depending on your configured storage cycle. Only logs for which indexes have been created can be queried for analysis. **Therefore, modifying an index rule or disabling an index only affects new input data. Unexpired legacy data will still be searchable.**

#### 6.2 Searching logs

Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and click **Log Search** in the left sidebar to enter the log search page.
Select the time range and log topic before using the search box. The searcg syntax supports searching by keyword, fuzzy match, and scope. For more information, see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439). Now, click **Search Analysis** to begin searching for logs.

- Sample 1: Querying failure logs
  Search statement: `status:fail`
![](https://main.qcloudimg.com/raw/2030b7b0b6cdd506a45ae3c16cc582c7.png)
- Sample 2: Querying logs of downloaded files over 300 KB
  Search statement: `action:download and size>300`
![](https://main.qcloudimg.com/raw/dca434bd2571fc77aa1f3ecff610e05d.png)

### 7. Shipping logs to COS

CLS can ship logs to Cloud Object Storage (COS) for long-term storage at a low cost. This also enables you to perform big data analysis offline.

To enable log shipping, you need to first create a [COS bucket](https://intl.cloud.tencent.com/document/product/436/13309). Next, log in to the [CLS Console](https://console.cloud.tencent.com/cls) and navigate through the logset management page. Go to the **Shipping Configuration** tab and click **Add Shipping Task** to create a shipping task.
Currently, CLS supports shipping in [CSV format](https://intl.cloud.tencent.com/document/product/614/31582) and [JSON format](https://intl.cloud.tencent.com/document/product/614/31583). Once you created a shipping task, CLS asynchronously ships data to the destination bucket. You can view the shipping status by clicking **Shipping Task** in the left sidebar of the console.
![](https://main.qcloudimg.com/raw/c9e92b7a0a5f2e0423c60c285ea16d93.png)
