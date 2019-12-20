## Overview

Cloud Log Service (CLS) is a platform service integrating log collection, log storage and log search analysis. CLS can collect scattered logs for centralized storage management and index analysis; meanwhile, CLS can also collect data and ship it to COS and other cloud products for further analysis.

To help you get started, this article demonstrates the basic functions of CLS. The demonstrations include:

- How to collect logs with LogListener
- How to search logs
- How to ship logs

## Directions

### 1. Activating Service

First, you need to apply for activation of [CLS](https://intl.cloud.tencent.com/product/cls) on the official website of Tencent Cloud.

### 2. Downloading and Installing LogListener  

[LogListener](https://intl.cloud.tencent.com/document/product/614/30449) is the collection client of CLS. LogListener collects log data to CLS in a fast and non-intrusive way. The detailed installation procedures are as follows.

#### 2.1 Determining If the Internet Is Reachable

Installing LogListener requires the network of the log source server and the available region network of CLS to be inter-reachable. Tencent Cloud Virtual Machine (CVM) accesses CLS via the private network by default.
You may execute the following commands to check the network connectivity, among which `<region>` is the short form for the region of CLS. For detailed region information, please see the [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940) document.

```shell
telnet <region>.cls.myqcloud.com 80
```

#### 2.2 Viewing (or Creating) a Key Pair

Log in to the [Access Management](https://console.cloud.tencent.com/cam/capi) in the Tencent Cloud account, view (or create) a key pair, and confirm that the status of the key is enabled.
![](https://main.qcloudimg.com/raw/5da40a4e08e052ea6935038960ee563e.png)

#### 2.3 Installing LogListener

The log collection environment demonstrated in this article is built in the Cloud Virtual Machine CentOS 7.2 (64 digits) environment.
Download the [Loglistener installer package](https://main.qcloudimg.com/raw/8656fcadd12ab9689674df09b510b52b/loglistener.2.2.2.tar.gz), decompress the package and open the directory `/loglistener/tools`, and then execute the following installation commands as Admin. For detailed installation procedures, please see the [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/30449).

```sh
./install.sh [SecretId] [SecretKey] [region] 
```
After installation, you may execute the command `./p.sh` to see if the installation is successful. If the following processing is shown, you have installed LogListener successfully.
![](https://main.qcloudimg.com/raw/9a0a184bcae1805e179e73045ddf0b6e.png)

### 3. Creating Logset and Log Topic 

CLS differs by regions. To lower the network delay, create log resources in a CLS service region close to your business region. (For supported regions, please see the [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).) Log resource management involves management of logsets and log topics. A logset represents a project, while a log topic represents a type of service. A single logset may contain multiple log topics.

#### 3.1 Creating Logset

Log in to the [CLS Console](https://console.cloud.tencent.com/cls), and click **Logset Management** on the left sidebar to open the logset management page. Select the appropriate region at the top of the page, and click **Create Logset** to start creating a logset.
For example, if you create a logset named `cls_project`, the created logset can appear in the logset list.
![](https://main.qcloudimg.com/raw/f1a918059ef2da5868fabbaa4e199a26.png)

#### 3.2 Creating Log Topic

Click **Logset Name** to open the log topic management page. Click **Add Log Topic** to start creating a log topic. For example, if you create a log topic named `nginx_access`, the created log topic can appear in the log topic list.
![](https://main.qcloudimg.com/raw/012e53bd7b979c7e250c067cc175e04c.png)

### 4. Creating a Server Group 

CLS uses a [Server Group](https://intl.cloud.tencent.com/document/product/614/30449) to manage the same group of log source servers in an unified manner.
When you log in to the [CLS Console](https://console.cloud.tencent.com/cls), click **Server Group Management** on the left sidebar to open the server group management page. Select the appropriate region at the top of the page, and click **Create Server Group** to start creating. Multiple IP addresses can be entered into one server group (one IP address per line). For CVM, please enter the private IP address directly. For more information, please see [Server Group Management](https://intl.cloud.tencent.com/document/product/614/17412).

After you create a server group, click **View** in the server group list to check the connection status of LogListener to the server. If the status is normal, the client LogListener has been connected to CLS successfully. If the status is abnormal, please see the [Server Group Exceptions](https://intl.cloud.tencent.com/document/product/614/17424) document for troubleshooting.
![](https://main.qcloudimg.com/raw/3a3e3eca80cfb7e86b787e4800db3708.png)

### 5. Configuring LogListener 


When you log in to the [CLS Console](https://console.cloud.tencent.com/cls), click **Logset Management** on the left sidebar, and then open the corresponding logset and log topic management page in sequence. In the logset management page, click **Collection Configuration** to assign a collection path, a parsing mode and an bound server group for the log topic. This only describes how to use LogListener to collect logs. For more information, please see [Collection Methods](https://intl.cloud.tencent.com/document/product/614/12502).

#### 5.1 Configuring the Collection Path

The collection path needs to match the absolute path of the log file on the server. You are required to enter two parameters: the directory prefix and the log file name. The entry format is **[directory prefix expression]/\*\*/[file name expression]**. LogListener matches all public prefix paths that meet the rules according to**[directory prefix expression]**, and monitors all log files that meet the **[file name expression]** rule under these directories (including subdirectories). The detailed descriptions of the parameters are as follows:

| Field     | Description                                                         |  
| -------- | ------------------------------------------------------------ |
| Directory prefix | The directory prefix structure of a log file supports only the wildcard characters “\*” and question marks (?). The wildcard character “\*” indicates that any multiple characters can be matched and the question mark (?) indicates that any single character can be matched. |
| /\*\*/     | Current directory and all its subdirectories                                 |
| File name   | A log file name supports only the wildcard characters “\*” and question marks (?). The wildcard character “\*” indicates that any multiple characters can be matched and the question mark (?) indicates that any single character can be matched. |

For example, if the absolute path of the file to be collected is `/cls/logs/access.log`, the directory prefix entered by the collection path is `/cls/logs`, and the log file name entered is `access.log`, which is shown as below:
![](https://main.qcloudimg.com/raw/012b8d755dcbba0b695da250c78eaeed.png)

#### 5.2 Binding a Server Group

When you select the pre-created server group to bind the current log topic with the server group, LogListener monitors the log files on the collection server group according to the configured rules. You may bind a log topic to multiple server groups, but report a log file to only one log topic.

#### 5.3 Configuring the Parsing Mode

CLS provides various log parsing modes, e.g. full text in a single line, separators, JSON, Full RegEx, etc. This article takes the separator format log as a case for description. For more information, please see [Separator Format](https://intl.cloud.tencent.com/document/product/614/32285). The log sample is as follows:
```sh
Tue Jan 22 14:49:45 2019;download;success;194;a31f28ad59434528660c9076517dc23b
```
- Selecting an Extraction Mode
  This article takes the case of separator format logs. Therefore, select the separator in the configuration option of **Key-value Extraction Mode**, and select the semicolon as the log separator.
- Entering the Log Sample and Extracting the Key-Value Pair
  After you enter a complete log in the log sample field and confirm it, a key-value pair is automatically extracted, and then you can define the unique key name for each set of key-value pairs.
	In this case, the log is parsed into `Tue Jan 22 14:49:45 2019`, `download`, `success`, `194` and `a31f28ad59434528660c9076517dc23b`. Define the key name for each field: `time`, `action`, `status`, `size`, and `hashcode`. In this way, LogListener will collect data according to the defined structured format.
![](https://main.qcloudimg.com/raw/9d498fdbb6d3e9773cac3bd8e6a3c273.png)

### 6. Searching Logs

#### 6.1 Configuring the Index

The search analysis feature of CLS is mainly based on the segment index. Currently, two types of indexes are provided: the full-text index and the key-value index. You may manage the index on the index configuration page of the log topics. (You may enable two indexes at the same time.)

| Index Type | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Full-Text Index | Divide the complete log into multiple segments by delimiters, and then perform a keyword query based on the segments. |
| Key-Value Index | Divide the complete log into multiple key-value pairs by formats, and then perform a field query based on the key-value pairs. |

This chapter uses the key-value index as an example to describe the configuration method. On the logset management page, click **Index Configuration** to open the index management page, select the key-value index for editing, configure the field (key) to be analyzed into the key value index, and then assign the data type for the key value index of each field. Currently, supported data types include `long`, `double`, `text`, etc., while the `text` type may assign a delimiter. (Delimiters separate a string into multiple segments.)In the case above, set the key-value index for `time`, `action`, `status`, `size`, `hashcode`, among which you should set `size` to the `long` type.
![](https://main.qcloudimg.com/raw/17412e632d973788dc12a482a51c61fc.png)


When the index is enabled, new data can build the index according to the configured rules. The index will be stored for a period of time (depending on the storage cycle you configure). Only the parts with built indexes can perform log query analysis. **Therefore, modifying the index rules or closing the index are only effective for newly written data, while you can still search unexpired historical data**.

#### 6.2 Searching Logs

When you log in to the [CLS Console](https://console.cloud.tencent.com/cls), click **Log Search** on the left sidebar to open the log search page.
Select the time range and the log topic for the search, and then enter the search syntax in the input box. (The syntax supports keyword search, fuzzy search, range search, etc. For more information, please see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439).) Finally, click **Search** to search logs.

- Sample 1: Query of failed logs
  Search statement: `status:fail`
![](https://main.qcloudimg.com/raw/2030b7b0b6cdd506a45ae3c16cc582c7.png)
- Sample 2: Query of logs with downloaded files over 300 KB
  Search statement: `action:download and size>300`
![](https://main.qcloudimg.com/raw/dca434bd2571fc77aa1f3ecff610e05d.png)

### 7. Shipping the Logs to COS

CLS can ship data to the Cloud Object Storage (COS) to store logs for a long time at a low cost while performing offline log big data analysis.

To enable log shipping, you need to create a [COS bucket](https://intl.cloud.tencent.com/document/product/436/13309) and log in to the [CLS Console](https://console.cloud.tencent.com/cls). On the logset management page, click **Shipping Configuration** to open the shipping configuration page, and then click **Add shipping Task** to create a shipping task.
Currently, CLS supports shipping in the [CSV format](https://intl.cloud.tencent.com/document/product/614/31582) and [JSON format](https://intl.cloud.tencent.com/document/product/614/31583). After you create a shipping task, CLS asynchronously ships data to the destination bucket. You can view the shipping status in **Shipping Task Management** on the left sidebar of the console.
![](https://main.qcloudimg.com/raw/c9e92b7a0a5f2e0423c60c285ea16d93.png)
