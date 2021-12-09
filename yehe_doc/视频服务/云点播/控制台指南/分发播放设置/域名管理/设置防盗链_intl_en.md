To support video playback permission control, Tencent Cloud VOD has launched a hotlink protection solution that can prevent hotlinking by checking the referer or generating a key.
>? Once configured, it will take around 5 minutes for the hotlink protection to take effect on all CDN nodes.

## Referer Hotlink Protection
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and click **Distribution and Playback** > **Domain Name** on the left sidebar.
2. Click **Settings** in the row of the target domain name to enter the configuration page.
3. Click **Access Control**, and then toggle **Referer Hotlink Protection** on or off.	If you enable it, configure as follows:
 - Allow Empty Referer: select **Yes** or **No**.
 - Select Object: select **Blocklist** or **Allowlist** and enter the desired domain name in the text box below.
4. Click **OK** to save the configuration.

>?For more information, please see [Referer Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33985).

## Key Hotlink Protection
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and click **Distribution and Playback** > **Domain Name** on the left sidebar.
2. Click **Settings** in the row of the target domain name to enter the configuration page.
3. Click **Access Control**, and then toggle **Key Hotlink Protection** on or off.	If you enable it, configure as follows:
 Click **Generate Random Key** and the system will automatically generate a hotlink protection key.
4. Click **OK** to save the configuration.

>? For more information, please see [Key Hotlink Protection](https://intl.cloud.tencent.com/document/product/266/33986).






