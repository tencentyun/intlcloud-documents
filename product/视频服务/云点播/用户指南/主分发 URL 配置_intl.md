## Operation Scenario
After a domain name is successfully added and resolved, you can access your video resources through it; however, the Host in a video URL obtained through the API or in the console remains the original domain name. In order to update the Host information in the URL, you need to log in to the [VOD Console](https://console.cloud.tencent.com/video/cdnlog) to set the master distribution URL.
## Steps
1. Log in to the [VOD Console](https://console.cloud.tencent.com/video/cdnlog) and select **Distribution and Playback** > **Primary Distribution URL** in the left navigation pane.
2. Click **Edit** on the right of the configuration information to set the following parameters based on the actual situation:
 - Master distribution protocol type: HTTP and HTTPS are supported.
 - Master distribution domain name: By default, the system-assigned `xxx.vod2.myqcloud.com` is used. You can also [add]() and [resolve]() a custom domain name as the master distribution domain name.

 ![](https://main.qcloudimg.com/raw/79f80fab63425e219f44a1f663c43870.png)
