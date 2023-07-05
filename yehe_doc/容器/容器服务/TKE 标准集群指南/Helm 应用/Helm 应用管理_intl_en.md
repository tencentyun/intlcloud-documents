## Scenario

You can create, delete, and modify Helm applications in the console. You can also perform such operations on the Helm CLI after installing the Helm client locally and connecting it to a cluster.

## Prerequisite

- A TKE cluster is available, and at least 0.28 cores and 180 MiB memory have been reserved for the installation of Helm tiller components.
- Has Helm application management function enabled.
- Only clusters with Kubernetes v1.8 or later are supported.

## Notes

- If the Helm application management feature is not enabled, apply to enable it in [Helm Applications](https://console.cloud.tencent.com/tke2/helm).
- After the Helm application management feature is enabled, Helm tiller-related components will be installed in the cluster.

## Directions

### Creating a Helm application

1. Log in to the [Tencent Cloud TKE console](https://console.cloud.tencent.com/tke2) and click **Clusters** in the left sidebar.
2. At the top of the "Helm Application" page, choose **Location** > **Run Cluster**, and click **Create**.
3. On the "Create a Helm Application" page, configure the following parameters as needed.
   - **Application Name**: enter a custom name.
   - **Origin**: it can be a third-party repository, an official Helm repository, or a self-built Helm repository.
    - **Download Address**: enter the download address for Chart as needed. Note that the value must start with `http` and end with `.tgz`, for example, `http://139.199.162.50/test/nginx-0.1.0.tgz`.
    - **Type**: both the public and private types are available. Select one of them as needed.
   - **Key-Value**: you can replace the default configuration of the Chart package by setting custom parameters such as `image.repository = nginx`.
4. Click **Finish** to finish the creation.

### Updating a Helm application

1. Log in to the [Helm application console](https://console.cloud.tencent.com/tke2/helm) and go to the "Helm list" page.
2. In the "Helm Applications" list, click **Update Application** for the Helm application to be updated.
3. In the "Update a Helm Application" window, enter "Chart_url" again and configure the custom parameters as needed.
4. Click **Confirm** to finish the update.

### Rolling back a Helm application

1. Log in to the [Helm application console](https://console.cloud.tencent.com/tke2/helm) and go to the "Helm List" page.
2. In the "Helm Applications" list, click the name of the Helm application to be updated to go to the application details page.
3. Click the **Version History** tab and click **Rollback** for the version to be rolled back.

>Only updated Helm applications can be rolled back.


### Deleting a Helm application

1. Log in to the [Helm application console](https://console.cloud.tencent.com/tke2/helm) and go to the "Helm List" page.
2. In the "Helm Applications" list, click **Delete** for the Helm application to be deleted.
3. In the window that appears, click **OK**.
