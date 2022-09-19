
This document describes how to enable/disable public read-write and read-only addresses of a cluster in the console.
>! 
>- After enabling public network access, you can connect to TDSQL-C for MySQL by using system-assigned domain name and port. It takes about five minutes for the configuration to take effect.
>- TDSQL-C for MySQL public network access should be used only for development or auxiliary management. For business production, be sure to use the private network access.
>- After TDSQL-C for MySQL public network access is enabled, it will be controlled by the network access policies in the security group. You need to configure the corresponding policies in advance.
>- Currently, the public network access feature is free of charge, but the stability of the public network bandwidth and traffic cannot be guaranteed.

## Limit on regions
Currently, public network access can be enabled only for read-write and read-only instances in Beijing, Shanghai, Guangzhou, Chengdu, and Nanjing regions.

## Enabling a cluster's public read-write/read-only addresses
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster details page.
2. On the cluster details page, click **Enable** after the target public network address.
![](https://qcloudimg.tencent-cloud.cn/raw/ce17ab554b308169e9aa87f06e090fdf.png)
3. In the pop-up window, confirm that everything is correct and click **OK**.

## Disabling a cluster's public read-write/read-only addresses
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb) and click a cluster ID in the cluster list to enter the cluster details page.
2. On the cluster details page, click **Disable** after the target public network address.
![](https://qcloudimg.tencent-cloud.cn/raw/8dc3207064f0157dd0f54e4d0335bac3.png)
3. In the pop-up window, confirm that everything is correct and click **OK**.



