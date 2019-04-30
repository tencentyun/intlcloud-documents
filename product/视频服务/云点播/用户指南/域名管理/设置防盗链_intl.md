To support the permission control of video playback, Tencent Cloud has launched a hotlink protection solution that can prevent hotlinking based on referer and key.
## Referer-based Hotlink Protection
1. Log in to the [VOD console](https://console.cloud.tencent.com/video).
2. Select **Distribution and Playback Settings** > **Domain name management**.
3. In the row of the target domain name, click **Settings** to go to the configuration page.
4. Click **Edit** in the **Referer-based hotlink protection** module and toggle on **Enable referer-based hotlink protection** and configure the following options:
 - Allow empty referer: Select whether to allow an empty referer to request the video (i.e., whether to allow playing the video by directly entering the video URL in a browser).
 - Select the object to be added: Select a blacklist or whitelist and enter the domain name. For more information about the configuration, see [Precautions](https://cloud.tencent.com/document/product/266/14046#referer).
![](https://main.qcloudimg.com/raw/040def2f466235c943d2d94b60e32cfe.png)
5. Click **OK** to save the referer-based hotlink protection configuration, which takes around five minutes to take effect on all CDN nodes.

## Key-based Hotlink Protection
1. Log in to the [VOD console](https://console.cloud.tencent.com/video).
2. Select **Distribution and Playback Settings** > **Domain name management**.
3. In the row of the target domain name, click **Settings** to go to the configuration page.
4. Click **Edit** in the **Key-based hotlink protection** module as shown below:
 ![](https://main.qcloudimg.com/raw/a53061db324c8cbce895729210ad00cd.png)
5. Toggle on **Enable key-based hotlink protection** and click **Generate a key** as shown below:
 ![](https://main.qcloudimg.com/raw/1b66a9481353e5fd9bfbaf3d6ea3e48e.png)
6. Click **OK** to save the configuration, which takes around five minutes to take effect on all CDN nodes.
