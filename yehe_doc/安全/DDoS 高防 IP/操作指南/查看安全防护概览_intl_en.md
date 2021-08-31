After connecting your business and switching the business traffic to Anti-DDoS Advanced, you can view the business traffic and DDoS attack protection details in the console. You can download the attack data by capturing the packets for easier attack analysis and tracing.
## Viewing DDoS Protection Details
1. Log in to the [new Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/overview) and click **Protection Overview** on the left sidebar.
2. On the protection overview page, click **DDoS Protection**, set the query period, and select target instance and protected IP to check whether the instance has been attacked.
   >You can query the attack traffic and DDoS attack events in the last 180 days.
   >
	- View the information of attacks suffered by the selected Anti-DDoS Advanced instance within the queried period, such as the trends of **attack traffic bandwidth/attack packet rate**. When the instance is under attack, you can intuitively view the attack bandwidth peak in the bandwidth trend diagram.
    ![](https://main.qcloudimg.com/raw/f14181d3ef2ea79c7deff1f47556acc9.png)
	- View the total attack traffic, number of attack packets, and total number of attacks to understand the attack details within the queried period.
		- **Total Attack Traffic** displays how the traffic of attacks suffered by the selected Anti-DDoS Advanced instance distribute across different protocols within the queried period.
		- **Number of Attack Packets** displays how the packets of attacks suffered by the selected Anti-DDoS Advanced instance distribute across different protocols within the queried period.
		- **Total Number of Attacks** displays how the attacks suffered by the selected Anti-DDoS Advanced instance distribute across different attack types within the queried period.
        ![](https://main.qcloudimg.com/raw/f4be2a769b6128a2d9aa3d9bad912013.png) 
	- In "DDoS Attack Details", you can view details of the DDoS attack events within the queried period, including the start time, duration, type, and status of each attack event.
        ![](https://main.qcloudimg.com/raw/72694d7acf0f35eb962070d20c584e69.png)
        >
        > - You can query the attack source information of only one single protected IP at a time.
        > - Attack source information is sampled data, which is randomly collected for statistics. The data will be displayed around 5 minutes after an attack ends.
        >
   
## Viewing CC Protection Details
1. Log in to the [new Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/overview) and click **Protection Overview** on the left sidebar.
3. On the protection overview page, click **CC Protection**, set the query period, and select target instance and protected IP to check whether the instance has been attacked.
   >You can query the number of attack requests and CC attack events in the last 180 days.
   >
	- You can select **Today** to view the trend in the number of attack requests to the selected Anti-DDoS Advanced instance. You can check whether the total number of requests is far higher than the normal QPS, whether the attack QPS has a value, and whether the value is extremely high.
	- If the protected IP is under CC attack, the system will record the attack start time, end time, attacked domain names, attacked URLs, total request peak, attack request peak, and attack sources.
		-   **Total request peak**: the peak of the total request traffic the Anti-DDoS Advanced instance receives when the attack occurs.
		-   **Attack request peak**: the peak number of requests blocked by the instance when the attack occurs.
![](https://main.qcloudimg.com/raw/a3b0a551327f25f1d2f4c6aed1a6600c.png)

## Viewing Business Traffic Details
1. Log in to the [new Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/overview) and click **Protection Overview** on the left sidebar.
3. On the protection overview page, click **Business**, set the query period, and select the target instance and protected IP to view the **inbound/outbound business traffic bandwidth trend**, **inbound/outbound business packet rate trend**, and **active/new connection trends** in the selected period. In addition, you can view the peaks of business traffic bandwidth, number of connections to business, and number of requests to business.
	- **Number of Active Connections**: all established TCP connections at the current time.
	- **Number of New Connections**: number of new TCP connections that are established between clients and Anti-DDoS in one second.
 >You can query the business information in the last 180 days.
 >
![](https://main.qcloudimg.com/raw/db756411b028843031821ae3924dcda8.png)

