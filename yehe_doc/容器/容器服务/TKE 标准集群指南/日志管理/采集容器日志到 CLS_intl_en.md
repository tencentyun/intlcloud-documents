This document introduces how to configure log collection rules in the TKE console and ship logs to [Tencent Cloud Log Service (CLS)](https://www.tencentcloud.com/zh/products/cls).

## Directions
### Creating log collection rules

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **OPS Center** > **Log Rules** in the left sidebar.
2. At the top of the **Log Rules** page, select the region and the cluster where you want to configure the log collection rules and click **Create**, as shown in the figure below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/AMJP139_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226153528.png)
3. On the **Create Log Collecting Policy** page, configure the consumer of logs: Set **Type** to **CLS** in the **Consumer end** area, as shown in the figure below.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/zCY5744_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226153647.png)
  - Rule name: You can customize the log collection rule name.
  - Log region: CLS supports cross-region log shipping. You can click **Modify** to select the destination region for log shipping.
  - Logset: Created logsets are displayed by log region. If the existing logsets are not suitable, you can create a new one in the [CLS console](https://console.cloud.tencent.com/cls). For operation details, see [Creating logset](https://intl.cloud.tencent.com/document/product/614/34238).
  - Log topic: Select the corresponding log topic under the logset. Two modes are supported: **Auto-create log topic** and **Select existing log topic**.
  - Advanced settings:
     - Default metadata: CLS sets the metadata `pod_name`, `namespace`, and `container_name` as indexes for log search by default.
     - Custom metadata: You can customize metadata and log indexes.
>?
>- CLS does not support cross-region log shipping (from Chinese mainland to outside the Chinese mainland and vice versa). For regions where CLS is not activated, logs can be shipped only to the nearest regions. For example, the container logs collected from a Shenzhen cluster can be shipped only to Guangzhou, and the containers logs collected from a Tianjin cluster can be shipped only to Beijing. You can find more information in the console.
>- Currently, a log topic only supports the collection configuration of one type of logs. That is, the log, audit, and event types cannot use the same topic. If they use the same topic, logs will be overwritten. Please ensure that the selected log topic is not occupied by other collection configurations. A logset can contain up to 500 log topics.
>- Custom metadata and metadata indexes cannot be modified once created. You can go to the [CLS console](https://console.cloud.tencent.com/cls) to modify the configuration.
>
4. Select the collection type and configure the log source. Currently, log collection types include **Container standard output**[](id:stout), **Container file path**[](id:insideDocker), and **Node file path**[](id:inside).
<dx-tabs>
::: Container Standard Output Logs
**Log source** supports **All containers**, **Specify workload**, and **Specify Pod Labels**, as shown in the figure below:
![](https://staticintl.cloudcachetci.com/yehe/backend-news/RXIn726_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226154431.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XpPd027_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226154553.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QhCS274_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226154637.png)

:::
::: Container File Logs 
- **Log source** supports **Specify workload** and **Specify Pod Labels**.
- You can specify a file path or use wildcards for the collection path. For example, when the container file path is `/opt/logs/*.log`, you can specify the collection path as `/opt/logs` and the file name as `*.log`.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HV7r317_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226154816.png)
![](https://staticintl.cloudcachetci.com/yehe/backend-news/M2z4825_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226154907.png)
<dx-alert infotype="notice" title="">
For **Container file path**, the corresponding path <b>cannot be a soft link</b>. Otherwise, the actual path of the soft link will not exist in the collector's container, resulting in log collection failure.
</dx-alert>

:::
::: Node File Logs
- You can specify a file path or use wildcards. For example, when the container file paths for collection are `/opt/logs/service1/*.log` and `/opt/logs/service2/*.log`, you can specify the folder of the collection path as `/opt/logs/service*` and the file name as `*.log`.
- You can attach metadata in key-value pair format to log records as needed.
![](https://main.qcloudimg.com/raw/7c5c8341315408c5668add566a3ff550.png)
<dx-alert infotype="explain" title="">
Each node log file can be collected to only one log topic.
</dx-alert>
:::
</dx-tabs>
<dx-alert infotype="explain" title="">
For **Container standard output** and **Container file path** (excluding **Node file path**/not mounted in hostPath), besides the original log content, the metadata related to the container or Kubernetes (such as the ID of the container that generated the logs) will also be reported to the CLS. Therefore, when viewing logs, users can trace the log source or search based on the container identifier or characteristics (such as container name and labels).
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
5. Configure the collection policy (**Full** or **Incremental**).
	- Full: Collecting logs from the beginning of the log file.
	- Incremental: Collecting logs 1 MB ahead of the end of the log file (for a log file less than 1 MB, incremental collection is equivalent to full collection).
6. Click **Next** and choose a log parsing method, as shown below:
    ![](https://staticintl.cloudcachetci.com/yehe/backend-news/KL5a497_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226155828.png)

  - Encoding Mode: Supports **UTF-8** and **GBK**.
  - Extraction Mode: Supports multiple extraction modes, as described below:
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
7. Click **Done**. 

### Updating the log rules
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Log Management** > **Log Rules** in the left sidebar.
2. At the top of the **Log Rules** page, select the region and the cluster where you want to update the log collection rules and click **Edit Collecting Rule** at the right, as shown in the figure below:
![](https://main.qcloudimg.com/raw/31dad4c82bdb27197873b5141dcfa3b0.png)
3. Update the configuration as needed and click **Done**.
>! The logset and log topic cannot be modified later.

## References
Besides using the TKE console, you can also configure log collection by using the Custom Resource Definitions (CRD). For more information, see [Using CRD to Configure Log Collection](https://intl.cloud.tencent.com/document/product/457/43936).
