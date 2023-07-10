## Overview

CLS allows you to collect/store/search/ship logs, analyze charts, and monitor alarms. With CLS, you can collect logs for central management, search, and analysis. Also, you can set monitor alarms for log topics and ship the collected logs to COS or other products for further analysis.

To get you started, instructions to the following CLS features are described in this document:

- Collecting logs with LogListener
- Searching logs
- Shipping logs

## Directions

### 1. Activate CLS

First, you need to request to activate [CLS](https://intl.cloud.tencent.com/product/cls) on Tencent Cloud.

### 2. Download and install LogListener

[LogListener](https://intl.cloud.tencent.com/document/product/614/30449) is a client that collects log data and sends it to CLS in a fast and non-intrusive way. You can install it as follows:

#### 2.1 Check the network connection

To install LogListener, the source server and the CLS region must be able to connect to each other. Tencent’s Cloud Virtual Machine (CVM) accesses CLS via a private network by default.
You can run the following command to check the network connectivity, where `<region>` is the abbreviation for the CLS region. For more information about regions, please see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).

```shell
telnet <region abbreviation>.cls.tencentyun.com 80
```

#### 2.2 View/Create a key pair

Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi), view (or create) a key pair, and make sure that the key is enabled.


#### 2.3 Install LogListener

In this example, the CLS service runs in the CVM CentOS 7.2 (64-bit) environment. To download and install LogListener, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).

### 3. Create a log topic

CLS introduces various regions. To lower network latency, please create log resources in a region closest to your business region. For supported regions, please see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940). Log topic management includes the management of logsets and log topics. A logset represents a project, while a log topic represents a type of service. A single logset may contain multiple log topics.

#### 3.1 Create a log topic

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
2. On the left sidebar, click **Log Topic** to go to the log topic management page.
3. Select a region and click **Create Log Topic**.

4. Configure as needed on the page that is displayed.</br>

 - Log topic name: name of the log topic, such as topic_test.
 - Logset: **Select an existing logset** is selected by default. Alternatively, you can select **Create Logset** and set the logset’s name (e.g., cls_test) as needed.
5. Click **OK**.
 - A created log topic will be displayed in the log topic list.

 - You can click **Manage Logset** to view the created logset.


### 4. Create a machine group

