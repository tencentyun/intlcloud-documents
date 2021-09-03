Tencent Cloud will send you alarm messages via the channels (including Message Center, SMS, and email) you configured in **[Message Center** -> **Message Subscription](https://console.cloud.tencent.com/message/subscription)** when:
- An attack starts.
- An attack ended 15 minutes ago.
- An IP is blocked.
- An IP is unblocked.

You can modify the recipients and how they receive the alarm messages as needed.

## Configuring the alarm threshold:
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console and select **Anti-DDoS Advanced** -> **Alarm Thresholds** on the left sidebar.
2. You can now set the **Inbound Traffic Threshold Per IP**, **DDoS Cleansing Threshold** and **CC Traffic Cleansing Alarm**.
![](https://main.qcloudimg.com/raw/c2d882b40deb8abdaa4423fbd8c5e2e9.png)
3. Click the pencil icon next to thresholds to modify them, and click **OK**.
![](https://main.qcloudimg.com/raw/d1e4844a203c925f5f97f1b8118e1244.png)
4. Click **Advanced Settings** of each section to enter its alarm setting list, and then click **Modify** to set different thresholds for each instance.
 - Setting the inbound traffic threshold for an IP
![](https://main.qcloudimg.com/raw/9bcf2a473b36d17024f456eb57bb4a4e.png) 
 - Setting the DDoS cleansing threshold
![](https://main.qcloudimg.com/raw/60eb8cd5f224f471206f9787d2b3b202.png)
 - Setting the CC traffic cleansing alarm
![](https://main.qcloudimg.com/raw/2f84bd73d4ae1cf71440478b8466c0b3.png)
5. Instances can be edited in batch. After selecting multiple instances, click **Batch Modify** to modify them.
![](https://main.qcloudimg.com/raw/0eb4eb5959157a362537bf13632917aa.png)

## How to Set Message Channel
1. Log in to your Tencent Cloud account and go to [Message Center](https://console.cloud.tencent.com/message/detail/45743360).
 >?You can also log in to the [console](https://console.cloud.tencent.com/ddos/antiddos-native/overview/ddos), click ![](https://main.qcloudimg.com/raw/b1a8f001baaea4b7d9027ec1340fab9e.png) on the top bar, and click **More** to enter the Message Center.
2. Click **Message Subscription** in the left sidebar.
3. Tick message channels in **Security Notification** and click **Modify Message Receiver**.
![](https://main.qcloudimg.com/raw/cddcb841a332a16fed3beaf2e9c96ff5.png)
4. Tick recipients on the setting page and click **OK**.
![](https://main.qcloudimg.com/raw/6d28bab83d16c94d626205aedea6a198.png)
