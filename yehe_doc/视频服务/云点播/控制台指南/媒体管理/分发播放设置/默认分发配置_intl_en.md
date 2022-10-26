## Overview
On the **Default Distribution Domain** page, you can perform the following actions:
1. View and modify the default distribution domain.
You can access your videos through your own domain after adding the domain in the console and configuring a CNAME for it. However, to update the hosts of the video URLs obtained through APIs or from the console, you need to modify the default distribution domain information in the VOD console.
2. View and modify the playback key.
A playback key is used to generate a [player signature](https://intl.cloud.tencent.com/document/product/266/38099). A playback device can access the content only within the validity period of the signature.

## Directions
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and select **Application Management** on the left sidebar.
2. Select the target application.
3. By default, you will be directed to **Media Assets > Video Management > Uploaded**.
4. Select **Distribution and Playback > Default Distribution Domain** on the left sidebar.
5. Click **Edit** on the right to modify the default distribution domain information.
 - Default distribution protocol: HTTP or HTTPS.
 - Default distribution domain: By default, the domain assigned by the system (`xxx.vod2.myqcloud.com`) is used. You can also use your own domain after [adding](https://intl.cloud.tencent.com/document/product/266/35572) it in the console and [configuring a CNAME](https://intl.cloud.tencent.com/document/product/266/35572) for it.
 - Playback key: A random playback key is assigned by the system when you sign up. You can modify this key. Please note that if you are already using the key in a production environment, changing it will invalidate the signature generated based on the key.
![](https://qcloudimg.tencent-cloud.cn/raw/63d948da67e7b1d9c48b7bcfae3567c9.png)
