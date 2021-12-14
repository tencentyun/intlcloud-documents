After an IP address is bound to an Anti-DDoS Pro instance, when you receive a DDoS attack alarm message or notice any issue with your business, you need to view the attack details in the console, including the attack traffic and current protection effect. Enough information is critical for you to take measures to keep your business running smoothly.
## Viewing DDoS Protection Details
1. Go to the [Protection Overview](https://console.cloud.tencent.com/ddos/antiddos-native/overview/) page in the new Anti-DDoS Pro console to view DDoS protection details of each IP protected by your Anti-DDoS Pro instance.
2. On the **DDoS Protection** tab, select a query period, target region, and instance to check whether the instance has been attacked.
>?You can query attack traffic and DDoS attack events in the past 180 days.

- View the information of attacks suffered by the selected Anti-DDoS Pro instance within the queried period, such as the trends of **attack traffic bandwidth/attack packet rate**.
	![](https://main.qcloudimg.com/raw/13548d64b02a1a600b6628017ee01111.png)
- View the information of DDoS attack events in **Attack events**.
	 - **View All** displays the start time, duration, type, maximum attack traffic bandwidth, maximum packet rate, and blocking status.
	![](https://main.qcloudimg.com/raw/a21a483296aa5b8b75bb90bcad0e04f3.png)
	 - **Attack Details** displays the attack source information, source region, generated attack traffic, and attack packet size for attack and source analyses.
	 ![](https://main.qcloudimg.com/raw/a21a483296aa5b8b75bb90bcad0e04f3.png)
	- View how the attacks distribute across different attack traffic protocols, attack packet protocols, and attack types.
		- **Attack Traffic Protocol Distribution** displays how the attacks suffered by the selected Anti-DDoS Pro instance distribute across different attack traffic protocols within the queried period.
		- **Attack Packet Protocol Distribution** displays how the attacks suffered by the selected Anti-DDoS Pro instance distribute across different attack packet protocols within the queried period.
		- **Attack Type Distribution** displays how the attacks suffered by the selected Anti-DDoS Pro instance distribute across different attack types within the queried period.
	![](https://main.qcloudimg.com/raw/6f0fdfda81b3cbe3ef75ee044061d7d9.png)
	- In the **Attack Source Distribution** section, you can view the distribution of DDoS attack sources in and outside Mainland China within the queried period, so that you can take further protective measures based on the displayed information.
	![](https://main.qcloudimg.com/raw/1481ba535a9e9499175f22167adb4bbc.png)

## Viewing CC Protection Details[](id:CC)
1. Go to the [Protection Overview](https://console.cloud.tencent.com/ddos/antiddos-native/overview/) page in the new Anti-DDoS Pro console to view CC protection details of each IP protected by your Anti-DDoS Pro instance.
2. On the **CC Protection** tab, select a query period, target region, and an instance to check whether the instance has been attacked.
>?You can query the number of attack requests and CC attack events in the last 180 days.

 - You can select **Today** to view the following data to identify the impact of attacks on your business.
    - Total request rate: the rate of total traffic (in QPS).
    - Attack request rate: the rate of attack traffic (in QPS).
    - Total requests: the total number of requests received.
    - Attack requests: the number of attack requests received.
 - If the protected IP is under CC attack, the system will record the attack start time, end time, attacked domain names, attacked URLs, total request peak, attack request peak, and attack sources.
 ![](https://main.qcloudimg.com/raw/e3982483e414040fbfbfe0a3b04cee55.png)
