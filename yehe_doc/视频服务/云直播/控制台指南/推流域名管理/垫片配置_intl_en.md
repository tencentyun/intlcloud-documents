This document shows you how to bind a standby stream template to a push domain to enable the standby stream feature for that domain, as well as how to unbind a template to disable the feature. The standby stream feature is disabled by default.

## Notes
- A template takes effect about 5-10 minutes after it is bound to a domain.
- After a template is successfully bound to a push domain, the standby stream configured will take effect for all push addresses under that domain.

## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live) and added a [push domain](https://intl.cloud.tencent.com/document/product/267/35970).
- You have [created a standby stream template](https://intl.cloud.tencent.com/document/product/267/31073).


## Binding a Standby Stream Template
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), and click the target **push domain** or click **Manage** to enter the domain details page.
2. Select the **Template Configuration** tab and click **Edit** in the **Standby stream configuration** area.
![](https://qcloudimg.tencent-cloud.cn/raw/a78db30c69aa234230026808020ca45e.png)
3. Select a standby stream template and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/420d4315d6eed1d163d71fca02700202.png)
>? You can click **Preview** in the **Operation** column to preview the standby stream.

## Unbinding a Standby Stream Template
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), and click the target **push domain** or click **Manage** to enter the domain details page.
2. Select the **Template Configuration** tab and click **Edit** in the **Standby stream configuration** area.
3. Unselect the template and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/c0fc088cfbb2b18270078c3a3fa7a56e.png)
