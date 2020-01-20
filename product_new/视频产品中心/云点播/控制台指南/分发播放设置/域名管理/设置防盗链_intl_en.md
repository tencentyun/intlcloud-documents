To support the permission control of video playback, VOD has launched a hotlink protection solution that can prevent hotlinking based on referer and key.

## Referer Hotlink Protection
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod) and click **Distribution and Playback** > **Domain Names** on the left sidebar.
2. Click **Settings** in the row of the target domain name to enter the configuration page.
3. Click **Edit** on the right of **Referer Hotlink Protection**, toggle it on, and configure the following options:
 - Allow Empty Referer: select **Yes** or **No**.
 - Select Object: select **Blacklist** or **Whitelist** and enter the desired domain name in the text box below.
4. Click **OK** to save the configuration.



## Key Hotlink Protection
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod) and click **Distribution and Playback** > **Domain Names** on the left sidebar.
2. Click **Settings** in the row of the target domain name to enter the configuration page.
3. Click **Edit** on the right of **Key Hotlink Protection**, toggle it on, and configure the following options:
	1. Click **Generate Random Key** and the system will automatically generate a hotlink protection key.
	2. Click **Copy** and the system will copy the key to the clipboard.
4. Click **OK** to save the configuration.

>
>- Once configured, it will take around five minutes for the hotlink protection to take effect on all CDN nodes.
>- For more information on referer hotlink protection, please see [Referer Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33985).
>- For more information on key hotlink protection, please see [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986).



