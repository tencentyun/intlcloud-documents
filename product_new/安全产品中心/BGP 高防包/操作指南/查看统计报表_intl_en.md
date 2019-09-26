After the protected IP accesses Anti-DDoS Pro, when you receive a DDoS attack alarm message or find exceptional issues occurring to the business, you can log in to the console to quickly understand the attack information, such as the attack traffic and protection effect. Enough information is the bases for effective measures to maintain smooth business in time.
## Viewing Anti-DDoS Protection Conditions
1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview).
1. Choose **Anti-DDoS Pro** -> **Statistics Report**. Select **Single IP Instance**.
   Note: When you select **Multi-IP Instance**, you can view the Anti-DDoS protection of each protected IP in this Anti-DDoS Pro instance.
1. In the **Anti-DDoS Protection** tab, set tattack packethe query time range and select the target region and instance to check whether an attack exists.
   >You can query up to 180 days of attack traffic information and DDoS attack events.
   >
	- Check the attacks to Anti-DDoS Pro within the time range, including network **attack traffic bandwidth/attack packet speed** trends.
![](https://main.qcloudimg.com/raw/e2cad2b0653173aa060516a42999d41b.png)
	- Check the attack distribution under the dimensions of attack traffic protocol distribution, attack packet protocol distribution, and attack type distribution.
		- **Attack traffic protocol distribution**: Check the percentage of the total attack traffic of all protocols among attack events that occur to the selected instance within the time range.
		- **Attack package protocol distribution**: Check the percentage of the total number of attack packets of all protocols that occur to the selected instance within the time range.
		- **Attack type distribution**: Check the percentage of the total number of attack types that occur to the selected instance within the time range.
![](https://main.qcloudimg.com/raw/3938c0e41b9197e424e64a03036773a4.png)
	-  In **DDoS Attack Record**, check the DDoS attack events within the time range, and understand the attack (starting) time, lasting time, attack type and attack status of each attack event.
		- You can download attack packets to analyze and trace the DDoS attacks.
		- Click **Attack Details** to understand the maximum package speed, maximum attack traffic bandwidth, and total cleansing traffic of DDoS attack events.
		- Click **Attack Source Information** to check the attack source IP addresses, original regions, generated attack traffic, and attack packet size of the attacks.
>Attack source information is sampled data, which is randomly grabbed for statistics. The data will appear around 2 hours after the attack ends.
>
![](https://main.qcloudimg.com/raw/517c3e6013d00c94758e300fbc3641e3.png)

## Checking CC Protection
1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview).
1. Choose **Anti-DDoS Pro** -> **Statistics Reports** and select **Single IP Instance**.
   Note: When you select **Multi-IP Instance**, you can check the CC protection of each protected IP in this instance.
1. Click the **CC Protection** tab, set the query time range and select the target region and instance to check whether CC attack exists.
   >You can query up to 180 days of attack request number information and CC attack events.
   >
	- You can select **Today** to check the attack request number trend of the selected instance. Check whether the total request numbers are far bigger than the normal QPS, and check whether the attacked QPS has a value and whether the value is extremely big.
	- If a CC attack exists, the system will record the start time, end time, target domain name, target URL, total request bandwidth, request bandwidth, and source of the attack.
		-  **Total Request Bandwidth**: Calculates the total request traffic bandwidth Anti-DDoS Pro receives when the attack occurs.
		- **Attack Request Bandwidth**: Calculates the request number bandwidth blocked by the Anti-DDoS Pro system when the attack occurs.
![](https://main.qcloudimg.com/raw/5555350b5de6d54039030a0c90c99195.png)

