This document introduces the use cases of different protection levels and the actions Anti-DDoS Advanced (Global Enterprise Edition) takes to defend against DDoS attacks. You can follow this guide to set the DDoS protection levels in the console.

## Use Cases
Anti-DDoS Advanced provides three available protection levels for you to adjust protection policies against different DDoS attacks. The details are as follows:
<dx-tabs>
::: Loose
| Protection Level | Protection Action                                                     | Description                                                         |
| -------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| Loose     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Filters UDP data packets with explicit attack attributes.</li> | <li>This cleansing policy is loose and only defends against explicit attack packets.</li><li>We recommend choosing this protection level when normal requests are blocked. Complex attack packets may pass through the security system.</li> |
:::
::: Medium
| Protection Level | Protection Action                                                     | Description                                                         |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Medium     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Filters UDP data packets with explicit attack attributes.</li><li>Filters common UDP-based attack packets.</li><li>Actively verifies the source IPs of some access attempts.</li> | <li>This cleansing policy is suitable for most businesses and capable of defending against common attacks.</li><li>The level Medium is chosen by default.</li> |
:::
::: Strict
| Protection Level | Protection Action                                                     | Description                                                 |
| -------- | ------------------------------------------------------------ | ---------------------------------------------------- |
| Strict     | <li>Filters SYN and ACK data packets with explicit attack attributes.</li><li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li><li>Filters UDP data packets with explicit attack attributes.</li><li>Filters common UDP-based attack packets.</li><li>Actively verifies the source IPs of some access attempts.</li><li>Filters ICMP attack packets.</li><li>Filters common UDP attack data packets.</li><li>Strictly checks UDP data packets.</li> | This cleansing policy is strict. We recommend choosing this level when attack packets pass through the security system on Normal mode. |
:::
</dx-tabs>

>?
 >- If you need to use UDP in your business, please contact [Tencent Cloud Technical Support](https://cloud.tencent.com/about/connect) to customize an ideal policy for not letting the level Strict affect normal business process.
>- The level Medium is chosen by default for your Anti-DDoS Advanced (Global Enterprise Edition) instance. You can set the DDoS protection level for your business needs and also the cleansing threshold. Attack traffic will be cleansed when it is detected higher than the threshold you set.

## Prerequisites
You have purchased an [Anti-DDoS Advanced (Global Enterprise Edition)](https://cloud.tencent.com/document/product/1014/56255) instance and set your target to protect.

## Directions
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition) Console](https://console.cloud.tencent.com/ddos/ddos-basic) and select **Anti-DDoS Advanced** -> **Configurations** on the left sidebar.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "xxx.xx.xx.xx bgpip-000003n2".
![](https://main.qcloudimg.com/raw/d6586694f3fc6b1cbc6099b6b1498c38.png)
3. Set the "level" and "cleansing threshold" in the **DDoS Protection** block on the right.
 >?If you have a clear concept about the threshold, set it as required. Otherwise leave it to the default value. Anti-DDoS will automatically learn through AI algorithms and calculate the default threshold for you.
 >
![](https://main.qcloudimg.com/raw/5493d666511df983f24362189d39901f.png)
**Parameter Description:**
	- **Level**
	If the protection is enabled, the level Medium is chosen by default for your Anti-DDoS Advanced (Global Enterprise Edition) instance. You can adjust the DDoS protection level for your business needs.
	- **Cleansing Threshold**
		- This indicates a value to trigger cleansing. Cleansing will not be triggered by the traffic below the threshold you set even though it is found malicious.
		- If the protection is enabled, your Anti-DDoS Advanced instance will use the default cleansing threshold after your business is connected, and the system will generate a baseline based on historical patterns of your business traffic. You can also set the cleansing threshold for your business needs.