CLS uses a [machine group](https://intl.cloud.tencent.com/document/product/614/30449) to manage a list of log source machines.

1. On the left sidebar, click **Machine Group** to go to the management page.
2. Select the desired region and click **Create Machine Group**.
3. Configure as needed on the page that is displayed.
Multiple IPs can be input in a machine group (one IP per line). For CVM instances, please input the private IP addresses directly. For more information, please see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).
4. Click **OK**.
After a machine group is created, you can click **View** in the **Operation** column to check the connection between LogListener and servers.

 - Normal: The client’s LogListener has successfully connected to CLS.
 - Abnormal: You can troubleshoot by referring to [Machine Group Exception](https://intl.cloud.tencent.com/document/product/614/17424).


### 5. Configure LogListener

1. On the left sidebar, click **Log Topic** to go to the management page.
2. Click the desired log topic ID/name to go to the log topic management page.
3. Select the **Collection Configuration** tab to specify the collection path, bound machine group, and parsing mode.
>? The following describes how to collect logs using LogListener. For more information, please see [Collection Methods](https://intl.cloud.tencent.com/document/product/614/12502).
>

#### 5.1 Configure a collection path

The collection path needs to match the absolute path of the log file on the server. You are required to enter two parameters: the directory prefix and the file name in the format of **[directory prefix expression]//\*\*//[file name expression]**. LogListener matches all paths with common prefixes that satisfy the **[directory prefix expression]**, and monitors all log files under these directories (including subdirectories) that satisfy the **[file name expression]**. The parameters are described as follows:

| Parameter     | Description       |
| :------- | :----------------------------------------------------------- |
| Directory Prefix | Directory prefix for log files, which supports only the wildcard characters `*` and `?`. \* indicates to match any multiple characters. `?` indicates to match any single character. |
| /\*\*/     | Current directory and all its subdirectories.   |
| File Name   | Log file name, which supports only the wildcard characters `\*` and `?`. `\*` indicates to match any multiple characters. `?` indicates to match any single character. |

For example, if the absolute path of the file to be collected is `/cls/logs/access.log`, then the directory prefix entered for the collection path should be `/cls/logs`, and the file name `access.log`.

#### 5.2 Bind a machine group

Select an existing machine group, and associate it with the current log topic. Then, LogListener will monitor the log files in this machine group according to the rules you set. You may bind a log topic to multiple machine groups, but a log file will only be collected into one log topic.

#### 5.3 Configure a parsing mode

CLS supports various log parsing modes such as full text in a single line, separator, JSON, and full regex. The following log sample uses the separator mode (for more information, please see [Separator Format](https://intl.cloud.tencent.com/document/product/614/32285)).

```sh
Tue Jan 22 14:49:45 2019;download;success;194;a31f28ad59434528660c9076517dc23b
```

- Selecting an extraction mode
  This sample uses separators to separate logs. Therefore, select **Separator** for the **Extraction Mode** field and **Semicolon** for **Separator**.
- Inputting a sample log and extracting key-value pairs
  Enter a complete log in the log sample field, and key-value pairs will be automatically extracted. Then, you can define a unique key for each key-value pair.
  In this example, the log is parsed into `Tue Jan 22 14:49:45 2019`, `download`, `success`, `194`, and `a31f28ad59434528660c9076517dc23b`. The keys defined for these 5 fields are `time`, `action`, `status`, `size`, and `hashcode` respectively. LogListener will then use this defined structure to collect data.


### 6. Configure indexes

CLS offers a log search and analysis feature based on segment indexing. We currently offer two index types: full-text index and key-value index. They can be managed on the index configuration tab on the log topic management page. Both index types can be enabled at the same time.

| Index Type | Description                                                         |
| :------- | :----------------------------------------------------------- |
| Full-Text | Breaks a full log into segments by delimiter, and executes keyword query based on the segments |
| Key-Value | Breaks a full log into key-value pairs according to the specifications, and executes field query based on the key-value pairs |

Here we use key-value indexes as an example to describe how to configure indexes. On the log topic management page, go to the **Index Configuration** tab, click **Edit**, and toggle the key to enable index status. Toggle on **Key-Value Index**. Click **Add** to add keys. Select a field type for each key. Currently, `long`, `double`, and `text` are supported. The `text` type allows you to specify delimiters, which separate a character string into segments. Continuing the above example, enter `time`, `action`, `status`, `size`, and `hashcode` as key-value indexes, and set the field type of `size` to `long`.


Once the index rule is enabled, indexes will be created for new input data accordingly, and stored over a specified period of time depending on your configured storage cycle. Only logs for which indexes have been created can be queried for analysis. **Therefore, modifying an index rule or disabling an index only affects new input data. Unexpired legacy data will still be searchable.**

### 7. Ship logs

With CLS, you can ship data to COS or CKafka to store logs for a longer period at a lower cost. Moreover, you can analyze big data logs offline.

#### 7.1 Ship logs to COS

To ship logs to COS, you can perform the following steps:
1. Create a [COS bucket](https://intl.cloud.tencent.com/document/product/436/13309).
2. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
3. Select the desired log topic ID/name to go to the management page.
4. Select the **Ship to COS** tab.
5. Click **Add Shipping Configuration** to create a shipping task.
Currently, CLS supports shipping logs in [CSV](https://intl.cloud.tencent.com/document/product/614/31582) and [JSON](https://intl.cloud.tencent.com/document/product/614/31583) formats.

After a shipping task is created, CLS asynchronously ships data to the destination bucket. To view the shipping status, you can click the desired log topic and then choose the **Ship to COS** tab. Alternatively, you can click **Shipping task** on the left sidebar of the console.



#### 7.2 Ship to CKafka

Only logs generated after the configuration can be shipped.
To ship logs to CKafka, you can perform the following steps:
1. [Create a CKafka instance and topic](https://intl.cloud.tencent.com/document/product/597/39718).
2. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
3. Select the desired log topic ID/name to go to the management page.
4. Select the **Ship to CKafka** tab.
5. Click **Edit**.
6. Select the desired CKafka instance and click **OK** to enable CKafka consumption.

Currently, CLS supports shipping original logs and JSON-formatted logs. To view the shipping status, you can click the consumed log topic and then select the **Ship to CKafka** tab.

