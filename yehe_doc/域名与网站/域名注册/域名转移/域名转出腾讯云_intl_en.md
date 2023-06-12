

## Overview

Domain transfer out is to transfer your domain from DNSPod to another domain registrar that will continue to provide domain services. The transfer process takes about **5–7** business days. After transfer out, your domain will no longer be entitled to the Tencent Cloud domain service; therefore, proceed with caution.
>!
>- As stipulated by the domain registry, a new domain cannot be transferred out in the first 60 days after registration. If you select **Enable the 60-day registrar transfer lock period** when modifying the domain information, you also need to wait for 60 days before you can transfer out the domain.
>- Domains in the **serverTransferProhibited** status cannot be transferred out.
>- Verify the domain information carefully. The auth-code will be sent to the email address specified in the domain information.
>- In 15 days before a domain expires (for Chinese mainland domains) or after it expires, it cannot be transferred out. You need to renew it before transferring it. For detailed directions, see [Domain Renewal](https://intl.cloud.tencent.com/zh/document/product/242/42871).
>- If an expired domain was renewed or redeemed less than 45 days ago, transferring it out is not recommended, as doing so may invalidate the renewal, shorten the renewal period, or fail.
>- To ensure the domain security, quick transfer out is not supported.
>- For more applicable rules, see [Domain Transfer Out Rules](https://intl.cloud.tencent.com/document/product/242/42858).


## Directions

### Getting domain auth-code

1. Log in to the [Domains console](https://console.intl.cloud.tencent.com/domain/manage). 
2. In the row of the domain to be transferred out, click **Manage** as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/94367b164256c72c8942b93b15c282f4.png)
3. Enter the **Domain Name Info** page, select the **Domain Transfer Out** tab, and click **Transfer Out** after **Cross-Account Transfer** as shown below:
>?Before transferring out a domain, check whether **Transfer Prohibition Lock** is enabled, and if so, the domain cannot be transferred out. You need to disable this option before you can transfer the domain out. For detailed directions, see [Enabling Domain Security Protection](https://intl.cloud.tencent.com/zh/document/product/242/42864).
>
![](https://qcloudimg.tencent-cloud.cn/raw/59f537cc0f19e5be52bd5ce7115c4d2a.png)
4. On the **Domain Transfer Out** page, check the email address, read and agree to the **Notes for Domain Transfer Out**, and click **Get Auth-Code** as shown below:
>? Before getting the auth-code, check whether your email address can receive emails normally.
>
 ![](https://qcloudimg.tencent-cloud.cn/raw/a0bda8e4e304147d60a3a2f1c66e5d30.png)
5. If the page that you are redirected to displays "Sent the auth-code successfully", the auth-code has been sent to your email address as shown below:
>? 
>- If you haven't received the email, click **Resend**.
>- If the email address is incorrect, click **Cancel Transfer Out** and get a new auth-code after [modifying the owner information](https://console.intl.cloud.tencent.com/domain/manage).
>


### Entering auth-code

Enter the obtained auth-code in the domain transfer information at the new registrar and complete the transfer process as prompted.
>?
> - Domain transfer out generally takes **5–7** business days, subject to the handling time of the registry and target registrar. Please wait patiently.
> - An auth-code is valid for 5 days. If you don't transfer your domain to another registrar within this period, you need to get a new auth-code.

