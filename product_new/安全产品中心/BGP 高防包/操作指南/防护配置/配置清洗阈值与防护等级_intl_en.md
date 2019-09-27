Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), choose **Anti-DDoS Pro** -> **Protection Configuration**, and select the target instance from the drop-down list. In the **DDoS Protection** section, configure **Protection Status**, **Cleansing Threshold**, **Protection Level**, **Scenario**, and **Advanced Policy**.
>The configuration items are visible only when **Protection Status** is <img src="https://main.qcloudimg.com/raw/9f12e685bdc6e7269f8b6d56932972e5.png"  style="margin:0;">. If you disable the protection, the configuration items will be hidden and do not take effect. After you enable the protection again, the items will be visible and retain the original configuration.

![](https://main.qcloudimg.com/raw/0d3630ce0fbaedb31703322638d9acd6.png)
- ### Protection Status
You can enable or disable the protection as required. You can set the duration for disabling the protection. Currently, the duration is 1-6 hours. The protection automatically takes effect after the set duration or when the attack traffic exceeds 1 million pps or 2 Gbps.

- ### Cleansing Threshold
Indicates the the threshold to trigger cleansing. If the traffic is below the threshold, the cleansing operation is not executed even if attacks are detected.
>If you have a clear concept about the threshold, set it as required. Otherwise please leave it to the default value. Anti-DDoS will automatically learn through AI algorithms and generate the default threshold for you.

- ### Protection Level
You can set the protection level as required. The following table details the operations for each protection level.
<table>
    <tr>
        <th>Protection Level</th>
        <th>Protection Operation</th>
				<th>Description</th>
    </tr>
    <tr>
        <td>Loose</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack attributes</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specification.</li>
                     <li>Filters UDP data packets with explicit attack attributes</li></ul></td>
				<td>The cleansing policy is loose and only protects against explicit attack packages.<br/>It’s recommended only to use this mode when requests are misblocked. Attack packets may pass through the security system in case of complex attacks.</td>
    </tr>
    <tr>
        <td>Normal</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack attributes.</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li>
                     <li>Filters UDP data packets with explicit attack attributes.</li>
                     <li>Filters common attack UDP data packets.</li>
                     <li>Actively verifies the source IPs of some access attempts.</li></ul></td>
				<td>The cleansing policy applies to most services and effectively protects against common attacks.<br/>The normal mode is configured by default.</td>
    </tr> 
		<tr>
        <td>Strict</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack attributes</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specification</li>
                     <li>Filters UDP data packets with explicit attack attributes</li>
                     <li>Filters common UDP-based attack packages</li>
                     <li>Actively verifies the source IPs of some access attempts</li>
                     <li>Filters ICMP attack packages.</li>
                     <li>Filters common UDP attack data packets.</li>
                     <li>Strictly checks UDP data packets.</li></ul></td>
				<td>The cleansing policy is strict. It’s recommended to use this mode when attack packets pass through the security system the Normal mode.</td>
    </tr>
</table>

 >If you need to use UDP protocol, please contact [Tencent Cloud Technical Support](https://intl.cloud.tencent.com/support) to formulate a policy to avoid impact on business operations when in strict mode.


- ###  Scenarios
 Select a matching one from the created scenarios, and modify its configuration as required. After you have selected a scenario, the corresponding advanced policy will automatically match the policy generated for the scenario.
	
- ### Advanced Policy
You can select a matching one from the created advanced policies as required. You can also modify an existing advanced policy.
