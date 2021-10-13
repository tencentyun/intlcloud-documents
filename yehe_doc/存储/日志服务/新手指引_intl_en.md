
This document describes how to get started with Cloud Log Service (CLS).

## 1. CLS Basics

- [Features](https://intl.cloud.tencent.com/document/product/614/11254)
- [Advantages](https://intl.cloud.tencent.com/document/product/614/11265)
- [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940)


-----

## 2. CLS Billing Modes

CLS provides a daily pay-as-you-go billing option in all the supported regions. You pay for what you use and no upfront payment is required. For more information, please see [Product Pricing](https://intl.cloud.tencent.com/document/product/614/37510).

-----

## 3. Getting Started

### Step 1. Activate CLS
First, you need to request to activate [CLS](https://intl.cloud.tencent.com/product/cls) on Tencent Cloud.


### Step 2. Download and install LogListener  

[LogListener](https://intl.cloud.tencent.com/document/product/614/30449) is a client that collects log data and sends it to CLS in a fast and non-intrusive way. You can install it as follows:

#### Check the network connection

To install LogListener, the source server and the CLS region must be able to connect to each other. Tencent's Cloud Virtual Machine (CVM) accesses CLS via a private network by default.
You can run the following command to check the network connectivity, where `<region>` is the abbreviation for the CLS region. For more information about regions, please see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).
```shell
telnet <region abbreviation>.cls.tencentyun.com
```

#### View/Create a key pair

Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi), view (or create) a key pair, and make sure that the key is enabled.


#### Install LogListener

In this example, the CLS service runs in the CVM CentOS 7.2 (64-bit) environment. To download and install LogListener, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).

### Step 3. Create a log topic 

CLS service is differentiated by region. To lower network latency, try to create log resources in a CLS region closest to your business region. For supported regions, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940). Log resource management involves the management of logsets and log topics. A logset represents a project, while a log topic represents a type of service. A single logset may contain multiple log topics.

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Log Topic** to go to the log topic management page.
3. Select a region and click **Create Log Topic**.

4. Configure as needed on the page that is displayed.</br>

 - Log topic name: name of the log topic, such as topic_test.
 - Logset: **Select an existing logset** is selected by default. Alternatively, you can select **Create Logset** and set the logset’s name (e.g., cls_test) as needed.
5. Click **OK**.
 - A created log topic will be displayed in the log topic list.

 - You can click **Manage Logset** to view the created logset.


### Step 4. Create a machine group 

CLS uses a [machine group](https://intl.cloud.tencent.com/document/product/614/30449) to manage a list of log source machines.
Log in to the CLS console(https://console.cloud.tencent.com/cls), and click **Machine Group** on the left sidebar to open the machine group management page. Select the appropriate region at the top of the page, and click **Create Machine Group**. A machine group can contain multiple machine IP addresses (one IP address per line). For CVM, enter the private IP address directly. For more information, see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).

After a machine group is created, click **View** in the machine group list to check the connection between the LogListener client and servers. If the status is normal, the LogListener client is successfully connected to CLS. Otherwise, please see [Machine Group Exception](https://intl.cloud.tencent.com/document/product/614/17424) for troubleshooting.


### Step 5. Configure LogListener 

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Log Topic** to go to the log topic management page.
3. On the log topic management page, click **Collection Configuration**, specify a collection path and parsing mode for the log topic, and bind the log topic to a machine group.
>? This step takes the LogListener-based log collection method as an example. For more information, please see [Collection Methods](https://intl.cloud.tencent.com/document/product/614/12502).
>

#### Configure a collection path

The collection path needs to match the absolute path of the log file on the server. You are required to enter two parameters: the directory prefix and the file name in the format of **[directory prefix expression]//\*\*//[file name expression]**. LogListener matches all paths with common prefixes that satisfy the **[directory prefix expression]**, and monitors all log files under these directories (including subdirectories) that satisfy the **[file name expression]**. The parameters are described as follows:

| Parameter     | Description       |
| -------- | ------------------------------------------------------------ |
| Directory Prefix | Directory prefix for log files, which supports only the wildcard characters `\*` and `?`\*` indicates to match any multiple characters. `?` indicates to match any single character. |
| /\*\*/     | Current directory and all its subdirectories.   |
| File Name   | Log file name, which supports only the wildcard characters `\*` and `?`. `\*` indicates to match any multiple characters. `?` indicates to match any single character. |

For example, if the absolute path of the file to be collected is `/cls/logs/access.log`, then the directory prefix entered for the collection path should be `/cls/logs`, and the file name `access.log`.

#### Bind a machine group

Select an existing machine group, and associate it with the current log topic. Then, LogListener will monitor the log files in this machine group according to the rules you set. You may bind a log topic to multiple machine groups, but a log file will only be collected into one log topic.

#### Configure a parsing mode

CLS supports various log parsing modes such as full text in a single line, separator, JSON, and full regex. The following log sample uses the separator mode (for more information, please see [Separator Format](https://intl.cloud.tencent.com/document/product/614/32285)).
```sh
Tue Jan 22 14:49:45 2019;download;success;194;a31f28ad59434528660c9076517dc23b
```
- Selecting an extraction mode
  Select `Separator` for the **Extraction Mode**, and `Semicolon` for the log separator.
- Inputting a sample log and extracting key-value pairs
  Enter a complete log in the log sample field, and key-value pairs will be automatically extracted. Then, you can define a unique key for each key-value pair.
	In this example, the log is parsed into `Tue Jan 22 14:49:45 2019`, `download`, `success`, `194`, and `a31f28ad59434528660c9076517dc23b`. The keys defined for these 5 fields are `time`, `action`, `status`, `size`, and `hashcode` respectively. LogListener will then use this defined structure to collect data.


### Step 6. Search for logs

#### Configure indexes

CLS offers a log search and analysis feature based on segment indexing. We currently offer two index types: full-text index and key-value index. They can be managed on the index configuration tab on the log topic management page. Both index types can be enabled at the same time. 

| Index Type | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Full-Text | Breaks a full log into segments by delimiter, and executes keyword query based on the segments |
| Key-Value | Breaks a full log into key-value pairs according to the specifications, and executes field query based on the key-value pairs |

Here we use key-value index as an example to describe how to configure indexes. On the log topic management page, go to the **Index Configuration** tab, click **Edit**, and toggle the key to enable index status. Toggle on **Key-Value Index**. Click **Add** to add keys. Select a field type for each key. Currently, `long`, `double`, and `text` are supported. `text` type allows you to specify delimiters, which separate a character string into segments. Continuing the above example, enter `time`, `action`, `status`, `size`, and `hashcode` as key-value indexes, and set the field type of `size` to `long`.



Once the index rule is enabled, indexes will be created for new input data accordingly, and stored over a specified period of time depending on your configured storage cycle. Only logs for which indexes have been created can be queried for analysis. **Therefore, modifying an index rule or disabling an index only affects new input data. Unexpired legacy data will still be searchable.**

#### Search for logs

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Search and Analysis** to go to the search and analysis page.
3. Select the target region, log topic, and time range, and enter the search syntax (the syntax supports searching by keyword, fuzzy match, and scope. For more information, please see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439)). Click **Search Analysis** to begin searching for logs.


- Sample 1: Querying failure logs
  Search statement: `status:fail`

- Sample 2: Querying logs of downloaded files over 300 KB
  Search statement: `action:download and size>300`


### Step 7. Ship logs to COS

CLS can ship logs to Cloud Object Storage (COS) for long-term storage at a low cost. This also enables you to perform big data analysis offline.

To ship logs to COS, perform the following steps:
1. Create a [COS bucket](https://intl.cloud.tencent.com/document/product/436/13309).
2. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
3. On the log topic management page, click **Shipping Configuration** to go to the shipping configuration page.
4. Click **Add Shipping Configuration** to create a shipping task.
Currently, CLS supports shipping in [CSV format](https://intl.cloud.tencent.com/document/product/614/31582) and [JSON format](https://intl.cloud.tencent.com/document/product/614/31583). Once you create a shipping task, CLS asynchronously ships data to the destination bucket. You can view the shipping status by clicking **Shipping Task** on the left sidebar of the console.


-----

## 4. Console Interface

The following is the overview page of the CLS console:



-----

## 5. Overview of Console Features

<table>
<thead>
<tr>
<th>Desired Operation</th>
<th>Reference Document</th>
</tr>
</thead>
<tbody><tr>
<td>Manage logsets via console</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/34238" target="_blank">Managing Logset</a></td>
</tr>
<tr>
<td>Learn about machine groups</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/17412" target="_blank">Machine Group Management</a></td>
</tr>
<tr>
<td>Configure and enable indexes</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/39594" target="_blank">Configuring Index</a></td>
</tr>
<tr>
<td>Select an appropriate chart type to display the analysis results as needed</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/37803" target="_blank">Log Analysis</a></td>
</tr>
<tr>
<td>Ship log data to COS to further meet the needs of log scenarios and unlock the value of log data</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/32940" target="_blank">Shipping to COS</a></td>
</tr>
<tr>
<td>Use CKafka instances to consume log topic data</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/30444" target="_blank">Shipping to CKafka</a></td>
</tr>
<tr>
<td>Understand authorization configuration in different operation scenarios</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/37888" target="_blank">Shipping Authorization</a></td>
</tr>
</tbody></table>

-----

## 6. FAQs
#### LogListener
- [Machine Group Exception](https://intl.cloud.tencent.com/document/product/614/17424)
- [LogListener FAQs](https://intl.cloud.tencent.com/document/product/614/38444)
- [LogListener Installation Exception](https://intl.cloud.tencent.com/document/product/614/30445)


#### Log Search

[Log Search Failure](https://intl.cloud.tencent.com/document/product/614/38446)

-----

## 7. Feedback and Suggestions
If you have any doubts or suggestions when using CLS products and services, you can submit your feedback through the following channels. Dedicated personnel will contact you to solve your problems.
- If you have any questions regarding CLS documentation, such as links, content, or APIs, please click **Send Feedback** on the right of the documentation page.
- If you have any questions regarding the CLS service, contact [smart customer service](https://intl.cloud.tencent.com/contact-sales) or [submit a ticket](https://console.cloud.tencent.com/workorder/category).

