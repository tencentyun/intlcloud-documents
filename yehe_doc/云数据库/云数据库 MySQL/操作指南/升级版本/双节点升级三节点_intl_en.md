
## Overview
This document describes how to upgrade a TencentDB for MySQL instance from [two-node](https://intl.cloud.tencent.com/document/product/236/38329) to [three-node](https://intl.cloud.tencent.com/document/product/236/39783) in the console.
>?
>- Only TencentDB for MySQL two-node instances can be upgraded to three-node.
>- The upgrade will not interrupt the instance service.
>- You can also purchase three-node instances on the [purchase page](https://buy.cloud.tencent.com/cdb).

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. In the **Configuration Info** section, click **Upgrade to Three-node** next to **Architecture**.
![](https://main.qcloudimg.com/raw/cbc0ef63b4b4824a8eedf92898a039f6.png)
3. In the pop-up dialog box, specify the data replication mode and availability zones and click **OK**.
 - **Data Replication Mode**: for more information, please see [Database Instance Replication](https://intl.cloud.tencent.com/document/product/236/7913).
 - **Multi-AZ Deployment**: multi-AZ deployment protects database service from being interrupted in case of database failures or availability zone failures.
    - For a three-node instance, its replicas can be deployed in the source availability zone or different availability zones. We recommend you deploy one replica in the source availability zone and another replica in a different availability zone.
    - Currently, only some source availability zones support selecting different availability zones as replica availability zones. You can view these source availability zones and the supported replica availability zones on the [purchase page](https://buy.cloud.tencent.com/cdb).
![](https://main.qcloudimg.com/raw/6b1a4c2b43587cc99c7b01d544f53cd2.png)
4. After the payment is completed, you will be redirected to the instance list. After the status of the instance changes from **Changing configuration** to **Running**, it can be used normally.

## FAQs
#### How do I view the architecture information of an instance?
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, view the architecture information in the **Configuration** column; or click an instance ID or **Manage** in the **Operation** column to enter the instance details page, where you can view the architecture information in the **Configuration Info** > **Architecture** section.
![](https://main.qcloudimg.com/raw/e783ce5c7070b8084cf03b053d7e5077.png)

#### How do I view the source and replica availability zones of an instance?
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance details page, where you can view the source and replica availability zones in the **Availability Info** section.
![](https://main.qcloudimg.com/raw/f022ef04a1db5bf566cc626990e534f5.png)

