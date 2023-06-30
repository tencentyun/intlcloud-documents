## Overview

You can create, delete, modify, view, configure and manage distribution policies (Subscription) in the Tencent Kubernetes Engine Distributed Cloud Center console. You can bind distribution policies to target clusters (subscribers) and resources (feeds), and you can view the topology map and distribute instances among clusters.

## Directions

### Creating a distribution policy
 1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Distribution Policy** in the left sidebar.
 2. Click **Create distribution policy**. The pop-up page is as follows:
 ![](https://qcloudimg.tencent-cloud.cn/raw/3d9fc88c75ef7b32f84b366b64dfdfa4.png)
 - **Clusters to be associated**: You can add the target clusters that will receive the distributed resources, or configure LabelSelector to select suitable clusters.
 - **Resources to be associated**: You can add the K8s resources associated with the distribution policy. The associated K8s resources will be distributed to the specified clusters according to the distribution policy. For more information on how to create K8s application resources, see [Application Management](https://intl.cloud.tencent.com/document/product/1144/45546).
 3. Click **Create distribution policy** at the bottom of the page to complete the creation.


### Viewing a distribution policy

1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Distribution Policy** in the left sidebar.
2. On the list page, you can view and configure the associated clusters and K8s resources.
	 - **Name**: The name of the distribution policy.
	 - **Number of associated clusters**: The number of clusters that are associated with the distribution policy.
	 - **Number of associated resources**: The number of resources that are associated with the distribution policy.
	 - **Creation time**: The time when the distribution policy is created.
	 - **Operation**: The operations supported by the distribution policy, including “Associate with cluster”, “Associate with resource” and “Delete”.
3. Click the name of a distribution policy to enter the **Details** page.
 ![](https://qcloudimg.tencent-cloud.cn/raw/1e205348e5e206e4a4139cf9b90a2f85.png)
 - **Topology map**: Display on graphs the application resources and target clusters associated with the distribution policy, the localization policies, as well as other status information.
 - **Basic information**: The details of the distribution policy.
4. Click **Instance list** tab to view the instances that are running in the target cluster.
 ![](https://qcloudimg.tencent-cloud.cn/raw/2b86d638249c6809adaa22b3ea2dbc59.png)
	 - **Instance name**: The name of the K8s resource in the target cluster. You can click the name to enter the details page of the application.
	 - **Cluster**: The name of the target cluster where the instance is located. You can click the cluster name to enter the cluster management page.
	 - **Namespace**: The namespace where the instance is located.
	 - **Status**: The instance status.
	 - **Update localization policy**: You can create, update and delete the localization policy. For the description of the **localization policy** configuration, see [Localization Policy](https://intl.cloud.tencent.com/document/product/1144/45548).

### Modifying the distribution policy

1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Distribution Policy** in the left sidebar.
2. Click **Associate with cluster**. In the pop-up dialog box, configure the target cluster associated with the policy. Click **OK**. You can select multiple clusters or leave it empty.
![](https://qcloudimg.tencent-cloud.cn/raw/91c6c69d66a3967c6e1391a1f279de9b.png)
3. Click **Associate with resource**. In the pop-up dialog box, configure the K8s resources associated with the policy. Click **OK**. You can select multiple resources or leave it empty.
![](https://qcloudimg.tencent-cloud.cn/raw/a5c5aa0332eaaec2230953ed3a30e6cb.png)

### Configuring a localization policy

1. If you want to configure a localization policy for a K8s resource in a cluster, click **Instance list**, locate the desired instance and click **Create localization policy** to configure the policy. For more information on localization policy, see [Localization Policy](https://intl.cloud.tencent.com/document/product/1144/45548).
 ![](https://qcloudimg.tencent-cloud.cn/raw/fd9c19c18e565e1a31142e2fa0156cf0.png)
2. If you want to modify or cancel the localization configuration, click **Instance list**, and click **Update localization policy** or **Delete localization policy** for the specific instance.

### Deleting a distribution policy

1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Distribution Policy** in the left sidebar.
2. Select the desired policy and click **Delete** to delete it.
>!All K8s resources distributed to the target clusters are deleted if you delete the associated distribution policy.
