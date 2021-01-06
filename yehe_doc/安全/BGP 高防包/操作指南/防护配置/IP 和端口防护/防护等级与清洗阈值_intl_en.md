This document introduces the use cases of different protection levels and the actions Anti-DDoS Pro takes to defend against DDoS attacks. You can follow this guide to set the DDoS protection levels in the console.
## Use Cases
Anti-DDoS Pro provides three available protection levels for you to adjust protection policies against different DDoS attacks. The details are as follows:
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
 >- The level Medium is chosen by default in each Anti-DDoS Pro instance.

## Prerequisites
You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the protected target.

## Directions
1. Log in to the [DDoS console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and click **Anti-DDoS Pro (New)** -> **Configurations** on the left sidebar.
2. Select an Anti-DDoS Pro ID from the left list, e.g., `bgp-000000iu`, and then open the **IP and Port Protection** tab.
3. Choose a protection level in the **DDoS Protection Level** section.

