Before using the time shifting feature of StreamLive, you need to activate Cloud Streaming Services (CSS) and StreamLive. In CSS, use the time shifting domain name as the playback domain name and add it according to the process of adding a domain name.



### Activating the StreamLive time shifting feature

[Submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for activating the StreamLive time shifting feature, during which you need to provide your account APPID and time shifting domain name.


### Configuring StreamLive time shifting

After activating the time shifting feature, you can enable the time shifting capability for StreamLive output groups via the console or API and bind the time shifting domain name.

>! Time shifting can be enabled only for HLS_ARCHIVE and DASH_ARCHIVE output groups.

1. Go to the StreamLive console and enter the **Channel Management** page.
2. Create a channel. Or select a channel for which time shifting is to be configured and click **Edit Channel**.
3. On the **Output Group Setting** page, set **Output Group Type** in the **Basic Information** area to **HLS_ARCHIVE** or **DASH_ARCHIVE**. 
4. In the **TimeShift Information** area, toggle on the time shifting switch and enter the time shifting duration.

>! The time shifting duration must be between 300 seconds and 1,209,600 seconds.

![](https://qcloudimg.tencent-cloud.cn/raw/46388651f1047edb0a1a8b8128ae2e02.png)
