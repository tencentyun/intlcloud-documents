## Overview

The shipping feature of CLS interconnects the upstream linkages of the product ecosystem to import logs from Tencent Cloud's Cloud Object Storage (COS) to CLS for further operations such as log data query and analysis and processing. You only need to complete simple configurations in the CLS console to import data.

## Prerequisites

- Activate CLS, create a logset and a log topic, and collect log data.
- Activate COS and ensure that the files to be imported have already been uploaded to a COS bucket. For more information, please see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/13321).
- Set the COS access permission for the current operation account, that is, authorize CLS to use the CLS_QcsRole role to access COS resources.


## Configuration

1. **Select a log topic**: select an existing log topic or create a log topic for storing the data to be imported from COS to CLS.
2. **Configure the data source**: path to the COS object to be imported and the corresponding compression mode (GZIP, LZOP, SNAPPY, or no compression).
3. **Configure parsing**: parsing format of the imported file. Currently, the following formats are supported: full text in a single line, JSON, and CSV.
4. **Configure indexes**: you need to configure indexes for the current topic, and enable index configuration before you can perform searches. If you select an existing log topic, the new index configuration takes effect only for the modified data.

## Directions

### Step 1. Select a log topic

- If you want to create a new log topic, perform the following operations:
 1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
 2. On the left sidebar, click **Overview** to go to the overview page.
 3. In the **Other Logs** area, locate **Import from COS** and click **Integrate Now**.
![](https://qcloudimg.tencent-cloud.cn/raw/514ecd8031f341cc6d16096075aaf0ae.png)
 4. On the log topic creation page, configure the log topic information such as the log topic name and log retention period as needed, and click **Next**.
- If you want to select an existing log topic, perform the following operations:
 1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).
 2. On the left sidebar, click **Log Topic** and select a log topic to be shipped to go to the log topic management page.
 3. Click the **Collection Configuration** tab and click **Add** in the **Data Import Configuration** area.
![](https://qcloudimg.tencent-cloud.cn/raw/adcb729aa16256f01552c354b6a6bc03.png)

### Step 2. Configure the data source

1. On the data source configuration page, configure the following information in sequence:
<table>
	<tr><th>Configuration Item</th><th>Description</th><th>Rule</th><th>Required</th></tr>
	<tr><td>Task Name</td><td>Set the name of the import task.</td><td>The value can contain letters, numbers, underscores (_), and hyphens (-).</td><td>Yes</td></tr>
	<tr><td>Bucket Region</td><td>Set the region of the bucket where the file to be imported resides. If the file to be imported and the destination log topic are in different regions, public network fees will incur due to cross-region access.</td><td>Select an option from the list.</td><td>Yes</td></tr>
	<tr><td>Bucket</td><td>Select the bucket where the file to be imported resides. The drop-down list box provides all buckets in the selected region for you to choose.</td><td>Select an option from the list.</td><td>Yes</td></tr>
	<tr><td>File Prefix</td><td>Enter the prefix of the folder where the COS file to be imported resides for accurate locating. You can enter the file prefix **csv/** or the complete file path **csv/object.gz**.</td><td>Enter a value.</td><td>Yes</td></tr>
	<tr><td>Compression Mode</td><td>Select the compression mode of the COS file to be imported. CLS decompresses the file and reads data according to the compression mode of the file. Supported compression modes are: GZIP, LZOP, SNAPPY, and no compression.</td><td>Select an option from the list.</td><td>Yes</td></tr>
</table>
2. Click **Preview**. The system selects an eligible path to display and provides the total number of files with the specified file prefix.

3. After confirming that the data for preview is correct, click **Next**.

### Step 3. Configure parsing

1. On the parsing configuration page, configure the following information:
 - Extraction mode: select **Full text in a single line**, **JSON**, or **CSV**.
     - Full text in a single line: each log will be parsed into a complete string with \_\_CONTENT\_\_ as the key value. If the index feature is enabled, you can search for log content via full-text search. The collection time is the log time.

     - JSON: you can extract key-value pairs in JSON format.

     - CSV: you can specify a separator to split each log. You need to define the key name for each split field. Invalid fields (fields that do not need to be collected) can be left empty. However, it's not supported to leave all fields empty.

 - Filter:
    - Filters are designed to help you extract valuable log data by adding log collection filter rules based on your business needs. If the filter rule is a Perl regular expression, the created filter rule will be used for matching; in other words, only logs that match the regular expression will be collected and reported.
    - For separator-formatted logs, you need to configure a filter rule according to the defined custom key-value pair. For example, if you want to collect all log data with a **status** field whose value is 400 or 500 after the sample log is parsed in separator mode, you need to configure `key` as `status` and the filter rule as `400|500`.
 - Use Collection Time: when this option is toggled on, log time is marked by the collection time. When it is disabled, you need to specify a field as the log time.
>? 
> - The log time is measured in seconds. If the log time is entered in an incorrect format, the collection time is used as the log time.
> - The time attribute of a log is defined in two ways: collection time and original timestamp.
> - Collection time: the time attribute of a log is determined by the time when the log is imported from COS to CLS.
> - Original timestamp: the time attribute of a log is determined by the timestamp in the raw log.
> - Use the original timestamp as the time attribute of logs.
> - Disable **Collection Time** and enter the time key of the original timestamp and the corresponding time parsing format in **Time Key** and **Time Parsing Format** respectively. For more information on the time parsing format, please see [Configuring Time Format](https://intl.cloud.tencent.com/document/product/614/32942).
> 
 - Separator: the system segments the sample log according to the selected separator and displays it in the extraction result box. You need to define a unique key for each field. Currently, log collection supports a variety of separators. Common separators include space, tab, comma, semicolon, and vertical bar. If your log data uses other separators such as `:::`, it can also be parsed through custom delimiter.
2. Click **Next**.

### Step 4. Configure indexes

1. On the index configuration page, configure the following information:

 - Index Status: select whether to enable it.
 - Full-Text Index: select whether to set it to case-sensitive.
    - Full-Text Delimiter: the default value is `@&()='",;:<>[]{}/ \n\t\r` and can be modified as needed.
    - Allow Chinese Characters: select whether to enable this feature.
 - Key-value Index: disabled by default. You can configure the field type, delimiters, and whether to enable statistical analysis according to the key name as needed. To enable key-value index, you can set ![](https://qcloudimg.tencent-cloud.cn/raw/811e3ac22419f001dd68e20312c6a4a5.png) to ![](https://qcloudimg.tencent-cloud.cn/raw/581d30911cccb58092b8c8f1529a5109.png).
>! 
> - Index configuration must be enabled before you can perform searches.
> - The modified index rules take effect only for newly written logs. The existing data is not updated.
> 
2. Click **Submit**.

## Related Operations

#### Querying the import progress

1. If the current log topic contains a COS import task, click **Search** to go to the **Search and Analysis** page to view the progress of the import task.

2. The floating balloon in the upper-right corner of the **Search and Analysis** page shows the import progress. Click the balloon to view the details of the import task.

3. On the task details page, click **View Details** to redirect to the collection configuration page to query the detailed configuration of the import task.
