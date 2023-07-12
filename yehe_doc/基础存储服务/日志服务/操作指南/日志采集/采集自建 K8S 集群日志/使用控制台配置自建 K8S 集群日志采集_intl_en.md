This document describes how to configure log collection rules in a self-built Kubernetes environment and ship logs to [CLS](https://www.tencentcloud.com/products/cls).
## Use Cases
The self-built Kubernetes log collection feature is a non-Tencent Cloud Kubernetes cluster log collection tool, which can ship logs in the specified paths of cluster services or nodes to CLS. This feature is suitable for users who want to store and analyze service logs in a Kubernetes cluster.
You need to manually enable log collection for each cluster, and configure the collection rules. After log collection is enabled for a cluster, the log collection agent runs as a DaemonSet in the cluster, collects logs from the collection source based on the collection source, CLS log topic, and log parsing method configured in the log collection rules, and sends the collected logs to the consumer. Log collection supports the following operations.
## Prerequisites
- You have activated CLS.
- You have [installed LogListener in the self-built Kubernetes cluster](https://intl.cloud.tencent.com/document/product/614/43573) and deployed it.
- You have configured the target log reporting permission as instructed in [Access Policy Templates](https://intl.cloud.tencent.com/document/product/614/45004).

## Directions
### Creating log collection rules
### Configuring self-built Kubernetes collection rules in the CLS console
#### **Step 1. Select a log topic**
- To select a new log topic, perform the following steps: Log in to the [CLS console](https://console.cloud.tencent.com/cls).
	1. On the left sidebar, click **Overview** to enter the overview page.
	2. In the **Other Logs** section, find self-built Kubernetes cluster collection and click **Access Now**.

	3. On the **Create Log Topic** page, configure the log topic information such as the name and log retention period as needed and click **Next**.
- To select an existing log topic, perform the following steps: Log in to the [CLS console](https://console.cloud.tencent.com/cls).
  1. On the left sidebar, click **Log Topic** and select a log topic to be shipped to enter the log topic management page.
  2. On the **Collection Configuration** tab, click **Add** in the **Self-Built Kubernetes Cluster Collection** section.


#### **Step 2. Configure a machine group**
On the **Machine Group Management** page, select the target machine group and click **Next** to proceed to collection configuration. For more information, see [Machine Group Management](https://intl.cloud.tencent.com/document/product/614/17412).

#### **Step 3. Configure collection in the self-built Kubernetes cluster**
- Log source configuration  
 1. Collection rule name: You can enter a custom name for a log collection rule.  
 1. Select the collection type and configure the log source.
 Currently, log collection types include container standard output, container file path, and node file path.
   - Standard output logs of a container
Log sources include **all containers**, **specified workloads**, and **specified Pod labels**.

   - Container file logs 
      - Log sources include **specified workloads** and **specified Pod labels**.
      - You can specify a file path or use wildcards for the collection path. For example, when the container file path is `/opt/logs/*.log`, you can specify the collection path as `/opt/logs` and the filename as `*.log`.

<dx-alert infotype="notice" title="">
For **Container file path**, the corresponding path <b>cannot be a soft link</b>. Otherwise, the actual path of the soft link will not exist in the collector's container, resulting in log collection failure.
</dx-alert>

   - Node file logs
      - You can specify a file path or use wildcards. For example, when the container file paths for collection are `/opt/logs/service1/*.log` and `/opt/logs/service2/*.log`, you can specify the folder of the collection path as `/opt/logs/service*` and the file name as `*.log`.


 1. Metadata configuration
Besides the original log content, the metadata related to the container or Kubernetes (such as the ID of the container that generated the logs) will also be reported to the CLS. Therefore, when viewing logs, users can trace the log source or search based on the container identifier or characteristics (such as container name and labels). You can select whether to report such metadata as needed.
The metadata related to the container or Kubernetes is as shown below:
<table>
	<tr>
		<th  width=24%>Field</th> <th width=71%>Description</th>
	</tr>
	<tr>
		<td>container_id</td> <td>ID of the container to which logs belong</td>
	</tr>
	<tr>
		<td>container_name</td> <td>The name of the container to which logs belong</td>
	</tr>
	<tr>
		<td>image_name</td> <td>The image name IP of the container to which logs belong</td>
	</tr>
	<tr>
		<td>namespace</td> <td>The namespace of the Pod to which logs belong</td>
	</tr>
	<tr>
		<td>pod_uid</td> <td>The UID of the Pod to which logs belong</td>
	</tr>
	<tr>
		<td>pod_name</td> <td>The name of the Pod to which logs belong</td>
	</tr>
	<tr>
		<td>pod_lable_{label name}</td> <td>The labels of the Pod to which logs belong (for example, if a Pod has two labels: app=nginx and env=prod, 
the reported log will have two metadata entries attached: pod_label_app:nginx and pod_label_env:prod).
</td>
	</tr>
</table>

</dx-alert>

>? To collect logs with a certain Pod label, you need to manually enter the target label key (or enter multiple ones, each of which ends with a carriage return). Logs will be collected if their label is hit.
>
- Parsing rule configuration  
 1. Configure the collection policy (**Full** or **Incremental**).
	- Full: Collecting logs from the beginning of the log file.
	- Incremental: Collecting logs 1 MB ahead of the end of the log file (for a log file less than 1 MB, incremental collection is equivalent to full collection).
 2. Encoding Mode: It can be **UTF-8** or **GBK**.
 3. Extraction Mode: The following types of extraction modes are supported:
<table>
<thead>
<tr>
<th width="15%">Parsing Mode</th>
<th width="60%">Description</th>
<th width="20%">Documentation</th>
</tr>
</thead>
<tbody><tr>
<td>Full text in a single line</td>
<td>A log contains only one line of content, and the line break `\n` to mark the end of a log. Each log will be parsed into a complete string with <strong>CONTENT</strong> as the key value. When log Index is enabled, you can search for log content via full-text search. The time attribute of a log is determined by the collection time.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/32287">Full Text in a Single Line</a></td>
</tr>
<tr>
<td>Full text in multi lines</td>
<td>A log with full text in multi lines spans multiple lines and a first-line regular expression is used for match. When a log in a line matches the preset regular expression, it is considered as the beginning of a log, and the next matching line will be the end mark of the log. A default key value, <strong>CONTENT</strong>, will be set as well. The time attribute of a log is determined by the collection time. The regular expression can be generated automatically.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/32284">Full Text in Multi Lines</a></td>
</tr>
<tr>
<td>Single line - full regex</td>
<td>The single-line - full regular expression mode is a log parsing mode where multiple key-value pairs can be extracted from a complete log. When configuring the single-line - full regular expression mode, you need to enter a sample log first and then customize your regular expression. After the configuration is completed, the system will extract the corresponding key-value pairs according to the capture group in the regular expression. The regular expression can be generated automatically.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/39589">Full Regular Format (Single-Line)</a></td>
</tr>
<tr>
<td>Multiple lines - full regex</td>
<td>The multi-line - full regular expression mode is a log parsing mode where multiple key-value pairs can be extracted from a complete piece of log data that spans multiple lines in a log text file (such as Java program logs) based on a regular expression. When configuring the multi-line - full regular expression mode, you need to enter a sample log first and then customize your regular expression. After the configuration is completed, the system will extract the corresponding key-value pairs according to the capture group in the regular expression. The regular expression can be generated automatically.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/39590">Full Regular Format (Multi-Line)</a></td>
</tr>
<tr>
<td>JSON</td>
<td>A JSON log automatically extracts the key at the first layer as the field name and the value at the first layer as the field value to implement structured processing of the entire log. Each complete log ends with a line break `\n`.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/32286">JSON Format</a></td>
</tr>
<tr>
<td>Separator</td>
<td>Structure the data in a log with the specified separator, and each complete log ends with a line break `\n`. Define a unique key for each separate field. Leave the field blank if you don’t need to collect it. At least one field is required.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/32285">Separator Format</a></td>
</tr>
</tbody></table>
- Filter: LogListener collects only logs that meet the filter rules. **Key** supports exact match, and **Filter Rule** supports regular expression matching. For example, you can specify to collect only logs where `ErrorCode` is `404`. You can enable the filter and configure rules as needed.
	<dx-alert infotype="explain" title="">
	Currently, one log topic supports only one collection configuration. Ensure that all container logs that adopt the log topic can accept the log parsing method that you choose. If you create different collection configurations under the same log topic, the earlier collection configurations will be overwritten.
	</dx-alert>  
	

Click **Next**. 
#### **Step 4. Configure an index**
On the index configuration page, configure the following information:
- Index Status: select whether to enable it.
- Full-Text Index: Select whether to set it to case-sensitive. Full-Text Delimiter: It is "@&()='",;:\<\>[]{}/ \n\t\r" by default and can be modified as needed.
- Allow Chinese Characters: select whether to enable this feature.
- Key-Value Index: Disabled by default. You can configure the field type, delimiters, and whether to enable statistical analysis according to the key name as needed. To enable key-value index, toggle the switch on.

>!
>- Index configuration must be enabled first before you can perform searches.
>- The modified index rules take effect only for newly written logs. The existing data is not updated.
