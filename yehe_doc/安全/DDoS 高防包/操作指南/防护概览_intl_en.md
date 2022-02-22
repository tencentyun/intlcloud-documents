## Protection Overview
The protection overview page of the Anti-DDoS console shows you complete, real-time indicators for basic protection, Anti-DDoS Pro, and Anti-DDoS Advanced applications, including the protection status and DDoS attack events, which can be used for analysis and source tracing.

### Viewing attack statistics
1. Log in to the new [Anti-DDoS console](https://console.cloud.tencent.com/ddos/dashboard/overview), and select **Overview** on the left sidebar to enter the **Protection Overview** page.
![](https://qcloudimg.tencent-cloud.cn/raw/d43fa663afebd05e6807dde663b90258.png)
2. In the "Attacks" module, you can view the application security status, the latest attack and the attack type. To obtain higher protection, you can click **Upgrade Protection**.
3. This module also displays the details of the following data.
![](https://qcloudimg.tencent-cloud.cn/raw/4ecad368488ce05e5c54d6ac8b316fa4.png)
**Field description:**
 - Attacked IPs: the total number of attacked application IPs of basic protection, Anti-DDoS Pro and Anti-DDoS Advanced.
 - Protected IPs: the total number of protected application IPs of Anti-DDoS Pro and Anti-DDoS Advanced.
 - Blocked IPs: the total number of blocked IPs of basic protection, Anti-DDoS Pro and Anti-DDoS Advanced.
 - Attacked domain names: the total number of domain names of attacked Anti-DDoS Advanced instances and ports.
 - Protected domain names: the number of domain names connected to Anti-DDoS Advanced instances.
 - Peak attack bandwidth: the maximum attack bandwidth of the current attack events.


### Viewing defense statistics
1. Log in to the new [Anti-DDoS console](https://console.cloud.tencent.com/ddos/dashboard/overview), and select **Overview** on the left sidebar to enter the **Protection Overview** page.
2. In the "Defense" module, you can easily see the application IP security status.
![](https://qcloudimg.tencent-cloud.cn/raw/7a88a800c181831dc4580e3dc923102f.png)
**Field description:**
 - Total IPs: the total number of application IPs, including IPs of basic protection, Anti-DDoS Pro and Anti-DDoS Advanced.
 - Protected IPs: the total number of protected application IPs of Anti-DDoS Pro and Anti-DDoS Advanced.
 - Blocked IPs: the total number of blocked IPs of basic protection, Anti-DDoS Pro and Anti-DDoS Advanced.
3. This module also displays the total number of attacks on your applications, giving you a picture of the distribution of attacks.
![](https://qcloudimg.tencent-cloud.cn/raw/63ed220cf237d856528e1f2b1a80e49e.png)
3. Meanwhile, this module provides recommended actions for the attacked IPs connected to basic protection, allowing you to quickly upgrade your Anti-DDoS service.
![](https://qcloudimg.tencent-cloud.cn/raw/7cce1b85e81dab27cae83e03cfabeb13.png)

### Viewing instance statistics
1. Log in to the new [Anti-DDoS console](https://console.cloud.tencent.com/ddos/dashboard/overview), and select **Overview** on the left sidebar to enter the **Protection Overview** page.
2. The "Anti-DDoS Instances" module visualizes the Anti-DDoS instance status data, providing an easy and complete way to know the distribution of insecure applications.
![](https://qcloudimg.tencent-cloud.cn/raw/5a08a7115062914ecccf1674762a541a.png)

### Viewing recent events
1. Log in to the new [Anti-DDoS console](https://console.cloud.tencent.com/ddos/dashboard/overview), and select **Overview** on the left sidebar to enter the **Protection Overview** page.
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
 - Attack traffic protocol distribution: displays how attacks on the selected Anti-DDoS Pro instance distribute over different attack traffic protocols within the queried period.
 - Attack type distribution: displays how attacks on the selected Anti-DDoS Pro instance distribute over different attack types within the queried period.
6. The "Top 5" modules of the event details page displays the top 5 attacker IP addresses and the top 5 attacker regions, which is helpful to precise protection configuration.
>?This module provides sampled data in the attack period.

![](https://qcloudimg.tencent-cloud.cn/raw/5e70e40264c9511b6357bce58ee1cc14.png)
7. In the "Attacker Information" module of the event details page, you can view the sampled data of the attack period, including the attacker IP, region, total attack traffic, and total attack packets.
>?This module provides sampled data in the attack period.

![](https://qcloudimg.tencent-cloud.cn/raw/146b6107c5ceac3a3d1afccd66798c01.png)


## Anti-DDoS Pro Overview
After an IP address is bound to an Anti-DDoS Pro instance, when you receive a DDoS attack alarm message or notice any issue with your business, you need to view the attack details in the console, including the attack traffic and current protection effect. Enough information is critical for you to take measures to keep your business running smoothly.



### Viewing DDoS protection details
1. Log in to the new [Anti-DDoS console](https://console.cloud.tencent.com/ddos/dashboard/native), select **Overview** on the left sidebar and then open the **Anti-DDoS Pro** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/e570488f7b63bff477cbe4abe6affe51.png)
1. On the **DDoS Attack** tab, select a query period, target region, and an instance to check whether the instance has been attacked. The complete attack data is displayed by default.
>?You can query attack traffic and DDoS attack events in the past 180 days.

![](https://qcloudimg.tencent-cloud.cn/raw/76cc02f33eb770e0e7552a5ffcd095dc.png)
2. View the information of attacks suffered by the selected Anti-DDoS Pro instance within the queried period, such as the trends of attack traffic bandwidth/attack packet rate.
![](https://qcloudimg.tencent-cloud.cn/raw/8e6bb837d604bb4042af8e979cbd2461.png)
3. You can view the recent DDoS attacks in the **Recent Events** section.
 - Select an event and click **View Details**. You will see the attacker IP, source region, generated attack traffic, and attack packet size on the right, which can be used for attack and source analyses.
![](https://qcloudimg.tencent-cloud.cn/raw/08a170ae73173b5594d58e84dcb7001e.png)
 - Select an event and click **Packet Download**. In the pop-up packet list, select an ID, and click **Download** to download the attack packet sample data, with which you can create a protection plan.
![](https://qcloudimg.tencent-cloud.cn/raw/ac90b3f843fca7dc836b00b632f732b5.png)
4. In the **Attack Statistics** section, you can view how the attacks distribute across different attack traffic protocols, attack packet protocols, and attack types.
![](https://qcloudimg.tencent-cloud.cn/raw/9ada84e0e755295eecd7b45b27827169.png)
**Field description:**
 - Attack traffic protocol distribution: displays how attacks on the selected Anti-DDoS Pro instance distribute over different attack traffic protocols within the queried period.
 - Attack packet protocol distribution: displays how the attacks suffered by the selected Anti-DDoS Pro instance distribute across different attack packet protocols within the queried period.
 - Attack type distribution: displays how attacks on the selected Anti-DDoS Pro instance distribute over different attack types within the queried period.
5. In the attack source section, you can view the distribution of DDoS attack sources in and outside the Chinese mainland within the queried period, so that you can take further protective measures.
![](https://qcloudimg.tencent-cloud.cn/raw/7678c28535ad0f5e014d46c656e89ac4.png)


### Viewing CC protection details
1. On the **CC Protection** tab, select a query period, target region, and an instance to check whether the instance has been attacked.
![](https://qcloudimg.tencent-cloud.cn/raw/78d555997d55ee8db3e693089524726b.png)
2. You can select **Today** to view the following data to identify the impact of attacks on your business.
![](https://qcloudimg.tencent-cloud.cn/raw/90f3e174ac16b9f0776d765a8addb985.png)
**Field description:**
 - Total request rate: the rate of total traffic (in QPS).
 - Attack request rate: the rate of attack traffic (in QPS).
 - Total requests: the total number of requests received.
 - Attack requests: the number of attack requests received.
3. You can view recent CC attacks in the **Recent Events** section. Click **View Details** on the right of an event to display the attack start and end time, attacked domain name, total request peak, attack request peak, and attacker IP. You can also check the attack information, attack trends, and detailed CC records.
![](https://qcloudimg.tencent-cloud.cn/raw/4312a4f7778fbdb3c9dd0f03b9501561.png)
