Alarm messages for Anti-DDoS Advanced will be sent to you through Message Center, SMS, or email in the following conditions (the receipt methods configured on the [Message Center Subscription](https://console.cloud.tencent.com/message/subscription) page shall prevail):
- An attack starts.
- An attack ended 15 minutes ago.
- An IP is blocked.
- An IP is unblocked.

You can modify the recipients and how they receive the alarm messages as needed.

## Setting Alarm Threshold
1. Log in to the [new Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/alarm) and select **Alarm Notification** on the left sidebar.
2. You can set the "inbound traffic alarm threshold for single IP" and "DDoS cleansing threshold" in the feature blocks on the right.
![](https://main.qcloudimg.com/raw/7c7d59b086c91ff552dc61a6f53d78be.png)
3. Click the pencil icon on the right of the default threshold for one single IP to modify the default threshold. After the modification is completed, click **OK**.
![](https://main.qcloudimg.com/raw/6cd5ae21ef240a8b1eeb3bbb43664559.png)
4. Click **Advanced Settings** in a block to enter the IP alarm settings list, where you can set different alarm thresholds for different IPs.
	- Inbound traffic alarm for single IP
![](https://main.qcloudimg.com/raw/011822c5e67d2b7c00a7ed6cbddc0763.png)
	- DDoS cleansing threshold
![](https://main.qcloudimg.com/raw/1a5902f1cc4e60807fddf06b0976b75f.png)


## Setting Notification Method
1. Log in to your Tencent Cloud account and go to the [Message Center](https://console.cloud.tencent.com/message/detail/45743360).
 >Alternatively, you can log in to the [console](https://console.cloud.tencent.com/ddos/antiddos-native/overview/ddos), click ![](https://main.qcloudimg.com/raw/b1a8f001baaea4b7d9027ec1340fab9e.png) in the top-right corner, and then click **View More** in the pop-up window to enter the Message Center.
2. Click **Message Subscription** on the left sidebar to enter the message list.
3. In the message list, select the receipt methods on the row of **Security Event Notification** and click **Modify Message Recipient** to enter the message recipient modifying page.
![](https://main.qcloudimg.com/raw/0cf55387be49197d6614ce84d150a39f.png)
4. On the message recipient modifying page, set the message recipients. After completing the settings, click **OK**.
![](https://main.qcloudimg.com/raw/27a545a7ccb0096a0c9a85c868745bef.png)
