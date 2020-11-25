## Overview
### Add-on description

The log collection feature is a tool provided by TKE for users to collect logs in clusters. It is used to send the logs of services in the cluster or those of files on a specific path in the cluster node to a specified Kafka topic or specified log topic of CLS.

The log collection feature must be manually enabled for each cluster. After this feature is enabled, the log collection Agent runs as a Daemonset in the cluster. Users can configure the sources and consumers of logs based on log collection rules. The log collection Agent collects logs from the configured source and sends these logs to the consumer specified by users. To use the log collection feature, you must ensure that nodes in the Kubernetes cluster can access the log consumer.

## Kubernetes Objects Deployed in a Cluster



| Kubernetes Object Name | Type | Default Resource Consumption | Namespaces |
| -------------- | --------- | ------------------- | ------------ |
| log-collector  | DaemonSet | 0.3-core CPU and 250-MB memory for each node | kube-system |

## Use Cases

The log collection feature is applicable to users who need to store and analyze service logs in the Kubernetes cluster. Users can collect logs in the cluster by configuring log collection rules and can send collected logs to a specified topic of Kafka or to a specified log topic of CLS for consumption by other infrastructures of users.


## Usage

### Installing the add-on

1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-On Management** to go to the "Add-On List" page.
4. On the "Add-On List" page, click **Create**. On the "Create an Add-On" page that appears, select **LogCollector**.
5. Click **Finish** to create the add-on.

### Configuring log collection rules
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and select **Log Rules** in the left sidebar.
2. At the top of the "Log Rules" management page, select the region and cluster where you have installed LogCollector and click **Create** to create log collection rules, as shown in the figure below:
![](https://main.qcloudimg.com/raw/43c0c4f0ce35f1c90eb48e729900d0db.png)
3. On the "Create Log Collection Rules" page, create rules by referring to [Log Collection](https://intl.cloud.tencent.com/document/product/457/32419). You can use these rules after the creation.


