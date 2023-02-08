This document shows you how to bind a time shifting template to a push domain to enable time shifting for the domain, as well as how to unbind a template to disable the feature. Time shifting is disabled by default.

[](id:limit)
## Use Limits
- A template takes effect about 5-10 minutes after it is bound to a domain. 
- After a template is successfully bound to a push domain, time shifting will be enabled for push addresses under that domain.
- One domain can be bound to only one time shifting template. After binding, time shifting will be enabled for all streams under the domain.

## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live) and added a [push domain](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a time shifting template.

[](id:conect)

## Binding a Time Shifting Template
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), and click the target **push domain** or click **Manage** to enter the domain details page.
2. Select the **Template Configuration** tab and click **Edit** in the **Time shifting configuration** area.
![](https://qcloudimg.tencent-cloud.cn/raw/3acef7dcbe2071d27240fc6a92cc973c.png)
3. Select a time shifting template and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/025f28e64fdd0a2641bdf3d7feabdfb8.png)

[](id:unite)
## Unbinding a Time Shifting Template
1. Go to [Domain Management](https://console.cloud.tencent.com/live/domainmanage), and click the target **push domain** or click **Manage** to enter the domain details page.
2. Select the **Template Configuration** tab and click **Edit** in the **Time shifting configuration** area.
3. Unselect the template and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/b9c561b2e231811483e4737413ab6b2d.png)

>? Unbinding a time shifting template will not affect ongoing live streams.