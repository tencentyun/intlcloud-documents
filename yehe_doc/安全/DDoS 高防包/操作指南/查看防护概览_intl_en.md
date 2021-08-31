After an IP address is bound to an Anti-DDoS Pro instance, when you receive a DDoS attack alarm message or notice any issue with your business, you need to view details of the attacks in the console, including the attack traffic and current protection effect. Enough information is critical for you to take measures in time to keep your business running smoothly.
## Viewing DDoS Protection Details
1. Go to the [Protection Overview](https://console.cloud.tencent.com/ddos/antiddos-native/overview/) page in the new Anti-DDoS Pro Console to view DDoS protection details of each IP protected by your Anti-DDoS Pro instance.
2. On the **DDoS Protection** tab, select a query period, target region, and instance to check whether the instance has been attacked.
   >You can query the attack traffic and DDoS attack events in the last 180 days.
   >
	- View the information of attacks suffered by the selected Anti-DDoS Pro instance within the queried period, such as the trends of **attack traffic bandwidth/attack packet rate**.
    ![](https://main.qcloudimg.com/raw/13548d64b02a1a600b6628017ee01111.png)
	- View how the attacks distribute across different attack traffic protocols, attack packet protocols, and attack types.
		- **Attack Traffic Protocol Distribution** displays how the attacks suffered by the selected Anti-DDoS Pro instance distribute across different attack traffic protocols within the queried period.
		- **Attack Packet Protocol Distribution** displays how the attacks suffered by the selected Anti-DDoS Pro instance distribute across different attack packet protocols within the queried period.
		- **Attack Type Distribution** displays how the attacks suffered by the selected Anti-DDoS Pro instance distribute across different attack types within the queried period.
    ![](https://main.qcloudimg.com/raw/6f0fdfda81b3cbe3ef75ee044061d7d9.png)
	- In the **Attack Source Distribution** section, you can view the distribution of DDoS attack sources in and outside Mainland China within the queried period, so that you can take further protective measures based on the displayed information.
	![](https://main.qcloudimg.com/raw/1481ba535a9e9499175f22167adb4bbc.png)
	- In "DDoS Attack Records", you can view details of the DDoS attack events within the queried period, including the start time, duration, type, and status of each attack event.
		- You can download DDoS attack packets to analyze and trace the attacks.
		- Click **Attack Details** to view the maximum packet rate, maximum attack traffic bandwidth, and total amount of traffic cleansed during the DDoS attack event.
		- Click **Attack Source Info** to view the attack source IP addresses, source regions, generated attack traffic, and attack packet size.
>Attack source information is sampled data, which is randomly collected for statistics. The data will be displayed around 5 minutes after an attack ends.
>
![](https://main.qcloudimg.com/raw/a21a483296aa5b8b75bb90bcad0e04f3.png)
 
## Viewing CC Protection Conditions
1. Go to the [Protection Overview](https://console.cloud.tencent.com/ddos/antiddos-native/overview/) page in the new Anti-DDoS Pro Console to view CC protection details of each IP protected by your Anti-DDoS Pro instance.
2. On the **CC Protection** tab, select a query period, target region, and instance to check whether the instance has been attacked.
   >You can query the number of attack requests and CC attack events in the last 180 days.
   >
	- You can select **Today** to view the trend in the number of attack requests to the selected Anti-DDoS Pro instance. You can check whether the total number of requests is far higher than the normal QPS, whether the attack QPS has a value, and whether the value is extremely high.
	- If the protected IP is under CC attack, the system will record the attack start time, end time, attacked domain names, attacked URLs, total request peak, attack request peak, and attack sources.
		-  **Total request peak**: the peak of the total request traffic the Anti-DDoS Pro instance receives when the attack occurs.
		- **Attack request peak**: the peak number of requests blocked by the instance when the attack occurs.
![](https://main.qcloudimg.com/raw/34100945d2753e849fb945abc253052e.png)

