This document describes how to create a mount point. CVM, CPM 2.0, or TKE accesses data in CHDFS through a mount point, which is the destination address of CHDFS for access in a VPC and corresponds to a domain name.

## Directions
1. Log in to the [CHDFS console](https://console.cloud.tencent.com/chdfs), click **File Systems** on the left sidebar, and select the target region, such as Guangzhou.
2. Find the target CHDFS instance and click **Configure** to view its basic configuration and mount information.
3. Select **Mount Points** > **Add Mount Point** and enter the name and specify the VPC and permission group on the mount point addition page.
 - Name: mount point name, which can contain 4–64 letters, digits, hyphens, and underscores.
 - VPC Name/ID: select a VPC.
 - Permission Group: select a permission group. If there are no permission groups, please [create one](https://intl.cloud.tencent.com/document/product/1106/41962) first.
![](https://main.qcloudimg.com/raw/71dd4afeeaf75de0ca946951bd6fd1f7.png)
3. Click **Save**.

