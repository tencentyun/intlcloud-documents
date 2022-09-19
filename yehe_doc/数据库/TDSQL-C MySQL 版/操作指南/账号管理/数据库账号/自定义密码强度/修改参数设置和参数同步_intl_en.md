After the custom password strength feature is enabled, you can modify the feature parameters in the current cluster and sync them to other clusters under your account. This document describes how to modify such parameters and configure parameter sync.

## Prerequisites
You have enabled the custom password strength feature as instructed in [Enabling/Disabling Custom Password Strength Feature](https://intl.cloud.tencent.com/document/product/1098/49979).

## Modifying custom password strength parameters
>?To modify the custom password strength parameters, click **Strength Settings**, and the console will display parameters based on the password strength level configured when you enabled the feature (**MEDIUM** or **STRONG**; the **Non-Compliant Dictionary** parameter will be displayed only under the **STRONG** level). You can modify the parameters as needed.
>
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
3. On the cluster management page, select **Account Management** and click **Strength Settings** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/815ac6f6bafd833375f337b14b8ed403.png)
4. In the pop-up window, click **Next** to enter the **Parameter Settings** page.
5. Set parameters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/2d4df5dbd9c20c86f06642f7f9e04dd7.png)

## Setting parameter sync
After enabling the custom password strength feature in a cluster, you can use the parameter sync feature to sync the configured custom password strength parameters, including **Non-Compliant Dictionary**, to other clusters in the same region under the current Tencent Cloud account. If this feature is disabled in a target cluster, it will be enabled to sync the parameters.
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb).
2. Select the region at the top, find the target cluster in the cluster list, and click the cluster ID to enter the cluster management page.
3. On the cluster management page, select **Account Management** and click **Strength Settings** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/d941037339a3488dca51c590df6797f5.png)
4. On the parameter modification page, click **Parameter Sync**.
![](https://qcloudimg.tencent-cloud.cn/raw/5b8666e55587ac801b14d4494947b0bb.png)
5. On the **Parameter Sync** page, select or deselect one or multiple clusters and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/b7984d85a41435c53c786d295b93adf1.png) 
