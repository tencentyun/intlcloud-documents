## Introduction
TKE's log collection feature allows you to collect logs in a cluster and send logs in specific paths of cluster services or nodes to Kafka, Elasticsearch, or [Tencent Cloud Log Service (CLS)](https://intl.cloud.tencent.com/product/cls). Log collection applies to users who need to store and analyze service logs in Kubernetes clusters.

Log collection must be manually enabled for each cluster. After log collection is enabled for a cluster, the log collection agent runs as a DaemonSet in the cluster, collects logs from the collection source, and sends the collected logs to the consumer based on the collection source and consumer configured using the log collection rules. Log collection supports the following operations:
- [Collecting standard output logs of a container](#output)
- [Collecting File logs of a pod](#insideDocker)
- [Collecting File logs in specified node paths](#inside)
- [Configuring the consumer of logs](#consumer)



## Prerequisites
- The cluster node has sufficient resources before log connection is enabled. Enabling log collection will occupy approximately 0.3 CPU cores and 250 MB memory of each cluster node by default.
 - CPU resources occupied: 0.3 CPU cores by default. You can increase this value if the log quantity is too large. We recommend that `request` be set to 1 core and `limit` be set to 2 cores.
 - Memory resources occupied: 250 MB by default. You can increase this value if the log quantity is too large. We recommend that `request` be set to 1 GB and `limit` be set to 1.5 GB.
 - Maximum log length: 512 KB for a log. A log will be truncated if its length exceeds the limit.
- To use log collection, ensure that nodes in a Kubernetes cluster can access the log consumer. Only Kubernetes clusters of version 1.10 or later support the following log collection features.

## Concepts

- **Log Collection Agent**: the agent that TKE uses to collect logs. It is developed based on Fluentd and runs as a DaemonSet in a cluster.
- **Log Collection Rules**: you can specify the log collection source and the consumer to which the collected logs are sent.
 - The log collection agent monitors changes in the log collection rules, and changed rules take effect within 10 seconds.
 - Multiple DaemonSets will not be created if there are multiple log collection rules. However, too many log collection rules cause the log collection agent to occupy more resources.
- **Log Source**: this includes specified container logs and node path logs.
 - To collect standard output logs of services in a cluster, you can set the source to the specified container logs or service logs of all or several namespaces.
 - To collect logs in specific paths of cluster nodes, you can set the source to the node path logs. For example, to collect logs under paths in the format of `/var/lib/docker/containers/<container-id>/<container-id>.json-log`, you can specify the log collection path as `/var/lib/docker/containers/*/*.json-log`.
- **Consumer end**: after the log collection agent collects logs from the specified source, it will send these logs to the specified consumer.
 - The log collection service allows you to set the off-premises Elasticsearch, Kafka, Tencent Cloud's Ckafka service or Tencent Cloud Log Service (CLS) as the consumer of logs.
 - The log collection agent sends collected logs to the specified consumer in JSON format.


## Directions
<span id="output"></span>
### Collecting standard output logs of a container 
The log collection feature allows you to collect standard output logs of a specified container in Kubernetes clusters. You can configure collection rules flexibly based on your needs.
The collected logs are sent to the specified consumer in JSON format with Kubernetes metadata, including the labels and annotations of the pod to which the container belongs.

#### Configuration method
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Log Collection** in the left sidebar.
2. After selecting the region and cluster at the top of the log collection page, click **Create**, as shown below:
![](https://main.qcloudimg.com/raw/bcee30ade672b8a4e114d25f3d5abd16.png)
3. On the Create a log collection policy page, select **Container standard output** and configure the log source, as shown below:
![](https://main.qcloudimg.com/raw/8f10a39a943ccce8724dff252ee00e88.png)
When you select container standard output as the collection type, the metadata below will be added for each log by default. `log` indicates the raw log information. This log source type allows you to select workloads of multiple namespaces at the same time.
<table>
	<tr>
		<th>Field</th> <th>Description</th>
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
		<td>kubernetes.host</td> <td>Host IP address of the pod to which logs belong</td>
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
		<td>log</td> <td>Raw log information</td>
	</tr>
</table>
4. Configure the consumer of logs. We recommend that Tencent Cloud CLS be set as the consumer of logs, as shown below:
![](https://main.qcloudimg.com/raw/2a6f0cbb9efcc749f78bc531076b865d.png)
5. Click **Done** to complete the creation.



<span id="insideDocker"></span>
### Collecting file logs of a pod 
The log collection feature also allows you to collect file logs of a specified pod in a cluster.
The collected logs are sent to the specified consumer in JSON format with Kubernetes metadata, including the labels and annotations of the pod to which the container belongs.
> Currently, you can only collect log files stored in volumes. You must mount volumes such as emptyDir and hostpath when creating a workload and save the log files to the specified volume.


#### Configuration method
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Log Collection** in the left sidebar.
2. After selecting the region and cluster at the top of the log collection page, click **Create**, as shown below:
![](https://main.qcloudimg.com/raw/31e736aeb7c96977d2978eff5e9b83ba.png)
3. Set the collection type to **Container file path** and configure the log source, as shown below:
> You can specify a path or use wildcards, for example, `/var/log/nginx.log` or `/var/lib/docker/containers/*/*.log` to collect log files in the corresponding paths of the pod.

![](https://main.qcloudimg.com/raw/42b80d3b0ee85a4898a7ab1bf13352c6.png)
When you select container file path as the collection type, the metadata below is added for each log by default. `message` indicates the raw log information. This log source type does not support selecting workloads of multiple namespaces.
<table>
	<tr>
		<th>Field</th> <th>Description</th>
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
		<td>kubernetes.host</td> <td>Host IP address of the pod to which logs belong</td>
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
		<td>message</td> <td>Raw log information</td>
	</tr>
</table>
4. Configure the consumer of logs. We recommend that Tencent Cloud CLS be set as the consumer of logs, as shown below:
 ![](https://main.qcloudimg.com/raw/154f1564c65d9d2e221ab484d47c1fb1.png)
5. Click **Done** to complete the creation.

<span id="inside"></span>

### Collecting file logs in specified node paths 

The log collection feature allows you to collect logs in specified node paths of all nodes in a cluster. You can configure the required paths flexibly based on your needs. The log collection agent collects file logs in paths that meet the specified path rules of all nodes in the cluster.
The collected logs are sent to the specified consumer in JSON format with specified metadata, including the source file path and custom metadata.


#### Configuration method
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Log Collection** in the left sidebar.
2. After selecting the region and cluster at the top of the log collection page, click **Create**, as shown below:
![](https://main.qcloudimg.com/raw/deee5dca8f7ed69419df61ecd149b9ca.png)
3. On the Create a log collection policy page, select **Node file path**, as shown below:
> You can specify a path or use wildcards, for example, `/var/log/nginx.log` or `/var/lib/docker/containers/*/*.log` to collect log files in the corresponding paths of all nodes in the cluster.

![](https://main.qcloudimg.com/raw/e0991c11fb20bfea9c99e8c404ef5d44.png)
You can add custom `metadata` as needed and attach `metadata` specified in key-value format to the collected logs as their metadata tags.
Attached metadata will be added to the logs in JSON format, as shown below:
![](https://main.qcloudimg.com/raw/01772444d71cde15876aaffec7101d2c.png)
For example, **Without** specified metadata attached, the collected logs appear as below:
![](https://mc.qcloudimg.com/static/img/5386281fc3ed14c4f41ba723a23dc3ec/host-log-without-metadata.png)
**With** specified metadata attached, the collected logs appear as below:
![](https://mc.qcloudimg.com/static/img/c571be8fbc995ab083c2676e3b10861f/host-log-with-metadata.png)
Compared with logs without specified metadata attached, JSON logs with metadata attached have an additional key `service`.
Log metadata is defined as follows:
<table>
	<tr>
		<th>Field</th> <th>Description</th>
	</tr>
	<tr>
		<td>path</td> <td>Source file of logs</td>
	</tr>
	<tr>
		<td>message</td> <td>Log information</td>
	</tr>
	<tr>
		<td>Custom key</td> <td>Custom value</td>
	</tr>
</table>
4. Configure the consumer of logs. We recommend that Tencent Cloud CLS be set as the consumer of logs, as shown below:
![](https://main.qcloudimg.com/raw/2a6f0cbb9efcc749f78bc531076b865d.png)
5. Click **Done** to complete the creation.



<span id="consumer"></span>
### Configuring consumer of logs 
The log collection feature allows you to set off-premises Kafka pods, topics specified by Tencent Cloud Ckafka pods, or log topics specified by Tencent Cloud Log Service (CLS) as the consumer of logs. The log collection agent will send the collected logs to the topic specified by Kafka or the log topic specified by CLS.

#### Configuring Kafka as the consumer of logs
Only Kafka pods without access authentication are supported. All nodes in the cluster must be able to access the specified Kafka topic.
If you use the Ckafka service provided by Tencent Cloud, select a Ckafka pod. Otherwise, enter the Kafka access address and topic, as shown below:
![](https://main.qcloudimg.com/raw/941c5737edc5ca069d83a6764fdaaf58.png)

#### Configuring CLS as the consumer of logs
> Currently, CLS only supports log collection and reporting for intra-region container clusters.
>
1. Because TKE's logs can be independently collected, you don't have to enable **LogListener** to create a logset, as shown below:
For more information on how to create a log set, see [Creating a logset and a log topic](https://intl.cloud.tencent.com/document/product/614/31592).
![](https://main.qcloudimg.com/raw/654d3d2408519b7fbb515f1aaf1da65c.png)
2. Enable the log topic's **Log Index**, as shown below:
![](https://main.qcloudimg.com/raw/c37bd895071f8d9b27c78318ebdc8a26.png)

#### Configuring Elasticsearch as the consumer of logs
Only Elasticsearch services without access authentication are supported. All nodes in the cluster must be able to access the specified Elasticsearch service.
Enter the Elasticsearch service's access address and storage index, as shown below:
![](https://main.qcloudimg.com/raw/92d93f1b25c2b9afd64e5523cca5afed.png)

