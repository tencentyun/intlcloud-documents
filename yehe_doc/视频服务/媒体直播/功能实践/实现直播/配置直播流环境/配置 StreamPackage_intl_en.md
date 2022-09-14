This document shows you how to configure StreamPackage.

1. Log in to the [StreamPackage console](https://console.tencentcloud.com/mdp/channel), select a region near to your operations.![](https://qcloudimg.tencent-cloud.cn/raw/9e2a246d5681ee392a1c8c70cd342de3.png)
2. Click **Create Channel** and enter the required information in the pop-up window.![](https://qcloudimg.tencent-cloud.cn/raw/beef79acbc0bb01fdc795adabd23cf83.png)
- **Input Protocol**: HLS or DASH. HLS is selected in this example.
- **Max Segment Duration**: The maximum duration of TS segments pushed to this channel. We recommend you set this to four seconds.
- **Max Playlist Duration**: The maximum duration of M3U8 playlist files pushed to this channel. We recommend you set this to 12 seconds (i.e., three TS segments in an M3U8 playlist).

3. Click **Create**. You will enter the advanced configuration page. You can view existing configuration information under the **Information** tab, or configure push URLs, playback URLs, and CDN acceleration under the **Input**, **Endpoints**, and **CDN** tabs.

4. **Input**: The system will automatically assign two input URLs for the channel, which can be used for failover to ensure high availability.
![](https://qcloudimg.tencent-cloud.cn/raw/48526b3405cd4373f41f95aa254c4a37.png)
- You can configure independent authentication information for each input. After you enable **Input Authentication**, the system will automatically generate **a username and a password** for the input.[](https://qcloudimg.tencent-cloud.cn/raw/c32de384eda1fa084d50b13f243a9021.png)
- You can click **Rotate credentials** to generate new authentication information. The original information cannot be recovered.
- If you want to push content to the input URL from a third-party service, make sure you note the **Input URL** and authentication information.

5. **Endpoint**: Select the **Endpoints** tab, click **Create Endpoint** to create a playback URL. Two access control methods are supported: **IP Restriction** and **AuthKey**. Because HLS is selected as the input protocol, an HLS URL will be generated. The URL is the full path of the main.m3u8 file.
![](https://qcloudimg.tencent-cloud.cn/raw/43f73db0ecaba6c72d7eb4677397caad.png)

6. You have now completed configuration for StreamPackage. Return to **Channel Management**, find the channel you created in the list, and note the **ID** and **Endpoint URL** for later use.
![](https://qcloudimg.tencent-cloud.cn/raw/5eb1b481f758f89ec7a1279d7bd4d873.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3f7c30d33e17425a44dca05a701e8ad7.png)