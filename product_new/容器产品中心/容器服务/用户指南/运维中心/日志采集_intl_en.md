## Operation Scenario
TKE's log collection feature allows you to collect logs within the cluster. It sends logs for services in the cluster or specific paths in a cluster node to Kafka, Elasticsearch, or [Tencent Cloud Log Service (CLS)](https://cloud.tencent.com/product/cls). Log collection is suited to users who need to store and analyze service logs in Kubernetes clusters.

Log collection must be manually enabled for each cluster. After enabling, the log collection agent runs as a DaemonSet within the cluster and sends the collected information to the consumer based on the collection source and consumer configured by users in the log collection rules. Enable log collection according to the operations below:
- [Collecting Container Standard Output Logs](#output)
- [Collecting File Logs in Container](#insideDocker)
- [Collecting File Logs on Node](#inside)
- [Configuring Consumer of Logs](#consumer)



## Prerequisites
- Please ensure the cluster node has sufficient resources before enabling. Enabling log collection occupies some cluster resources. By default, each node occupies approximately 0.3 cores of CPU and 250 MB of memory.
 - CPU resources occupied: 0.3 cores by default. You can increase this as needed if the quantity of logs is too large. The maximum recommended configurations are 1 core for **request** and 2 cores for **limit**.
 - Memory resources occupied: 250 MB by default. You can increase this as needed if the quantity of logs is too large. The maximum recommended configurations are 1GB for **request** and 1.5GB for **limit**.
 - Maximum log length: Up to 512 K for one log. The log is truncated if this limit is exceeded.
- To use log collection, confirm that nodes in the Kubernetes cluster can access the consumer of logs. Only Kubernetes clusters of version 1.10 or higher support the following log collection features.

## Concepts

- **Log Collection Agent**: The agent that TKE uses to collect log messages. It is based on Fluentd and runs within the cluster as a DaemonSet.
- **Log Collection Rules**: You can specify the log collection source and the consumer to which the collected logs are sent.
 - The log collection agent monitors changes in the log collection rules, and rule changes take effect within 10 seconds.
 - Multiple log collection rules do not create multiple DaemonSets, but too many log collection rules cause the log collection agent to occupy more resources.
- **Log Source**: This includes specified container logs and node path logs.
 - To collect logs that are printed to standard output from services in the cluster, you can set the source to the specified container logs, or all or several specified logs of Namespace.
 - To collect logs under specific paths in a cluster node, you can set the source to the node path log. For example, to collect logs under paths in the format of `/var/lib/docker/containers/<container-id>/<container-id>.json-log`, you can specify the log collection path as `/var/lib/docker/containers/*/*.json-log`.
- **Consumer**: The log collection agent collects logs from the specified source and sends these logs to the consumer specified by the user.
 - The log collection service supports setting user-built Elasticsearch, Kafka, Tencent Cloud's Ckafka service or Tencent Cloud Log Service (CLS) as the consumer of logs.
 - Logs collected by the log collection agent are sent to the user-specified consumer in JSON format.


## Steps
<span id="output"></span>
### Collecting Container Standard Output Logs 
The log collection feature supports collecting standard output logs of specified containers in Kubernetes clusters. You can configure collection rules flexibly based on your needs.
The collected log messages are output to the user-specified consumer in JSON format with Kubernetes metadata attached, including the information of the pod to which the container belongs, such as label, annotation, etc.

#### Configuration Method
1. Log in to [TKE Console](https://console.cloud.tencent.com/tke2) and click **Log Collection** on the left sidebar.
2. After selecting the region and cluster at the top of the log collection page, click **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/200096f6e53ecad93e926288e4fff039.png)
3. On the "Create a log collection policy" page, select the **Container standard output** collection type and then configure the log source. See the figure below:
![](https://main.qcloudimg.com/raw/6dae58e1ecc389a3e547c815251f8942.png)
When you select container standard output as the collection type, the metadata below is added for each log by default, with `log` as the raw log message. This type of log source supports selecting workloads of multiple Namespaces at the same time.
<table>
	<tr>
		<th>Field Name</th> <th>Description</th>
	</tr>
	<tr>
		<td>docker.container_id</td> <td>ID of the container to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.annotations</td> <td>Annotations of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.container_name</td> <td>Name of the container to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.host</td> <td>IP address of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.labels</td> <td>Labels of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.namespace_name</td> <td>Namespace of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.pod_id</td> <td>ID of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.pod_name</td> <td>Name of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>log</td> <td>Raw log message</td>
	</tr>
</table>
4. Configure the consumer of logs. It is recommended to set Tencent Cloud CLS as the consumer of logs. See the figure below:
![](https://main.qcloudimg.com/raw/058f4e0daedc7aeb937334b533ab784c.png)
5. Click **Complete** to complete the creation.



<span id="insideDocker"></span>
### Collecting File Logs in Container 
The log collection feature also supports collecting logs of files in a specified pod within a cluster.
The collected log messages are output to the user-specified consumer in JSON format with Kubernetes metadata attached, including the label of the pod to which the container belongs, annotation, etc.
>!Currently, you can only collect log files stored in volumes. You must mount volumes such as emptyDir, hostpath, etc. when creating a workload and save the log files to the specified volume.


#### Configuration Method
1. Log in to [TKE Console](https://console.cloud.tencent.com/tke2) and click **Log Collection** on the left sidebar.
2. After selecting the region and cluster at the top of the log collection page, click **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/0cf8d00fafa57911e01c34b75998d898.png)
3. Set the collection type as **Container file path** and configure the log source. See the figure below:
>?You can specify a path or use wildcards to collect the log file under the corresponding path on the pod. For example: `/var/log/nginx.log` or `/var/lib/docker/containers/*/*.log`.
>
![](https://main.qcloudimg.com/raw/58420318770b988bd7dcc8d5640e2e22.png)
When you select container file path as the collection type, the metadata below is added for each log by default, with `message` as the raw log message. This type of log source does not support selecting workloads of multiple Namespaces.
<table>
	<tr>
		<th>Field Name</th> <th>Description</th>
	</tr>
	<tr>
		<td>docker.container_id</td> <td>ID of the container to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.annotations</td> <td>Annotations of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.container_name</td> <td>Name of the container to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.host</td> <td>IP address of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.labels</td> <td>Labels of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.namespace_name</td> <td>Namespace of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.pod_id</td> <td>ID of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>kubernetes.pod_name</td> <td>Name of the pod to which logs belong</td>
	</tr>
	<tr>
		<td>file</td> <td>Source log file</td>
	</tr>
	<tr>
		<td>message</td> <td>Raw log message</td>
	</tr>
</table>
4. Configure the consumer of logs. It is recommended to set Tencent Cloud CLS as the consumer of logs. See the figure below:
 ![](https://main.qcloudimg.com/raw/65ac9ab0f28015c1332fb06729d39b0d.png)
5. Click **Complete** to complete the creation.


<span id="inside"></span>
### Collecting File Logs on Node 

The log collection feature allows you to collect logs under the specified node paths on all nodes in the cluster. You can configure the required paths flexibly based on your own needs. The log collection agent collects file logs under the paths that meet the specified path rules on all nodes in the cluster.
The collected log messages are output to the user-specified consumer in JSON format with user-specified metadata attached, including the path of the source file and custom metadata.


#### Configuration Method
1. Log in to [TKE Console](https://console.cloud.tencent.com/tke2) and click **Log Collection** on the left sidebar.
2. After selecting the region and cluster at the top of the log collection page, click **Create**. See the figure below:
![](https://main.qcloudimg.com/raw/bad4e979f12a5e688bf28db4ae441dc5.png)
3. On the "Create a log collection policy" page, select **Node file path** collection type. See the figure below:
>?You can specify a path or use wildcards to collect the log file under the corresponding path on the node in the cluster. For example: `/var/log/nginx.log` or `/var/lib/docker/containers/*/*.log`.
>
![](https://main.qcloudimg.com/raw/deaa30ef8bbd990c7eadbcdf07727d0d.png)
You can add custom `metadata` as needed. Attach `metadata` to the collected log messages, specified in key-value format, to serve as metadata tags for the log messages.
Attached metadata will be added to the log record in JSON format. See the figure below:
![](https://main.qcloudimg.com/raw/5b443aca528640c5666b1b7e328ef275.png)
For example: **Without** specified metadata attached, the collected logs appear as below:
![](https://mc.qcloudimg.com/static/img/5386281fc3ed14c4f41ba723a23dc3ec/host-log-without-metadata.png)
**With** specified metadata attached, the collected logs appear as below:
![](https://mc.qcloudimg.com/static/img/c571be8fbc995ab083c2676e3b10861f/host-log-with-metadata.png)
Compared to logs without specified metadata attached, JSON logs with metadata attached have an additional key `service`.
Log metadata is defined as follows:
<table>
	<tr>
		<th>Field Name</th> <th>Description</th>
	</tr>
	<tr>
		<td>path</td> <td>Source file of log</td>
	</tr>
	<tr>
		<td>message</td> <td>Log message</td>
	</tr>
	<tr>
		<td>Custom key</td> <td>Custom value</td>
	</tr>
</table>
4. Configure the consumer of logs. It is recommended to set Tencent Cloud CLS as the consumer of logs. See the figure below:
![](https://main.qcloudimg.com/raw/3d55fcd2a828f0ca74eb1e985e35a518.png)
5. Click **Complete** to complete the creation.



<span id="consumer"></span>
### Configuring Consumer of Logs 
The log collection feature supports setting user-built Kafka pods, topics specified by Tencent Cloud Ckafka pods, or log topics specified by Tencent Cloud Log Service (CLS) as the consumer of log content. The log collection agent will send the collected logs to the topic specified by Kafka or the log topic specified by CLS.

#### Configuring Kafka as Consumer of Logs
Only Kafka pods without access authentication are supported. All nodes in the cluster must be able to access the Kafka topic specified by users.
If you use the Ckafka service provided by Tencent Cloud, select Ckafka Pod. Otherwise, enter the Kafka access address and topic. See the figure below:
![](https://main.qcloudimg.com/raw/f7103fec732ee1fde9f54bf2729253ad.png)

#### Configuring CLS as Consumer of Logs
>!CLS currently only supports log collection and reporting for intra-region container clusters.
>
1. Because TKE’s logs have an independent collection capability, you don’t have to enable **LogListener** to create a logset. See the figure below:
![](https://main.qcloudimg.com/raw/7444cb3e96707452a021188c9a3d83e2.png)
2. Enable **Log Indexing** for the log topic. See the figure below:
![](https://main.qcloudimg.com/raw/a8413fb410367e01acfa9ff62e7a291d.png)

#### Configuring Elasticsearch as Consumer of Logs
Only Elasticsearch services without access authentication are supported. All nodes in the cluster must be able to access the Elasticsearch service specified by users.
Enter the Elasticsearch service's access address and storage index. See the figure below:
![](https://main.qcloudimg.com/raw/cd011bdea14e7d47dce4779d1a77af52.png)

