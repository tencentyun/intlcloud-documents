CSS ensures a better viewing experience for end users. This document shows you how to configure CSS.

1. After you complete the following configuration in [StreamPackage](https://www.tencentcloud.com/products/mdp), Tencent Cloud will automatically add origin server settings for the corresponding playback domain in CSS. In the StreamPackage console, click the StreamPackage channel you created, select the **CDN** tab, and click **Edit Configuration**.
![](https://qcloudimg.tencent-cloud.cn/raw/91fdb17fa19c8c2cc98a230017b9e2f8.png)

2. In the pop-up window, enter the playback domain you want to use and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/3d9b5fc8f4fbffb56fb9a14d17726be5.png)

3. After the CSS origin server configuration is completed, the current page will display information including the **Playback Domain Name**, **CNAME**, **Acceleration Region**, and **Status**. The default acceleration region is outside the Chinese mainland.
![](https://qcloudimg.tencent-cloud.cn/raw/0d0f202a0394c67926da815e460b7ca4.png)

4. If you also want to configure access control, referer allowlist/blocklist, and HTTPS for the playback domain, click **Go to the CSS CDN Console to Perform More Actions**.

5. If you don’t need to perform further configuration, note the **CNAME** assigned by the system and add it in your DNS platform.
![](https://qcloudimg.tencent-cloud.cn/raw/2696cd0cda9bb9412c4d799457b9698e.png)

6. To get the final URL for playback, splice the CSS playback domain and the StreamPackage endpoint path.
