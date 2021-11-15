After connecting your application to and routing its traffic to the DDoS Edge Defender service, you can view the DDoS, CC, and web protection states and the application traffic state on the console.
>?DDoS Edge Defender is currently available for beta users. To use it, please [contact us](https://intl.cloud.tencent.com/contact-us).

## Viewing DDoS Protection Details
1. Log in to the [DDoS Edge Defender Console](https://console.cloud.tencent.com/ddos/antiddos-edge/overview/ddos), click **Overview** on the left sidebar, and then select **DDoS Protection**.
2. On the **DDoS Protection** page, select a query period.
>?You can query attack traffic and DDoS attack events in the past 180 days.

![](https://qcloudimg.tencent-cloud.cn/raw/d81f2ef90e98950154227f4a5e6b660f.png)
3. Click ![](https://main.qcloudimg.com/raw/74853a065cabb2c2d5df9fccd42fe984.png) to search the protected instance in the drop-down list and view whether it is hit by DDoS attacks.
![](https://qcloudimg.tencent-cloud.cn/raw/3f81e2e57dc682eaa4e178bac0267deb.png)
 - **Attack Traffic Bandwidth**
Displays the changes of the attack traffic bandwidth/attack packet rate within the selected time period. As shown below, you can spot a spike in the bandwidth trend graph when the instance is attacked.
 ![](https://qcloudimg.tencent-cloud.cn/raw/6314869b3536ce5bf3b00f38ab817d38.png)
 - **Attack Event**
Displays the start time, duration, type and status of an attack event.
>!
>- Only the details of a single attacker IP can be queried.
>- Attacker IP information is randomly collected for statistics. The data will appear around 5 minutes after an attack ends.

 ![](https://qcloudimg.tencent-cloud.cn/raw/efb5a5d77f70cc2a61888d9eb00f9038.png)
 - **Attack Statistics**
Displays the total number of attacks, attack traffic and packets, giving you an overall picture of attacks within the selected time period.
>?
>- Total attack traffic: presents how the attack traffic distributes over different protocols within the selected time period.
>- Attack packets: presents how the attack packets distribute over different protocols within the selected time period.
>- Total attacks: presents how the attacks distribute over different attack types within the selected time period.

 ![](https://qcloudimg.tencent-cloud.cn/raw/59f8a2c0c90cf269479f0b464312edea.png)


## Viewing CC Protection Details
1. Log in to the [DDoS Edge Defender Console](https://console.cloud.tencent.com/ddos/antiddos-edge/overview/ddos), click **Overview** on the left sidebar, and then select **CC Protection**.
2. On the **CC Protection** page, select a query period.
>?You can query the number of attack requests and CC attack events in the last 180 days.

![](https://qcloudimg.tencent-cloud.cn/raw/d5f5aaa806aada8fc9be8e06aa76418d.png)
3. Click ![](https://main.qcloudimg.com/raw/74853a065cabb2c2d5df9fccd42fe984.png) to search the protected instance in the drop-down list and view whether it is hit by CC attacks.
![](https://qcloudimg.tencent-cloud.cn/raw/860193f7a2d1f9570ff6ca6e9303cf61.png)

- **Attack Traffic Bandwidth**
    - You can select **Today** to view the trend in the number of attack requests. You can check whether the total number of requests is far higher than the normal QPS, whether the attack QPS has a value, and whether the value is extremely high.
>?
>- Total request peak: the peak number of total attack requests received by the protected IP.
>- Attack request peak: the peak number of attack requests blocked by the Edge Defender system.

![](https://qcloudimg.tencent-cloud.cn/raw/e9018d9bfc96d8c60692a7be8b2b0986.png)

- **CC Attack Records**
If the protected instance is subject to CC attacks, the system will record the attack start time and end time, attacked domain names, attacked URLs, total request peak, attack request peak, and attacker IP.


## Viewing Web Protection Details
1. Log in to the [DDoS Edge Defender Console](https://console.cloud.tencent.com/ddos/antiddos-edge/overview/ddos), click **Overview** on the left sidebar, and then select **Web Protection**.
2. On the **Web Protection** page, select a query period.
>?You can query attack traffic and web attack events in the past 180 days.

![](https://qcloudimg.tencent-cloud.cn/raw/8bac3facf58a7061fe7a3e1d4e6121b0.png)
3. Click ![](https://main.qcloudimg.com/raw/74853a065cabb2c2d5df9fccd42fe984.png) to search the protected instance in the drop-down list and view whether it is hit by web attacks.
![](https://qcloudimg.tencent-cloud.cn/raw/a353cea39b68f991b11e494e8238cf91.png)
 - **Attack Trend**
Displays the attack trend within the selected time period in terms of the attack peak and total number of attacks.
![](https://qcloudimg.tencent-cloud.cn/raw/472470e7080f7f98d8ce2e4153bd6819.png)
 - **Attack Event**
Displays the start time, attacked domain names, attacked URLs and type of an attack event.
![](https://qcloudimg.tencent-cloud.cn/raw/2e32e6ef07290c8d1b0e4adf97014fc1.png)
 - **Attack Statistics**
Displays the total number of attacks, attack traffic and packets, giving you an overall picture of attacks within the selected time period.
>?
>- Top 5 most attacked domain names: presents the top five domain names that are bound to the protected instance subject to most attacks within the selected time period.
>- Top 5 attackers (IP): presents the top five attacker IPs that launch most attacks to the protected instance within the selected time period.
>- Attack type distribution: presents the attack type distribution within the selected time period.

![](https://qcloudimg.tencent-cloud.cn/raw/93ee1a1a8af91cb8dd17dc3c1d4306a9.png)

## Viewing User Traffic Details
1. Log in to the [DDoS Edge Defender Console](https://console.cloud.tencent.com/ddos/antiddos-edge/overview/ddos), click **Overview** on the left sidebar, and then select **Scenario**.
2. On the **Scenario** page, select a query period.
>?You can query scenario details in the past 180 days.

![](https://qcloudimg.tencent-cloud.cn/raw/fcabf582cd95fb9c6f721a61d568f2fc.png)
3. Click ![](https://main.qcloudimg.com/raw/74853a065cabb2c2d5df9fccd42fe984.png) to search the protected instance in the drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/3a646391dc4c86940e5a7769b0ade00d.png)

 - You can view the application bandwidth peak, maximum application connections, and application request peak.
 ![](https://qcloudimg.tencent-cloud.cn/raw/ea3c1c11a67a6d45cfdb9a708895fae1.png)

 - You can view the trends for inbound/outbound application traffic bandwidth, inbound/outbound application packet rate, and the number of active connections and new connections within the selected time period.
![](https://qcloudimg.tencent-cloud.cn/raw/8f463bf3ebc782567a4403560cf47012.png)

 - You can view the trends for the number of active connections and new connections, and the status code within the selected time period.
>?
>- Active connections: the number of TCP connections that are already established and currently active.
>- New connections: the number of TCP connections that are newly established per second for communication between the client and Edge Defender system.

 ![](https://qcloudimg.tencent-cloud.cn/raw/f8d93ebc6eb4576b2a99471f1dddc5c2.png)
