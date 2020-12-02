This document describes how to create a callback configuration template in the LVB Console and configure the callback under a push domain name.


## Notes
- After the template is successfully created, you need to associate the [callback configuration](https://intl.cloud.tencent.com/document/product/267/31065) with the corresponding push domain name. The association will take effect in about 5–10 minutes.
- You can also create callback templates for live channels through the API.
- For more information on LVB callback protocol, please see [Event Message Notification Protocol](https://intl.cloud.tencent.com/document/product/267/31566).
>- For LVB callback parameters and samples, please see [Event Message Notification Parameter Description](https://intl.cloud.tencent.com/document/product/267/31566).

## Creating Callback Template
1. Log in to the [LVB Console](https://console.cloud.tencent.com/live).
2. Select **Feature Template** > **[Callback Configuration](https://console.cloud.tencent.com/live/config/callback)** on the left sidebar.
3. Click **+** to create a callback template. Enter the callback information in the callback settings pop-up window and click **Save**.
>The **callback key** is a user-defined string of up to 32 uppercase and lowercase letters and digits. For instructions, please see [Event Message Notification](https://intl.cloud.tencent.com/document/product/267/31566).

![](https://main.qcloudimg.com/raw/870c6dd664a4eb618bdc1a7fcdf922dc.png)
## Associating Domain Name with Template
After creating the callback template, you need to associate it in the following steps:
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, select the push domain name to be configured, and click **Manage** on the right.
2. Enter the domain name details page and select **Template Configuration**.
3. Click **Edit** on the right on the **Callback Configuration** tab, select the created callback template, and click **Save**.
![](![img](https://main.qcloudimg.com/raw/e18e4c7f58950bd2dbe74f038c455cd9.png)


## Disassociating Template
To unbind the callback configuration from the domain name, click **Edit** in **Template Configuration** > **Callback Configuration**, deselect the corresponding template, and click **Save**.
> The callback templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled there for the time being. If you associated a specified stream through the APIs related to callback and want to disassociate them, you need to call the [callback template deletion API](https://intl.cloud.tencent.com/document/product/267/30813) to do so.
>
