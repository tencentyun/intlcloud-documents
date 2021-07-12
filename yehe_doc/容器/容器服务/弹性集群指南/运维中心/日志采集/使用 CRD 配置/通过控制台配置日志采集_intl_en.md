

## Overview
In EKS, you can [use environment variables to configure log collection](https://intl.cloud.tencent.com/document/product/457/37907), and collect logs by line without parsing, or use custom resource definitions (CRD) to configure log collection.

CRD is non-intrusive to Pod and supports single-line, multi-line, separator, full regex, JSON and other log parsing methods. It sends standard output and file logs in the container to [Tencent Cloud CLS](https://intl.cloud.tencent.com/product/cls), which provides various services such as search and analysis, visualization applications, log download and consumption. It is recommended to use CRD to configure log collection.

To use CRD to configure log collection, you need to manually enable the log collection feature and set the collection rules for each cluster. The collector will collect logs from the collection source based on the collection source, CLS log topic, and log parsing method configured in the log collection rules, and send the log content to the CLS for storage. You can refer to the following directions to use CRD to configure the log collection of the EKS cluster:
<dx-steps>
-[Authorization on first use](#role)
-[Enabling log collection](#open)
-[Configuring the log rules](#rules)
-[Configuring the log consumer end](#cls)
-[Configuring the log extraction mode](#index)
</dx-steps>

#### Notes
- Using CRD to configure log collection is currently only valid for Pods created after May 25, 2021. If you need to use CRD to configure log collection for the Pods created before, please terminate the Pod and recreate one.
- If the Pods are configured with environment variables and CRD to collect logs at the same time, it will cause repeated collection and repeated billing. Therefore, when using CRD to configure log collection, please delete the relevant environment variables.


## Concepts

- **Log rule**: users can use log rules to specify the log collection source, log consumer end, and log parsing method, configure filters, and upload the log that failed to parse etc. The log collector will monitor the changes of the log collection rules, and the changed rules will take effect within 10 seconds.
- **Log source**: includes the standard output of the specified container and the files in the container.
  - When collecting container standard output logs, users can select TKE logs in all containers or specified workloads and specified Pod labels as the log collection source.
  - When collecting container file path logs, users can specify container file path logs in workloads or Pod labels as the collection source.
- **Consumer**: users can select the logsets and log topics of the CLS as the consumer end.
- **Extraction mode**: the log collection agent supports the delivery of collected logs to the user-specified log topic in the format of single-line text, JSON, separator-based text, multi-line text, or full regex.
- **Filter**: after filter is enabled, logs will be collected according to the specified rules. "key" supports full matching and the rule supports regex matching. For example, you can set to collect logs containing "ErrorCode = 404".
- **Upload the log that failed to parse**: after this feature is enabled, all logs that failed to parse (as the “Key”), and the original log content (as the “Value”) are uploaded. When this feature is disabled, the logs that failed to parse will be discarded.

## Directions



### Authorization on first use[](id:role)
When using the log collection feature of the EKS cluster for the first time, you need to authorize the CLS and other related permissions to ensure that the logs are normally uploaded to the CLS.
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=4), and select **Cluster OPS** > **[Feature Management](https://console.cloud.tencent.com/tke2/ops/list?rid=1)** in the left sidebar.
2. At the top of the **Feature Management** page, select the region and **Elastic Cluster**. On the right side of the cluster for which you want to enable log collection, click **Set**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/3cfd54126fa59a0fb1e6346e97e93c63.png)
3. On the **Configure Features** page, click **CAM** to complete authorization.
After authorization is completed, the role TKE_QCSLinkedRoleInEKSLog will be bound to your account by default, and the default policy configured for this role is QcloudAccessForTKELinkedRoleInEKSLog.

>?You only need to authorize when you use the log collection feature for the first time. If you delete the above roles, you need to authorize again.



### Enabling log collection[](id:open)

After completing the authorization, you can enable the log collection.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=4), and select **Cluster OPS** > **[Feature Management](https://console.cloud.tencent.com/tke2/ops/list?rid=1)** in the left sidebar.
2. At the top of the **Feature Management** page, select the region and **Elastic Cluster**. On the right side of the cluster for which you want to enable log collection, click **Set**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/3cfd54126fa59a0fb1e6346e97e93c63.png)
3. On the "Configure Features" page, click **Edit** for log collection, enable log collection, and confirm this operation, as shown in the figure below:
![](https://main.qcloudimg.com/raw/9b4a3bbf281cbde5515c34484f55ff40.png)




### Configuring the log rule[](id:rules)

After enabling the log collection, you need to configure the log rules including the log source, consumer end, log parsing method, and so on.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=4), and select **Cluster OPS** > **[Log Collection Rules](https://console.cloud.tencent.com/tke2/ops/list?rid=1)** in the left sidebar.
2. At the top of the “Log Rules” page, select the region and the EKS cluster where you want to configure the log collection rules and click **Create**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/38f9678feea9197bd6127a732919f4e4.png)
3. On the "Create Log Collecting Policy" page, select the collection type and configure the log source, consumer end, log parsing method. Currently, the following collection types are supported: [container standard output](#stout) and [container file path](#insideDocker).
<dx-tabs>
::: Collecting standard output logs of a container[](id:stout)
Select **Container standard output** as the collection type, and configure the log source as needed, as shown below:
![](https://main.qcloudimg.com/raw/6c7cf280bd2ab0a0f5532b4d89bd5dd1.png)
This type of log source supports:
- **All containers**: all namespaces or all containers under a namespace.
- **Specify workload**: the containers of a specified workload under a namespace. You can add multiple namespaces.
- **Specify Pod Labels**: specify multiple Pod Labels under a namespace, and collect all containers that match the Labels.

:::
::: Collecting file logs in container[](id:insideDocker) 
Select **Container file path** as the collection type, and configure the log source as needed, as shown below:
![](https://main.qcloudimg.com/raw/2a85238ed6eca7dfdf6391d814dca755.png)
This type of log source supports:

- **Specify workload**: the specified file path of a container of a specified workload under a namespace.
- **Specify Pod Labels**: specify multiple Pod Labels under a namespace, and collect the specified file path of all containers that match the Labels.

You can specify a file path or use wildcards for the collection path. For example, when the container file path is `/opt/logs/*.log`, you can specify the collection path as `/opt/logs` and the file name as `*.log`.

:::
</dx-tabs>
<dx-alert infotype="explain" title="">
For container standard output and container files, besides the original log content, the metadata related to the container or Kubernetes (such as the name of the Pod that generated the logs) will also be reported to the CLS. Therefore, when viewing logs, users can trace the log source or search based on the container identifier or characteristics (such as container name and labels).
The metadata related to the container or Kubernetes is shown in the table below:
<table>
	<tr>
		<th>Field Name</th> <th>Description</th>
	</tr>
	<tr>
		<td>cluster_id</td> <td>The ID of the cluster to which logs belong</td>
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
		<td>pod_ip</td> <td>The IP of the Pod to which logs belong</td>
	</tr>
	<tr>
		<td>pod_lable_{label name}</td> <td>The labels of the Pod to which logs belong (for example, if a Pod has two labels: app=nginx and env=prod, 
the reported log will have two metadata entries attached: pod_label_app:nginx and pod_label_env:prod).
</td>
	</tr>
</table>
</dx-alert>
4. [](id:cls)Configure the CLS as the consumer end. Select the desired logset and log topic. It is recommended to select **Auto-create Log Topic**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/72b49b6cc19d95253786443ae33bf171.png)
<dx-alert infotype="notice" title="">
- CLS currently only supports log collection and reporting for intra-region container clusters.
- The log set and log topic cannot be updated after the log rule is configured.
</dx-alert>
5. [](id:index)Click **Next** and choose a log extraction mode, as shown below:
![](https://main.qcloudimg.com/raw/da5dbe45f89a3acac6aca2f575b2074a.png)

<b>Extraction modes</b>

<table>
<thead>
<tr>
<th>Parsing Mode</th>
<th>Description</th>
<th>Related Document</th>
</tr>
</thead>
<tbody><tr>
<td>Single-line text</td>
<td>A log contains only one line of content, and the line break `\n` to mark the end of a log. Each log will be parsed into a complete string with <strong>CONTENT</strong> as the key value. When log Index is enabled, you can search for log content via full-text search. The time attribute of a log is determined by the collection time.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/32287">Full Text in a Single Line</a></td>
</tr>
<tr>
<td>Multi-line texts</td>
<td>A log with full text in multi lines spans multiple lines and a first-line regular expression is used for match. When a log in a line matches the preset regular expression, it is considered as the beginning of a log, and the next matching line will be the end mark of the log. A default key value, <strong>CONTENT</strong>, will be set as well. The time attribute of a log is determined by the collection time. The <a href="#auto">regular expression</a> can be generated automatically.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/614/32284">Full Text in Multi Lines</a></td>
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

<dx-alert infotype="notice" title=""> 
Currently, one log topic supports only one collection configuration. Ensure that all container logs that adopt the log topic can accept the log parsing method that you choose. If you create different collection configurations under the same log topic, the earlier collection configurations will be overwritten.
</dx-alert>
6. Enable other features as needed.
	- Enable the filter and configure the rules.
	After the filter is enabled, only the logs that meet the filter rules will be collected. Key supports full matching and the rule supports regex matching. For example, you can set to collect logs containing "ErrorCode = 404".
	- Enable the upload of the log that failed to parse
	After this feature is enabled, all logs that failed to parse (as the “Key”), and the original log content (as the “Value”) are uploaded. When this feature is disabled, the logs that failed to parse will be discarded.
7. Click **Done** to complete the creation.


### Updating the log rules

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster?rid=4), and select **Cluster OPS** > **[Log Collection Rules](https://console.cloud.tencent.com/tke2/ops/list?rid=1)** in the left sidebar.
2. In the **Log Collection Rules** page, select the log rule to update, and click **Edit Collecting Rule** on the right side of the rule, as shown below:
   ![](https://main.qcloudimg.com/raw/1734b1c00233c6cd9c2fd8309933c233.png)
3. Update the configuration as needed and click **Done**.



## FAQ
If you have problems, you can refer to [EKS Log Collection FAQs](https://intl.cloud.tencent.com/document/product/457/40582). If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1) to contact us.
