VOD offers hotlink protection solutions that allow you to use a key or referer field to control playback permissions.
>? Once configured, it will take around 5 minutes for the hotlink protection to take effect on all CDN nodes.

## Referer Hotlink Protection
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Find the target application and click its name.
4. Select **Distribution and Playback > Domain Name** on the left sidebar.
5. Click **Set** in the row of the target domain name to enter the configuration page.
6. Under the **Access Control** tab, toggle on **Referer Hotlink Protection**, and complete the following settings:
 - Whether to allow empty referer
 - Referer Type: If you select **Blocklist**, the domains entered will be blocked; if you select **Allowlist**, only requests from the domains entered will be accepted.
6. Click **Confirm**.

>? For more information, see [Referer Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33985).


## Key Hotlink Protection
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Find the target application and click its name.
4. Select **Distribution and Playback > Domain Name** on the left sidebar.
5. Click **Set** in the row of the target domain name to enter the configuration page.
6. Under the **Access Control** tab, toggle on **Key Hotlink Protection**, and complete the following settings:
	1. Click **Generate** to generate a hotlink protection key.
	2. Copy the key.
7. Click **Confirm**.

>? 
>- For more information, see [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986).
>- Currently, the preview feature of key hotlink protection does not support audio files.
