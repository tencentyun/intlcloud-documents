To strengthen video playback permission control, Tencent Cloud VOD has launched a hotlink protection solution that can prevent hotlinking by checking the Referer or generating a Key.

## Referer Hotlink Protection
1. Log in to [VOD console](https://console.cloud.tencent.com/video).
2. Select **Distribution and Playback Settings** > **Domain Name Management**.
3. In the row of the target domain name, click **Settings** to go to the configuration page.
4. Click **Edit** in the **Referer Hotlink Protection** module and toggle on **Enable Referer Hotlink Protection** and configure the following options:
 - Allow empty referer: Select whether to allow an empty referer to request the video (i.e., whether video playback is allowed when the video URL is directly entered in a browser).
 - Select the object to be added: Select a blacklist or whitelist and enter the domain name. For more information, see [Precautions](https://cloud.tencent.com/document/product/266/14046#referer).
![](https://main.qcloudimg.com/raw/040def2f466235c943d2d94b60e32cfe.png)
5. Click **OK** to save the referer hotlink protection configuration. This takes approximately five minutes to take effect on all CDN nodes.

## Key Hotlink Protection
1. Log in to [VOD console](https://console.cloud.tencent.com/video).
2. Select **Distribution and Playback Settings** > **Domain Name Management**.
3. In the row of the target domain name, click **Settings** to go to the configuration page.
4. Click **Edit** in the **Key Hotlink Protection** module as shown below:
 ![](https://main.qcloudimg.com/raw/a53061db324c8cbce895729210ad00cd.png)
5. Toggle on **Enable key hotlink protection** and click **Generate Key** as shown below:
 ![](https://main.qcloudimg.com/raw/1b66a9481353e5fd9bfbaf3d6ea3e48e.png)
6. Click **OK** to save the configuration. This takes approximately five minutes to take effect on all CDN nodes.

