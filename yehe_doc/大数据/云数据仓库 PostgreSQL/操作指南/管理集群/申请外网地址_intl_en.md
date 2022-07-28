## Overview
If you want to access a CDWPG cluster through a CVM instance in another subnet or a server on the public network other than the CVM instance in the specified subnet, you need to apply for a public IP for the cluster.
>!The CDWPG cluster can be accessed at its public IP. However, after applying for one, you need to add it to the allowlist for actual access as instructed in [IP Allowlist](https://intl.cloud.tencent.com/document/product/1138/45133).

## Directions
1. Click **Manage** in the cluster list to enter the cluster details page.
2. Select the **Basic Configuration** page and click **Apply for Public IP**. A public IP will be generated for access to the CDWPG cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/670cc741f1dcbf6d84cb5613761b7230.png)

>?When the public IP is no longer needed, click **Release Public IP** to delete it.
