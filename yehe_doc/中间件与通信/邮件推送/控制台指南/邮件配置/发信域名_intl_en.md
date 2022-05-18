## Overview
You can configure sender domains in the SES console. This document describes how to create a sender domain.

## Prerequisites
- You must have the admin permissions on the sender domain.
- If your domain is hosted with Tencent Cloud, log in to the [DNSPod console](https://console.cloud.tencent.com/cns) to configure the domain. Otherwise, configure it as instructed in the checklist.

## Directions
1. Log in to the [SES console](https://console.cloud.tencent.com/ses/domain), click **Configuration** > **Sender Domain** to go to the **Sender Domain** page, and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/50a47b56343acb2cb2289f705bd7514e.png)
2. In the **Create Sender Domain** dialog box, enter a domain and click **Submit** to complete the configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/7e53b2e8ecfaf818c8cb56bb38b9ed4e.png)
3. Go back to the **Sender Domain** page, and verify the domain before sending emails with it. For verification methods, see [Identity Verification and Configuration](https://intl.cloud.tencent.com/document/product/1084/42371).
![](https://qcloudimg.tencent-cloud.cn/raw/040ac5bd4115f1739c65e01629a5f51b.png)
<table>
   <tr>
      <th width="0px" >Attribute</td>
      <th width="0px" >Description</td>
   </tr>
   <tr>
      <td>Sender domain</td>
      <td>The sender domain address you have configured</td>
   </tr>
   <tr>
      <td>Status</td>
      <td>Pending verification: You must verify the domain before sending emails with it.<br>Verified: The domain has been verified and can be used to send emails.</td>
   </tr>
   <tr>
      <td>Operation</td>
      <td>If the status is pending verification, you can click <b>Verify</b> to perform verification, or click <b>Delete</b> to remove this sender domain configuration.</td>
   </tr>
</table>

<dx-alert infotype="explain" title="">
- To avoid SPF and MX records conflicts, do not use corporate email domains.
- If you want to change a sender domain, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
</dx-alert>

