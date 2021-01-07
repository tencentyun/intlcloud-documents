This document introduces the use cases of different protection levels and the actions Anti-DDoS Advanced takes to defend against DDoS attacks. You can follow this guide to set the DDoS protection levels in the console.
## Use Cases
Anti-DDoS Advanced provides three available protection levels for you to adjust protection policies against different DDoS attacks. The details are as follows:
<table>
    <tr>
        <th>Protection Level</th>
        <th>Protection Action</th>
				<th>Description</th>
    </tr>
    <tr>
        <td>Loose</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack attributes.</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li>
                     <li>Filters UDP data packets with explicit attack attributes.</li></ul></td>
				<td><li>This cleansing policy is loose and only defends against explicit attack packets.</li><li>We recommend choosing this protection level when normal requests are blocked. Complex attack packets may pass through the security system.</li></td>
    </tr>
    <tr>
        <td>Medium</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack attributes.</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li>
                     <li>Filters UDP data packets with explicit attack attributes.</li>
                     <li>Filters common UDP-based attack packets.</li>
                     <li>Actively verifies the source IPs of some access attempts.</li></ul></td>
				<td><li>This cleansing policy is suitable for most businesses and capable of defending against common attacks.</li><li>The level Medium is chosen by default.</li></td>
    </tr> 
		<tr>
        <td>Strict</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack attributes.</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li>
                     <li>Filters UDP data packets with explicit attack attributes.</li>
                     <li>Filters common UDP-based attack packets.</li>
                     <li>Actively verifies the source IPs of some access attempts.</li>
                     <li>Filters ICMP attack packets.</li>
                     <li>Filters common UDP attack data packets.</li>
                     <li>Strictly checks UDP data packets.</li></ul></td>
				<td>This cleansing policy is strict. We recommend choosing this level when attack packets pass through the security system on Normal mode.</td>
    </tr>
</table>

 >?
 >- If you need to use UDP in your business, please [contact sales](https://intl.cloud.tencent.com/contact-sales) to customize an ideal policy for not letting the level Strict affect normal business process.
>- The level Medium is chosen by default in each Anti-DDoS Advanced instance, and you can adjust the protection level as needed. Also, you can set the cleansing threshold, so that the traffic exceeding the set value can be automatically cleansed.

## Prerequisites
You have successfully purchased an [Anti-DDoS Advanced](https://intl.cloud.tencent.com/document/product/297/37241) instance and set the protected target.

### Directions
1. Log in to the [DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) and click **Anti-DDoS Advanced (New)** -> **Configurations** on the left sidebar.
2. Select an Anti-DDoS Advanced ID or port from the left list, e.g., `212.64.xx.xx bgpip-000002jt` or`119.28.xx.xx bgpip-000002ju` -> `tcp:8000`.
3. Choose a protection level and set the cleansing threshold in the **DDoS Protection Level** section.
**Configuration Parameters**
	- **Protection Level**
	For each Anti-DDoS Advanced instance with the protection enabled, the level Medium is chosen by default and you can adjust the protection level as needed.
	- **Cleansing Threshold**
		- It refers to the threshold to trigger cleansing. If the traffic is below the threshold, the cleansing action will not be taken even if attacks are detected.
		- For each Anti-DDoS Advanced instance with the protection enabled, the cleansing threshold has a default value, and you can set the cleansing threshold as needed. The system will learn the change patterns of business traffic to generate a baseline.
>?If you have a clear concept about the threshold, set it as needed. Otherwise please leave it to the default value. Anti-DDoS will automatically learn through AI algorithms and generate the default threshold for you.
