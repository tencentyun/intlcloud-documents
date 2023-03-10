## Overview

Domain push is a point-to-point transaction mode. A domain transaction loop is closed after the buyer accepts the domain transferred by the seller.
After the domain seller and buyer make a deal, the seller can transfer the domain to the buyer via domain push.


>! 
> - Tencent Cloud is just an online platform for domain transaction services and cannot issue invoices for payments involved in transactions.
> - Currently, Tencent Cloud supports only free push but not push with domain prices.


## Comparison with Cross-Account Transfer

Domain push and cross-account transfer are compared as follows:
<table>
<tr>
<td rowspan="1" colSpan="1" >Item</td>
<td rowspan="1" colSpan="1" >Domain Push</td>
<td rowspan="1" colSpan="1" >Cross-Account Transfer</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Purpose</td>
<td rowspan="1" colSpan="1" >To meet user demands for domain transactions.</td>
<td rowspan="1" colSpan="1" >A free service to meet user demands for transferring domain management permissions between Tencent Cloud accounts.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Procedure</td>
<td rowspan="1" colSpan="1" >The recipient can accept or reject the domain. If the recipient rejects the domain, domain push fails, and the domain still belongs to the initiator.</td>
<td rowspan="1" colSpan="1" >Only the initiator can confirm the transfer, which is completed once initiated.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Basic domain information</td>
<td rowspan="1" colSpan="1" >The recipient must modify the identity information of the domain after domain push.</td>
<td rowspan="1" colSpan="1" >The original identity information of the domain can be retained.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Domain settings</td>
<td rowspan="1" colSpan="1" >During acceptance, the recipient can change the domain settings such as the automatic renewal feature and the setting of whether to enable 60-day inter-registrar transfer lock.</td>
<td rowspan="1" colSpan="1" >After acceptance, the recipient can view the domain status and select domain settings in the domain list.</td>
</tr>
</table>


## Prerequisites
- The update prohibition lock is not enabled for the domain.

- You are the domain owner, and the domain is under the initiator's account.

- The domain is valid.

- Identity verification has been completed for the domain.

- The domain is not being processed by judiciaries, arbitration institutions, or domain dispute resolution agencies.

- The domain is not being registered, reviewed for naming, reviewed for identity by the registry, transferred in, transferred out, transferred between accounts, renewed, or pushed, or its registrar qualification is not being upgraded.

- More than seven days have passed since the domains in the Chinese mainland (.cn) are registered or transferred in.

- More than one day has passed since the domains outside the Chinese mainland are registered or transferred in.


## Directions

### Initiating a push
1. Log in to the Domains console and select **[Domain Push](https://console.cloud.tencent.com/domain/push)** on the left sidebar.

2. On the **Domain Push** page, click **Initiate Push**.

3. On the **Initiate Push** page, enter the target domain (you can push up to 4,000 domains at a time), enter and confirm the Tencent Cloud account ID of the recipient, specify whether to reset DNS query, enter or skip the remarks, and click **Next**.

4. After confirming that everything is correct, click **Submit**.

   >!
   > 
   > - A domain push cannot be canceled once initiated successfully by the initiator. Proceed with caution.
   > - You can go to the [account information](https://console.cloud.tencent.com/developer) page to get the account ID of the recipient.

5. After the domain is successfully accepted by the recipient, the domain status on the **Initiated Requests** tab will become **Accepted**, that is, the domain has been pushed successfully.


### Accepting a push
1. Log in to the Domains console and select **[Domain Push](https://console.cloud.tencent.com/domain/push)** on the left sidebar.

2. A number in a red dot on the **Received Requests** tab of the **Domain Push** page indicates the domain(s) to be accepted. Click the tab to view the received domain(s).

3. Select the verified registrant profile, set the domain status, and click **Pay and Accept**.
   

   >!
   > 
   > - The accepted domain will enter the "Identity being reviewed by the registry" status, which usually takes 1–3 days.
   > - The operation cannot be undone after successful acceptance.
