## Prerequisites
To connect to bot traffic management, you need to purchase a WAF [value-added service](https://intl.cloud.tencent.com/document/product/627/47799).

## Directions
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-botconfig) and select **Configuration center** > **Bot and application security** on the left sidebar.
2. On the **Bot and application security** page, select the target domain name in the top-left corner and click ![](https://qcloudimg.tencent-cloud.cn/raw/0b613028c41243c1b53951862a3284e9.png) in **Bot management rules**.
![](https://qcloudimg.tencent-cloud.cn/raw/bb5032ca5dcbbfaa400a5a44bc8d9d3f.png)
**Field description**
 - **Enable bot rule management**: It is disabled by default and can be enabled as needed.
>?The bot traffic analysis feature takes effect only when the WAF switch of the domain name is enabled.

 - **Effective scenario**: Displays the number of bot analysis scenario modules enabled currently. They include the browser bot defense module, threat intelligence module, AI evaluation module, and bot flow statistics module.
 - **Total scenarios**: Displays the number of bot analysis scenario modules existing under the current domain name.
 - **Current global scenario**: Displays the name of the effective global scenario under the current domain name.
 - **Total custom rules**: Displays the number of custom bot rules enabled currently.