## Basic Information
Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), choose **Anti-DDoS Pro -> **Protection Configuration**, and select the target instance from the drop-down list. You can view the basic information of the instance in the **Instance Information** area.
![](https://main.qcloudimg.com/raw/dd5af2fd4bc4482b7a4625302b33be11.png)

### Instance Name
Name of the Anti-DDoS Pro instance. It is used to identify and manage Anti-DDoS Pro instances. The length is 1-20 characters. You can set the instance name as required. For more information, please see [Setting Instance Name](https://intl.cloud.tencent.com/document/product/1029/31755).

### Region
 The **Region** you select when you [purchase the Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/31748).

### Binding IPs
The actual business IPs protected by the Anti-DDoS Pro instance.

### Base Protection Bandwidth
Base protection bandwidth of the Anti-DDoS Pro instance, that is, the **base protection bandwidth** you select when you [purchase](https://intl.cloud.tencent.com/document/product/1029/31748) the instance. If the elastic protection is disabled, the base protection bandwidth is the maximum bandwidth of the Anti-DDoS Pro instance.

### Status
Current status of the Anti-DDoS Pro instance, including **Running**, **Cleansing**, and **Blocked**.

### Expiration Time
It is calculated according to the selected **Purchase Duration** when you [purchase](https://intl.cloud.tencent.com/document/product/1029/31748) the instance and the order submit time. The expiration time is accurate to second. Tencent Cloud will inform the account creator and related cooperators of the expiration and renewal information through internal messages, SMSs, and emails 7 days before the actual expiration date.

## Elastic Protection Information
Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), choose **Anti-DDoS Pro -> **Protection Configuration**, and select the target instance from the drop-down menu. You can view the elastic protection information of the instance in the **Elastic Protection** section.
![](https://main.qcloudimg.com/raw/eae8c95abe37a189eb9e6dcb4014b4ef.png)

### Status
Specifies whether the elastic protection is enabled. If the elastic protection is not enabled when you [purchase the Anti-DDoS Pro instance](https://intl.cloud.tencent.com/document/product/1029/31748), you can enable it during usage. For more information, please see [Configuring Elastic Protection](https://intl.cloud.tencent.com/document/product/1029/31756).

### Elastic Bandwidth
The maximum elastic protection bandwidth of the Anti-DDoS Pro instance. You can [adjust the elastic protection bandwidth](https://intl.cloud.tencent.com/document/product/1029/31756) as required.
>This parameter item is visible only when the elastic protection is enabled.

## Anti-DDoS Protection
Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), choose **Anti-DDoS Pro** -> **Protection Configuration**, and select the target instance from the drop-down menu. You can view the anti-DDoS protection policy of the instance in the **DDoS Protection** section.
![](https://main.qcloudimg.com/raw/2bc835ded4fc3d1a629db69d69b9e5ea.png)
### Protection Status
Specifies whether the DDoS protection is enabled. It is enabled <img src="https://main.qcloudimg.com/raw/9f12e685bdc6e7269f8b6d56932972e5.png"  style="margin:0;"> by default. If you disable DDoS protection, your server may crash due to DDoS attacks.

### Cleansing Threshold
The threshold for Anti-DDoS Pro to execute cleansing operations. If the traffic is under the threshold, the cleansing operation is not executed even if attacks are detected.
>If you know the threshold, see [Configuring the Cleansing Threshold and Protection Level](https://intl.cloud.tencent.com/document/product/1029/31760) to set a threshold. If you do not know the threshold, the anti-DDoS protection system will automatically learn through AI algorithms and generate the default threshold for you.

### Protection Level
The protection levels include **Loose**, **Normal**, and **Strict**. The default level is **Normal**. You can customize the protection level as required. For more information, please see [Configuring the Cleansing Threshold and Protection Level](https://intl.cloud.tencent.com/document/product/1029/31760).
The following table details the operations for each level.

<table>
    <tr>
        <th>Protection Level</th>
        <th>Protection Operation</th>
				<th>Description</th>
    </tr>
    <tr>
        <td>Loose</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack attributes.</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specification.</li>
                     <li>Filters UDP data packets with explicit attack attributes.</li></ul></td>
				<td>The cleansing policy is loose and only protects against explicit attack packets.<br/>You are advised to enable it when normal requests are misblocked. Attack packets may pass through the security system in case of complex attacks.</td>
    </tr>
    <tr>
        <td>Normal</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack attributes.</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol.</li>
                     <li>Filters UDP data packets with explicit attack attributes.</li>
                     <li>Filters common attack UDP data packets.</li>
                     <li>Actively verifies the source IPs of some access attempts.</li></ul></td>
				<td>The cleansing policy applies to most services and effectively protects against common attacks.<br/>The normal mode is configured by default.</td>
    </tr> 
		<tr>
        <td>Strict</td>
        <td><ul><li>Filters SYN and ACK data packets with explicit attack attributes.</li>
                     <li>Filters TCP, UDP, and ICMP data packets that are not compliant with the protocol specifications.</li>
                     <li>Filters UDP data packets with explicit attack attributes.</li>
                     <li>Filters common attack UDP data packets.</li>
                     <li>Actively verifies the source IPs of some access attempts.</li>
                     <li>Filters ICMP attack packages.</li>
                     <li>Filters common UDP attack data packets.</li>
                     <li>Strictly checks UDP data packets.</li></ul></td>
				<td>The cleansing policy is strict. You are advised to enable it when pass-through attacks occur under the normal mode.</td>
    </tr>
</table>

 >If your business needs to use UDP protocol, you are advised to contact [Tencent Cloud Technical Support](https://intl.cloud.tencent.com/support) to formulate a policy to avoid impact on business operations when in strict mode.

### Scenarios
Anti-DDoS Pro supports scenarios settings. After you create a scenario, the backend collects, identifies, and automatically generates an advanced protection policy to implement flexible configuration or maintain the protection policy. For more information, please see [Configuring Scenarios](https://intl.cloud.tencent.com/document/product/1029/31761).
### Advanced Policy
Anti-DDoS Pro provides advanced protection policies against DDoS attacks. You can adjust and optimize the anti-DDoS protection policy as required through blacklists/whitelists, disabling protocols and ports, packet feature filtering policies, and null session protection. For more information about how to add and manage advanced policies, please see [Managing DDoS Advanced Protection Policies](https://intl.cloud.tencent.com/document/product/1029/31762).
### Alarm Threshold of DDoS Attacks
The triggering threshold for the system to push alarm messages in the event of DDoS attacks. When the detected alarm metric is under the threshold, the system will not push alarm messages to specified users in the event of DDoS attacks.


