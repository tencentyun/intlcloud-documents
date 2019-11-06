This document describes how to delete an ENI.
1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **IP and ENI** -> **ENI** in the left sidebar to enter the ENI list page.
 ![1](https://main.qcloudimg.com/raw/6045caabd952283e71fd8d30ebbed3e1.png)
3. Locate the row of the ENI and click **Delete** in the operation column.
 ![2](https://main.qcloudimg.com/raw/15bb91ace6033e6e43f426625773f68c.png)
4. Click **OK** in the pop-up window.

>
>- When an ENI is deleted, its associated private IPs, EIPs, and security groups are automatically unbound.
>- You can only delete ENIs that are not associated with CVMs.
>- The primary ENI is deleted when the CVM is deleted.
