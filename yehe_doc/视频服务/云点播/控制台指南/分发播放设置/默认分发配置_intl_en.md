## Operation Scenarios
After a domain name is added and resolved, you can access your video resources through it; however, the `Host` in a video URL obtained through the API or console remains that in the original domain name. Therefore, you need to log in to the console and update the `Host` information of URL in the default distribution configuration.
## Directions
1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod/overview) and click **Distribution and Playback** > **Default Distribution Configuration** on the left sidebar to enter the "Default Distribution Configuration" page.
2. Click **Edit** in the top-right corner and set the corresponding parameters:
 - Primary Distribution Protocol: HTTP and HTTPS are supported.
 - Default Distribution Domain Name: by default, the system-assigned `xxx.vod2.myqcloud.com` is used. You can also [add](https://intl.cloud.tencent.com/document/product/266/35572) and [resolve](https://intl.cloud.tencent.com/document/product/266/35572) a custom domain name as the default distribution domain name.
 
![](https://qcloudimg.tencent-cloud.cn/raw/63d948da67e7b1d9c48b7bcfae3567c9.png)
