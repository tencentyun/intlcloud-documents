Tencent Cloud will send you alarm messages via the channels (including Message Center, SMS, email, and WeChat) you configured in **[Message Center** -> **Message Subscription](https://console.cloud.tencent.com/message/subscription)** when:
- Attack to your protected IP starts
- 15 minutes after the attack ends
- Protected IP is blocked
- Protected IP is unblocked

You can modify the recipients and how they receive the alarm messages according to your situation.

## Configuring the alarm threshold:
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console, click **Anti-DDoS Advanced (New)** -> **Alarm Thresholds**.
2. You can now set the **Inbound Traffic Threshold Per IP** and **DDoS Cleansing Traffic Alarm**.
![](https://main.qcloudimg.com/raw/01969aff5f8e651c054d8eb8c86e1c6a.png)
3. Click the pencil icon next to thresholds to modify them, and click **OK**.
![](https://main.qcloudimg.com/raw/7cb53a1a61752a8ddbcddef05f114b05.png)
4. Click **Advanced Settings** of each section to enter its alarm setting list, and then click **Modify** to set different thresholds for each instance.
 - Modifying thresholds in **Inbound Traffic Threshold Per IP**
![](https://main.qcloudimg.com/raw/f8504b778fe85ebf573c13f399a9d5e5.png) 
 - Modifying thresholds in **DDoS Cleansing Traffic Alarm**
![](https://main.qcloudimg.com/raw/e71d93de382549971ffc6db27c55e24d.png)

## Setting the message channels
1. Log in to your Tencent Cloud account and go to [Message Center](https://console.cloud.tencent.com/message/detail/45743360).
 >?You can also log in to the [console](https://console.cloud.tencent.com/ddos/antiddos-native/overview/ddos), click ![](https://main.qcloudimg.com/raw/b1a8f001baaea4b7d9027ec1340fab9e.png) on the top bar, and click **More** to enter the Message Center.
2. Click **Message Subscription** in the left sidebar.
3. Tick message channels in **Security Notification** and click **Modify Message Recipient**.
![](https://main.qcloudimg.com/raw/0cf55387be49197d6614ce84d150a39f.png)
4. Tick recipients on the setting page and click **OK**.
![](https://main.qcloudimg.com/raw/27a545a7ccb0096a0c9a85c868745bef.png)
