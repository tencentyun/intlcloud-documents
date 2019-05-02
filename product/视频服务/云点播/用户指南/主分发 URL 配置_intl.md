## Operation Scenario
After a domain name is successfully added and resolved, you can access your video resources through the new domain name; however, for the URL of the video obtained via the API or in the console, the Host remains the original domain name. In order to update the Host information, you need to log in to the [VOD Console](https://console.cloud.tencent.com/video/cdnlog) to set the master distribution URL.
## Steps
1. Log in to the [VOD Console](https://console.cloud.tencent.com/video/cdnlog) and select **Distribution and Playback** > **Primary Distribution URL** in the left navigation pane.
2. Click **Edit** on the right of the configuration information to set the following parameters:
 - Supported protocol types for master distribution: HTTP and HTTPS.
 - Master distribution domain name: The default is `xxx.vod2.myqcloud.com` that is auto-assigned by the system. You can also [add]() and [resolve]() a custom domain name as the master distribution domain name.

 ![](https://main.qcloudimg.com/raw/79f80fab63425e219f44a1f663c43870.png)
