
## Overview
This document describes how to upgrade a TencentDB for MySQL instance from [two-node](https://intl.cloud.tencent.com/document/product/236/38329) to [three-node](https://intl.cloud.tencent.com/document/product/236/39783) in the console.
>?
>- Only TencentDB for MySQL two-node instances can be upgraded to three-node.
>- The upgrade will not interrupt the instance service.
>- You can also purchase three-node instances on the [purchase page](https://buy.cloud.tencent.com/cdb).

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. In the **Configuration Info** section, click **Upgrade to Three-Node** next to **Architecture**.
![](https://qcloudimg.tencent-cloud.cn/raw/8a5a1df13737501d7c9633ad4a3d7676.png)
3. In the pop-up dialog box, specify the data replication mode and availability zones and click **Submit**.
 - **Data Replication Mode**: For more information, see [Database Instance Replication](https://intl.cloud.tencent.com/document/product/236/7913).
 - **Multi-AZ Deployment**: Multi-AZ deployment protects database service from being interrupted in case of database failures or availability zone failures.
    - For a three-node instance, its replicas can be deployed in the source AZ or different AZ. We recommend that you deploy one replica in the source AZ and another replica in a different AZ.
    - Currently, only some source AZs support selecting different AZs as replica AZs. You can view these source AZs and the supported replica AZs on the [purchase page](https://buy.cloud.tencent.com/cdb).
![](https://qcloudimg.tencent-cloud.cn/raw/6fd7ffdd2ade0b1bec3fca2130b1f438.png)
4. After the payment is completed, you will be redirected to the instance list. After the status of the instance changes from **Changing configuration** to **Running**, it can be used normally.

## FAQs
#### How do I view the architecture information of an instance?
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, view the architecture information in the **Configuration** column; or click an instance ID or **Manage** in the **Operation** column to enter the instance details page, where you can view the architecture information in the **Configuration Info** > **Architecture** section.
![](https://main.qcloudimg.com/raw/e783ce5c7070b8084cf03b053d7e5077.png)

#### How do I view the source and replica AZs of an instance?
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page, where you can view the source and replica AZs in the **Availability Info** section.
![](https://main.qcloudimg.com/raw/f022ef04a1db5bf566cc626990e534f5.png)

