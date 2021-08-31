## Use Cases
Alarm messages for Anti-DDoS Pro will be sent to you through Message Center, SMS, or email in the following conditions (the receipt methods configured on the [Message Center Subscription](https://console.cloud.tencent.com/message/subscription) page shall prevail):
- An attack starts.
- An attack ended 15 minutes ago.
- An IP is blocked.
- An IP is unblocked.

You can modify the recipients and how they receive the alarm messages as needed.

## Setting Alarm Threshold
1. Log in to the [new Anti-DDoS Pro Console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and click **Alarm Notification** on the left sidebar.
2. You can set the "inbound traffic alarm threshold for single IP" and "DDoS cleansing threshold" in the feature blocks on the right.
![](https://main.qcloudimg.com/raw/77c22fa67022cc5ce14dfc3a17164ffa.png)
3. Click **Advanced Settings** in a feature block to enter the alarm configuration list, where you can set different alarm thresholds for different Anti-DDoS Pro resources.
 - Configure the inbound traffic alarm for single IP
![](https://main.qcloudimg.com/raw/5f34e67f4c0d7c6aa9dd4d6f0899fa40.png)
 - Set the DDoS cleansing threshold
![](https://main.qcloudimg.com/raw/f6bf54951ec7c2236e91a4b885ec64ac.png)


## Setting Notification Method
1. Log in to your Tencent Cloud account and go to the [Message Center](https://console.cloud.tencent.com/message/detail/45743360).
 >Alternatively, you can log in to the [console](https://console.cloud.tencent.com/dayu/overview), click ![](https://main.qcloudimg.com/raw/b1a8f001baaea4b7d9027ec1340fab9e.png) in the top-right corner, and then click **View More** in the pop-up window to enter the Message Center.
2. Click **Message Subscription** on the left sidebar to enter the message list.
3. In the message list, select the receipt methods on the row of **Security Event Notification** and click **Modify Message Recipient** to enter the message recipient modifying page.
![](https://main.qcloudimg.com/raw/deaa7bc482f9a1f8e60115e1880fbad7.png)
4. On the message recipient modifying page, set the message recipients. After completing the settings, click **OK**.
![](https://main.qcloudimg.com/raw/fa1d1131a717a911ad80259b34ad186e.png)
