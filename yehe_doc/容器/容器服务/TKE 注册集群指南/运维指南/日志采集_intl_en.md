This document describes how to ship logs of a registered cluster to [CLS](https://www.tencentcloud.com/products/cls) in the console.

## Overview
The log collection feature is a cluster log collection tool offered by TKE, which can ship logs in the specified cluster Services or node paths to [CLS](https://www.tencentcloud.com/products/cls). It is suitable for users who want to store and analyze service logs in a Kubernetes cluster.

You need to manually enable log collection for each cluster, and configure the collection rules. After log collection is enabled for a cluster, the log collection agent runs as a DaemonSet in the cluster, collects logs from the collection source based on the collection source, CLS log topic, and log parsing method configured by users in the log collection rules, and sends the collected logs to the consumer. Log collection supports the following operations:
- [Enabling log collection](#open)
- [Collecting standard output logs of a container](#stout)
- [Collecting file logs in containers](#insideDocker)
- [Collecting file logs on nodes](#inside)

## Notes
- You have created a registered cluster, and it is in **Running** status.
- Currently, logs of a registered cluster can be shipped to only [CLS](https://www.tencentcloud.com/products/cls) but not other log consumers.
- Before enabling log collection, ensure that there are sufficient resources on cluster nodes.
    - 0.11–1.1 CPU cores are required. You can increase the CPU resources on your own as needed.
    - 24 to 560 MB memory is required. You can increase the memory resources on your own as needed.
    - An individual log can be up to 512 KB in size and will be truncated if the limit is exceeded.
- To use the log collection feature, check whether nodes in the Kubernetes cluster can access the log consumer. Here, TKE ships logs over the public and private networks. You can select one option based on your business needs.
    - Shipping over public network: Cluster logs will be shipped to CLS over the public network. This requires that the cluster nodes can access the public network.
    - Shipping over private network: Cluster logs will be shipped to CLS over the private network. This requires that the cluster nodes are interconnected with CLS over the private network. Before choosing this option, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for confirmation.

## Concepts

- **Log Collection Agent**: The agent that TKE uses to collect logs. It adopts Loglistener and runs within the cluster as a DaemonSet.
- **Log Rules**: Configures rules to specify the log collection source, log topic, and log parsing method and configure the filter.
	- The log collection agent monitors changes in log collection rules. Such changes take effect within ten seconds.
	- Multiple log collection rules do not create multiple DaemonSets, but too many log collection rules cause the log collection agent to occupy more resources.
- **Log Source**: It includes the specified container standard output, files in containers, and node files.
	- When collecting container standard output logs, users can select TKE logs in all containers or specified workloads and specified Pod labels as the log collection source.
	- When collecting container file path logs, users can specify container file path logs in workloads or Pod labels as the collection source.
	- When collecting node file path logs, users can set the node file path as the log collection source.
- **Consumer**: It can be a logset or a log topic.
- **Extraction mode**: The log collection agent can ship the collected logs to the specified log topic in the format of single-line text, JSON, separator-based text, multi-line text, or full regex.
- **Filter**: Sets filters to collect only logs match the rules. "key" supports full matching and the rule supports regex matching. For example, you can set to collect logs containing "ErrorCode = 404".

## Directions

### Enabling log collection[](id:open)

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Ops Feature Management** on the left sidebar.
2. At the top of the **Feature Management** page, select the **Region** and **Registered Cluster**. Then, click **Set** on the right of the target cluster.
3. On the **Configure Features** page, click **Edit** for log collection, select **Enable Log Collection**, select the **Shipping Method**, and click **Confirm**.

### Configuring the log rules

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Ops Feature Management** on the left sidebar.
2. At the top of the **Feature Management** page, select the **Region** and **Registered Cluster**, select the target cluster, and click **Create**.
3. On the **Create Log Collection Rule** page, select the collection type and configure the log source. Currently, log collection types include **Container Standard Output**[](id:stout), **Container File Path**[](id:insideDocker), and **Node File Path**[](id:inside).
<dx-tabs>
::: Collecting standard output logs of a container
Select **Container Standard Output** as the collection type and configure the log source as needed. This type of log source allows you to select the workloads of multiple namespaces at a time.

:::
::: Collecting file logs in containers
Select **Container File Path** as the collection type and configure the log source.
You can specify a file path or use wildcards for the collection path. For example, when the container file path is `/opt/logs/*.log`, you can specify the collection path as `/opt/logs` and the file name as `*.log`.
<dx-alert infotype="notice" title=" ">
If the collection type is selected as "Container File Path", the corresponding path <b>cannot be a soft link</b>. Otherwise, the actual path of the soft link will not exist in the collector's container, resulting in log collection failure.
</dx-alert>

:::
::: Collecting file logs on nodes
Select **Node File Path** as the collection type. You can add custom `metadata` as needed. Attach `metadata` with a specified key-value pair to the collected log information to add the attached metadata to log records.
<dx-alert infotype="notice" title=" ">
Each node log file can be collected to only one log topic.
You can specify a file path or use wildcards. For example, when the container file paths for collection are `/opt/logs/service1/*.log` and `/opt/logs/service2/*.log`, you can specify the folder of the collection path as `/opt/logs/service*` and the file name as `*.log`.
</dx-alert>
:::
</dx-tabs>
<dx-alert infotype="explain" title=" ">
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

4. Configure the CLS consumer. Select the target **Log Set** and **Log Topic**. You can create a log topic or select an existing one.
   
>!
>- Currently, [CLS](https://www.tencentcloud.com/products/cls) only supports log collection and reporting for TKE clusters in the same region.
>- If there are already 500 log topics in the logset, no more log topics can be created.
>
5. You can specify a key value in **Advanced Settings** to ship logs to the specified partition. This feature is disabled by default, and logs are shipped to random partitions. After it is enabled, logs with the same key are shipped to the same partition. You can enter the `TimestampKey` (which is `@timestamp` by default) and specify the timestamp format.



6. Click **Next** and choose a log extraction mode.
>! Currently, you can configure the log parsing method only for logs shipped to CLS.
>
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
<td><a href="https://intl.cloud.tencent.com/document/product/614/39589">Full Regex Format (Single-Line)</a></td>
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
<td>Structure the data in a log with the specified separator, and each complete log ends with a line break `\n`. Define a unique key for each separate field. Leave the field blank if you don't need to collect it. At least one field is required.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/32285">Separator Format</a></td>
</tr>
</tbody></table>

6. Enable the filter and configure rules as needed and then click **Done**.

### Updating the log rules
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Log Management** > **Log Rules** on the left sidebar.
2. At the top of the **Log Rules** page, select the **Region** and **Registered Cluster**, select the target cluster, and click **Edit Collection Rule** on the right.
3. Update the configuration as needed and click **Done**.
>! The logset and log topic cannot be modified later.

## References
- [Using CRD to Configure Log Collection via YAML](https://intl.cloud.tencent.com/document/product/457/43936)
