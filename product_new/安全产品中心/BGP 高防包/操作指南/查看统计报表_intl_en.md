After an IP address is bound to an Anti-DDoS Pro instance, when you receive a DDoS attack alarm message or notice any issue with your business, you can log in to the console to view details about the attacks, including the attack traffic bandwidth and the protection effect. Enough information is critical for you to take measures to keep your business running smoothly.
## Viewing DDoS Protection Details
1. Log in to [Anti-DDoS Pro Console](https://console.cloud.tencent.com/dayu/bgp_v2).
2. Select **Statistical Report** and choose **Single IP Instance** on the top.
   Note: If you choose **Multi-IP Instance**, you will be able to view DDoS protection details of each IP protected by your Anti-DDoS Pro instance.
3. In the **DDoS Protection** tab, select a query period, a region, and an instance to check whether the instance has been attacked.
   >You can query attack traffic and DDoS attack events in the past 180 days.
   >
	- Check the details about the attacks to the instance within the queried period, including trends in **attack traffic bandwidth/attack packet rate**.
![](https://main.qcloudimg.com/raw/e2cad2b0653173aa060516a42999d41b.png)
	- Check how the attacks distribute over different attack traffic protocols, attack packet protocols, and attack types.
		- **Attack traffic protocol distribution**: Check how the attacks distribute over different attack traffic protocols within the queried period.
		- **Attack package protocol distribution**: Check how the attacks distribute over different attack packet protocols within the queried period.
		- **Attack type distribution**: Check how the attacks distribute over different attack types within the queried period.
![](https://main.qcloudimg.com/raw/3938c0e41b9197e424e64a03036773a4.png)
	-  In **DDoS Attack Records**, check details about the DDoS attack events within the queried period, including the starting time, duration, type and status of each attack event.
		- You can download attack packets to analyze and trace the DDoS attacks.
		- Click **Attack Details** to view the maximum package rate, maximum attack traffic bandwidth, and total amount of traffic cleansed during the DDoS attack events.
		- Click **Attack Source Information** to check the attack source IP addresses, original regions, generated attack traffic, and attack packet size, etc.
>!Attack source information is sampled data, which is randomly collected for statistics. The data will appear around 2 hours after an attack ends.
>
![](https://main.qcloudimg.com/raw/517c3e6013d00c94758e300fbc3641e3.png)

## Checking CC Protection
1. Log in to [Anti-DDoS Pro Console](https://console.cloud.tencent.com/dayu/bgp_v2).
2. Select **Statistical Report** and choose **Single IP Instance** on the top.
   Note: If you choose **Multi-IP Instance**, you will be able to view CC attack protection details of each IP protected by your Anti-DDoS Pro instance.
3. In the **CC Attack Protection** tab, select a query period, a region, and an instance to check whether the instance has been attacked.
   >You can query the number of attack requests and CC attack events in the past 180 days.
   >
	- You can select **Today** to view the trend in the number of attack requests. You can check whether the total number of requests is far higher than the normal QPS, whether the attack QPS has a value, and whether the value is extremely big.
	- If the protected IP is subject to CC attacks, the system will record the attack start time, end time, attacked domain names, attacked URLs, total request peak, attack request peak, the attack source, etc.
		-  **Total Request Peak**: represents the peak of the total request traffic the instance receives when the attack occurs.
		- **Attack Request Peak**: represents the peak number of requests blocked by the instance when the attack occurs.
![](https://main.qcloudimg.com/raw/5555350b5de6d54039030a0c90c99195.png)

