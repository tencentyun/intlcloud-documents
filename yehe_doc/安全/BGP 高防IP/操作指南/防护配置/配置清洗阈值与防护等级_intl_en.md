## Use Cases
Anti-DDoS Advanced allows you to adjust protection policies and provides three protection levels against DDoS attacks. The protection operations at each level are as described below:
>If you need to use the UDP protocol, please contact [Tencent Cloud Technical Support](https://intl.cloud.tencent.com/support) to customize a policy and avoid impact on business operations when in strict mode.
<table>
    <tr>
        <th>Protection Level</th>
        <th>Protection Operation</th>
				<th>Description</th>
    </tr>
    <tr>
        <td>Loose</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack characteristics.</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specification.</li>
                     <li>Filters UDP data packets with explicit attack characteristics.</li></ul></td>
				<td>This cleansing policy is loose and only protects against explicit attack packets.<br/>You are recommended only to use this mode when requests are blocked mistakenly. Attack packets may pass through the security system in case of complex attacks.</td>
    </tr>
    <tr>
        <td>Normal</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack characteristics.</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specification.</li>
                     <li>Filters UDP data packets with explicit attack characteristics.</li>
                     <li>Filters common attack UDP data packets.</li>
                     <li>Actively verifies the source IPs of certain access requests.</li></ul></td>
				<td>This cleansing policy applies to most businesses and effectively protects against common attacks.<br/>The normal mode is configured by default.</td>
    </tr> 
		<tr>
        <td>Strict</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack characteristics.</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specification.</li>
                     <li>Filters UDP data packets with explicit attack characteristics.</li>
                     <li>Filters common attack UDP data packets.</li>
                     <li>Actively verifies the source IPs of certain access requests.</li>
                     <li>Filters ICMP attack packages.</li>
                     <li>Filters common UDP attack data packets.</li>
                     <li>Strictly checks UDP data packets.</li></ul></td>
				<td>This cleansing policy is strict. You are recommended to use this mode when attack packets pass through the security system in Normal mode.</td>
    </tr>
</table>
By default, your purchased Anti-DDoS Advanced instance uses the Normal protection level, which can be changed based on your actual business needs. In addition, you can customize the cleansing threshold. If the attack traffic exceeds the threshold, the cleansing policy will be automatically triggered.

## Configuration Samples
This section takes instance "bgpip-000002ai" in South China (Guangzhou) as an example to describe the configurations.
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), select **Anti-DDoS Advanced** > **Asset List** on the left sidebar, and click **South China (Guangzhou)** in the region selection box.
2. Find the Anti-DDoS Advanced instance whose ID is "bgpip-000002ai" and click **Protection Configuration** in the "Operation" column on the right.
3. In the pop-up Anti-DDoS configuration page, enable **Protection Status** to set the cleansing threshold and protection level.
>The configuration items are visible only when **Protection Status** is <img src="https://main.qcloudimg.com/raw/9f12e685bdc6e7269f8b6d56932972e5.png"  style="margin:0;">. If you disable the protection, the configuration items will be hidden and will not take effect. After you enable the protection again, the items will be visible again and retain the original configurations.
>**Configuration parameter descriptions:**

- **Protection status**
	  Protection is enabled by default. You can enable or disable it as needed and set the duration for disablement. Currently, the duration can only be 1–6 hours. The Anti-DDoS Advanced instance will automatically enable protection after the set duration elapses or when the attack traffic bandwidth exceeds 1 million pps or 2 Gbps.
  - **Cleansing threshold**
		- It indicates the threshold to trigger cleansing. If the traffic is below the threshold, no cleansing operation will be executed even if attacks are detected.
		- After protection is enabled, the Anti-DDoS Advanced instance, if just connected to your business, will use the default cleansing threshold value by default. As the business traffic changes, the system will automatically learn to calculate a baseline value. You can set the cleansing threshold based on your business protection needs at any time.
	If you have a clear concept about the threshold, set it as needed; otherwise, please use the default value. Anti-DDoS will automatically learn through AI algorithms and calculate the default threshold for you.
   >- **Protection level**
	After protection is enabled, the Anti-DDoS Advanced instance, if just connected to your business, will use the Normal protection level by default. You can adjust the level based on your business protection needs at any time.
- **Other configuration items**
		- **Business scenario**
	    You can select and modify a matched business scenario from the created ones as needed. When a business scenario is selected, the corresponding "advanced policy" will be automatically generated accordingly. For more information on how to create a business scenario, please see [Configuring Business Scenarios](https://intl.cloud.tencent.com/document/product/297/34091).
  	- **Advanced policy**
	    You can select and modify a matched advanced policy from the created ones based on your business protection characteristics. For more information on how to create an advanced policy, please see [Managing Anti-DDoS Advanced Policies](https://intl.cloud.tencent.com/document/product/297/34217).
  	- **Alarm threshold for DDoS attacks**
	 You can configure an alarm threshold for DDoS attacks. If the detected metric exceeds the set threshold, an alarm will be triggered and alarm notifications will be pushed to you. For more information on how to set an alarm threshold, please see [Configuring Attack Alarm Thresholds](https://intl.cloud.tencent.com/document/product/297/34098).
  	- **AI-based enhanced protection for TCP business**
	    For layer-4 TCP business, Anti-DDoS Advanced provides AI-based enhanced protection. After this feature is enabled, through self-learning of business routine characteristics with the aid of AI models, Anti-DDoS Advanced can automatically distinguish between business traffic and attack traffic, effectively defending your business against layer-4 CC attacks.
  Currently, AI-based enhanced protection for TCP business is only available to users in the whitelist.
