## Overview
To facilitate the configuration and management of Kubernetes component parameters in TKE clusters, Tencent Cloud supports custom Kubernetes component parameters. This document describes how to configure custom Kubernetes component parameters in clusters.


## Notes
- To use custom Kubernetes component launch parameters, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for it.
- While submitting the ticket, you need to provide custom Kubernetes component launch parameters, including your account ID, cluster ID, and the component and component parameters.
- For Kubernetes cluster version upgrade, due to the potential incompatibility of launch parameters after a Kubernetes version upgrade, major version upgrades will not retain the custom Kubernetes component parameters from your original cluster version. Therefore, you need to reconfigure custom Kubernetes component parameters.


## Directions
### Configuring custom Kubernetes component parameters when creating a cluster
1. <span id="step1">Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2), and click **Clusters** in the left sidebar.</span>
2. On the "Cluster Management" page, click **Create** above the cluster list.
3. On the "Create a cluster” page, choose **Advanced Settings** > **Configure Custom Kubernetes Component Parameters**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/faa5c17e26c1a09fd0b5f30d72c4bc3e.png)

### Configuring the custom Kubelet parameters of a node
On the **Create a cluster node**, **Add existing nodes**, **Create a node pool**, and **Add nodes** pages, you can configure the custom Kubelet parameters of a node, as shown in the figure below:
![](https://main.qcloudimg.com/raw/43036b5fe2678f01313cee8c12520120.png)


### Configuring custom Kubernetes component parameters when upgrading a cluster
1. Log in to the TKE console and click **[Cluster](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar.
2. On the **Cluster Management** page, select the ID of the desired cluster, and enter the cluster details page.
3. On the cluster’s **Basic Information** page, click **Upgrade** to the right of the Kubernetes version. At the same time, set the Kubernetes component launch parameters.
