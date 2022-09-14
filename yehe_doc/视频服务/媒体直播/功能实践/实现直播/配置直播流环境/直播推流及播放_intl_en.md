This document shows you how to use OBS to push streams and VLC to play streams. Open OBS, go to **Settings > Stream**, and enter the input URL in **Server** and the stream name in **Stream Key**.
![](https://qcloudimg.tencent-cloud.cn/raw/d19308151baf27053d3ef774f416274c.png)

Open VLC (VLC for macOS is used in the example), click **File > Open Network…**, select the **Network** tab, and enter the StreamPackage endpoint URL (replace the domain part with the playback domain configured in CSS).
![](https://qcloudimg.tencent-cloud.cn/raw/e5d6e5f9c304f6b38fffafca19c0b456.png)

You have now implemented a high-reliability live streaming service based on StreamLive, StreamPackage, and CSS.
![](https://qcloudimg.tencent-cloud.cn/raw/3096992f56506043045b681624e12770.png)