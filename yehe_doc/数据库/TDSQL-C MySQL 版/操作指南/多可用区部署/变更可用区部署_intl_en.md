
This document describes how to switch the instance deployment mode between single-AZ and multi-AZ in the TDSQL-C for MySQL console.

## Upgrading from Single-AZ to Multi-AZ
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click a cluster name in the cluster list or **Manage** in the **Operation** column to enter the cluster details page.
2. In the **Availability Info** module on the cluster details page, click **Modify** after **Deployment Mode**.
![](https://qcloudimg.tencent-cloud.cn/raw/ef010ca16f873e782db9f7a32b5db8c5.png)
3. In the pop-up window, select **Yes** for **Multi-AZ Deployment**, select the secondary AZ, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/9fd1ec4d7972bff8347d0cf6f76b7238.png)
4. When the cluster status becomes **Running**, you can view the information of the primary and secondary AZs on the cluster details page.

## Downgrading from Multi-AZ to Single-AZ
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click a cluster name in the cluster list or **Manage** in the **Operation** column to enter the cluster details page.
2. In the **Availability Info** module on the cluster details page, click **Modify** after **Deployment Mode**.
![](https://qcloudimg.tencent-cloud.cn/raw/8bd296341015848f33beea31fbb1b68d.jpg)
3. In the pop-up window, select **No** for **Multi-AZ Deployment** and click **OK**.
>?Only the secondary AZ can switch between single-AZ and multi-AZ deployment mode, but the primary AZ cannot.
>

## FAQs
#### Where can I query the AZ information of a cluster?
- In the **AZ** column in the cluster list.
- In **Basic Info** > **Region/AZ** on the cluster details page.
- In **Availability Info** on the cluster details page.

#### Will my cluster run normally during the AZ modification?
- During the start and modification operations of the AZ modification task, normal access to read-only and read-write instances will be unaffected.
- The database connection addresses (cluster’s read-write address and read-only address) will remain unchanged after the AZ is modified, so you can continue to access your cluster at these addresses.

