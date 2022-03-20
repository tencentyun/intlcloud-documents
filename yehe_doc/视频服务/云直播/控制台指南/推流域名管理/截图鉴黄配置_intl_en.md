The screencapture and porn detection feature is disabled by default for live push. This document describes how to bind/unbind a push domain name to/from a screencapture and porn detection template to enable/disable the screencapture and porn detection feature.

## Notes
- The template configuration will take effect in about **5–10 minutes**.
- After configuring the screencapture and porn detection template, you need to configure a callback template before you can receive screencapture or porn detection results. For more information on how to configure a callback template, please see [Callback Configuration](https://intl.cloud.tencent.com/document/product/267/31065).
- One domain name can be bound to only one screencapture and porn detection template. After binding, all streams under it will be screencaptured and porn detected according to this template.

## Prerequisites
 - You have logged in to the [CSS console](https://console.cloud.tencent.com/live) and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970). 
 - You have created a [screencapture and porn detection template](https://intl.cloud.tencent.com/document/product/267/31072).


## Binding Screencapture and Porn Detection Template

1. 	Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the push domain name to be configured or **Manage** to enter the domain name details page.
2. Select **Template Configuration** and click **Edit** in the **Screencapture & Porn Detection Configuration** section.
![](https://main.qcloudimg.com/raw/13d8bdd830ed06a6c3e16960628c04a5.png)
3. Select a screencapture and porn detection template and click **Confirm**.
![](https://main.qcloudimg.com/raw/1b237b96fb034d4795f5512769f0a34b.png)


## Unbinding Screencapture and Porn Detection Template
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the push domain name to be configured or **Manage** to enter the domain name details page.
2. Select **Template Configuration** and click **Edit** in the **Screencapture & Porn Detection Configuration** section.
3. Clear the target template and click **Confirm**.
![](https://main.qcloudimg.com/raw/1258bc65cb1ea0627d6c2f23e9fdc023.png)
