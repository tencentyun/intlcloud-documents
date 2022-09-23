## Overview

<dx-alert infotype="alarm" title="">
This add-on will not be updated. If you want to use the log collection feature, please refer to [Log Management](https://intl.cloud.tencent.com/document/product/457/32419). The new log collection feature supports multiple log parsing methods such as single-line, multi-line, separator, full regex, and JSON. The standard output and the file logs in the container will be sent to the Tencent CLS, which provides the search and analysis, visual application, log download and consumption, and other services.

</dx-alert>



### Add-on description

The log collection feature is a tool provided by TKE for users to collect logs in clusters. It is used to send the logs of services in the cluster or those of files under a specific path in the cluster node to a specified Kafka topic or specified log topic of CLS.

The log collection feature needs to be manually enabled for each cluster. After this feature is enabled, the log collection Agent runs as a Daemonset in the cluster. Users can configure the sources and consumers of logs based on the log collection rules. The log collection Agent collects logs from the configured source and sends these logs to the consumer specified by users. To use the log collection feature, you must ensure that nodes in the Kubernetes cluster can access the log consumer.

### Kubernetes objects deployed in a cluster



| Kubernetes Object | Type | Required Resources | Namespaces |
| -------------- | --------- | ------------------- | ------------ |
| log-collector | DaemonSet | 0.3 core CPU and 250 MB memory for each node | kube-system |

## Use Cases

Log collection feature is applicable to users who need to store and analyze service logs in the Kubernetes cluster. Users can collect logs in the cluster by configuring log collection rules and can send collected logs to a specified topic of Kafka or to a specified log topic of CLS for consumption by other infrastructures of users.


## Usage

### Installing the add-on

1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the “**Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. On the "Add-On List" page, click **Create**. On the "Create Add-On" page that appears, select **LogCollector**.
5. Click **Confirm**.

### Configuring log collection rules
1. Log in to [TKE console](https://console.cloud.tencent.com/tke2/log?rid=1) and click **Log Collection(Legacy)** in the left sidebar.
2. At the top of the **Log Collection** page, select the region and cluster where you have installed LogCollector and click **Create** to create log collection rules, as shown in the figure below:
![](https://main.qcloudimg.com/raw/43c0c4f0ce35f1c90eb48e729900d0db.png)
3. In the **Create Log Collecting Policy** page, select the **Log Source** and **Consumer End**, configure other related parameters, and click **Done** to complete the creation.





### Searching for the log in the CLS console

Log in to the CLS console and select **[Log Search](https://console.cloud.tencent.com/cls/search)** in the left sidebar. Select the log topic configured in the log rule in the **Logset** and **Log Topic** drop-down list, as well as the time period for which to search logs, and click **Search and Analysis** to view the event data, as shown in the following figure:

![](https://main.qcloudimg.com/raw/348f807a187842b773a200c986185012.png)

>!You need to enable the full-text index for the log topic to search for the logs.
