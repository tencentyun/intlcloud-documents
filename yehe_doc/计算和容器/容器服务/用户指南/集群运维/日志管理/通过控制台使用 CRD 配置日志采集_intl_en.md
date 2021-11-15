## Overview
TKE's log collection feature allows you to collect logs in a cluster and send logs in specific paths of cluster services or nodes to [Tencent Cloud Log Service (CLS)](https://intl.cloud.tencent.com/product/cls). Log collection applies to users who need to store and analyze service logs in Kubernetes clusters.

You need to manually enable log collection for each cluster, and configure the collection rules. After log collection is enabled for a cluster, the log collection agent runs as a DaemonSet in the cluster, collects logs from the collection source based on the collection source, CLS log topic, and log parsing method configured by users in the log collection rules, and sends the collected logs to the CLS for storage. Log collection supports the following operations:
- [Enabling log collection](#open)
- [Collecting standard output logs of a container](#stout)
- [Collecting file logs in containers](#insideDocker)
- [Collecting file logs on nodes](#inside)



## Prerequisites
- Before enabling log collection, ensure that there are sufficient resources on cluster nodes. Enabling log collection will occupy some cluster resources.
  - CPU resources occupied: 0.11 to 1.1 cores by default. You can increase the CPU resources as needed if the quantity of logs is too large.
  - Memory resources occupied: 24 to 560 MB by default. You can increase the memory resources as needed if the quantity of logs is too large.
  - Maximum log length: 512 K for a log. The log is truncated if this limit is exceeded.
- To use log collection, confirm that nodes in the Kubernetes cluster can access CLS. Only Kubernetes clusters of version 1.10 or later support the following log collection features.

## Concepts

- **Log Collection Agent**: the agent that TKE uses to collect logs. It adopts Loglistener and runs within the cluster as a DaemonSet.
- **Log Rules**: users can use log rules to specify the log collection source, log topic, and log parsing method and configure the filter.
  - The log collection agent monitors changes in the log collection rules, and rule changes take effect within 10 seconds.
  - Multiple log collection rules do not create multiple DaemonSets, but too many log collection rules cause the log collection agent to occupy more resources.
- **Log Source**: log sources include specified container standard output, files in containers, and node files.
  - When collecting container standard output logs, users can select TKE logs in all containers or specified workloads and specified Pod labels as the log collection source.
  - When collecting container file path logs, users can specify container file path logs in workloads or Pod labels as the collection source.
  - When collecting node file path logs, users can set the node file path as the log collection source.
- **Consumer**: users can select the logsets and log topics of the CLS as the consumer end.
- **Extraction mode**: the log collection agent supports the delivery of collected logs to the user-specified log topic in the format of single-line text, JSON, separator-based text, multi-line text, or full regex.
- **Filter**: after filter is enabled, logs will be collected according to the specified rules. "key" supports full matching and the rule supports regex matching. For example, you can set to collect logs containing "ErrorCode = 404".

## Directions
[](id:open)
### Enabling log collection

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and choose **Cluster OPS** > **Feature Management** in the left sidebar.
2. At the top of the **Feature Management** page, select the region. On the right side of the cluster for which you want to enable log collection, click **Set**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/3f0743029e71e20e4f3b3bfdd7045bab.png)
3. On the "Configure Features" page, click **Edit** for log collection, enable log collection, and confirm this operation, as shown in the figure below:
![](https://main.qcloudimg.com/raw/9c1a88b996982ab6112f9032bfa15040.png)

### Configuring the log rules

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster OPS** > **Log Rules** in the left sidebar.
2. At the top of the “Log Rules” page, select the region and the cluster where you want to configure the log collection rules and click **Create**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/e94605fda5b4039d2c3eb285ffb415c0.png)
3. On the **Create Log Collecting Policy** page, select the collection type and configure the log source. Currently, the following collection types are supported: **Container Standard Output**, **Container File Path**, and **Node File Path**.
<dx-tabs>
::: Collecting standard output logs of a container
Select **Container Standard Output** as the collection type and configure the log source as needed. This type of log source allows you to select the workloads of multiple namespaces at a time, as shown in the figure below:
![](https://main.qcloudimg.com/raw/698a5beae709d6a78ac79579592dc70e.png)

:::
::: Collecting file logs in containers 
Select **Container File Path** as the collection type and configure the log source, as shown in the figure below:
![](https://main.qcloudimg.com/raw/5f1e65b240377f296eaf17a5750c9f91.png)
You can specify a file path or use wildcards for the collection path. For example, when the container file path is `/opt/logs/*.log`, you can specify the collection path as `/opt/logs` and the file name as `*.log`.
<dx-alert infotype="notice" title="">
If the collection type is selected as "Container File Path", the corresponding path <b>cannot be a soft link</b>. Otherwise, the actual path of the soft link will not exist in the collector's container, resulting in log collection failure.
</dx-alert>



​	

:::
::: Collecting file logs on nodes
Select **Node File Path** as the collection type. You can add custom `metadata` as needed. Attach `metadata` with a specified key-value pair to the collected log information to add the attached metadata to log records, as shown in the figure below:

>! One node log file can be collected for only one log topic.
>
![](https://main.qcloudimg.com/raw/7c5c8341315408c5668add566a3ff550.png)
You can specify a file path or use wildcards. For example, when the container file paths for collection are `/opt/logs/service1/*.log` and `/opt/logs/service2/*.log`, you can specify the folder of the collection path as `/opt/logs/service*` and the file name as `*.log`.
:::
</dx-tabs>
<dx-alert infotype="explain" title="">
For container standard output and container files (not mounted in hostPath), besides the original log content, the metadata related to the container or Kubernetes (such as the ID of the container that generated the logs) will also be reported to the CLS. Therefore, when viewing logs, users can trace the log source or search based on the container identifier or characteristics (such as container name and labels).
The metadata related to the container or Kubernetes is shown in the table below:
<table>
	<tr>
		<th>Field Name</th> <th>Description</th>
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

4. Configure the CLS as the consumer end. Select the desired logset and log topic. You can select new or existing log topics, as shown in the figure below:
>!
>- CLS currently only supports log collection and reporting for intra-region container clusters.
>- If there are already 10 log topics, you cannot create a new one.
>
![](https://main.qcloudimg.com/raw/3f51e21168a1cd506f6421c7dec06b52.png)



5. Click **Next** and choose a log extraction mode, as shown below:
>! Currently, one log topic supports only one collection configuration. Ensure that all container logs that adopt the log topic can accept the log parsing method that you choose. If you create different collection configurations under the same log topic, the earlier collection configurations will be overwritten.
>
![](https://main.qcloudimg.com/raw/7b1d1338253aba3082aa1d824b942e09.png)
<table>
<thead>
<tr>
<th>Parsing Mode</th>
<th>Description</th>
<th>Related Document</th>
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
<td><a href="https://cloud.tencent.com/document/product/614/32817">Full Regular Format (Single-Line)</a></td>
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
<td>In a separator log, the entire log data can be structured according to the specified separator, and each complete log ends with a line break `\n`. When CLS processes separator logs, you need to define a unique key for each separate field. Invalid fields, which are fields that need not be collected, can be left blank. However, you cannot leave all fields blank.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/32285">Separator Format</a></td>
</tr>
</tbody></table>

6. Enable the filter and configure rules as needed and then click **Done**, as shown in the figure below.
![](https://main.qcloudimg.com/raw/0fe472207c3c923caeb664533c44ae00.png)


### Updating the log rules
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster OPS** > **Log Rules** in the left sidebar.
2. At the top of the “Log Rules” page, select the region and the cluster where you want to update the log collection rules and click **Edit Collecting Rule** at the right, as shown in the figure below:
![](https://main.qcloudimg.com/raw/31dad4c82bdb27197873b5141dcfa3b0.png)
3. Update the configuration as needed and click **Done**.
>! The logset and log topic cannot be updated.
