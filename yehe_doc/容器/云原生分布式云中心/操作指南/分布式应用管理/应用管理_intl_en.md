## Overview

You can create and operate native Kubernetes resources in the Tencent Kubernetes Engine Distributed Cloud Center console, such as Deployment, Configmap and Service, as well as external CRDs.
For description of Kubernetes objects, see [Types of Objects](https://intl.cloud.tencent.com/document/product/457/30658). You can create, delete, modify and view these resources, and bind distribution policies to K8s resources and distribute the resources to multiple clusters based on the policies.


## Directions
### Creating K8s application resources
 1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
 2. Click **Create** to create a resource. For details about all kinds of resources, see [Types of Objects](https://intl.cloud.tencent.com/document/product/457/30658).
 3. Configure parameters for the new resource. At the bottom of the page, you need to configure the distribution policy. You can select **Create distribution policy**, **Existing distribution policy** or **Do not associate with distribution policy**.
	 - **Do not associate with distribution policy**: This resource is not distributed. You can specify a distribution policy for it later.
	 - **Create distribution policy**: You can add the clusters to which the resource is distributed, or configure the LabelSelector based on the prompts.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/a385f8bee0561a1b3bc8930ccf5199b0.png)
	 -**Existing distribution policy**: Select an existing distribution policy.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/8224523c5d0c24148e8ba5dfd8900e2d.png)
 4. Click **Create** to complete the creation.


### Viewing K8s application resources

1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. On the resource list page, you can see the K8s resources and the associated distribution policies. You can filter them by **distribution policy**.
 - **Name**: The name of the K8s resource.
 - **Namespace**: The namespace where the resource resides.
 - **Distribution policy**: The distribution policy that is associated with the resource. You can edit the policy.
 - **Operation**: The operations that you can perform on the resource, including editing YAML, deleting the resource and others.
3. Click the resource name to enter the details page.
 ![](https://qcloudimg.tencent-cloud.cn/raw/d4f333225806b7e189214365f27825d8.png)
 - **Distribution policy**: The distribution policy associated with the resource.
 - **Topology map**: Display on graphs the distribution policies associated with the resource, and the target clusters, localization configurations, as well as status information.
 - **Basic information**: The details of the K8s resource.
4. Click **Instance management** tab to view the instances that are running in the target cluster.
 ![](https://qcloudimg.tencent-cloud.cn/raw/59047057fd265652146b318bcbdd7ec9.png)
 - **Instance name**: The name of the K8s resource in the target cluster. You can click the name to enter the details page of the application.
 - **Cluster**: The name of the target cluster where the instance is located. You can click the cluster name to enter the cluster management page.
 - **Distribution policy**: The instance is distributed according to the distribution policy.
 - **Namespace**: The namespace where the instance is located.
 - **Status**: The instance status.
 - **Update localization policy**: You can create, update and delete the localization policy. For the description of the **localization policy** configuration, see [Localization Policy](https://intl.cloud.tencent.com/document/product/1144/45548).
5. Click **YAML** tab to view the YAML configuration of the resource.


### Modifying the associated distribution policy
1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click the modification icon in the **Distribution policy** column. Specify another **distribution policy** for the resource in the pop-up dialog box.
 ![](https://qcloudimg.tencent-cloud.cn/raw/dbc1eaca7fc3d384a412180d9313697e.png)
>! If you **cancel** a distribution policy, the instance of the application distributed according to the policy is deleted at the same time.


### Modifying a K8s application resource

1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Click **Edit YAML**, and edit the resource configuration in the pop-up dialog box.
3. Click **Complete**. The modified configuration will be automatically synced to **all** target clusters based on the distribution policies.


### Configuring localization policy

1. If you want to configure a localization policy for a K8s resource in a cluster, click **Instance management** tab, locate the desired instance and click **Create localization policy** to configure the policy. For more information on localization policy, see [Localization Policy](https://intl.cloud.tencent.com/document/product/1144/45548).
 ![](https://qcloudimg.tencent-cloud.cn/raw/890e44c8ca23769dcd91f10f37faa27e.png)
2. If you want to modify or cancel the localization configuration, click **Instance management**, and click **Update localization policy** or **Delete localization policy** for the specific instance.

### Deleting a K8s application resource

1. Log in to the [Tencent Kubernetes Engine Distributed Cloud Center console](https://console.cloud.tencent.com/tdcc). Click **Distributed Application Management** > **Application Management** in the left sidebar.
2. Select the desired resource. Click **Delete** if you confirm that no distribution policy is associated with the resource.
>! If any distribution policy is associated with the resource, you will be prompted to delete all distribution policies associated with it before you can delete the resource.
