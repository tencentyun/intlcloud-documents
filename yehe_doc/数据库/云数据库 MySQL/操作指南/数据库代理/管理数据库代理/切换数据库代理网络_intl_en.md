This document describes how to modify the database proxy network in the TencentDB for MySQL console.

## Prerequisites
You have [enabled the database proxy](https://intl.cloud.tencent.com/document/product/236/42052).

## Notes
- Changing the network may cause the change of the instance's database proxy IP. The old IP will be retained for 24 hours by default and up to 168 hours. Then, it will become invalid. Therefore, modify the IP on the client promptly.
- If "Valid Hours of Old IP" is set to 0 hours, the IP is released immediately after the network is changed.
- You can only select a VPC in the region of the instance, but you can choose a subnet in any AZ and view its IP range.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the region at the top of the page, and click the ID of the target instance to enter the instance management page.
2. On the instance management page, select the **Database Proxy** tab.
3. On the **Database Proxy** tab, click ![](https://qcloudimg.tencent-cloud.cn/raw/0286958e4f0522141375f4080708ceec.png) under **Overview** > **Connection Address** > **Network**.
![](https://qcloudimg.tencent-cloud.cn/raw/ee84c770775763a4c4d20beee04a36ae.png)
4. In the pop-up window, set the relevant configuration items and click **OK**.
   - Set **Valid Hours of Old IP** to 0–168 hours.
   - Select **Auto-Assign IP** or **Specify IP**.
![](https://qcloudimg.tencent-cloud.cn/raw/f48ad92683bd8eae4baa76580af03d7b.png)
5. After successfully changing the network, you can view the new network under **Connection Address**.

