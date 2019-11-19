## Overview
TKE users can directly configure a log collection rule in the console to collect cluster logs and send the collected logs to a specific Cloud Log Service (CLS) log topic. Through the log collection feature, the CLS platform supports real-time search, consumption, and shipping of cluster service logs.

## Access directions

### 1. Creating a logset and a log topic

Log in to the [CLS Console](https://console.cloud.tencent.com/cls) and create a logset and a log topic. TKE logs can be collected using independent collector. So, when creating a log topic, you do not need to enable **LogListener**. For more information, see [Creating a Logset and a Log Topic](https://intl.cloud.tencent.com/document/product/614/31592).
![](https://main.qcloudimg.com/raw/2e4dd19d4e257d4485b878c23497d302.png)
>Currently, TKE cluster logs can only be shipped to CLS within the same region.



### 2. Associating a TKE cluster

 (1) Log in to the [TKE Console](https://console.cloud.tencent.com/tke2). In the left sidebar, click **Log Collection**. At the top of the log collection page, select region and cluster, and then click **Create**.
(2) Create a log collection rule.
![](https://main.qcloudimg.com/raw/4c610f0d00a6c30f743a22276331d81b.png)
Rule configuration items are described as follows.
<table>
   <tr>
      <th>Configuration Item</th>
      <th>Details</th>
   </tr>
   <tr>
      <td>Collection rule name</td>
      <td>A name contains up to 63 characters, including lowercase letters, numbers, and separators ("-"), and must begin with a lowercase letter and end with a number or lowercase letter.<br>Once set, the name cannot be modified.</td>
   </tr>
   <tr>
      <td>Type</td>
			<td>3 types of collection tasks are supported: <a href="#log1">Collecting container standard output Logs</a>, <a href="#log2">Collecting container file logs</a>, and <a href="#log3">Collecting CVM file logs</a>.
   </tr>
   <tr>
      <td>Log source</td>
      <td>You can choose to collect logs from all containers or a specified container.</td>
   </tr>
   <tr>
      <td>Consumption end</td>
      <td>Select CLS.</td>
   </tr>
   <tr>
      <td>CLS instance</td>
      <td>Select logset and log topic.</td>
   </tr>
</table>

>TKE supports 3 types of collection tasks. The following describes in detail how to configure these 3 types of collection tasks.

<span id="log1"></span>
#### Collecting container standard output logs

You can configure shipping standard output logs to CLS from a specified container in the Kubernetes cluster. The shipped logs carry the relevant Kubernetes metadata, including the label and annotation of the pod to which the container belongs.

(1) On the **Create a log collection policy** page, select the **Container standard output** collection type and then configure the log source.
 ![](https://main.qcloudimg.com/raw/634fde6b7a666ea98f835aeba8e65c6a.png)
(2) When you select container standard output as the collection type, the metadata below is added for each log by default, with `log` as the raw log message. This type of log source supports selecting workloads of multiple Namespaces at the same time.

| Field Name                    | Description                        |
| ------------------------- | --------------------------- |
| docker.container_id       | ID of the container to which logs belong     |
| kubernetes.annotations    | Annotations of the pod to which logs belong |
| kubernetes.container_name | Name of the container to which logs belong   |
| kubernetes.host           | IP address of the pod to which logs belong  |
| kubernetes.labels         | Labels of the pod to which logs belong      |
| kubernetes.namespace_name | Namespace of the pod to which logs belong   |
| kubernetes.pod_id         | ID of the pod to which logs belong          |
| kubernetes.pod_name       | Name of the pod to which logs belong         |
| log                       | Raw log message                |


<span id="log2"></span>
### Collecting file logs in container

You can configure the shipping of logs of files in a specified pod in the cluster to CLS. Logs must be shipped in JSON format, and will carry the relevant Kubernetes metadata, including the label and annotation of the pod to which the container belongs.

>Currently, you can only collect log files stored in volumes. You must mount volumes such as emptyDir and hostpath when creating a workload and save the log files to the specified volume.

(1) In the **Type** field, select **Container file path**, and configure a log source.
You can specify a file path or use wildcards to collect the log file under the corresponding path on the pod, for example, `/var/log/nginx.log` or `/var/lib/docker/containers/*/*.log`.
![](https://main.qcloudimg.com/raw/1b6411fcdb6608ecfabfa3a3dcc7ff44.png)
(2) When you select the container file path as the collection type, the metadata below is added for each log by default, with `message` as the raw log message. This type of log source does not support selecting workloads of multiple Namespaces.

| Field Name                    | Description                        |
| ------------------------- | --------------------------- |
| docker.container_id       | ID of the container to which logs belong     |
| kubernetes.annotations    | Annotations of the pod to which logs belong |
| kubernetes.container_name | Name of the container to which logs belong   |
| kubernetes.host           | IP address of the pod to which logs belong  |
| kubernetes.labels         | Labels of the pod to which logs belong      |
| kubernetes.namespace_name | Namespace of the pod to which logs belong   |
| kubernetes.pod_id         | ID of the pod to which logs belong          |
| kubernetes.pod_name       | Name of the pod to which logs belong         |
| file                      | Source log file                  |
| message                   | Raw log message                |


<span id="log3"></span>
#### Collecting file logs on CVM

You can configure shipping logs for all nodes in a cluster from the specified CVM path to CLS. The logs are shipped in JSON format with user-specified metadata attached, including the path of the source file and custom metadata.

(1) On the **Create a log collection policy** page, select **Node file path** in the **Type** field.
You can specify a file path or use wildcards to collect the log file under the corresponding path on the node in the cluster, for example, `/var/log/nginx.log` or `/var/lib/docker/containers/*/*.log`.
![](https://main.qcloudimg.com/raw/44e1288b51b78d1217bc830db2880620.png)
(2) You can add custom `metadata` as needed. Attach `metadata` to the collected log messages, specified in key-value format, to serve as metadata tags for the log messages.
Attached metadata will be added to the log record in JSON format.
![](https://main.qcloudimg.com/raw/c2ebaa3b482c16beaaabbc8182cd595a.png)
For example:
- **Without** specified metadata attached, the collected logs appear as follows:
![](https://main.qcloudimg.com/raw/efcef670013f184cc5b32f21dd9f3e6a.png)
- **With** specified metadata attached, the collected logs appear as follows:
![](https://main.qcloudimg.com/raw/4cb172b191581b00e6f7c77eecba9e70.png)

Compared to logs without specified metadata attached, JSON logs with metadata attached have an additional key `service`.
Log metadata is defined as follows:

| Field Name     | Description           |
| ---------- | -------------- |
| path       | Source file of the logs |
| message    | Log message       |
| Custom key | Custom value   |



### 3. Searching TKE logs

**Prerequisites**: Before performing the log search, you need to configure and enable the index. For more information, see [Enabling Index](<https://intl.cloud.tencent.com/document/product/614/16981>).

(1) Log in to the [CLS Console](https://console.cloud.tencent.com/cls). Click **Log Search** in the left sidebar to enter the search page.
(2) Select a log topic associated with TKE, and click **Search**.

![](https://main.qcloudimg.com/raw/a84d51ae441f1e46d170acf4c7a58e4e.png)





