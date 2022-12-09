## Protection Overview
After connecting your application to and routing its traffic to the Anti-DDoS Advanced (Global Enterprise Edition) service, you can check the application traffic status and Anti-DDoS protection status in the console. Attack packet data can be downloaded for source tracing and analysis.


### Viewing attack statistics
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console and select **Overview** > **Protection Overview**.
![](https://qcloudimg.tencent-cloud.cn/raw/d43fa663afebd05e6807dde663b90258.png)
2. In the "Attacks" module, you can view the application security status, the latest attack and the attack type. To obtain higher protection, you can click **Upgrade Protection**.

3. This module also displays the details of the following data.
![](https://qcloudimg.tencent-cloud.cn/raw/4ecad368488ce05e5c54d6ac8b316fa4.png)
   **Field description:**
    - Attacked IPs: The total number of attacked application IPs of basic protection, Anti-DDoS Pro and Anti-DDoS Advanced.
    - Protected IPs: The total number of protected application IPs of Anti-DDoS Pro and Anti-DDoS Advanced.
    - Blocked IPs: The total number of blocked IPs of basic protection, Anti-DDoS Pro and Anti-DDoS Advanced.
    - Attacked domain names: The total number of domain names of attacked Anti-DDoS Advanced instances and ports.
    - Protected domain names: The number of domain names connected to Anti-DDoS Advanced instances.
    - Peak attack bandwidth: The maximum attack bandwidth of the current attack events.


### Viewing defense statistics
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console and select **Overview** > **Protection Overview**.
2. In the "Defense" module, you can easily see the application IP security status.
![](https://qcloudimg.tencent-cloud.cn/raw/7a88a800c181831dc4580e3dc923102f.png)
   **Field description:**
    - Total IPs: The total number of application IPs, including IPs of basic protection, Anti-DDoS Pro and Anti-DDoS Advanced.
    - Protected IPs: The total number of protected application IPs of Anti-DDoS Pro and Anti-DDoS Advanced.
    - Blocked IPs: The total number of blocked IPs of basic protection, Anti-DDoS Pro and Anti-DDoS Advanced.
3. This module also displays the total number of attacks on your applications, giving you a picture of the distribution of attacks.
![](https://qcloudimg.tencent-cloud.cn/raw/63ed220cf237d856528e1f2b1a80e49e.png)
3. Meanwhile, this module provides recommended actions for the attacked IPs connected to basic protection, allowing you to quickly upgrade your Anti-DDoS service.
![](https://qcloudimg.tencent-cloud.cn/raw/7cce1b85e81dab27cae83e03cfabeb13.png)

### Viewing Anti-DDoS Advanced instance statistics
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console and select **Overview** > **Protection Overview**.
2. The "Anti-DDoS Instances" module visualizes the Anti-DDoS instance status data, providing an easy and complete way to know the distribution of insecure applications.
![](https://qcloudimg.tencent-cloud.cn/raw/5a08a7115062914ecccf1674762a541a.png)

### Viewing recent events
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console and select **Overview** > **Protection Overview**.
2. The "Recent Events" module shows you all the recent attack events. For attack analysis and source tracing, click **View Details** to enter the event details page.
![](https://qcloudimg.tencent-cloud.cn/raw/61528176e7f8297f3532901bca36c761.png)
3. In the "Attack Information" module of the event details page, you can view the detailed attack information for the selected period, including the attacked IP, status, attack type (which is sampled data), peak attack bandwidth and attack packet rate, and attack start and end time.
![](https://qcloudimg.tencent-cloud.cn/raw/4aa25f97c6f9dbaee1a1d747f315b428.png)
4. In the "Attack Trend" module of the event details page, you can view the trend of attack bandwidth and attack packet rate and easily find the peak spikes.
>?This module provides complete, real-time data in the attack period.

![](https://qcloudimg.tencent-cloud.cn/raw/1df1d09926470f122ea43afa351dcf7f.png)
5. In the "Attack Statistics" module of the event details page, you can view how attacks distribute over different attack traffic protocols and attack types.
>?This module provides sampled data in the attack period.

![](https://qcloudimg.tencent-cloud.cn/raw/8c72fbac90522d2aa0eccda6a56d9e7d.png)
   **Field description:**
   - Attack traffic protocol distribution: It displays how attacks on the selected Anti-DDoS Advanced instance distribute over different attack traffic protocols within the queried period.
   - Attack type distribution: It displays how attacks on the selected Anti-DDoS Advanced instance distribute over different attack types within the queried period.
6. The "Top 5" modules of the event details page displays the top 5 attacker IP addresses and the top 5 attacker regions, which is helpful to precise protection configuration.
>?This module provides sampled data in the attack period.

![](https://qcloudimg.tencent-cloud.cn/raw/5e70e40264c9511b6357bce58ee1cc14.png)
7. In the "Attacker Information" module of the event details page, you can view the sampled data of the attack period, including the attacker IP, region, total attack traffic, and total attack packets.
>?This module provides sampled data in the attack period.

![](https://qcloudimg.tencent-cloud.cn/raw/146b6107c5ceac3a3d1afccd66798c01.png)

## Anti-DDoS Advanced Overview
After an IP address is bound to an Anti-DDoS Advanced instance, when you receive a DDoS attack alarm message or notice any issue with your business, you need to view the attack details in the console, including the attack traffic and current protection effect. Enough information is critical for you to take measures to keep your business running smoothly.


### Viewing DDoS protection details
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition)](https://console.cloud.tencent.com/ddos/ddos-basic) console and select **Overview** > **Protection Overview**.
![](https://qcloudimg.tencent-cloud.cn/raw/be67d057c2ece542e53b3730a5cf9945.png)
1. On the **DDoS Protection** tab, set a query period, and select **All Lines** > **Anycast** to check whether there are attacks. The complete attack data is displayed by default.
>?You can query attack traffic and DDoS attack events in the past 180 days.

![](https://qcloudimg.tencent-cloud.cn/raw/f35b004d7113c0874a569d0dcc7cdbdd.png)
2. View the information of attacks suffered by the selected Anti-DDoS Advanced instance within the queried period, such as the trends of attack traffic bandwidth/attack packet rate.
![](https://qcloudimg.tencent-cloud.cn/raw/7fa11d7c8ff40d20534259e9159134b7.png)
3. You can view the recent DDoS attacks in the **Recent Events** section. To view event details, you can click **View Details**.
![](https://qcloudimg.tencent-cloud.cn/raw/61528176e7f8297f3532901bca36c761.png)
    - Information including attacker IP, attack source region, generated attack traffic, and attack packet size will be displayed for source analysis and tracing.
![](https://qcloudimg.tencent-cloud.cn/raw/4aa25f97c6f9dbaee1a1d747f315b428.png)
    - To view sampled attack data within a specified period, click **Packet Download**.
![](https://qcloudimg.tencent-cloud.cn/raw/5bcbb304872f4271d7c431bcecc37486.png)
    - The sampled attack packet data can be downloaded to help customize a protection plan.
    ![](https://qcloudimg.tencent-cloud.cn/raw/eab5a834b67e6d95e8283b54aeedb37c.png)
4. In the **Attack Statistics** section, you can view how the attacks distribute across different attack traffic protocols, attack packet protocols, and attack types.
![](https://qcloudimg.tencent-cloud.cn/raw/e065d87c5e7a90bc920f1658f4f45ad2.png)
   **Field description:**
    - Attack traffic protocol distribution: It displays how attacks on the selected Anti-DDoS Advanced instance distribute over different attack traffic protocols within the queried period.
    - Attack packet protocol distribution: It displays how the attacks suffered by the selected Anti-DDoS Advanced instance distribute across different attack packet protocols within the queried period.
    - Attack type distribution: It displays how attacks on the selected Anti-DDoS Advanced instance distribute over different attack types within the queried period.
5. In the attack source section, you can view the distribution of DDoS attack sources in and outside the Chinese mainland within the queried period, so that you can take further protective measures.
![](https://qcloudimg.tencent-cloud.cn/raw/ade8f4dcbcdd71e35af7116b2a7b8941.png)

### Viewing CC protection details
1. On the **CC Protection** tab, set a query period, and select **All Lines** > **Anycast** to check whether there are attacks.
![](https://qcloudimg.tencent-cloud.cn/raw/0a53677659c3787cdc8664799aab047a.png)
2. You can select **Today** to view the following data to identify the impact of attacks on your business.
![](https://qcloudimg.tencent-cloud.cn/raw/1a4919ceb93c145acc3a4a80ff4c5dda.png)
   **Field description:**
    - Total request rate: The rate of total traffic (in QPS).
    - Attack request rate: The rate of attack traffic (in QPS).
    - Total requests: The total number of requests received.
    - Attack requests: The number of attack requests received.
3. You can view recent CC attacks in the **Recent Events** section. Click **View Details** on the right of an event to display the attack start and end time, attacked domain name, attacked URI, total request peak, attack request peak, and attacker IP. You can also check the attack information, attack trends, and detailed CC records.
![](https://qcloudimg.tencent-cloud.cn/raw/68b909b0b2d13eff52d6f1f1c7733bdc.png)