

## Use Cases
If Tencent Cloud accounts in your organization are de-registered due to employee resignation or transfer, you can use TKE to **quickly clear** the accounts or have them **automatically cleared**. This document describes how to use the TKE console to clear the RBAC resource objects of Tencent Cloud accounts that have been de-registered.



## Principle

RBAC controls user access to clusters. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/457/37366).

## Directions


### Viewing de-registered Tencent Cloud accounts
You can view de-registered Tencent Cloud accounts in your cluster in the following steps:
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster) and select **Cluster** on the left sidebar.
2. On the cluster management page, select the target region.
3. In the cluster list, click a cluster ID to enter the cluster details page.
4. Select **Authorization Management** > **ClusterRoleBinding** or **RoleBinding**. Under the **Account Username** in the list, a de-registered Tencent Cloud account will be red. Hover over it, and you'll be prompted to clear relevant resource objects.





### Clearing invalid accounts
You can quickly clear the RBAC resource objects of the de-registered Tencent Cloud accounts **manually** or **automatically** in the following steps:


1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2/cluster) and select **Cluster** on the left sidebar.
2. On the cluster management page, select the target region.
3. In the cluster list, click a cluster ID to enter the cluster details page.
4. Select **Authorization Management** > **ClusterRoleBinding** or **RoleBinding**. On the **ClusterRoleBinding** or **RoleBinding** page, click **Clear invalid account** in the top-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/e76cfa89e3692bbd9da428a1db20478c.png)
5. In the **Clear De-registered Tencent Cloud Account** pop-up window, click **Clear now** to clear those that haven't been cleared.
    You can also enable **automatic clearing** to have de-registered accounts cleared in an automatic and scheduled manner.
	![](https://qcloudimg.tencent-cloud.cn/raw/5bfec424ce0f445de5422ab566d1907b.png)
