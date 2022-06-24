You can add IPs to the precise allowlist to allow access requests of specific public network users to the specified sites.


## Adding to Precise Allowlist
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-iplist) and select **Configuration Center** > **IP Blocklist/Allowlist** on the left sidebar to enter the IP blocklist/allowlist page.
2. On the blocklist/allowlist page, select the target domain name in the top-left corner and click **Precise allowlist**.
3. On the precise allowlist page, click **Add address**, and the IP adding window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/00d1015755a50b58a32f8fbc3c095c78.png)
4. In the pop-up window, configure relevant parameters and click **OK**.

>? WAF precise allowlist enables you to use masks to allow access requests from source IPs within a range. We can enter a specific IP range (e.g. `10.10.10.0/24`) in **Content**.

5. Now the rule will take effect immediately, and allow all HTTP access requests from specific source IPs.

## Editing Precise Allowlist
1. On the [blocklist/allowlist page](https://console.cloud.tencent.com/guanjia/tea-iplist), select the target domain name in the top-left corner and click **Precise allowlist**.
2. On the precise allowlist page, select the target rule, click **Edit**, and the editing window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/9dfc181406a81fabbbf2ee032d018bf3.png)
3. In the pop-up window, modify relevant parameters and click **OK**.


## Removing from Precise Allowlist
1. On the [blocklist/allowlist page](https://console.cloud.tencent.com/guanjia/tea-iplist), select the target domain name in the top-left corner and click **Precise allowlist**.
2. On the precise allowlist page, select the target rule, click **Delete**, and the deletion confirmation window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/af059269de3e25e87d24a156be71ef27.png)
3. In the pop-up window, click **OK**.
>?Once deleted, it cannot be restored and takes effect only after being added again.
