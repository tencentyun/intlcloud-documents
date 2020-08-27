The callback feature is disabled by default for LVB push. This document describes how to associate/unassociate a push domain name with/from a callback template to enable/disable the callback feature.

## Notes
- The template configuration will take effect in about 5–10 minutes.
- When an LVB event is triggered after the callback feature has been enabled, you can receive the event information via the [event message notification](https://intl.cloud.tencent.com/document/product/267/31566).

## Prerequisites
- You have logged in to the [LVB Console](https://console.cloud.tencent.com/live), and have added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a [callback template](https://intl.cloud.tencent.com/document/product/267/31074).

## Associating a Callback Template
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the push domain name you want to configure or click **Manage** to enter the domain details page.
2. Select **Template Configuration** and click **Edit** in the **Callback Configuration** tab.
![](https://main.qcloudimg.com/raw/d3e31f428ab1463335e234007c663311.png)
3. Select a callback template and click **Save**.
![](https://main.qcloudimg.com/raw/27f9da682e20283e25cc2478e1a53a0b.png)

## Unassociating a Callback Template

1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the push domain name you want to unassociate or click **Manage** to enter the domain details page.
2. Select **Template Configuration** and click **Edit** in the **Callback Configuration** tab.
3. Deselect the template and click **Save**.
![](https://main.qcloudimg.com/raw/0f8ec4ae49d2f1c5329bdb509f056366.png)

