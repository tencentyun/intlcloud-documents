The watermark feature is disabled by default for live push. This document describes how to bind/unbind a push domain name to/from a watermark template to enable/disable the watermark feature.
 
## Notes
- The template configuration will take effect in about 5–10 minutes.
- After the template is bound successfully, the watermark feature will be enabled for push addresses under the specified push domain name.
- One domain name can be bound to only one watermark template. After they are bound, all streams under the domain name will be watermarked according to this template.

## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live) and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a [watermark template](https://intl.cloud.tencent.com/document/product/267/31073).


## Binding Watermark Template
1. 	Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **push domain name** to be configured or **Manage** to enter the domain name details page.
2. 	Select **Template Configuration** and click **Edit** in the **Watermark Configuration** section.
![](https://main.qcloudimg.com/raw/c46b5fc50d2bfaaa995f55750a05cca1.png)
4. 	Select a watermark template and click **Confirm**.
![](https://main.qcloudimg.com/raw/94a9695a9b3f824356de93bbdd004822.png)
>? You can click **Preview** in the **Operation** column to view the watermark.

## Unbinding Watermark Template
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **push domain name** to be configured or **Manage** to enter the domain name details page.
2. Select **Template Configuration** and click **Edit** in the **Watermark Configuration** section.
3. Clear the target template and click **Confirm**.
![](https://main.qcloudimg.com/raw/94a9695a9b3f824356de93bbdd004822.png)
