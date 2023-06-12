


## Overview

This document describes how to use cross-account domain transfer to transfer a domain under your account A to account B.
>!
>- After a domain is successfully transferred, the target account will have its management permissions, such as information modification, domain transfer, and DNS management. To add DNS records for this domain under account B, see [Domain Reclaim](link).
>- Cross-account domain transfer is to change the Tencent Cloud account of a domain while keeping its identity verification information and owner unchanged. You should note that this feature cannot be used for trade.
>- Cross-account transfer only supports Tencent Cloud root accounts but not collaborators and sub-users.
>
## Directions

1. Log in to the [Domains console](https://console.intl.cloud.tencent.com/domain/manage), enter the **My Domains** page, and view the information of all purchased domains.
2. In the row of the domain to be transferred, click **Manage** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/b34df866d595d8b6cdea2966dd7c12d4.png)
3. Enter the **Domain Name Info** page, select the **Domain Transfer** tab, and click **Transfer** after **Cross-Account Transfer** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7818c6d4c83a31d0c4cd0553a15a334e.png)
4. In the **Identity Verification** window that pops up, get and enter the SMS verification code, and then click **Confirm** as shown below:

5. On the **Cross-Account Transfer** page, confirm the relevant information, enter the target account ID, and click **Confirm** > **Next** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/05231418aa924327a9b2a72f8d54f01a.png)
 - **Transferred Domain**: check whether the domain to be transferred is correct.
 - **Specify Account**:
    - Target Account: enter the account ID of the transfer recipient. You can get the account ID in the basic account information.
    - DNS Transfer: if you want to transfer the DNS records of the domain under the current account, select **Transfer DNS Records**.
<dx-alert infotype="notice" title="">
<ul><li>After this option is selected, the corresponding DNS record management permissions will also be transferred to the target account. If there are any DNS plans, they will also be transferred.<b>This operation cannot be undone</b>.</li>
<li>If there are no DNS records under the current account, no transfer will be performed.</li></ul>
</dx-alert>
6. In the **Confirm Transfer Information** window that pops up, check the ID and alias of the target account and click **Confirm** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/20a6f5da1ee31774dadbcbf7db699ad5.png)
7. Log in to the new account to view the domain.




