The callback feature is disabled by default for CSS push. After a push domain name is bound to a callback configuration, the callback feature will be enabled for all push addresses under this domain name. If a callback event is triggered by the configured template during live streaming, Tencent Cloud will send a request to your server which is responsible for the response. After authentication, a JSON packet containing the porn detection callback information can be obtained.
This document describes how to bind/unbind a push domain name to/from a callback template to enable/disable the callback feature.



 
## Notes
- The template configuration will take effect in about 5–10 minutes.
- When an CSS event is triggered after the callback feature is enabled, you can receive the event information through the [event message notification](https://intl.cloud.tencent.com/document/product/267/38080).
- The callback templates are managed at the domain name level in the console, and rules created by APIs cannot be canceled for the time being. If you bound a template to a specified stream through the callback APIs and want to unbind it, you need to call the [DeleteLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30813) API.
- One domain name can be bound to only one callback template. After binding, all streams under it will be called back according to this template.

## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live) and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have created a [callback template](https://intl.cloud.tencent.com/document/product/267/31074).
<span id="related"></span>
## Binding Callback Template
1. 	Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **push domain name** to be configured or **Manage** to enter the domain name details page.
2. 	Select **Template Configuration** and click **Edit** in the **Callback Configuration** tab.
![](https://main.qcloudimg.com/raw/d3e31f428ab1463335e234007c663311.png)
3. 	Select a callback template and click **Save**.
![](https://main.qcloudimg.com/raw/27f9da682e20283e25cc2478e1a53a0b.png)
<span id="untie"></span>
## Unbinding Callback Template

1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **push domain name** to be configured or **Manage** to enter the domain name details page.
2. Select **Template Configuration** and click **Edit** in the **Callback Configuration** tab.
3. Deselect the template and click **OK**.
![](https://main.qcloudimg.com/raw/0f8ec4ae49d2f1c5329bdb509f056366.png)
