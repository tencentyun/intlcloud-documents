## Operation Scenario

You can create, delete, and manage Helm applications in the console. You can also perform such operations through the Helm command line after installing the Helm client locally and connecting to a cluster.

## Prerequisites

- There is a TKE cluster with resources of at least 0.28-core CPU and 180 MiB memory.
- The Helm application management feature has been enabled in the cluster.
 
> - If the Helm application management feature is not enabled, please apply for activation in [Helm application](https://console.cloud.tencent.com/tke2/helm).
> - After the Helm application management feature is enabled, the Helm tiller-related components will be installed in the cluster.

 ![](https://main.qcloudimg.com/raw/5a0a28f215950ad6e666de6a855ed741.png)

## Directions

### Creating a Helm Application

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, select **Application Center** and click **[Helm applications](https://console.cloud.tencent.com/tke2/helm)** to go to the Helm application management page.
3. Click **Create** to go to the "Create a Helm application" page.
4. Enter the application name and select the "Region", "Running cluster", the Helm Chart to be installed and the corresponding version. See the figure below:
 ![](https://main.qcloudimg.com/raw/b662048d70667b37e75e2952acdbad0a.png)
 Helm Chart sources are mainly divided into the following two types:
 - TencentHub: You can select public or private type. For details, see the [Operation Guide for TencentHub Helm Chart](https://cloud.tencent.com/document/product/857/31683).
 - Other: Select an official repository of Helm or a self-built Helm repository.
 If you select "Other" for the source type, the Chart_url attribute must be set to a parameter value beginning with "http" and ending with "tgz".
5. Click **Finish**.

### Updating a Helm Application

1. Go to the [Helm application console](https://console.cloud.tencent.com/tke2/helm).
2. In the **Helm applications** list, select the Helm application to be updated and click **Update application**.
3. In the **Update a Helm application** page that pops up, select the version you want to update to and enter the custom parameters based on your business needs. See the figure below:
![](https://main.qcloudimg.com/raw/19c866d8b2a09f9e2db2618f06bcc007.png)
 If the application to be updated is an application created by another repository, you need to manually enter the version number.
4. Click **Finish**.

### Rolling back a Helm Application

1. Go to the [Helm application console](https://console.cloud.tencent.com/tke2/helm).
2. In the **Helm applications** list, click the name of the Help application to be updated to go to the application details page.
3. Select the **Version history** tab and click **Roll back** in the row of the version to roll back to.

### Deleting a Helm Application

1. Go to the [Helm application console](https://console.cloud.tencent.com/tke2/helm).
2. In the **Helm applications** list, select the Helm application to be deleted and click **Delete**.
3. In the prompt box that pops up, click **OK**. See the figure below:
![](https://main.qcloudimg.com/raw/10e67636bd07a48a4e9c426157330994.png)

