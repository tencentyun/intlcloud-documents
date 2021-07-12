After connecting your application to and routing its traffic to the Anti-DDoS Advanced (Global Enterprise Edition) service, you can check the application traffic status and Anti-DDoS protection status in the console. Attack packet data can be downloaded for source tracing and analysis.

## Viewing Anti-DDoS Protection Details
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console, click **Anti-DDoS Advanced (New)** -> **Overview**.
2. Select the **DDoS protection** tab, specify a time period, then click the **All Lines** drop-down list and select **Anycast** to check whether there are any attacks.
>?You can query attack traffic information and DDoS attack events in the past 180 days.
>
![](https://main.qcloudimg.com/raw/a75888ad2754580475fd16c339582c88.png)
 - The pattern of the attacks on the protected IP within the selected time period is showed in the line chart, including the attack traffic bandwidth and attack packet rate trend. The traffic trend chart clearly shows the traffic peak when an IP is under attacks.
 ![](https://main.qcloudimg.com/raw/c23bcc1d54a0cdd5b9bc3b71eef27bdc.png)
 - Integrating data on the total number of attacks, attack traffic and packets, it gives you an overall view of attacks within the selected time period.
  >?
  >- Total attack traffic: presents how the attack traffic on the protected IP distributes over different protocols within the selected time period.
  >- Attack packets: presents how the attack packets to the protected IP distribute over different protocols within the selected time period.
  >- Total attacks: presents how the attacks on the protected IP distribute over different attack types within the selected time period.
  >
  ![](https://main.qcloudimg.com/raw/bf866b5e8166790ee0313e6f935a6ec5.png)
 -In **Attack Events**, you can check details about the DDoS attack events within the selected time period, including the starting time, duration, type, and status of each attack event.
![](https://main.qcloudimg.com/raw/b1f2a54753aeb207210fd479fb39a503.png)
>!
>- You can only query one protected IP for its attack source information each time.
>- Attack source information is sampled data, which is randomly collected for statistics. The data will appear around 5 minutes after an attack ends.
