## Overview
After you activate VOD, the system will assign you a default domain name `xxx.vod2.myqcloud.com`, which will be used by default for all VOD resources. You can also add and resolve a custom domain name in the [VOD console](https://console.cloud.tencent.com/vod/overview).
## Prerequisites
- You have activated the VOD service. For details, see [Purchase Guide](https://intl.cloud.tencent.com/document/product/266/39506).
- ICP filing is required for domain names used for business in Chinese mainland.

## Adding Domain Name
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and click **Distribution and Playback** > **Domain Name** on the left sidebar.
2. Click **Add Domain**, enter the domain in the pop-up, and click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/6ce1d60d21bf80b237a5a46a4b1aafed.png)

>?
>- It takes several minutes to add a domain name. After that, you can view its status, CNAME, and domain name type.
>?One Tencent Cloud account can add up to 20 domain names.

## Resolving Domain Name
After adding a domain name, you need to configure the CNAME at the specific DNS service provider of the domain name, so that users can access your video information through the domain name.

>?This document uses Tencent Cloud DNS as the DNS service provider to illustrate how to add a CNAME record. The detailed steps vary by provider. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/266/42076).

1. Log in to the [Domains console](https://console.cloud.tencent.com/domain) and click **Resolve** on the right of the domain name to be resolved.
2. Go to the **Record Management** page of the domain name and click **Add Record**.
3. In the pop-up, set **Record Type** to CNAME, **Host Record** to the domain name prefix (such as `www`), and **Record Value** to the CNAME domain name, and click **Confirm**.

>! After you add a custom domain name, it’s normal that a small amount of traffic will still be generated even if you do not add a video, for a small number of packets will be returned to the domain name.


