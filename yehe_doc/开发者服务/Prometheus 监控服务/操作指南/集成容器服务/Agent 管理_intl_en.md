Prometheus itself is the second project developed under [Cloud Native Computing Foundation (CNCF)](https://cncf.io/), so it has deep integration with Kubernetes, but there are still certain learning costs. To reduce your learning and use costs, TMP is deeply integrated with TKE, so you can quickly install the agent and enjoy native Prometheus services.

## Preparations

- Create a TKE cluster in the [TKE console](https://console.cloud.tencent.com/tke2/cluster). For detailed directions, please see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- Service role authorization: during the integration, you need to grant the permission to manipulate TKE. For detailed directions, please see Description of Role Permissions Related to Service Authorization.
- Enter the **Integrate with TKE** page.

## Directions

### Installing agent[](id:install_agent)

1. After successfully authorizing the service role, you can list the TKE clusters in the same VPC as the TMP instance in the current region.
 >?For network reasons, TKE clusters in other VPCs will not be displayed in the list.
2. Select the corresponding TKE cluster in the cluster list and click **Install** for automated integration. In the installation pop-up window, you can select the basic monitoring components that need to be integrated. The installation process is asynchronous and takes about 2–3 minutes. After the monitoring status shows **Installed**, the installation is successful.
![](https://qcloudimg.tencent-cloud.cn/raw/cdd10703106df78a59a4ee3adb5dfd6f.png)

### Uninstalling monitoring component

If you need to stop monitoring TKE clusters, follow the steps below to uninstall the Prometheus agent and its monitoring component.

Select the corresponding TKE cluster in the cluster list, click **Uninstall** for automated uninstallation, and confirm the uninstallation in the pop-up window. The uninstallation process is asynchronous and takes about 2–3 minutes.
