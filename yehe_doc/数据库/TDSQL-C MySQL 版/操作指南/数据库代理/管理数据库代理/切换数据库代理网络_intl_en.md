This document describes how to modify the database proxy network in the TDSQL-C for MySQL console.

## Prerequisite
You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://www.tencentcloud.com/document/product/1098/49999).

## Notes
- Changing the network may cause the change of the instance's database proxy IP. The old IP will be retained for 24 hours by default and up to 168 hours. Then, it will become invalid. Therefore, modify the IP on the client promptly.
- If **Valid Hours of Old IP** is set to 0 hours, the IP is released immediately after the network is changed.
- You can select only a VPC in the region where the cluster of TDSQL-C for MySQL resides, but you can choose a subnet in any AZ and view its IP range.

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql), select the region at the top of the page, and click the ID of the target cluster to enter the cluster management page.
2. On the cluster management page, select the **Database Proxy** tab.
3. On the **Database Proxy** tab, click ![](https://qcloudimg.tencent-cloud.cn/raw/0286958e4f0522141375f4080708ceec.png) under **Overview** > **Connection Address** > **Network**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/62rZ867_6.png)
4. In the pop-up dialog box, set the relevant configuration items and click **OK**.
   - **Select Network**: Select a VPC and subnet in the region and AZ where the cluster resides.
   - **Valid Hours of Old IP**: Its range is 0–168 hours and default value is 24 hours.
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/APC9799_7.png)
5. After successfully changing the network, you can view the new network under **Connection Address**.
