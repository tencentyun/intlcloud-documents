## Operation Scenario

You can create, delete, and modify Helm applications in the console. You can also perform such operations though the Helm command line after installing the Helm client locally and connecting to a cluster.

## Prerequisites

- There is a TKE cluster with at least 0.28-core CPU and 180 MiB memory.
- The Helm application management feature has been enabled in the cluster.
- Only clusters with Kubernetes version 1.8 and above are supported.

> - If the Helm application management feature is not enabled, please apply for activation in [Helm application](https://console.cloud.tencent.com/tke2/helm).
> - After the Helm application management feature is enabled, the Helm tiller-related components will be installed in the cluster.

 ![](https://main.qcloudimg.com/raw/e17225f3bb2e15c41ebb8e9c7d7d06c8.png)

## Directions

### Creating a Helm Application

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Helm applications](https://console.cloud.tencent.com/tke2/helm)** to go to the Helm application management page.
3. Click **Create** to go to the "New Helm Application" page.
4. Enter the application name, Chart_URL. Select the type of Helm Chart source: Public or Private. This is shown in the following figure:
   ![](https://main.qcloudimg.com/raw/87257d2d7c8c64f93ea4e4f3240547ba.png)
    Helm Chart source **other** has the following two possible selections:

- Official Helm repository
- Customer Helm Repo repository.

> If you select the **other** type for the Helm Chart source, the Chart_url attribute must be set to a parameter value beginning with “http” and ending with “tgz”.

5. Click **Finish**.

### Updating a Helm Application

1. Go to the [Helm Application Console](https://console.cloud.tencent.com/tke2/helm).
2. In the **Helm applications** list, select the Helm application to be updated and click **Update application**.
3. In the **Update Helm application** pop-up box, manually enter the Chart_url version number. This is shown in the following figure:
   ![](https://main.qcloudimg.com/raw/57a64278507ced270c489f863c9dbf2c.png)
4. Click **Finish**.

### Rolling Back a Helm Application

1. Go to the [Helm Application Console](https://console.cloud.tencent.com/tke2/helm).
2. In the **Helm Applications** list, click the name of the Helm application to be updated to go to the application details page.
3. Select the **Version History** tab and click **Rollback** in the row of the version to rollback to.

### Deleting a Helm Application

1. Go to the [Helm Application Console](https://console.cloud.tencent.com/tke2/helm).
2. In the **Helm Applications** list, select the Helm application to be deleted and click **Delete**.
3. In the prompt box that pops up, click **OK**. This is shown in the following figure:
   ![](https://main.qcloudimg.com/raw/90f2f47a828d75d7494f2ac749495746.png)

