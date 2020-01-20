## Overview
### Add-on description

Log collection feature is a tool provided by TKE for users to collect logs in clusters. It is used to send the logs of services in the cluster or those of files under a specific path in the cluster node to a specified Topic of Kafka or specified log topic of CLS.

Log collection feature is enabled manually for each cluster. After this feature is enabled, log collection Agent runs in a form of Daemonset in the cluster. Users can configure the source and consumer of logs using log collection rules. Log collection Agent collects logs from the configured source, and sends these logs to the consumer specified by users. Please note that to use the log collection feature you must ensure that nodes in the Kubernetes cluster can access the log consumer.

### Kubernetes objects deployed in a cluster

Deploying LogCollector Add-on in a cluster will deploy the following Kubernetes objects in the cluster:

| Kubernetes Object Name                                | Type                             | Default Resource Occupation | Namespaces |
| -------------- | --------- | ------------------- | ------------ |
| log-collector  | DaemonSet | Per node: 0.3 core CPU, 250MB memory | kube-system  |

## Use Cases

Log collection feature is applicable to users who need to store and analyze service logs in the Kubernetes cluster. Users can collect logs in the cluster by configuring log collection rules and can send collected logs to a specified Topic of Kafka or to a specified log topic of CLS for consumption by other infrastructures of users.

## Limits
- After LogCollector is installed, a log collection service will be created on all nodes of a cluster (including nodes that are added subsequently).
- Installing LogCollector occupies resources of 0.3 core CPU and 250M memory per node.

## Usage

### Installing the add-on
1. Log in to the [TKE Console](https://console.cloud.tencent.com/tke2), and select **Add-ons** in the left sidebar.
2. On the top of the **Add-ons** management page, select the region and the cluster for installing LogCollector, and click **Create**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/4b7f364107adde29df480403dfe3e43b.png)
3. In the **Create Add-on** page, select **LogCollector**, and click **Complete** to install it.

### Configuring log collection rules
1. Log in to [TKE Console](https://console.cloud.tencent.com/tke2) and click **Log Collection** on the left sidebar.
2. In the **Log Collection** management page, select the region and cluster where you want to install LogCollector, and click **Create** to create the log collection rules. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/47157223647e2d4f0eea5680b7dea989.png)
3. In the **Create Log Collection Rules** page, create rules by referring to [Log Collection](https://intl.cloud.tencent.com/document/product/457/32419). The rules can be used after creation.
