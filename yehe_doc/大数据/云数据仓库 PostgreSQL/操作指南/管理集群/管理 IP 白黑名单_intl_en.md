## Overview
If you want to access CDWPG clusters through CVM instances in other subnets or servers on the public network other than the CVM instances in the specified subnets, you need to add their IPs to the allowlist.

An IP range can be specified when an IP is added to the allowlist. Add one or more IPs in the IP range to the blocklist if you want to block the access to CDWPG clusters from them.
>!The blocklist takes precedence over the allowlist.

## Prerequisites
Before using the IP allowlist, make sure that you have applied for a public IP for a CDWPG cluster; otherwise, you will not be able to access the cluster from servers other than CVM instances in the specified subnets even if their addresses are added to the allowlist.

## Directions
### Managing IP allowlist
1. Click **Manage** in the cluster list to enter the cluster details page.
2. Select **Configure** > **Access Allowlist**.
3. Click **Create Allowlist** and enter the IP, username, database name, and CIDR block as required.
![](https://qcloudimg.tencent-cloud.cn/raw/b0d626516763efb645225a2f6c0a1054.png)
4. Click **OK** to allow the IP range specified by the CIDR block. Then, you can access the CDWPG cluster from a server at the IP or IP range.
>?When an IP address in the allowlist is no longer needed, select it in the allowlist and click **Delete** to remove it from the allowlist.

### Managing IP blocklist
1. Select **Configure** > **Access Blocklist**.
2. Click **Create Blocklist** and enter the IP, username, database name, and CIDR block as required.
3. Click **OK** to block the IP range specified by the CIDR block. Then, you cannot access the CDWPG cluster from a server at the IP or IP range.
>?To unblock an IP or IP range, select it in the blocklist and click **Delete** to remove it from the blocklist.
