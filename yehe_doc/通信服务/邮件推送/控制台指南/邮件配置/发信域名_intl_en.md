## Scenario
You can configure sender domains in the SES console. This document describe how to create a sender domain.

## Prerequisites
- You must have the admin permissions on the sender domain.
- If your domain is hosted with Tencent Cloud, log in to the [DNSPod console](https://console.cloud.tencent.com/cns) for configuration. If your domain is hosted with another domain service provider, configure it according to the checklist.

## Directions
1. Log in to the [SES console](https://console.cloud.tencent.com/ses/domain), click **Email Configuration** > **Sender Domain** to go to the **Sender Domain** page, and click **Create**.
![](https://main.qcloudimg.com/raw/7e4ba21b39ef0d2eb1de2e7ad8d8147a.png)

| Field | Description |
|---------|---------|
| Sender Domain | Configured sender domain |
| Status |<li>**Pending verification**: the domain must pass the verification before it can be used to send emails. </li><br><li>**Verified**: the domain is verified and can be used to send emails.</li> |
| Operation | If the status is **Pending verification**, you can click **Verify**to verify the domain or click **Delete** to remove it. |

2. In the **Create Sender Domain** dialog box, enter a domain and click **Submit** to complete the configuration.
![](https://main.qcloudimg.com/raw/c2c75b71aaaf762f545ad530c6554aeb.png)
>? To avoid conflicts between SPF and MX records, do not use corporate email domains.
